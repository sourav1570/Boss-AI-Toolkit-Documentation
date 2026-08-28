# Throw Objects

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/dKrvqXTHDIQ"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This setup provides a step-by-step guide on setting up the **Throw Objects Ability** for the **Bull Boss** using the Boss AI Toolkit. It covers ability binding, weapon unequipping/equipping logic, hand-carried object synchronization, destruction setup, arc trajectories, and full animation configurations.


## 1. Initial Ability Configuration

Set up the advanced custom ability inside the **Enemy Ability System** and isolate its probability for testing.

### Steps
1. Select the **Bull Boss New** GameObject in your scene hierarchy.
2. Expand the **Enemy Ability System** component in the Inspector.
3. Click **Add Ability Entry to Group**.
4. Set **Ability Type** to **Create Your Own Ability Advanced**.
5. Set **Ability Name** to **`Throw Objects`**.
6. Add Script: Drag and drop the **`Enemy Throwable Object Ability`** script.
7. Set Function: Select **`Activate Throwable Attack`**.
8. Set **Ability Lifetime** to `10` seconds.
9. Adjust probabilities for isolated testing:
   * Set **Throw Objects Probability** to `100%`.
   * Set all other ability probabilities to `0%`.
10. Adjust detection distance under general ability settings:
    * Set **Min Distance** to `0` and **Max Distance** to `50` meters (ensures reachable objects are detected across the area).

---

## 2. Core Ability Settings & References Setup

Assign the core component references and target search conditions on the **Enemy Throwable Object Ability** component.

### Steps
1. In the Inspector for **Enemy Throwable Object Ability**, assign the following references:
   * **Team Member**: Drag the boss's `Team Member` script.
   * **Animator**: Drag the boss's `Animator` component.
   * **Nav Mesh Agent**: Drag the boss's `NavMeshAgent` component.
   * **Pickup Bone**: Drag the boss's **Right Hand** transform (where weapons are held).
2. Configure search conditions:
   * **Search Mode**: `Find Closest Throwable Objects` (or `Find Random Throwable Objects`).
   * **Throwable Object Tag**: Set to `ThrowableItems`.
   * **Search Range**: `50` meters.

---

## 3. Hand-Carried Object & Back Weapon Setup

To create a seamless transition where the boss un-equips its weapon, picks up an object, throws it, and re-equips its weapon, you must configure carried references.

### Step 3.1: Hand-Carried Object (Visual Placeholder)
1. Locate the scene throwable object (e.g., a stone tagged `Throwable Items` with a `Throwable Object Key` set to `stone`).
2. Duplicate the stone and make it a child of the boss's **Right Hand** bone.
3. Reset its local position, scale it appropriately, and clean up unnecessary components:
   * Remove `NavMeshModifier` and `NavMeshObstacle`.
   * Set tag to **`Untagged`**.
   * Ensure `Throwable Object Key` script is attached with the key set to **`Stone`**.
4. Rename the object to **`Stone`** and **deactivate** it by default.

### Step 3.2: Back Weapon (Holstered Visual)
1. Duplicate the main **`Weapon`** GameObject on the boss's hand.
2. Parent it under the **`Spine_02`** bone transform and align it on the boss's back.
3. Rename it to **`Weapon Back`** and **deactivate** it by default.
4. On the **Enemy Throwable Object Ability** script:
   * Assign the active weapon to **Assign Weapon**.
   * Assign `Weapon Back` to **Back Weapon Transform**.

---

## 4. Animation Setup & Disarm Logic

Download necessary disarm/equip animations from Mixamo and configure timing logic.

### Step 4.1: Import & Setup Mixamo Animations
1. Download **`Standing Disarm`** (Unequip) and **`Unarmed Equip Over Shoulder`** (Equip) animations from Mixamo (Humanoid rig).
2. In Unity, set animation Rig type to **Humanoid**, check **Bake into Pose**, and set **Based Upon** to `Original`.
3. Open the **Animation Setup Tool** on the **Bull Boss**.
4. Add and name the animation parameters:
   * `Pickup` (Pickup animation)
   * `Throw` (Throw animation)
   * `Unequip Weapon` (Standing disarm animation)
   * `Equip Weapon` (Unarmed equip animation)
5. Click **Add to Animator**.

### Step 4.2: Timing & Delay Settings Configuration

Click **Add Config** on the **Enemy Throwable Object Ability** script and configure the timing parameters:

| Parameter | Value | Description |
| :--- | :--- | :--- |
| **Throwable Object Key Script** | `Stone` (Hand) | Link to the deactivated hand-carried stone object script. |
| **Stopping Distance to Object** | `2` meters | Distance from the object where the boss stops moving. |
| **Look At Target After Pickup** | `Checked` | Boss rotates to face the player after picking up the object. |
| **Look At Target Duration** | `1` second | Duration spent facing the target before throwing. |
| **Carried Objects Activation Delay** | `1` second | Delay during the pickup animation before the hand-held stone appears. |
| **Throw Animation Delay** | `0.5` seconds | Wait time after carried object activation before playing throw animation. |
| **Carried Objects Deactivation Delay** | `0.6` seconds | Time into throw animation when hand-carried stone hides and prefab spawns. |
| **Delay Unequipping Weapon Anim** | `0` seconds | Wait time upon reaching object before playing unequip animation. |
| **Weapon Deactivation Delay** | `0.8` seconds | Moment hand weapon hides and back weapon appears during unequip anim. |
| **Delay Before Pickup Anim** | `1` second | Delay after unequipping weapon before starting pickup animation. |
| **Delay Before Equip Weapon Anim** | `1.5` seconds | Delay after throw completes before starting weapon re-equip animation. |
| **Weapon Activation Delay** | `1` second | Moment back weapon hides and hand weapon reappears during equip anim. |
| **Walk Animation** | `Walking` | Locomotion animation parameter. |
| **Pickup Animation** | `Pickup` | Object pickup animation parameter. |
| **Throw Animation** | `Throw` | Throwing animation parameter. |
| **Idle Animation** | `Idle` | Resting animation parameter. |
| **Unequipped Weapon Anim** | `Unequip Weapon` | Disarming animation parameter. |
| **Equipped Weapon Anim** | `Equip Weapon` | Re-arming animation parameter. |

---

## 5. Destructible Projectile Prefab Setup

Create the throwable projectile prefab complete with fracturing logic, trajectory arcs, team damage detection, and automatic collision activation.

### Step 5.1: Mesh Fracturing Process
1. Import a stone model mesh and set up its material and scale.
2. Go to **Tools -> Boss AI Toolkit -> Mesh Structure**.
3. Drag the stone mesh into **Mesh Game Object**, set **Number of Pieces** to `8`, and click **Start Fracture Process**.
4. Click **Save as Mesh** to save the generated fragment pieces.
5. Unpack the fractured instance, parent the fragments under the main stone object (named **`Stone Projectile`**), and **deactivate** the fragment group by default.

### Step 5.2: Components Setup on `Stone Projectile`
Add the following components to the root **`Stone Projectile`** object:

1. **Sphere Collider**: Check **Is Trigger** and adjust radius.
2. **Rigidbody**: Standard physics component.
3. **Throwable Object Key**: Set Key Name to **`Stone`**.
4. **Team Member**: Set Team Name to **`Team2`** and assign `Stone Projectile` to **My Body Part Target**.
5. **Trigger Object Activator**:
   * Drag the attached **Team Member** script.
   * **Objects to Activate**: Add the fractured fragments group.
   * **Objects to Deactivate**: Add the static mesh object.
   * **Destroy Delay**: Set to `3` seconds (destroys root projectile after impact).
   * **Root Object to Destroy**: Drag `Stone Projectile`.
6. **Hitbox**:
   * **Damage**: `10`
   * **Owner**: `Stone Projectile`
   * **Compare Enemy**: Checked
   * **Script Team Member**: Drag attached `Team Member` script.
   * **Activation Mode**: `Auto Activate On Start` (`2` seconds activation delay).
7. **Projectile**:
   * **Moving Delay**: `0`
   * **Move Speed**: `15`
   * **Rotation Mode**: `Spin` (Set X=`50`, Y=`100`, Z=`360`).
   * **Move In Arc**: Checked
   * **Arc Type**: `Vertical`
   * **Arc Height Percentage**: `0.2`
   * **Horizontal Arc Intensity**: `0.4`
   * **Vertical Arc Intensity**: `1.1`
   * **Unparent On Move**: Checked
   * **Projectile Lifetime**: `10` seconds
   * **Offset From Target Position**: Checked (Set Min and Max offset Y to `0.6`).

### Step 5.3: Save Prefab & Link to Ability
1. Drag **`Stone Projectile`** into your `Prefabs` folder to create a prefab asset and delete the instance from the Hierarchy.
2. Select **Bull Boss New**, expand **Enemy Throwable Object Ability**, and assign `Stone Projectile` to the **Throwable Prefab** field.

---

## 6. Verification Checklist

Before running tests in Play Mode, verify all setups against this list:

- [ ] **Scene Object Tag**: Ground objects tagged with `ThrowableItems` and have a matching `Throwable Object Key` (`stone`).
- [ ] **Hand & Back References**: Inactive hand object (`Stone`) and back weapon (`Weapon Back`) created and linked.
- [ ] **Key Match**: Throwable key string (`Stone`) matches across scene items, hand placeholders, and projectile prefabs.
- [ ] **Animation Hooks**: Disarm, equip, pickup, and throw parameters registered in Animator and assigned in ability script.
- [ ] **Fracture Setup**: Static stone deactivates and fragment group activates via `Trigger Object Activator` on trigger contact.
- [ ] **Arc Settings**: `Move In Arc` enabled on projectile with vertical arc parameters.