# Spear Spawner Enemy Setup

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/D17rIwhrmNE"  
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This setup provides a guide for setting up a ranged **Spear Spawner Enemy** using the Boss AI Toolkit in Unity. It covers model setup, configuration cloning, custom animation registration, projectile spawner setup, and projectile prefab configuration.

---

## 1. Initial Setup

### Steps
1. Drag the 3D spear spawner model into the scene hierarchy.
2. Right-click the GameObject and select **Prefab > Unpack Prefab Completely**.
3. Rename the GameObject to **`Spear Spawner Enemy New`**.
4. Assign the required character material to the model mesh.

---

## 2. Cloning Enemy Configuration

Duplicate configuration settings from the existing `Spear Spawner Enemy` template prefab.

### Steps
1. Navigate to **Tools > Boss AI Toolkit > Duplicate Enemy**.
2. Configure cloning settings:
   * **Source Boss**: Drag in the template `Spear Spawner Enemy` prefab.
   * **Target Boss**: Drag in the newly prepared `Spear Spawner Enemy New` GameObject.
   * **New Boss Name**: Set to `Spear Spawner Enemy New`.
   * **Avatar**: Drag and drop the model's target Avatar asset.
   * **Create New Animator Controller**: Uncheck (reuses the base template's existing animation controller asset).
   * **Weapon**: Uncheck.
3. Click **Start Cloning Configuration** and close the window.

---

## 3. Global Settings & Rotation Animations

Configure turning behaviors and register turning clips.

### Steps
1. Select **Spear Spawner Enemy New** and expand **Enemy Ability System > Global Settings**:
   * **Use Rotation Animations**: Checked.
   * **Rotate Spine**: Unchecked.
2. Under **Rotation Animations**, add two direction entries:
   * **Left**: Choose the left turning clip (`turn left`), enable **Apply Root Motion**, and click **Auto Get Length**.
   * **Right**: Choose the right turning clip (`turn right`), enable **Apply Root Motion**, and click **Auto Get Length**.

> **Note:** If rotation animation clips are missing, add the **Animation Setup Tool** component to the enemy. Assign the Animator Controller, register the clips with parameter names, click **Add to Animator Controller**, and select them from the rotation animation dropdown.

---

## 4. Health UI & Hit Reactions

Configure health UI, death modes, and hit response timings.

### Settings
* **Health & UI**:
  * **Spawn Health Bar Prefab**: Enabled (spawns an health bar).
  * **Death Mode**: Set to **`Die Using Animations`**. Add a dying animation clip and check **Apply Root Motion**. (Or set to `Die Using Ragdoll Physics`).
* **Hit Reactions**:
  * **Time To Destroy Spawn Impact Effect**: `0.5` seconds.
  * **Min / Max Hit Interval**: `1` second.

---

## 5. Ranged Spawner Ability Configuration

### Step 5.1: Distance Group & Ability Setup
1. Under **Combat Attack System**, set **Phase 0 Health Range** (`0 - 100`) and **Initial Attack Delay** to `1` second.
2. Create/edit a distance group with range **`5` to `200`** meters.
3. Add an ability and set **Ability Type** to **`Projectile Attack`**.
4. Set power-up duration and assign the **Magic** animation clip to play while spawning.

### Step 5.2: Spawn Point Setup
1. Create an empty child GameObject under `Spear Spawner Enemy New` named **`Spear Spawn Point`**.
2. Position `Spear Spawn Point` in front of the enemy (copy transform from the template prefab).
3. In the Projectile Attack settings panel:
   * **Spawn Point**: Assign the `Spear Spawn Point` transform.
   * **Projectile Parent**: Assign the `Spear Spawn Point` transform.
     * *Purpose:* Parenting ensures the spawned spear rotates and stays aligned with the enemy while targeting before it is thrown.

---

## 6. Spear Projectile Prefab Configuration

Set up the projectile object and collision components.

### Projectile Alignment & Components
1. **Mesh Orientation**: Ensure the spear model's **+Z axis (forward)** points in the direction of movement.
2. **Team Member**: Assign the `Team Member` component with the same team name as the enemy.
3. **Capsule Collider**: Add a Capsule Collider and check **Is Trigger**.
4. **Hitbox Component**:
   * Set **Owner** to the spear itself and check **Compare Enemy** (assigning the spear's `Team Member` script).
   * **Auto Activate On Start**: Checked.
   * **Deactivate Hitbox On Hit**: Checked.
   * **Deactivate Hitbox After Time**: Checked (`5` seconds).
   * **Destroy Mode On Hit**: Set to `Destroy Owner` (destroys the spear upon impacting the player).

### Projectile Script Settings

| Parameter | Value | Description |
| :--- | :--- | :--- |
| **Moving Delay** | `0` | Delay before movement begins. |
| **Move Speed** | `20` | Forward travel velocity. |
| **Rotation Mode** | `None` | Disables spinning/facing changes during flight. |
| **Move Forward Only** | `Checked` | Forces the spear to fly straight ahead instead of tracking the player dynamically. |
| **Unparent On Move** | `Checked` | Detaches the spear from `Spear Spawn Point` as soon as movement begins. |

5. Apply changes to the Projectile Prefab asset and assign it to the **Projectile Prefab** field on the enemy's attack ability.

---

## 7. Verification Checklist

Before running tests in Play Mode, check the following configuration settings:

- [ ] **Rotation Animations**: Turn left and turn right parameters linked with root motion enabled.
- [ ] **UI & Hits**: Spawn health bar enabled and hit impact effect destroy delay set to `0.5`s.
- [ ] **Spawn Transforms**: `Spear Spawn Point` assigned as both Spawn Point and Projectile Parent.
- [ ] **Projectile Alignment**: Spear mesh Z-axis oriented forward.
- [ ] **Projectile Script Options**: `Move Forward Only` and `Unparent On Move` checked on the spear prefab.