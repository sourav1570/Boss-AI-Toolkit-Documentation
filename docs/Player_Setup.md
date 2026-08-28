# Player Setup

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/CxPMY77WzXw"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This setup provides a comprehensive guide on migrating components, logic, weapons, animations, hitboxes, and visual effects from the default toolkit player to a custom 3D player model using the **Boss AI Toolkit Player Setup Wizard** in Unity.

## 1. Automated Player Migration (Player Setup Wizard)

Use the built-in wizard tool to quickly transfer components, scripts, hitboxes, and bone references from an existing template player to a new custom player model.

### Step 1.1: Preparing the Model
1. Place your new 3D player model into the scene hierarchy and name it **`Player New`**
2. Align its position and rotation to match the original template player
3. Apply the appropriate player material to the mesh
4. Right-click **`Player New`** and create a child empty GameObject named **`Hit Point`** Position it around the chest/torso area

### Step 1.2: Running the Setup Wizard
1. Navigate to **Tools -> Boss AI Toolkit -> Player Setup**
2. Assign the fields as follows:
   * **Source Player**: Drag the original template player GameObject
   * **Target Player**: Drag **`Player New`**
   * **New Rig**: Drag the rig transform of the new player
   * **New Skinned Mesh Renderer**: Drag the Skinned Mesh Renderer of the new player
   * **Hit Point**: Drag the newly created **`Hit Point`** transform
   * **Weapon Parent**: Drag the **Right Hand** bone transform
   * **Shield Parent**: Drag the **Left Hand** bone transform
3. Add equipment entries:
   * **Weapon List**: Add element and assign `Player Sword`
   * **Shield List**: Add element and assign `Shield 2`
4. Click **Apply Changes to Target Player**
5. Click **Awesome** when prompted

---

## 2. Equipment Transforms & Materials Alignment

After running the wizard, manually adjust equipment positions, scales, and materials to fit the new character mesh.

### Steps
1. Select the spawned sword object under the right hand:
   * Copy the transform values (Position, Rotation, Scale) from the template weapon and paste them onto the new sword
   * Assign the sword material
2. Select the spawned shield object under the left hand:
   * Copy and paste the transform values from the template shield
   * Assign the shield material
3. Add Navigation Cutout Avoidance:
   * Add a **Nav Mesh Modifier** component to both the sword and shield GameObjects
   * Set **Mode** to **`Remove Object`**
   * *NOTE:* This prevents weapons from creating holes in the NavMesh during baking, which blocks Boss AI navigation

---

## 3. Animation Overrides & Animator Replacement

Replace standard animation clips (e.g., Idle, Walk, Attack) with custom animations using the Animator Clip Replacer.

### Steps
1. In the Project window, locate `Player Test Animator Controller`
2. Duplicate it (`Ctrl + D` or `Cmd + D`) and rename the copy to **`Player New Animator Controller`**
3. Assign **`Player New Animator Controller`** to the `Animator` component on **`Player New`**
4. Go to **Tools -> Boss AI Toolkit -> Animator Clip Replacer**
5. Drag **`Player New Animator Controller`** into the script field
6. Swap desired animation clips (e.g., replace `Idle 5` with `Idle 02`)
7. Click **Apply Animator Overrides**

---

## 4. Player Controller & UI Reference Bindings

Rebind scene references in the **Player Controller** and UI Canvas to direct control to the new player entity.

### Steps
1. Select **`Player New`** and locate the **Player Controller** component
2. Update the following fields:
   * **Player Reference**: Replace references pointing to the old player with **`Player New`**
   * **Hit Point**: Assign `Player New/Hit Point`
3. Set up the Shield Hit Point:
   * Duplicate **`Hit Point`**, parent it under the Shield GameObject, reset its transform, and position it on the front face of the shield
   * Assign this transform to **Shield Hit Effect Spawn Point** on the controller
4. **UI Canvas Update**: Select the `Canvas 2D` object in the hierarchy and re-assign **`Player New`** to any player reference slots (e.g., Shield Button)

