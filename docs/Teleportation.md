# Setting Up Teleportation Ability (Boss AI Toolkit)

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/zGtixkKoJtU"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This guide details how to configure the **Teleportation Ability** on the `Bull Boss New` AI entity[cite: 9]. It covers target spawning cycles, particle effect setup, trigger collider exclusions, and integrating the shader dissolve controller[cite: 9].

---

## 1. Ability Core Configuration

Add the Teleportation ability to the boss's ability system and configure its timing and targeting mechanics[cite: 9].

### Steps
1. Select the **Bull Boss New** GameObject in your scene hierarchy[cite: 9].
2. In the Inspector, locate the **Enemy Ability System** component[cite: 9].
3. Click to **Add Ability** and select **Teleportation**[cite: 9].
4. Remove any existing default events attached to this ability[cite: 9].
5. Adjust probabilities to isolate testing[cite: 9]:
   * Set **Teleportation Ability Probability** to `100`[cite: 9].
   * Set **Jump Attack Probability** (and other abilities) to `0`[cite: 9].
6. Configure timing and positioning parameters[cite: 9]:
   * **Disappear Animation Trigger**: Set to `Ground Slam` (or `Idle`)[cite: 9].
   * **Reappear Animation Trigger**: Set to `Idle`[cite: 9].
   * **Disappear Delay**: `3` seconds[cite: 9].
   * **Appear Delay**: `3` seconds[cite: 9].
   * **Appear/Disappear Max Range**: `15` meters[cite: 9].
   * **Total Teleport Cycles**: `3`[cite: 9].
   * **Spawn Location**: Select preferred spawn strategies such as `Spawn Behind Target`, `Spawn Left`, or `Spawn Right`[cite: 9].
   * **Idle Delay**: `2` seconds (delay before returning to normal behavior after cycles end)[cite: 9].

> **Note:** The boss will disappear after 3 seconds, perform 3 complete teleport cycles around the player within a 15-meter range, and then enter an idle state for 2 seconds[cite: 9].

---

## 2. Trigger Colliders & Range Visualization

To prevent physics bugs or unwanted damage during teleportation, assign all active hurtboxes/colliders to the ability setup[cite: 9].

### Steps
1. In the Inspector, lock the Inspector view on **Bull Boss New**[cite: 9].
2. Locate the **Colliders** array inside the Teleportation ability parameters[cite: 9].
3. Drag and drop all attached trigger colliders (e.g., the main character collider and weapon `Damage Point` colliders) into this list[cite: 9].
4. *(Optional)* Check **Visualize Range in Scene** if you need scene view gizmos to see the 15-meter teleportation boundary[cite: 9].
5. Unlock the Inspector view[cite: 9].

---

## 3. Visual FX (VFX) Setup

Combine smoke and lightning particle systems into a single parent object to handle disappear and reappear visual effects[cite: 9].

### 3.1 Preparing the Particle Prefabs
1. Search for the **`Explosion`** prefab in `Hover Studio -> Prefabs -> Smoke Hits and Explosion`[cite: 9].
2. Unpack the prefab completely in your scene[cite: 9]:
   * Delete the `Flash Shockwave` child object[cite: 9].
   * Remove the root `Particle System` component[cite: 9].
   * Remove any extra explosion particle sub-objects, leaving only the **Smoke** particle system[cite: 9].
   * Ensure **Is Looping** is **Unchecked** on the smoke particle component[cite: 9].
3. Search for **`VFX Lightning`** in the project tab and bring it into the scene[cite: 9]:
   * Unpack the prefab completely[cite: 9].
   * Adjust transform parameters: Scale to `(0.5, 0.5, 0.5)` and Rotation X to `-90`[cite: 9].

### 3.2 Creating the Combined VFX Parent
1. Right-click **Bull Boss New** -> **Create Empty** and name it **`Teleportation Effects`**[cite: 9].
2. Make both the modified **Smoke** object and **Lightning** object children of `Teleportation Effects`[cite: 9].
3. Ensure both child particle objects are active, but **deactivate** the parent `Teleportation Effects` GameObject by default[cite: 9].

