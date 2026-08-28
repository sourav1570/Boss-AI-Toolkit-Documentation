# Meteor Strike

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/bwmy5xCcSEM"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This setup provides a comprehensive guide on setting up the **Throw Weapon Ability** on the **Bull Boss** entity using the Boss AI Toolkit. It also details the workflow for binding custom abilities to the AI system using custom scripts, handling weapon hierarchy setups, configuring trajectory arcs, and integrating custom animations.

---

## 1. Custom Ability Creation Workflow

The Boss AI Toolkit allows you to call functions from any custom script via the **Create Your Own Ability** option.

### Steps
1. Select the **Bull Boss New** GameObject in the scene hierarchy.
2. Expand the **Enemy Ability System** component in the Inspector.
3. Click **Add Ability Entry to Group**.
4. Set **Ability Type** to **Create Your Own Ability**.
5. Rename the ability name to **`Throw Weapon`**.
6. Click **Add Script** and assign/drag the **`Enemy Weapon Throw Ability`** component onto it.
7. Select the target method function: **`Activate Throw`**.
8. Set **Ability Lifetime** to `5` seconds (the ability will auto-complete after 5 seconds).
9. Adjust probabilities for isolated testing:
   * Set **Throw Weapon Probability** to `100%`.
   * Set all other ability probabilities to `0%`.

> **NOTE:** This workflow works for any custom script. Drag your script into the custom ability entry, select the function you want to execute, and the Boss AI system will invoke it during the combat cycle.

---

## 2. Animation Integration

Download or locate the throwing animation clip and bind it to the animator via the **Animation Setup Tool**.

### Steps
1. Expand the **Animation Setup Tool** on the **Bull Boss**.
2. Locate the **`Throw`** animation clip inside your project's animation directory (`Boss AI Toolkit -> Animations`).
3. Click **Add Animation** and drag the `Throw` clip into the slot.
4. Set the **Parameter Name** to `Throw`.
5. Click **Add to Animator**.
6. Return to the **Enemy Weapon Throw Ability** component and set **Throw Animation** to `Throw`.

---

## 3. Weapon Hierarchy & References Setup

Ensure the weapon GameObject hierarchy is organized and assigned properly to the `Enemy Weapon Throw Ability` script.

### Steps
1. Locate the spiky weapon attached to the boss's hand in the Hierarchy.
2. *(Optional Alignment)* Rename the root weapon container to **`Weapon`** and the mesh child to **`Weapon Mesh`**.
3. Select **Bull Boss** and inspect the **Enemy Weapon Throw Ability** component:
   * Drag the **Weapon** GameObject into the **Weapon to Throw** slot.
4. Verify core parameters:
   * **Weapon Detach Delay**: `0.75` seconds (delay before the weapon leaves the boss's hand toward the target).
   * **Idle Delay**: `1` second.
5. Set rotation axes during flight:
   * Enable rotation on desired axes (**X**, **Y**, **Z**).
   * Set the rotation speed values as needed (e.g., enable **Y** rotation for standard spinning motion).
   * **Return Rotation Duration**: `0.2` seconds.

---

## 4. Trajectory Arc Configurations

You can adjust the projectile flight path of the thrown weapon using horizontal and vertical arcs.

### Arc Configurations & Behavior

| Trajectory Type | Horizontal Arc Checkbox | Horizontal Distance | Vertical Arc Checkbox | Vertical Height | Resulting Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Direct / Straight Line** | Unchecked | `0` | Unchecked | `0` | The weapon travels in a direct, straight line toward the target position. |
| **Horizontal Curve** | Checked | `-8` (or `-6`) | Unchecked | `0` | The weapon curves sideways along a horizontal arc before hitting the target. |
| **Vertical Arc** | Unchecked | `0` | Checked | `4` | The weapon arcs upward into the air and drops down onto the target. |
| **3D Parabolic Arc** | Checked | `-6` | Checked | `3` | The weapon curves both sideways and vertically, creating a full 3D arc trajectory. |

---

## 5. Pre-Combat & Testing Setup

To efficiently isolate and test the Throw Weapon ability in Play Mode without delays:

### Steps
1. Select the **Bull Boss** GameObject.
2. Set **Pre-Combat Value** to `4` or `5` (this skips long pre-combat sequences).
3. Set **Min Attack Delay** and **Max Attack Delay** to `2` seconds for rapid ability looping during testing.
4. Enter **Play Mode** to verify the throw trajectory, impact timing, and return animation.

---

## 6. Verification Checklist

Before finalizing the setup, verify the following configuration settings:

- [ ] **Custom Ability Hook**: Ability Type set to `Create Your Own Ability` targeting `EnemyWeaponThrowAbility.ActivateThrow`.
- [ ] **Probabilities**: `Throw Weapon` = `100%`, all other abilities = `0%`.
- [ ] **Animator Binding**: `Throw` animation parameter added via Animation Setup Tool and assigned in the script.
- [ ] **Detach Timing**: `Weapon Detach Delay` set to `0.75s`.
- [ ] **Arcs**: Trajectory parameters configured according to the desired attack path.