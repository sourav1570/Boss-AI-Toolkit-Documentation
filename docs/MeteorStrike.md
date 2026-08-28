# Meteor Strike

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/WyJ2P5S2jVI"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This setup provides a comprehensive step-by-step guide for setting up the **Meteor Strike Ability** on the **Bull Boss** using the Boss AI Toolkit in Unity. It covers ability configuration, animation setup, prefab damage/hitbox configuration, particle fading optimization, and visual effects setup.

---

## 1. Combat Ability Configuration

Set up the Meteor Strike ability parameters in the **Enemy Ability System** and isolate the ability to facilitate testing.

### Steps
1. Select the **Bull Boss** GameObject in your scene hierarchy.
2. In the Inspector, navigate to the **Enemy Ability System** component and add a new ability to the group.
3. Set the **Ability Type** to **Meteor Strike**.
4. Adjust probabilities for testing isolation:
   * Set **Chase and Attack Probability** (and other abilities) to `0%`.
   * Set **Meteor Strike Probability** to `100%`.
5. Configure target and animation parameters:
   * **Look Mode**: Set to `Target`.
   * **Idle Animation**: Set to `Idle`.
   * **Idle Delay**: Set to `1` second.

---

## 2. Magic Area Animation Setup

If the `magic area` animation is not currently present on your animator controller, use the **Animation Setup Tool** to add it.

### Steps
1. In the project folder, locate the animation clip named **`spell_01`** inside `Boss AI Toolkit -> Animations`.
2. Select the **Bull Boss** GameObject.
3. Open the **Animation Setup Tool**.
4. Add the **`spell_01`** animation clip and rename its parameter to **`magic area`**.
5. Click **Add to Animator Controller**.
6. Return to the **Meteor Strike** ability parameters in the Inspector and select **`magic area`** from the magic animation dropdown list.

---

## 3. Visual FX (Lightning Aura) Integration

Assign an aura effect to play on the boss during the ability casting phase.

### Steps
1. Search for **`lightning aura`** in the Project window and add it under the **Bull Boss** hierarchy.
2. Ensure the `lightning aura` GameObject is **deactivated** by default in the scene hierarchy.
3. Select the **Bull Boss** GameObject.
4. Drag and drop the `lightning aura` GameObject into the **Effects** field under the Meteor Strike ability settings.

---

## 4. Meteor Prefab & Hitbox Setup

Prepare the **Meteor AOE** prefab with physics colliders, a custom hitbox script, and team detection to properly damage the player.

### Step 4.1: Hitbox & Physics Setup
1. Search for the **`Meteor AOE`** prefab inside the `Hovl Studio` folder and drag it into the scene hierarchy.
2. Right-click the **Meteor AOE** object -> **Create Empty** and name it **`Hitbox`**.
3. Select **Hitbox** and click **Add Component** -> **Hitbox**:
   * **Auto Activate On Start**: Checked.
   * **Activation Delay**: `0.3` seconds.
   * **Damage**: `1`.
   * **Continuous Damage**: Checked.
   * **Damage Interval**: `0.25` seconds.
   * **Deactivate Hitbox On Hit**: Unchecked.
   * **Deactivate Hitbox After Time**: Unchecked.
4. Add a **Sphere Collider** to the **Meteor AOE** parent prefab:
   * Adjust the sphere size to fit the intended area of effect.
   * Check **Is Trigger**.

### Step 4.2: Team Member Component Setup
1. Select **Meteor AOE** and click **Add Component** -> **Team Member**.
2. Set **My Body Part Target** to `Meteor Strike` (or the root Meteor AOE object).
3. Copy the exact **Team Name** string from the **Bull Boss** and paste it into the **Team Member** component on the meteor.
4. Check **Compare Enemy**.
5. Drag and drop the **Meteor AOE** GameObject into the **Owner** reference slot.

### Step 4.3: Apply Changes to Prefab
1. Click **Overrides -> Apply All** at the top of the Inspector on **Meteor AOE** to save changes.
2. Delete the temporary **Meteor AOE** instance from the scene hierarchy.

---

## 5. Spawning & Timing Parameters

Configure how many meteors drop, their lifetime, and their spatial distribution around the player target.

### Steps
Select the **Bull Boss** GameObject and configure the following parameters under **Meteor Strike**:

| Parameter | Recommended Value | Description |
| :--- | :--- | :--- |
| **Spawn From Targets** | Checked | Spawns meteors relative to player location. |
| **Spawn Range** | `20` meters | Maximum radius around target where meteors land. |
| **Distance Between Spawned Objects** | `6` meters | Minimum spatial separation between individual meteors. |
| **Prefab Slot** | `Meteor AOE` Prefab | The configured meteor prefab. |
| **Spawn Count** | `5` | Total number of meteors spawned per ability. |
| **Delay Between Spawn** | `1` second | Delay before initiating the spawn wave. |
| **Delay Between Each Spawn** | `1` second | interval between each meteor dropping. |
| **Spawned Objects Lifetime** | `10` seconds | Duration before the meteor prefab object is destroyed. |

---

## 6. Particle Auto-Fade Optimization

To prevent particle looping bugs (where 5-second particle systems restart when `Spawned Objects Lifetime` is set to 10 seconds), configure particle looping and smooth fade-out behavior.

### Step 6.1: Particle Duration Modification
1. Drag the **`Meteor AOE`** prefab back into the scene.
2. Select all child particle systems attached to the meteor asset.
3. Change the **Duration** setting on all child particle components from `5` seconds to **`1` second** so particles spawn continuously without abruptly looping over long durations.

### Step 6.2: Adding Particle Auto Fade Component
1. Select the root **Meteor AOE** object and click **Add Component** -> **Particle Auto Fade**.
2. Set **Total Lifetime** to **`10` seconds** (matching the `Spawned Objects Lifetime`).
3. Set **Fade Duration** to **`5` seconds** (allowing a 5-second active phase followed by a 5-second smooth fade out).
4. Lock the Inspector window.
5. Highlight all child particle system components under **Meteor AOE** and drag them into the **Particle References** array field.
6. Click **Overrides -> Apply All** to update the prefab asset.
7. Unlock the Inspector and remove the instance from the hierarchy.

---

## 7. Verification Checklist

Before running the scene to test the Meteor Strike ability, verify the following:

- [ ] **Probabilities**: Meteor Strike probability is `100%`, and other abilities are `0%`.
- [ ] **Animation**: `magic area` animation clip is selected.
- [ ] **VFX State**: `lightning aura` is disabled in the hierarchy and assigned to the **Effects** field.
- [ ] **Collider**: A **Sphere Collider** with **Is Trigger** checked is attached to `Meteor AOE`.
- [ ] **Damage Settings**: `Continuous Damage` is enabled with `0.25s` interval and `0.3s` activation delay.
- [ ] **Fade Sync**: `Particle Auto Fade` total lifetime (`10s`) matches `Spawned Objects Lifetime` (`10s`).