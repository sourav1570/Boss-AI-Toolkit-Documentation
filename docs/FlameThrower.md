# Flamethrower

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/DMyEbaRE3YQ"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This guide details how to configure the **Flamethrower** combat ability for the `Bull Boss New` AI entity It covers importing and trimming animations, IK layer settings, parenting particle effects, setting up continuous hitbox damage, and attaching audio sources

---

## 1. Overview & Ability Configuration

Add the Flamethrower ability to the boss's active ability entry group and adjust its probability for testing

### Steps
1. Select the **Bull Boss New** GameObject in the hierarchy
2. Open the **Enemy Ability System** component
3. Set the probability of other abilities (e.g., **Ground Slam**) to `0%` to focus on testing the Flamethrower
4. Click **Add Ability Entry Group** and set the ability type to **Flamethrower**
5. Set **Rotation Mode** to `Rotate Only Upper Body`
6. Set **Flamethrower Probability** to `100%`

---

## 2. Animation Import, Trimming & Animator Setup

Download the required animation asset from Mixamo, optimize it, and bind it to the animator state

### 2.1 Importing & Trimming Animation
1. Go to Mixamo, search for the **`Yelling`** clip (specifically `Yelling Out`), and download it for **Unity**
2. Import the downloaded `.FBX` file into your project folder (e.g., `Mixamo Animations`)
3. Select the file in the **Project** view and change **Rig Type** to `Humanoid`, then click **Apply**
4. Open the **Animation** tab in the inspector:
   * Trim the start and end of the clip so only the core roaring/yelling duration remains
   * Set **Loop Time** to Checked
   * Set **Based Upon** to `Original` and click **Apply**

### 2.2 Adding to Boss Animator
1. Select **Bull Boss New** and expand the **Animation Setup Tool**
2. Drag and drop the trimmed `Yelling Out` clip into the tool and rename it to **`Roar`**
3. Click **Add to Animator** and **Optimize Animation Clip**
4. *(Optional)* Delete the original `Yelling Out` FBX file
5. Open the **Animator Window**:
   * Select the **`Roar`** state node and set **Speed** to `0.2`
   * Select the transition from **Any State -> Roar** and change **Transition Duration** to `0.4`
6. Navigate back to the **Enemy Ability System** on `Bull Boss New` and assign **`Roar`** as the animation clip for the Flamethrower ability

> **Important (Upper Body Tracking):** In the **Animator Window**, switch to the **Layers** tab and check the **IK Pass** checkbox This ensures the boss's upper body dynamically rotates to track the target while performing the ability

---

## 3. Particle Effect & Bone Placement

Attach the visual particle effect to the boss's head bone.

### Steps
1. In the **Project** window, search for the **`Flamethrower Loot`** particle prefab
2. Drag `Flamethrower Loot` into the scene hierarchy
3. In the hierarchy of `Bull Boss New`, expand the bone hierarchy:  
   `Bull Boss New -> Neck -> Head`
4. Drag and drop `Flamethrower VFX` to make it a direct child of the **`Head`** bone
5. Adjust the local position/rotation of the particle effect to align with the head  
6. **Deactivate** the `Flamethrower VFX` GameObject by default

---

## 4. Damage Area & Hitbox Setup (Continuous Damage)

Create an area-of-effect collider to deal continuous damage to the player during the flamethrower attack

### 4.1 Creating the Damage Area
1. Right-click the `Flamethrower VFX` GameObject -> **Create Empty** and name it **`Damage Area`**
2. Add a **Capsule Collider** component:
   * Set **Direction / Axis** to `Z-Axis`
   * Scale and shape the collider to match the length and spread of the flame cone
   * Check **Is Trigger**

### 4.2 Configuring the Continuous Hitbox
1. Add a **Hitbox** component to the `Damage Area` GameObject
2. Configure the properties:
   * **Damage**: `1`
   * **Owner**: Drag and drop `Bull Boss New`
   * **Compare Enemy**: Checked (Assign `Bull Boss New`)
   * **Activation Mode**: `Auto Activate On Start`
   * **Activation Delay**: `3` seconds
   * **Continuous Damage**: Checked
   * **Damage Interval**: `0.25` seconds *(Deals 1 damage every 0.25 seconds)*

---

## 5. Linking Ability Parameters

Assign the particle object and timing configuration back to the boss ability settings

### Steps
1. Select `Bull Boss New` in the hierarchy
2. In the **Flamethrower Ability Group**, configure the following:

| Parameter | Recommended Value | Description |
| :--- | :--- | :--- |
| **Effect** | Assign `Flamethrower VFX` | Particle object activated during ability |
| **Is Particle Effect** | Checked | Tells system to handle object as a particle |
| **Effect Delay** | `1` second | Delay after animation starts before activating flames |
| **Ability Lifetime** | `10` seconds | Total duration the flamethrower stays active |
| **Idle Delay** | `1` second | Delay before returning to idle after ability completes |

---

## 6. Sound Setup (Optional)

Add continuous loop audio for the flames

### Steps
1. Select the `Flamethrower VFX` GameObject in the hierarchy
2. Right-click -> **Create Empty** (or directly click **Add Component**) and select **Audio Source**
3. Assign your flamethrower sound effect clip to the **Audio Clip** field
4. Check **Play On Awake**
5. Check **Loop**
   > Since the audio source is a child of the `Flamethrower VFX` object, the sound automatically plays when the particle effect is enabled and stops when disabled

---

## 7. Testing & Verification Checklist

- [ ] **IK Pass**: Checked in the Animator Layer settings (enables body tracking while flaming)
- [ ] **Flamethrower Object**: Disabled/Deactivated in hierarchy by default
- [ ] **Continuous Hitbox**: `Continuous Damage` box checked with proper `Damage Interval`
- [ ] **Targeting Behavior**: When player walks behind the boss, the boss stops the ability, turns to face the player, and resumes attacking