---

## 5. Melee Hitbox & Team Configuration

Set up manual hitboxes on weapons to accurately trigger and apply damage to enemy entities.

### Steps
1. Under `Player New -> Right Hand -> Sword`, create an empty child GameObject named **`Hitbox`**
2. Add a **Capsule Collider**, adjust its size to cover the blade, and check **Is Trigger**
3. Add the **Hitbox** script and configure as follows:
   * **Damage**: `3`
   * **Owner**: `Player New`
   * **Compare Enemy**: Checked
   * **Script Team Member**: Drag `Team Member` script from `Player New`
   * **Activation Mode**: `Manual`
   * **Deactivate Hitbox On Hit**: Checked *(Prevents multi-hit damage on single swings)*
   * **Deactivate Hitbox After Certain Time**: Checked
   * **Hitbox Lifetime**: `3` seconds
4. On **`Player New`**:
   * Drag the new `Hitbox` into the **Hitbox Controller** component attack with the Player
   * Set **Team Member -> Team** to **`Team 1`**
   * Set **My Body Part To Target** to **`Hit Point`**

---

## 6. Weapon Slash VFX & Animation Events Setup

Configure directional slash particles and animation event triggers for combat actions, hitboxes, and footstep audio.

### Step 6.1: Slash Spawn Point Setup
1. Right-click **`Player New`** -> **Create Empty** and name it **`Slash Spawn Point 1`**
2. Position and rotate the point in front of the character (e.g., Position Y: `1.47`, Rotation X: `370`)
3. Child a slash particle effect (e.g., `Electro Slash`) under `Slash Spawn Point 1`
4. In the **Slash Activation Manager** on **`Player New`**:
   * Assign `Slash Spawn Point 1` to **Slash Spawn Point**
   * Set **Slash X Scale** to negative (e.g., `-1`) if flipping directions for left slashes
   * Assign the particle reference and set **Activation Delay** to `0.4` seconds

### Step 6.2: Animation Event Binding
Open **Window -> Animation -> Animation**:

* **Slash Activation**: On attack animation clips (e.g., `Left Slash`), add an event at frame 0 calling `SlashActivationManager.ActivateParticles` passing the configuration name string
* **Hitbox Activation/Deactivation**:
  * Add an event at the swing start frame calling `HitboxController.ActivateHitbox`
  * Add an event at the swing end frame calling `HitboxController.DeactivateHitbox`
* **Footstep Audio**: On locomotion clips (e.g., `Walk`, `Run`), add an event at contact frames calling `UniversalSoundPlayer.PlayAudioAction` with parameter string `"Footstep Sound"`

---

## 7. Movement & Combat Parameter Reference

Configure fine-tuning parameters inside the **Player Controller** script:

| Parameter | Recommended Value | Description |
| :--- | :--- | :--- |
| **Auto Rotate To Enemy** | `Checked` | Automatically rotates player toward target upon attacking |
| **Auto Rotate Range** | `3` meters | Detection range threshold for auto-targeting rotation |
| **Hit Animation Interval** | `1` second | Cooldown between hit-reaction stagger animations |
| **Health Settings** | `100` HP (`2s` Change Duration) | Smooth lerping duration for health UI depletion |
| **Slide To Enemy** | Optional | Enables automatic closing distance slide toward enemy on attack |

---

## 8. Verification Checklist

Before testing combat in Play Mode, verify all setups against this checklist:

- [ ] **NavMesh Modifiers**: Sword and Shield have `Nav Mesh Modifier` set to `Remove Object` to prevent navigation holes
- [ ] **Team ID**: Player set to `Team1`; Enemy entities set to `Team2`
- [ ] **Hitbox Flags**: `Deactivate Hitbox On Hit` and `Deactivate Hitbox After Certain Time` enabled on weapon hitbox
- [ ] **Animation Events**: `ActivateHitbox`, `DeactivateHitbox`, and `ActivateParticles` events are added on animation clips
