# Player Vs Spider Boss Setup

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/VjdP2Cb3cAY"  
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This setup provides a guide to setting up and configuring the **Spider Boss** using assets from the Mobile Spider and Worm Pack in Unity. It details how to clone configuration settings from an existing boss (such as the Bull Boss), swap/replace animations, reassign body nodes and visual components, configure specialized abilities, and set up hitbox collision.

---

## 1. Initial Scene Setup

Import and unpack the spider model and set up the duplication base.

### Steps
1. Navigate to `Mobile Spider and Worm Pack > Spider > FBX` in the Project window and drag the spider model into your scene hierarchy.
2. Apply your preferred texture (e.g., `fire` texture).
3. Right-click the spider GameObject in the hierarchy and select **Prefab > Unpack Completely**.
4. Duplicate the existing **Bull Boss New** GameObject in the hierarchy to serve as the cloning source, then deactivate the original.

---

## 2. Cloning Boss AI Configuration

Transfer components, scripts, and settings from the source boss to the spider using the toolkit cloning tool.

### Steps
1. Navigate to the top menu: **Tools > Boss AI Toolkit > Duplicate Enemy**.
2. Configure the tool parameters:
   * **Source Boss**: Drag in the duplicated `Bull Boss New` GameObject.
   * **Target Boss**: Drag in the unpacked `Spider` GameObject (rename it to **Spider Boss**).
   * **Target Avatar**: Select and assign the `Spider Avatar` from the project files.
3. Click **Start Cloning Configuration** and close the window upon completion.

---

## 3. Hierarchy & Visual GameObjects Transfer

Re-parent child GameObjects and attach effect origins to the spider rig.

Spider Boss (Root)
├── Spider Rig / Bones
│    └── Neck / Head Bone
│         └── Flamethrower Visual Effect Object
└── Projectiles / Effects (Transferred from Bull Boss)
├── Shockwave Effect
├── Stone / Rock Object
└── Teleportation Visual Effects

### Steps
1. Snap the position of **Spider Boss** to match **Bull Boss New**.
2. Move necessary child objects (effects, projectiles, stones) from the Bull Boss hierarchy to **Spider Boss**.
3. Attach the **Flamethrower** effect object to the spider's neck bone (`Spider Rig > Neck`).
4. Remove unneeded weapon GameObjects transferred from the Bull Boss.
5. Delete the empty Bull Boss source hierarchy from the scene.

---

## 4. Animator & Animation Replacement

Duplicate the controller and substitute animation clips using the Animator Clip Replacer tool.

### Step 4.1: Controller Setup
1. Duplicate the source Animator Controller asset in the Project window and rename it to **`Spider Boss Animator Controller`**.
2. Assign **Spider Boss Animator Controller** to the **Animator** component on **Spider Boss**.

### Step 4.2: Replacing Clips
1. Open **Tools > Boss AI Toolkit > Animator Clip Replacer**.
2. Assign the **Spider Boss Animator Controller**.
3. Replace the Bull Boss clips with corresponding Spider FBX clips:
   * **Idle** -> `Spider Idle`
   * **Walking/Movement** -> `Spider Crawl Backward` *(Set clip speed to `-1` in the Animator to make it walk forward)*
   * **Hit Reactions** -> Assign `Hit 1` to **hit reaction one** and **hit reaction two**.
   * Remove unused weapon state nodes (e.g., `Equipped Weapon`, `Unequipped Weapon`).
   * Uncheck **IK Pass** on the Animator layer if hand/foot IK is not required.

---

## 5. Dissolve & Teleportation Material Setup

Reconfigure skin mesh renderers and dissolve materials for teleportation and spawn/death FX.

### Steps
1. Select **Spider Boss** and expand the **Enemy Dissolve Controller** component.
2. Remove weapon dissolve entries from the array.
3. Configure skin dissolve entries:
   * **Skin Mesh Renderer**: Drag in the `Spider Rig Skinned Mesh Renderer`.
   * **Renderer Type**: Set to `Skinned Mesh Renderer`.
   * **Original Material**: Assign the default spider material.
   * **Dissolve Material**: Assign the spider-specific dissolve material.

---

## 6. Global Settings & Ability Adjustments

Fine-tune movement, rotation, and custom ability parameters for the spider model.

### Global & UI Parameter Tuning

| Parameter | Recommended Value | Description |
| :--- | :--- | :--- |
| **Rotation Speed** | `300` | Adjusts turning speed for spider movement. |
| **Smooth Look Rotation Delay** | `2.0` seconds | Delay window allowing player attacks before boss tracks. |
| **Rotate Spine Bone** | `Unchecked` | Disabled since the spider does not utilize a single spine pivot. |
| **Hit Interval (Min / Max)** | `2` / `2` seconds | Cooldown interval between hit reactions. |

### Teleportation Ability Tuning
1. Register custom clips using the **Animation Setup Tool**:
   * Add `Get In Ground` (Parameter Name: **`get in ground`**)
   * Add `Get Out Of Ground` (Parameter Name: **`get out of ground`**)
2. Under **Teleportation Ability**:
   * Set **Disappear Animation** to `get out of ground`.
   * Set **Appear Animation** to `get in ground`.
   * Enable **Spawn Behind Target**.
   * Assign teleportation particle effects and set **Idle Delay** to `0`.

### Flamethrower Ability Tuning
* Set **Rotation Mode** to **`Rotate Full Body`**.
* Assign the head/neck-mounted flamethrower particle origin.
* Set **Rotation Speed** to `50` and **Spine Rotation Speed** to `0`.

---

## 7. Hitbox Controller Setup

Configure manual hitboxes to deal damage during attack animations.

### Steps
1. Create a child GameObject named `Hitbox` under **Spider Boss**.
2. Add a **Capsule Collider** component, adjust its bounds over the spider's attack area, and check **Is Trigger**.
3. Add the **Hitbox** script component:
   * **Damage Value**: Set desired damage output.
   * **Owner**: Drag the **Spider Boss** reference.
   * **Team Member**: Assign the team member reference script.
   * **Activation Mode**: Set to **`Manual`**.
   * Check **Deactivate Hitbox On Hit** and **Deactivate Hitbox After Time**.
4. Open the Unity **Animation Window**, select attack clips (duplicate clips if read-only), and add animation events:
   * **Start of attack frame**: Call `HitboxController.ActivateHitbox()`.
   * **End of attack frame**: Call `HitboxController.DeactivateHitbox()`.

---

## 8. Verification Checklist

Before running tests in Play Mode, check the following configuration settings:

- [ ] **Cloned Configuration**: Settings cloned from source boss and avatar assigned.
- [ ] **Animator Assigned**: Duplicated `Spider Boss Animator Controller` assigned.
- [ ] **Forward Walk Animation**: Backward crawl animation speed set to `-1` in the Animator.
- [ ] **Hierarchy Re-parented**: Visual effects (flamethrower, ground slam) parented to the spider rig.
- [ ] **Dissolve Materials Mapped**: Skinned mesh renderer and spider dissolve materials linked.
- [ ] **Hitbox Events Configured**: Animation events set to trigger and deactivate hitboxes during attack animations.