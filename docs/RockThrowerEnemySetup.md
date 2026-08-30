# Rock Thrower Enemy Setup

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/Lm71Jn98AKc"  
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This setup provides a guide for setting up a ranged **Rock Thrower Enemy** using the Boss AI Toolkit in Unity. It covers FBX model preparation, configuration cloning, binding hand bone sockets for pickup animations, arc projectile setup, and fixing attack loop behaviors.

---

## 1. Initial Model Preparation

### Steps
1. Drag the target 3D stone enemy model into the scene hierarchy.
2. Assign the character material to the mesh renderer.
3. Remove any pre-existing **Animator** component from the model.
4. Right-click the model GameObject and select **Prefab > Unpack Prefab Completely**.
5. Copy transform position values from the template `Rock Thrower Enemy` prefab and paste them onto the new model.
6. Rename the model GameObject to **`Stone Enemy New`**.

---

## 2. Configuration Cloning

Duplicate components, scripts, and hitboxes from the template prefab onto the new model.

### Steps
1. Navigate to top menu: **Tools > Boss AI Toolkit > Duplicate Enemy**.
2. Configure settings:
   * **Source Boss**: Drag in the template `Rock Thrower Enemy` prefab.
   * **Target Boss**: Drag in the newly prepared `Stone Enemy New` GameObject.
   * **New Boss Name**: Set to `Stone Enemy New`.
   * **Target Avatar**: Drag in the model's Avatar asset from the Project folder.
   * **Create New Animator Controller Asset**: Uncheck (reuses template animator clips).
   * **Add Weapon**: Uncheck.
3. Click **Start Cloning Configuration** and close the wizard.
4. Deactivate the original template prefab in the scene hierarchy.

---

## 3. Core Component & Target Mapping

Ensure player attacks can register collisions against the enemy model.

### Steps
1. Select **Stone Enemy New** in the hierarchy.
2. Under **Team Member**:
   * **My Body Part To Target**: Assign the enemy's root mesh object reference so player hitboxes can target.
3. Under **Enemy Ability System > Global Settings**:
   * **Use Rotation Animations**: Uncheck (if using standard rotation).
   * **Rotate Spine**: Uncheck.

---

## 4. Spawner & Hand Socket Setup

Set up the world location where rocks spawn and map the right-hand bone socket so pickup animations hold the rock accurately.

### Steps
1. Create an empty child GameObject under `Stone Enemy New` named **`Spawn Point`**.
2. Match position transform values from the template's spawn point (ground position near the feet).
3. Select **Stone Enemy New** and expand **Enemy Ability System > Combat Attack System**.
4. Locate the **Projectile Attack** ability settings:
   * **Spawn Point**: Assign the `Spawn Point` transform.
   * **Projectile Parent**: Assign the **`Right Hand`** bone transform.
     * *Purpose:* Parenting the spawned rock to the right hand bone ensures the rock attaches to the hand during the pickup animation before being thrown.

---

## 5. Combat Attack & Ability Loop Configuration

Configure ranged engagement limits and projectile counts to ensure range checks execute properly.

### Combat Attack System

| Parameter | Recommended Value | Description |
| :--- | :--- | :--- |
| **Phase 0 Health Range** | `0 - 100` | Health threshold for Phase 0 behavior. |
| **Distance Range** | `5 - 200` meters | Ability only triggers when the target is between 5m and 200m away. |
| **Projectile Count** | `1` | Controls how many rocks are thrown per ability execution cycle. |
| **Cycle Mode** | `Restart Cycle` | Restarts ability cycle after cooldown completes. |
| **Min / Max Attack Delay** | `1` second | Cooldown time after ability completion before re-evaluating target distance. |
| **Power-up Animation** | `Pick` | Animation clip played while retrieving the rock from the ground. |
| **Throw Animation** | `Throw` | Animation clip played when launching the projectile. |

> **NOTE:** If `Projectile Count` is set to a high number (e.g., `30`), the enemy will ignore the minimum distance limit (5m) and continuously throw rocks at close range until all 30 projectiles are fired. Setting **`Projectile Count = 1`** forces the AI to finish the ability cycle after every single throw, allowing it to correctly re-check if the player has entered melee range (< 5m).

---

## 6. Rock Projectile & Damage Setup

Configure the rock projectile object to travel along an arc and prevent self-collision triggering.

### Step 6.1: Projectile Setup
1. Open the `Rock Projectile` prefab in the Project inspector.
2. Remove any obsolete components (e.g., remove `Throwable Object Key` if present).
3. Confirm the following component configurations:
   * **Projectile Script**:
     * **Moving Delay**: `0`
     * **Move Speed**: `20`
     * **Move in Arc**: `Checked` (Arc Type = `Combined`)
   * **Trigger Object Activator**:
     * **Delay Trigger**: `Checked`
     * **Activation Delay**: `1.5` seconds
     * *Purpose:* Prevents rock fragments from hitting the spawner enemy's own triggers/colliders when spawned.
     * **Auto Destroy**: Enabled after `2` seconds.
   * **Hitbox Script**:
     * **Owner**: Set to `Rock Projectile`
     * **Activation Mode**: `Auto Activate On Start` (Delay = `2` to `3` seconds)

---

## 7. Health UI, Impact FX & Death Behavior

Configure impact particle systems and auto-cleanup upon death.

### Steps
1. Expand **Hit Reactions**:
   * **Time To Destroy Spawn Impact Effect**: `0.5` seconds.
   * **Impact Effect Hit**: Replace default blood particle with **`Stones Hit`** FX asset.
2. Expand **Health & UI**:
   * **Destroy Enemy On Die**: `Checked` (Set delay to `5` seconds).
   * **Destroy Spawn Health Bar On Die**: `Checked`.

---

## 8. Verification Checklist

Before running tests in Play Mode, check the following configuration settings:

- [ ] **Hand Socket Mapped**: `Right Hand` bone transform assigned as `Projectile Parent`.
- [ ] **Spawn Point Assigned**: Ground spawn point transform linked in Projectile Attack ability.
- [ ] **Projectile Count Set to 1**: Prevents the enemy from ignoring minimum distance boundaries.
- [ ] **Arc Trajectory Active**: `Move in Arc` enabled on `Rock Projectile` prefab.
- [ ] **Trigger Delay Active**: `Trigger Object Activator` delay set to `1.5`s to avoid self-collision.
- [ ] **Impact Particle Updated**: `Stones Hit` FX assigned to `Impact Effect Hit`.
- [ ] **Cleanup Timers**: `Destroy Enemy On Die` checked with a `5`s destruction timer.