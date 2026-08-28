# Spit Attack

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/XpQqDi5GFB4"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This part guide on setting up the **Spit Attack Ability** on the **Bull Boss** using the Boss AI Toolkit in Unity. It covers ability configuration, particle system adjustments, trigger hitbox positioning, and animation timing.

## 1. Initial Ability Configuration

Set up the Spit Attack parameters inside the **Enemy Ability System** and adjust combat range and probability for isolated testing.

### Steps
1. Select the **Bull Boss New** GameObject in the scene hierarchy.
2. Expand the **Enemy Ability System** component and locate the active phase group (e.g., Phase 0).
3. Set **Min Distance** to `0` and **Max Distance** to `10` meters.
4. Click **Add Ability Entry to Group**.
5. Set **Ability Type** to **Spit Attack**.
6. Set **Spit Attack Probability** to `100%` for isolated testing.
7. Configure core settings:
   * **Look Mode**: `Target`
   * **Spit Attack Range**: `10` meters

---

## 2. Animation Binding

Bind the spit animation clip to the boss using the **Animation Setup Tool**.

### Steps
1. Expand the **Animation Setup Tool** on the **Bull Boss**.
2. Locate and select the **Spit** animation clip from your project directory.
3. Click **Add Animation** and drag the `Spit` clip into the field.
4. Set the parameter name to `Spit`.
5. Click **Add to Animator**.
6. Return to the **Enemy Ability System** -> **Spit Attack** settings and select **`Spit`** under **Spit Animation**.

---

## 3. VFX & Hitbox

Create the visual particle effect combined with a trigger hitbox to deal damage within the spit cone.

### Step 3.1: Particle FX Setup
1. Search for the prefab `Sparks Explode Green` (located in `Hovl Studio Magic Effects`).
2. Drag and drop it as a child under the **Bull Boss New** GameObject.
3. Rename the object to **`Spit Attack Effects`**.
4. Configure particle parameters:
   * **Duration**: `1` second
   * **Looping**: Uncheck (disable continuous looping)
   * **Scale**: `0.8` on X, Y, and Z
   * **Shape**: Set to **Cone**
   * **Rotation**: `30°` on X
   * **Angle**: `35°`
   * **Radius**: `2`
   * **Arc**: `180°`
5. Unpack the prefab completely in the Hierarchy.

### Step 3.2: Damage Hitbox Setup
1. Right-click **Spit Attack Effects** -> **Create Empty** and name it **`Hitbox`**.
2. Position the `Hitbox` object forward within the cone area where the spit effect lands.
3. Click **Add Component** -> **Sphere Collider**:
   * Check **Is Trigger**.
   * Adjust radius size to cover the intended damage cone area.
4. Click **Add Component** -> **Hitbox**:
   * **Damage**: `10`
   * **Owner**: Drag the **Bull Boss New** GameObject.
   * **Compare Enemy**: Checked
   * **Script Team Member**: Drag the boss's `Team Member` script reference into this slot.
   * **Activation Mode**: `Auto Activate On Start`
   * **Activation Delay**: `0` seconds
   * Check both default deactivation checkboxes.
5. Deactivate the **`Spit Attack Effects`** GameObject in the scene hierarchy by default.

---

## 4. Activation Delay & Particle Timing

Configure timing delays so the particle effect and hitbox align naturally with the spit animation keyframes.

### Steps
Select the **Bull Boss New** GameObject and set the following parameters under **Spit Attack**:

| Parameter | Value | Description |
| :--- | :--- | :--- |
| **Spit Attack Effects** | `Spit Attack Effects` | Reference to the child VFX/Hitbox container. |
| **Spit Attack Range** | `10` meters | Maximum distance for ability execution. |
| **Spit Effect Activation Delay** | `1.6` seconds | Delay during animation before enabling particles and hitbox. |
| **Spit Effect Particles Fade Time** | `1.2` seconds | Active particle emission and duration before fading. |
| **Delay Before Idle** | `1` second | Wait duration after ability completion before switching to idle. |
| **Idle Animation** | `Idle` | Resting state animation clip. |

---

## 5. Verification Checklist

Before testing the ability in Play Mode, check the following configuration settings:

- [ ] **Range Limits**: Min/Max distance set to `0 - 10` meters to trigger close to the target.
- [ ] **Probability**: Spit Attack set to `100%`.
- [ ] **Animation Bound**: `Spit` parameter registered in Animator and assigned in the ability slot.
- [ ] **VFX Active State**: `Spit Attack Effects` is **deactivated** in the hierarchy by default.
- [ ] **Hitbox Ownership**: Hitbox `Owner` linked to **Bull Boss New** with `Compare Enemy` checked.
- [ ] **Particle Alignment**: Cone shape, angle (`35°`), radius (`2`), and scale (`0.8`) verified in forward direction.