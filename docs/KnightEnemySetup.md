# Knight Enemy Setup

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/ZVNvCfogGz8"  
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This documentation provides a comprehensive guide for setting up a standard **Knight Enemy** (humanoid type) using the Boss AI Toolkit in Unity. It details cloning from a source template, binding weapons and hitboxes, configuring simple melee combat parameters, and setting up a floating world-space health bar.

---

## 1. Initial Setup & Model Preparation

Prepare the standard 3D humanoid model and unpack its prefab components.

### Steps
1. Place the target 3D Knight humanoid model into the scene hierarchy.
2. Align its transform position with the existing source prefab.
3. Remove any pre-existing **Animator** component on the model.
4. Right-click the model in the hierarchy and select **Prefab > Unpack Prefab Completely**.
5. Assign the character material (e.g., `knight material`) to the Mesh Renderer.

---

## 2. Cloning Enemy Configuration

Use the Duplicate Enemy wizard to clone setup parameters from an existing Knight prefab.

### Steps
1. Open the tool menu: **Tools > Boss AI Toolkit > Duplicate Enemy**.
2. Configure parameters:
   * **Source Boss**: Drag the template `Knight Enemy` prefab.
   * **Target Boss**: Drag the target Knight model GameObject.
   * **New Boss Name**: Set to `Knight New`.
   * **Avatar**: Assign the `Knight Avatar` asset.
   * **Animator Controller Asset**: Leave default to reuse the base Knight Animator Controller.
3. Add Weapon Socket:
   * Click **Add Weapon**.
   * **Weapon Object**: Drag in the weapon prefab/mesh asset (e.g., Axe/Sword).
   * **Weapon Socket**: Drag the character's **`Right Hand`** bone transform.
4. Click **Start Cloning Configuration** and close the wizard when finished.
5. Fine-tune the weapon's local transform/positioning on the hand socket.

---

## 3. Hitbox & Combat Target Configuration

Set up manual hitboxes and target body parts.

### Steps
1. Create or copy a `Hitbox` trigger volume as a child under the **Right Hand** bone.
2. Copy and match the position transform from the template hitbox.
3. Select the **Knight New** GameObject and expand the **Hitbox Controller** component.
4. Assign the new `Hitbox` GameObject to the **Hitbox Controller** reference field.
5. Expand the **Team Member** component:
   * **My Body Part To Target**: Assign the Knight root/mesh object so player attacks can locate target bounds.

---

## 4. Animation Event Hitbox Binding

Trigger damage hitboxes directly during attack keyframes in the Animator.

### Steps
1. Select **Knight New** and open **Window > Animation > Animation**.
2. Select the melee attack animation clip.
3. Locate the frame where the swing/damage hit begins:
   * Click **Add Event** (plus sign).
   * Select **`HitboxController.ActivateHitbox`**.
4. Locate the frame where the swing completes:
   * Click **Add Event**.
   * Select **`HitboxController.DeactivateHitbox`**.

---

## 5. Simplified Single-Group Combat Setup

Configure basic, predictable melee behavior for standard humanoid enemies.

### Steps
1. Select **Knight New** and expand **Enemy Ability System > Combat Attack System**.
2. Set **Group 0 Distance**: `0` to `100` meters (covers all combat ranges in one group).
3. Set **Melee Ability Probability**: `100%`.
4. Parameter Configuration:
   * **Min / Max Attack Delay**: Set to `1` second for fast, aggressive attacks (or `1-2` seconds).
   * **Attack Duration**: Set to `10` seconds.

---

## 6. Health Bar Setup

Configure a floating health bar prefab above the enemy rather than using screen UI.

### Settings Panel (`Health & UI`)

| Parameter | Recommended Value | Description |
| :--- | :--- | :--- |
| **Spawn Health Bar** | `Checked` | Spawns a world-space UI prefab on initialization. |
| **Health Bar Prefab** | `Enemy Health Bar` | Reference to the UI health bar prefab containing fill images. |
| **Spawn Offset** | Custom Vector3 (Y-axis) | Vertical offset to position the bar above the head. |
| **Follow Target Y Rotation** | `Checked` | Ensures health bar continuously faces towards active player camera. |
| **Death Mode** | `Die Using Animations` | Triggers animated death (or select `Die Using Ragdoll Physics`). |


## 8. Verification Checklist

Before running tests in Play Mode, check the following configuration settings:

- [ ] **Cloning Complete**: Configuration cloned and `Right Hand` weapon socket assigned.
- [ ] **Hitbox Mapped**: Right-hand hitbox assigned in the **Hitbox Controller** component.
- [ ] **Animation Events**: `ActivateHitbox` and `DeactivateHitbox` events added to attack clips.
- [ ] **Single Group Distance**: Range set to `0-100` meters for straightforward melee behavior.
- [ ] **Health Bar**: Floating prefab assigned with `Follow Target Y Rotation` checked.
- [ ] **Impact Effect Timer**: `Time To Destroy Spawn Impact Effect` set to `0.5` seconds.