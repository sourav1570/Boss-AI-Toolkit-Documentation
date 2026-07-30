# Non-Combat Behavior

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/MYlp7Vm2hOc"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This guide covers how to set up non-combat behaviors (Idle, Wander, and Patrol) for your enemy entities using downloaded Mixamo animations, configuring animation parameters, and setting up patrol route points.

---

## 1. Importing & Preparing Animations

To set up non-combat movement, download standard character animations from Mixamo.

### Step 1: Download Required Animations
1. Go to Mixamo and download the following animations with the skin for Unity:
   * **Mutant Walking** (for movement/patrolling/wandering) 
   * **Mutant Breathing Idle** (for idle standing)

### Step 2: Configure Animation Import Settings
1. In your Unity project, create a folder named `Mixamo Animations` and drag both downloaded FBX files inside.
2. Select both animation files, navigate to the **Rig** tab, and change the **Animation Type** to **Humanoid**.
3. Select the **Breathing Idle** clip and configure these settings:
   * Set **Base Upon** to **Original**.
   * Check **Bake Into Pose**.
   * Check both **Loop Time** and **Loop Pose**.
   * Click **Apply**.
4. Repeat the same settings (`Original`, check **Bake Into Pose**, **Loop Time**, and **Loop Pose**) for the **Walking** animation clip, then click **Apply**.

---

## 2. Assigning Animations to the Animator Controller

1. Select your target boss (e.g., `Bull Boss New`) and locate the **Animation Setup Tool** component attached with the Enemy.
2. Drag and drop the boss's Animator Controller into the controller slot.
3. Drag the `Mixamo Animations` folder into the **Custom Folder** field.
4. Click **Add Animation** twice to create slots for both clips.
5. Drag your idle and walking clips into the slots, naming them `idle` and `walking` respectively.
6. Click **Add to Animator Controller** to automatically generate and integrate the states.
7. Click **Optimize Animation Clips** to separate the animation data from the FBX files (you can then delete the source FBX models to reduce project size). Reassign the standalone clips to the idle and walking slots.

---

## 3. Disabling Player Detection for Testing

To isolate and test non-combat behaviors without triggering combat behaviour:
1. Expand the **Enemy Ability System** on `Bull Boss New`.
2. Lower the **Detection Radius** to `1`.
3. Scroll down to the **Team Member** script and also set its **Detection Radius** to `1` so the enemy remains unaware of the player.

---

## 4. Configuring Non-Combat Behavior Modes

Expand the **Non-Combat Behavior** section on your boss entity and choose between three primary behavior modes:

### Mode A: Idle
1. Set the **Behavior Mode** to **Idle**.
2. Select your imported `idle` animation clip from the animation dropdown.
3. Press **Play** to test; the boss will remain stationary playing the idle loop.

> **Smoothing Transitions note**: If the enemy snaps abruptly when transitioning states, select the Animator window, open the **Any State** transition settings, and increase the **Transition Duration** (e.g., from `0.1` to `0.5` or `1.0`) for smoother blending.

### Mode B: Wander
1. Set the **Behavior Mode** to **Wander**.
2. Configure wander parameters:
   * **Store Initial Position**: Recommended to keep checked so the wander radius calculates relative to spawned position.
   * **Wander Radius**: Set the distance limit (e.g., `15`).
   * **Min/Max Wait Time**: Set delay between movements (e.g., `2` to `3` seconds).
   * **Move Speed**: Set movement velocity (e.g., `2`).
   * **Stopping Distance**: Set to `0.3`.
   * **Animations**: Select `walking` to **Move Animation** and `idle` to **Idle Animation**.

### Mode C: Patrol
1. Set the **Behavior Mode** to **Patrol**.
2. Set **Move Animation** to `walking`.
3. **Set up Patrol Points**:
   * Right-click `Bull Boss New` in the hierarchy and create empty GameObjects or 3D Cubes as markers (remove box colliders from visual cubes and disable their Mesh Renderers if desired).
   * *Tip*: Attach an `Unparent Game Object` script to the patrol point cubes so they do not move when the boss moves.
   * Rename them sequentially (e.g., `Patrol Point 1`, `Patrol Point 2`, etc.).
4. Drag your created patrol point objects into the **Patrol Points** list on the boss component.
5. **Order Control**: 
   * Leave **Random Order** unchecked for sequential pathing.
   * Check **Random Order** if you want the boss to select subsequent patrol destinations randomly.