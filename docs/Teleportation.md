# Teleportation

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/zGtixkKoJtU"  
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This setup details how to configure the **Teleportation Ability** on the `Bull Boss New` AI entity. It covers target spawning cycles, particle effect setup, trigger collider exclusions, and integrating the shader dissolve controller.

---

## 1. Ability Core Configuration

Add the Teleportation ability to the boss's ability system and configure its timing and targeting mechanics.

### Steps
1. Select the **Bull Boss New** GameObject in your scene hierarchy.
2. In the Inspector, locate the **Enemy Ability System** component.
3. Click to **Add Ability** and select **Teleportation**.
4. Remove any existing default events attached to this ability.
5. Adjust probabilities to isolate testing:
   * Set **Teleportation Ability Probability** to `100`.
   * Set **Jump Attack Probability** (and other abilities) to `0`.
6. Configure timing and positioning parameters:
   * **Disappear Animation Trigger**: Set to `Ground Slam` (or `Idle`).
   * **Reappear Animation Trigger**: Set to `Idle`.
   * **Disappear Delay**: `3` seconds.
   * **Appear Delay**: `3` seconds.
   * **Appear/Disappear Max Range**: `15` meters.
   * **Total Teleport Cycles**: `3`.
   * **Spawn Location**: Select preferred spawn strategies such as `Spawn Behind Target`, `Spawn Left`, or `Spawn Right`.
   * **Idle Delay**: `2` seconds (delay before returning to normal behavior after cycles end).

> **Note:** The boss will disappear after 3 seconds, perform 3 complete teleport cycles around the player within a 15-meter range, and then enter an idle state for 2 seconds.

---

## 2. Trigger Colliders & Range Visualization

To prevent physics bugs or unwanted damage during teleportation, assign all active hitboxes/colliders to the ability setup.

### Steps
1. In the Inspector, lock the Inspector view on **Bull Boss New**.
2. Locate the **Colliders** array inside the Teleportation ability parameters.
3. Drag and drop all attached trigger colliders (e.g., the main character collider and weapon `Damage Point` colliders) into this list.
4. *(Optional)* Check **Visualize Range in Scene** if you need scene view gizmos to see the 15-meter teleportation boundary.
5. Unlock the Inspector view.

---

## 3. Visual FX (VFX) Setup

Combine smoke and lightning particle systems into a single parent object to handle disappear and reappear visual effects.

### 3.1 Preparing the Particle Prefabs
1. Search for the **`Explosion`** prefab in `Hovl Studio -> Prefabs -> Smoke Hits and Explosion`.
2. Unpack the prefab completely in your scene:
   * Delete the `Flash Shockwave` child object.
   * Remove the root `Particle System` component.
   * Remove any extra explosion particle sub-objects, leaving only the **Smoke** particle system.
   * Ensure **Is Looping** is **Unchecked** on the smoke particle component.
3. Search for **`VFX Lightning`** in the project tab and bring it into the scene:
   * Unpack the prefab completely.
   * Adjust transform parameters: Scale to `(0.5, 0.5, 0.5)` and Rotation X to `-90`.

### 3.2 Creating the Combined VFX Parent
1. Right-click **Bull Boss New** -> **Create Empty** and name it **`Teleportation Effects`**.
2. Make both the modified **Smoke** object and **Lightning** object children of `Teleportation Effects`.
3. Ensure both child particle objects are active, but **deactivate** the parent `Teleportation Effects` GameObject by default.

### 3.3 Binding Effects to the Ability
1. Select **Bull Boss New** and locate the Teleportation ability settings.
2. Enable both **Disappear Effects** and **Appear Effects** checkboxes.
3. Drag and drop `Teleportation Effects` into both the **Disappear Effect** and **Appear Effect** fields.
4. Set effect timings:
   * **Effect Activation Delay**: `0` seconds (triggers immediately upon teleport start).
   * **Effect Active Lifetime**: `1` second.

---

## 4. Dissolve Shader Event Hooks

Integrate the `Enemy Dissolve Controller` to visually fade out the character mesh and weapon materials during teleportation.

### 4.1 Configuring Dissolve Parameters
In the **Enemy Dissolve Controller** component attached to the boss, set up four elements:

| Element Name | Shader Property | Start Fill Amount | Target Fill Amount | Render Type | Assigned Mesh | Material Used | Delay / Duration |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **`Dissolve In`** | `_DissolveAmount` | `0` | `1` | Skinned Mesh Renderer | Boss Mesh | `Bull Dissolve` | Delay: `0s`, Duration: `1s` |
| **`Dissolve In Weapon`** | `_DissolveAmount` | `0` | `1` | Mesh Renderer | Weapon Mesh | `Spiky Weapon Dissolve` | Delay: `0s`, Duration: `1s` |
| **`Dissolve Out`** | `_DissolveAmount` | `1` | `0` | Skinned Mesh Renderer | Boss Mesh | `Bull Dissolve` | Delay: `0s`, Duration: `1s` |
| **`Dissolve Out Weapon`**| `_DissolveAmount` | `1` | `0` | Mesh Renderer | Weapon Mesh | `Spiky Weapon Dissolve` | Delay: `0s`, Duration: `1s` |

> **Crucial Note:** Ensure the **Original Material** field on `Dissolve Out` points to the `Bull Dissolve` material instead of standard materials to prevent the character model from turning plain white upon reappearing.

### 4.2 Binding Event Hooks
1. Locate **Event Hook Listener** on **Bull Boss New** and add two new event hooks:
2. **Hook 1: On Disappear**
   * **Target**: Drag `Enemy Dissolve Controller`.
   * **Function**: `EnemyDissolveController -> SetFillByName`.
   * **String Parameter**: Enter `Dissolve In`.
   * Add a second entry targeting `Enemy Dissolve Controller -> SetFillByName` with parameter `Dissolve In Weapon`.
3. **Hook 2: On Appear**
   * **Target**: Drag `Enemy Dissolve Controller`.
   * **Function**: `EnemyDissolveController -> SetFillByName`.
   * **String Parameter**: Enter `Dissolve Out`.
   * Add a second entry targeting `Enemy Dissolve Controller -> SetFillByName` with parameter `Dissolve Out Weapon`.

---

## 5. Verification Checklist

- [ ] **Probabilities**: Teleportation is set to `100%`, other abilities set to `0%` for testing.
- [ ] **Colliders**: All character and weapon Hitbox colliders are assigned in the ability parameters.
- [ ] **VFX Parent State**: `Teleportation Effects` parent object is deactivated in hierarchy by default.
- [ ] **Particle Loops**: Particle systems under `Teleportation Effects` have `Is Looping` unchecked.