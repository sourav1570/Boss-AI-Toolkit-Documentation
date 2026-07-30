# Ground Slam

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/Avkfs1DPA7c"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>


This guide walks through configuring the **Ground Slam** combat ability for the `Bull Boss New` AI entity. This includes setup for ability probability, ground slam animations, shockwave visual effects (VFX), area-of-effect (AoE) damage/knockback triggers, and event-driven camera and camera shake effects.

---

## 1. Overview & Ability Configuration

Add the Ground Slam ability alongside existing abilities (like Melee Attack) within the same distance range group.

### Steps
1. Select the **Bull Boss New** GameObject in the hierarchy.
2. Locate the **Enemy Ability System** component.
3. Under the existing distance range subgroup (`0 to 20` meters):
   * Click **Add Ability Entry Group** and select **Ground Slam**.
4. Adjust the **Melee Attack Probability** to `0%` temporarily during testing so the boss only uses the Ground Slam ability.
5. Set the **Slam Attack Range** to `10`.

---

## 2. Animation Setup

Import and bind the Ground Slam animation to the animator component.

### Steps
1. In the **Project** panel, locate the `Ground Slam` animation asset (found under `Animations`).
2. Expand the **Animation Setup Tool** on the `Bull Boss New` inspector.
3. Drag and drop the `Ground Slam` animation asset into the tool.
4. Name the animation entry `Ground Slam`.
5. Click **Add to Animator**.
6. Navigate back to the **Enemy Ability System**, click the **Ground Slam** entry, and assign the newly added `Ground Slam` animation state.

---

## 3. Shockwave Effect (VFX) & Damage Area Setup

Configure the visual shockwave effect and the corresponding collision detection volume.

### 3.1 Importing and Scaling the Shockwave
1. Import the free **Quick Effects Volume 1 (Built-in Render Pipeline)** asset package (by Gabriel Aguiar).
2. In the **Project** window, search for `Shockwave_FX`.
3. Drag and drop `Shockwave_FX` into the hierarchy as a child or placed scene object.
4. Adjust its transform settings:
   * **Position and Scale**: Place slightly below ground level and scale it
   * Ensure local position aligns properly on the X and Z axes (`0, 0`).
5. In the Particle System settings, ensure **Looping** is **unchecked**.

### 3.2 Setting Up the Damage Area & Hitbox
1. Right-click the `Shockwave_FX` GameObject -> **Create Empty** and name it `Damage Area`.
2. Add a **Sphere Collider** to `Damage Area`:
   * Set **Radius / Scale** to `2`.
   * Check **Is Trigger**.
3. Add a **Hitbox** component to `Damage Area`:
   * **Damage**: `10`
   * **Owner**: Drag and drop `Bull Boss New`.
   * **Compare Enemy**: Checked (assign `Bull Boss New`).
   * **Auto Activate on Start**: Checked.
   * **Activation Delay**: `0.4` or `0.5` seconds.
   * **Deactivate Hitbox on Hit**: Checked.
   * **Deactivate Hitbox After Time**: Checked (Set duration to `3` seconds).

---

## 4. Binding VFX to Boss Ability Parameters

Link the shockwave object and activation timing back to the boss AI system.

### Steps
1. Select `Bull Boss New` in the hierarchy.
2. In the **Ground Slam** ability settings, assign parameters:
   | Parameter | Recommended Value | Description |
   | :--- | :--- | :--- |
   | **Ground Slam Effect** | Assign `Shockwave_FX` | The visual game object spawned/activated. |
   | **Effects Trigger Delay** | `1.7` to `1.8` seconds | Delay after animation starts before activating VFX. |
   | **Particles Fade Time** | `3` seconds | Duration before particles fade out completely. |
   | **Delay Before Idle** | `2` seconds | Wait time after slam before returning to idle. |
3. **Deactivate** the `Shockwave_FX` GameObject in the hierarchy so it is disabled by default.

---

## 5. Knockback Trigger Setup

Replace the simple Hitbox with a **Knockback Trigger** to apply force and damage to the player simultaneously.

### Steps
1. Select the `Damage Area` object under `Shockwave_FX`.
2. **Remove** or **Disable** the standard `Hitbox` component (if using Knockback instead).
3. Click **Add Component** and search for `Knockback Trigger`.
4. Configure the settings:
   * **Collision Damage**: `10`
   * **Enemy Colliders**: Drag and drop the boss's colliders (e.g., main body collider and weapon collider) into the array so self-collision is ignored.

---

## 6. Camera Shake Trigger & Event Listener

Add visual impact to the ground slam by triggering a camera shake when the shockwave activates.

### 6.1 Adding the Camera Shake Trigger
1. Right-click on `Bull Boss New` -> **Create Empty** and name it `Camera Shake Trigger`.
2. Add the `Camera Shake Trigger` script component.
   > **Note:** Ensure a valid `Camera Shake` script exists on your Main Camera or Scene Manager in the hierarchy.
3. Configure the trigger settings:
   * **Return Duration**: `0.3`
   * **Min Rotation**: X = 0, Y = 0, Z = -0.3
   * **Max Rotation**: `X = 0, Y = 0, Z = 0.3

### 6.2 Binding to Ability Event Listener
1. Select `Bull Boss New` and open the **Enemy Ability System**.
2. Under the Ground Slam configuration, expand **Add Event Listener**.
3. Select the event **`On Ground Slam Effect Activated`**.
4. Click the **`+`** sign to add an action:
   * **Target**: Drag and drop the `Camera Shake Trigger` GameObject.
   * **Function**: Select `CameraShakeTrigger -> TriggerShake`.

---

## 7. Testing & Fine-Tuning Checklist

Verify all settings before playing:

- [ ] `Shockwave_FX` GameObject is disabled in the hierarchy.
- [ ] Particle System **Looping** is turned off.
- [ ] `Effects Trigger Delay` is fine-tuned so the visual wave matches the exact frame the boss hits the ground (~1.7s–1.8s).
- [ ] `Knockback Trigger` correctly deals damage and applies impulse to the target player upon collision.
- [ ] `Camera Shake Trigger` fires on the `On Ground Slam Effect Activated` event callback.