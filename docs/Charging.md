# Charging Attack

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/QHamIKxYqdc"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>


This guide details how to configure the **Charging Attack** combat ability for the `Bull Boss New` AI entity. It covers movement parameters, animation configuration, damage/knockback colliders, manual camera shake triggers, and animation event-driven footstep audio.

---

## 1. Overview & Ability Configuration

Add the Charging Attack ability to the boss's Phase 0 ability list and configure its target tracking and movement speeds.

### Steps
1. Select the **Bull Boss New** GameObject in the hierarchy.
2. Scroll down and expand the **Combat Attack System** component.
3. Under **Phase 0**, click **Add Ability Entry to Group**.
4. Set **Ability Type** to **Charging Attack**.
5. Set **Charging Attack Probability** to `100`.
6. Set all other previously created ability probabilities to `0` for focused testing.
7. Configure movement parameters:
   * **Move Speed**: `5`
   * **Look Mode**: `Target`
   * **Move Towards Target**: Checked
   * **Should Apply Root Motion**: Unchecked
   * **Idle Delay**: `0`

---

## 2. Animation Import & Setup

Download the run animation, set up humanoid rigging, and bake it.

### 2.1 Importing & Rigging Animation
1. Go to Mixamo, search for the **`Mutant Run`** animation, and download it for **Unity (With Skin)**.
2. Import the downloaded `.FBX` file into Unity.
3. Select the imported asset and set **Rig Type** to `Humanoid`, then click **Apply**.
4. Open the **Animation** tab in the inspector:
   * Check **Loop Time**.
   * Check **Loop Pose**.
   * Set **Based Upon** to `Original`.
   * Click **Apply**.

### 2.2 Binding to Boss Animator
1. Select **Bull Boss New** and locate the **Animation Setup Tool** in the inspector.
2. Drag and drop the `Mutant Run` clip into the animation slot.
3. Set the parameter name/label to **`Run`**.
4. Click **Add to Animator** and click **Optimize Animation Clips**.
5. *(Optional)* Delete the imported Mixamo FBX asset from the project folder.
6. In the **Charging Attack** ability parameters on `Bull Boss New`, set **Move Animation** to `Run`.

---

## 3. Charging Collider & Knockback Trigger

Create a dedicated trigger volume to deal contact damage and knock back the player when hit during the charge.

### Steps
1. Right-click **Bull Boss New** -> **Create Empty** and name it **`Charging Collider`**.
2. Add a **Capsule Collider** component:
   * Adjust radius to fit the front profile of the boss.
   * Check **Is Trigger**.
3. Add the **Knockback Trigger** script component.
4. Assign excluded colliders to avoid self-collision:
   * Lock the Inspector window.
   * Drag the main **Bull Boss New** collider, the weapon's **Damage Point** collider, and the **Charging Collider** itself into the **Enemy Colliders** array.
   * Unlock the Inspector.
5. Set **Collision Damage** to `10`.
6. Ensure **Destroy on Hit** is **Unchecked**.
7. Assign `Charging Collider` to the **GameObject to Activate** field in the **Charging Attack** ability inspector.
8. **Deactivate** the `Charging Collider` GameObject by default in the hierarchy.

---

## 4. Distance & Forward Drive Behavior

Configure how close the boss gets before locking its trajectory and rushing forward.

### Steps
1. In the **Charging Attack** ability inspector, set parameters:
   * **Stop Chasing Target Distance**: `5`
   * **Move Forward After Stop Chasing**: Checked
   * **Forward Distance**: `20`

> **Behavior Description:** When the player distance is 5 meters, the boss stops rotating to face the player and locks into driving straight forward for an additional 20 meters. Setting the chase stop distance to `0` would make the boss continuously move towards the player.

---

## 5. Camera Shake Setup (Manual Triggering)

Configure a camera shaker trigger that activates when the charge begins and stops when the charge ends.

### 5.1 Manual Shaker Configuration
1. Duplicate your existing `Camera Shake Trigger` GameObject.
2. Rename the new object to **`Camera Shake Trigger Manual`** (and rename the previous automated one to `Camera Shake Trigger Automatic` for clarity).
3. On `Camera Shake Trigger Manual`, set **Control Mode** to `Manual`.
4. Set **Oscillation Speed** to `3`.
5. Set **Return Duration** to `2`.

### 5.2 Event Hook Binding
1. Select **Bull Boss New** and scroll to the **Event Hook Listener** section.
2. Add two event hooks:
   * **Hook 1**: Select Event **`On Ability Start`**.
     * **Target**: Drag `Camera Shake Trigger Manual`.
     * **Function**: Select `CameraShakeTrigger -> TriggerShake`.
   * **Hook 2**: Select Event **`On Run Stopped`**.
     * **Target**: Drag `Camera Shake Trigger Manual`.
     * **Function**: Select `CameraShakeTrigger -> StopShake`.

---

## 6. Footstep Audio via Universal Sound Player

Sync movement audio to exact run animation frames using Animation Events.

### Steps
1. Select **Bull Boss New** and locate the **Universal Sound Player** component.
2. Assign footstep clips (e.g., `Gravel Step` or `Mud Step`).
3. Set sound properties:
   * **Volume**: `1`
   * **Is 3D Sounds**: Checked
   * **Max Distance**: `20`
4. Copy the Action Name corresponding to the footstep audio entry.
5. Open **Window -> Animation -> Animation** with `Bull Boss New` selected.
6. Select the **`Run`** clip from the animation dropdown.
7. Add Animation Events at the exact frames where the boss's feet hit the ground:
   * **Function**: Select `UniversalSoundPlayer.PlayAudioAction`.
   * **String Parameter**: Paste the footstep Action Name.

---

## 7. Testing & Verification Checklist

- [ ] **Probabilities**: Charging Attack set to `100%`, all other abilities set to `0%`.
- [ ] **Collider State**: `Charging Collider` is deactivated by default in the hierarchy.
- [ ] **Self Collision**: Enemy Colliders array includes boss body, weapon point, and charging collider.
- [ ] **Camera Shake**: Shake starts automatically on `On Ability Start` and stops on `On Run Stopped`.
- [ ] **Audio Sync**: Footstep sounds play in time with the running animation frames via the Universal Sound Player.