### 3.3 Binding Effects to the Ability
1. Select **Bull Boss New** and locate the Teleportation ability settings[cite: 9].
2. Enable both **Disappear Effects** and **Appear Effects** checkboxes[cite: 9].
3. Drag and drop `Teleportation Effects` into both the **Disappear Effect** and **Appear Effect** fields[cite: 9].
4. Set effect timings[cite: 9]:
   * **Effect Activation Delay**: `0` seconds (triggers immediately upon teleport start)[cite: 9].
   * **Effect Active Lifetime**: `1` second[cite: 9].

---

## 4. Dissolve Shader Event Hooks

Integrate the `Enemy Dissolve Controller` to visually fade out the character mesh and weapon materials during teleportation[cite: 9].

### 4.1 Configuring Dissolve Parameters
In the **Enemy Dissolve Controller** component attached to the boss, set up four elements[cite: 9]:

| Element Name | Shader Property | Start Fill Amount | Target Fill Amount | Render Type | Assigned Mesh | Material Used | Delay / Duration |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **`Dissolve In`** | `_DissolveAmount` | `0` | `1` | Skinned Mesh Renderer | Boss Mesh | `Bull Dissolve` | Delay: `0s`, Duration: `1s` |
| **`Dissolve In Weapon`** | `_DissolveAmount` | `0` | `1` | Mesh Renderer | Weapon Mesh | `Spiky Weapon Dissolve` | Delay: `0s`, Duration: `1s` |
| **`Dissolve Out`** | `_DissolveAmount` | `1` | `0` | Skinned Mesh Renderer | Boss Mesh | `Bull Dissolve` | Delay: `0s`, Duration: `1s` |
| **`Dissolve Out Weapon`**| `_DissolveAmount` | `1` | `0` | Mesh Renderer | Weapon Mesh | `Spiky Weapon Dissolve` | Delay: `0s`, Duration: `1s` |

> **Crucial Note:** Ensure the **Original Material** field on `Dissolve Out` points to the `Bull Dissolve` material instead of standard materials to prevent the character model from turning plain white upon reappearing[cite: 9].

### 4.2 Binding Event Hooks
1. Locate **Event Hook Listener** on **Bull Boss New** and add two new event hooks[cite: 9]:
2. **Hook 1: On Disappear**[cite: 9]
   * **Target**: Drag `Enemy Dissolve Controller`[cite: 9].
   * **Function**: `EnemyDissolveController -> SetFillByName`[cite: 9].
   * **String Parameter**: Enter `Dissolve In`[cite: 9].
   * Add a second entry targeting `Enemy Dissolve Controller -> SetFillByName` with parameter `Dissolve In Weapon`[cite: 9].
3. **Hook 2: On Appear**[cite: 9]
   * **Target**: Drag `Enemy Dissolve Controller`[cite: 9].
   * **Function**: `EnemyDissolveController -> SetFillByName`[cite: 9].
   * **String Parameter**: Enter `Dissolve Out`[cite: 9].
   * Add a second entry targeting `Enemy Dissolve Controller -> SetFillByName` with parameter `Dissolve Out Weapon`[cite: 9].

---

## 5. Verification Checklist

- [ ] **Probabilities**: Teleportation is set to `100%`, other abilities set to `0%` for testing[cite: 9].
- [ ] **Colliders**: All character and weapon hurtbox colliders are assigned in the ability parameters[cite: 9].
- [ ] **VFX Parent State**: `Teleportation Effects` parent object is deactivated in hierarchy by default[cite: 9].
- [ ] **Particle Loops**: Particle systems under `Teleportation Effects` have `Is Looping` unchecked[cite: 9].
- [ ] **Dissolve Material**: `Dissolve Out` uses the `Bull Dissolve` material to fix white texture bugs upon reappearing[cite: 9].