# Archer Enemy Setup

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/yClsl1JKYOA"  
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This setup provides a comprehensive guide for setting up an **Archer Enemy** using the Boss AI Toolkit in Unity. It details cloning from a source template, building Ragdoll physics, attaching sockets for the bow and target arrows, configuring the ranged archer ability system, and setting up the arrow projectile prefab.

---

## 1. Model Setup

### Steps
1. Drag the target 3D Archer model into the scene hierarchy.
2. Align its transform position with the existing source `Archer` prefab.
3. Assign the character material (e.g., `Archer Material`) to the Mesh Renderer.
4. Remove any pre-existing **Animator** component on the model.
5. Right-click the model in the hierarchy and select **Prefab > Unpack Prefab Completely**.
6. Rename the GameObject to **`Archer New`**.

---

## 2. Configuration Cloning

Use the Duplicate Enemy wizard to clone components and settings from the source Archer template.

### Steps
1. Open the menu: **Tools > Boss AI Toolkit > Duplicate Enemy**.
2. Configure parameters:
   * **Source Boss**: Drag the template `Archer` prefab.
   * **Target Boss**: Drag the `Archer New` GameObject.
   * **New Boss Name**: Set to `Archer New`.
   * **Target Avatar**: Assign the model's `Archer Avatar` asset.
   * **Create New Animator Controller Asset**: Uncheck (reuses the base template Animator Controller).
   * **Add Weapon**: Uncheck.
3. Click **Start Cloning Configuration** and close the wizard.
4. Deactivate the old template `Archer` prefab in the scene.

---

## 3. Ragdoll Physics Wizard Setup

### Steps
1. Select **Archer New** in the hierarchy.
2. Open top menu: **GameObject > 3D Object > Ragdoll...**
3. Drag the character's **Animator** component into the wizard field.
4. Click **Autofill** to map the limb bones (fill any missing bones manually).
5. Click **Create** to build the ragdoll setup.

---

## 4. Weapon & Socket Attachment

Attach the longbow, current held arrow, and projectile spawn point transforms to the character bones.

### Steps
1. **Bow Attachment**:
   * Locate or duplicate the longbow mesh (`Longbow`).
   * Attach it as a child of the **`Left Hand`** bone transform and copy transform alignment values from the template.
2. **Current Held Arrow**:
   * Duplicate the arrow mesh used for visual representation during the pick animation.
   * Attach it as a child of the **`Right Hand`** bone transform and align its position.
3. **Arrow Spawn Point**:
   * Create an empty child GameObject under `Archer New` named **`Arrow Spawn Point`**.
   * Position it at the bow string launch location (copy position values from the template).

---

## 5. Global & Health UI Settings

### Settings Panel

| Category | Parameter | Value | Description |
| :--- | :--- | :--- | :--- |
| **Global Settings** | Rotate Spine | `Unchecked` | Prevents automatic spine rotation. |
| **Health & UI** | Max Health | `10` | Set lower for testing/faster defeat. |
| | Spawn Health Bar | `Checked` | Spawns world-space health bar prefab. |
| | Death Mode | `Die Using Ragdoll Physics` | Triggers ragdoll physics on death. |
| **Hit Reactions** | Impact Effect Destroy Delay | `0.5` seconds | Lifetime for impact particle effects. |
| **Team Member** | My Body Part To Target | `Archer New` | Reference so player attacks can hit the archer. |

---

## 6. Archer Ability System Setup

Configure the main ranged attack system timing and animation sequences.

### Steps
1. Select **Archer New** and expand **Enemy Ability System > Combat Attack System**.
2. Set distance range (e.g., `0 - 100` meters).
3. Set **Ability Lifetime** to `5` seconds.
4. Expand **Enemy Archer System**:
   * **Arrow Spawn Point**: Assign the `Arrow Spawn Point` transform.
   * **Current Held Arrow**: Assign the held arrow object under the Right Hand bone.
   * **Locate Target On Y**: `Checked`.
   * **Rotation Speed**: `5`.

### Timing & Delay Parameters

| Parameter | Recommended Value | Description |
| :--- | :--- | :--- |
| **Pick Arrow Animation Delay** | `1.0`s | Delay before starting the arrow fetch animation clip. |
| **Current Held Arrow Activation Delay** | `0.5`s | Delay (after pick starts) before showing the arrow in hand. |
| **Arrow Shoot Animation Delay** | `1.0`s | Timing offset when the bow release animation starts. |
| **Current Held Arrow Deactivation Time**| `0`s | Hides the held arrow immediately when the projectile launches. |
| **Arrows To Spawn** | `1` or `3` | Quantity of arrows shot per attack cycle. |
| **Time Between Each Arrow** | `0.3`s | Interval timing between multi-arrow bursts. |

> **Note:** Custom animation clips (Idle, Pickup, Shoot) can be assigned or edited by adding the **Animation Setup Tool** component, linking the Animator Controller, and submitting parameter names to the Animator.

---

## 7. Arrow Projectile Prefab Setup

Configure the dynamic arrow projectile prefab instantiated during attacks.

### Prefab Components & Configuration
1. **Team Member**: Set to the same team name as the Archer. Set `Is Targetable` to `Unchecked` so players don't target flying arrows.
2. **Projectile Script**:
   * **Move Speed**: `25`
   * **Moving Delay**: `0.1`s
   * **Move Forward Only**: `Checked` (travels straight along forward orientation).
   * **Unparent On Move**: `Checked` (detaches projectile upon move start).
3. **Child Mesh & Colliders**:
   * **Capsule Collider**: Set to `Is Trigger`.
   * **Hitbox Component**:
     * **Damage**: `10`
     * **Owner**: Set to `Arrow Prefab`.
     * **Compare Enemy**: `Checked` (assign arrow's `Team Member`).
     * **Auto Activation Delay**: `3` seconds (or `1-2` seconds).
     * **Destroy Mode On Hit**: Set to `Destroy Owner` (destroys arrow upon hitting player).

4. Save changes to the arrow prefab and drag it into the **Arrow Prefab** field under the enemy's **Enemy Archer System**.

---

## 8. Verification Checklist

Before running tests in Play Mode, check the following configuration settings:

- [ ] **Cloned Configuration**: Setup duplicated from the base `Archer` template.
- [ ] **Ragdoll Active**: Bone colliders and Rigidbodies generated via the Ragdoll Wizard.
- [ ] **Bow & Arrow Sockets**: `Longbow` mounted on Left Hand, visual arrow mounted on Right Hand.
- [ ] **Spawn Point Set**: `Arrow Spawn Point` created and assigned in `Enemy Archer System`.
- [ ] **Held Arrow Animation Timings**: Activation delay set to `0.5`s and deactivation set to `0`s.
- [ ] **Projectile Alignment**: `Arrow Prefab` configured with `Move Forward Only` and `Destroy Owner` on hit.
- [ ] **Target Part Mapped**: `Archer New` assigned to `My Body Part To Target` in the `Team Member` script.