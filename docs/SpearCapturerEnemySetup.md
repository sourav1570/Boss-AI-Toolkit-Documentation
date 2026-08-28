# Spear Capturer Enemy Setup

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/_pirI5OiN0Q"  
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This setup provides a guide for setting up a ranged **Throw and Capture Spear Enemy** using the Boss AI Toolkit in Unity. It covers model setup, configuration cloning, custom Ragdoll physics creation, registering rotation animation parameters, custom ranged ability setup, and weapon capture mechanics.

---

## 1. Initial Model Setup

### Steps
1. Drag the 3D spear enemy model into the scene hierarchy.
2. Remove any pre-existing **Animator** component on the model.
3. Right-click the GameObject and select **Prefab > Unpack Prefab Completely**.
4. Rename the GameObject to **`Throw and Capture Spear Enemy`**.
5. Match the position transform values to align with the original source template prefab.
6. Assign character materials to the model mesh.
7. Duplicate the spear weapon asset and mount/position it under the character's **Right Hand** bone socket.

---

## 2. Cloning Enemy Configuration

Duplicate configuration settings from the existing `Throw and Capture` template prefab.

### Steps
1. Navigate to **Tools > Boss AI Toolkit > Duplicate Enemy**.
2. Configure cloning settings:
   * **Source Boss**: Drag in the template `Throw and Capture` enemy prefab.
   * **Target Boss**: Drag in the newly prepared `Throw and Capture Spear Enemy` GameObject.
   * **New Boss Name**: Set to `Throw and Capture Spear Enemy`.
   * **Avatar**: Drag and drop the model's target Avatar asset.
   * **Animator Controller**: Leave disabled/default to reuse the base prefab's existing animation controller asset.
3. Click **Start Cloning Configuration**.
4. Deactivate the old template prefab in the scene hierarchy.

---

## 3. Ragdoll Physics Wizard Setup

### Steps
1. Select **Throw and Capture Spear Enemy** in the hierarchy.
2. Go to top menu: **GameObject > 3D Object > Ragdoll...**
3. Drag the character's **Animator** component into the wizard field.
4. Click **Autofill** to auto-assign limb bones (assign missing transforms manually if needed).
5. Click **Create**.
6. Fine-tune generated colliders (e.g., adjust head bone sphere collider dimensions).

---

## 4. Animation Setup Tool: Rotation Animations

Register left and right turn animations into the Animator Controller for smooth turning.

### Steps
1. Add the **Animation Setup Tool** component to **Throw and Capture Spear Enemy** if not already present.
2. Assign the character's **Animator Controller**.
3. Click **Add Animation** and register two turn parameters:
   * `Idle Turn Left` clip -> Parameter Name: **`turn left`**
   * `Idle Turn Right` clip -> Parameter Name: **`turn right`**
4. Click **Add to Animator**.
5. Under **Enemy Ability System > Global Settings > Rotation Animations**:
   * Add 2 direction entries: **Left** (`turn left`) and **Right** (`turn right`).
   * Click **Auto Get Length** to fetch default animation durations.
   * Set idle animation reference and enable **Apply Root Motion**.

---

## 5. Ranged Attack & Weapon Throw Configuration

### Steps
1. Select **Throw and Capture Spear Enemy** and expand **Combat Attack System**.
2. Set distance limits: **Min Distance = 5**, **Max Distance = 200**.
   * *Behavior:* The enemy will only throw the spear when the target is between 5m and 200m away. Moving closer than 5m forces melee/hit reactions instead of throwing.
3. Expand **Custom Ability**:
   * **Ability Type**: Set to `Create Your Own Ability`.
   * **Script Reference**: Assign `Enemy Throw Ability`.
   * **Function**: Select `ActivateThrow`.
   * **Ability Lifetime**: `3` seconds (restarts ability after interval cooldown).
4. Expand **Enemy Weapon Throw Ability**:
   * **Weapon To Throw**: Drag the spear weapon transform from the right hand socket into this field.

---

## 6. Health UI & Death Settings

Configure health bars and ragdoll death transitions.

### Steps
1. Under **Health & UI**:
   * Check **Spawn Health Bar Prefab** and assign the health bar UI prefab.
   * **Death Mode**: Set to **`Die Using Ragdoll Physics`**.
2. Under **Hit Reactions**:
   * Set **Time To Destroy Spawn Impact Effect** to `0.5` seconds (ensures hit impact particles render properly on damage).
3. Under **Team Member**:
   * **My Body Part To Target**: Assign the enemy root mesh object reference.

---

## 7. Verification Checklist

Before running tests in Play Mode, check the following configuration settings:

- [ ] **Cloned Configuration**: Setup cloned from `Throw and Capture` template prefab.
- [ ] **Ragdoll Created**: Colliders and Rigidbodies generated via the 3D Ragdoll wizard.
- [ ] **Animator Parameters**: `turn left` and `turn right` parameters added via the Animation Setup Tool.
- [ ] **Combat Range Limits**: Ranged ability restricted to distances between `5` and `200` meters.
- [ ] **Weapon Reference**: Spear transform assigned to `Weapon To Throw` field.
- [ ] **Death Mode Selected**: `Die Using Ragdoll Physics` active in Health & UI.