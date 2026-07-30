# Pre Combat Behaviour

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/https:/lqI3rThVWBQ"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This guide covers the setup process for **Pre-Combat Behaviours** using the Boss AI Toolkit in Unity. This covers how to configure non-offensive tactical actions—such as target-relative strafing or environment destruction—while waiting for main combat cooldowns.


### 1. Global Pre-Combat Settings

Select your enemy GameObject (`Bull Boss New`) and locate the **Pre-Combat Abilities** section in the Inspector.

```
┌────────────────────────────────────────────────────────┐
│               PRE-COMBAT GLOBAL SETTINGS                │
├──────────────────────────┬─────────────────────────────┤
│ Property                 │ Recommended Default Value   │
├──────────────────────────┼─────────────────────────────┤
│ Initial Pre-Combat Delay │ 2.0 s                       │
│ Min Pre-Combat Wait      │ 3.0 s (or 5.0 s for testing)│
│ Max Pre-Combat Wait      │ 3.0 s (or 5.0 s for testing)│
│ Sequential               │ Enabled (Checked)           │
│ NavMesh Search Range     │ 40.0 (Visualized by Gizmos) │
│ Stopping Distance        │ 3.0                         │
└──────────────────────────┴─────────────────────────────┘
```

#### Parameter Explanations

* **Initial Pre-Combat Delay:** The waiting duration (in seconds) after the game starts before the AI enters its pre-combat loop.
* **Min / Max Pre-Combat Wait:** The delay between consecutive pre-combat abilities. Setting this (e.g., `3-3` or `5-5`) ensures a fixed resting period before triggering the next action.
* **Sequential:** When enabled (✓), abilities execute in order from top to bottom. If disabled, abilities are selected randomly.
* **NavMesh Search Range:** Defines the radius within which the AI looks for valid movement points or breakable objects. Can be visualized via Inspector Gizmos.
* **Stopping Distance:** Distance at which the AI completes its movement relative to the target point.

---

### 2. Setting Up the Strafing Ability

Strafing allows the AI to stay mobile while awaiting attack availability, switching movement direction based on target proximity.

#### Step 1: Configure Ability Properties

Click **Add Pre-Combat Ability** and set up the following parameters:

1. **Ability Type:** Set to `Normal Ability`.
2. **Move to Point:** Enable (✓).
3. **Max Move Time:** Set to `6` seconds (caps movement duration even if the target point is far away).
4. **Movement Radius:** Set to `20`.
5. **Allowed Directions:** Select **Left**, **Right**, and **Backward**.
6. **Check Interval Seconds:** Set to `2` seconds (frequency at which the AI evaluates its movement direction relative to the target).
7. **Configurations Count:** Set to `3` (matching the number of allowed directions).

---

#### Step 2: Download & Import Mixamo Animations

Download three strafing animations from [Mixamo](https://www.mixamo.com):
* **Right Strafe Walking**
* **Left Strafe Walking**
* **Unarmed Walk Back**

##### Asset Import Settings

1. Select all three imported animation clips in Unity.
2. **Rig Tab:** Change **Animation Type** to `Humanoid` and Click **Apply**.
3. **Animation Tab:**
   * Enable **Loop Time** and **Loop Pose** (✓).
   * Set **Based Upon (Root Transform Rotation)** to `Original`and Click **Apply**.

---

#### Step 3: Register Animations in Animator & Script

1. Select `Bull Boss New` and expand **Animation Setup Tool**.
2. Assign the clips and parameters:

| Source Clip | Assigned Parameter Name |
| :--- | :--- |
| Left Strafe Walking | `Left Strafe` |
| Right Strafe Walking | `Right Strafe` |
| Unarmed Walk Back | `Walk Back` |

3. Click **Add to Animator** and **Optimize Animation Clips**. *(You can delete the imported raw `.fbx` files after optimization)*.
4. Inside the **Pre-Combat Ability** inspector, map each direction:

| Direction Configuration | Matching Direction | Animation to Play | Move Speed |
| :--- | :--- | :--- | :--- |
| **Option 1** | Backward | `Walk Back` | `2.0` |
| **Option 2** | Right | `Right Strafe` | `2.0` |
| **Option 3** | Left | `Left Strafe` | `2.0` |

* Set **Fallback Move Animation** to `Walking`.
* Set **Idle Animation** to `Idle`.

> **Tip (Smooth Transitions):** In the **Animator Controller**, select the transitions originating from `Any State` to each strafe clip and increase **Transition Duration** from `0.1` to `0.5` for smoother animation blending.

---

### 3. Setting Up the Break Objects Ability

The **Break Objects** ability instructs the AI to locate and destroy destructible environmental props during pre-combat.

```
                     ┌────────────────────────┐
                     │  AI Finds Breakable    │
                     │  Object in Radius      │
                     └───────────┬────────────┘
                                 │
                                 ▼
                     ┌────────────────────────┐
                     │   Navigates to Object  │
                     │  (Walking Animation)   │
                     └───────────┬────────────┘
                                 │
                                 ▼
                     ┌────────────────────────┐
                     │ Plays Attack/Punch Anim│
                     └───────────┬────────────┘
                                 │
                                 ▼
                     ┌────────────────────────┐
                     │ Weapon Collider Hits   │
                     │  Object Trigger Box    │
                     └───────────┬────────────┘
                                 │
                                 ▼
                     ┌────────────────────────┐
                     │ Static Mesh Hidden     │
                     │  Fragments Activated   │
                     └────────────────────────┘
```

#### Step 1: Add and Configure the Ability

1. Click **Add Pre-Combat Ability** (`+`).
2. Set **Ability Type** to `Break Objects`.
3. Check **Find Closest Object** (✓).
4. Set parameters:
   * **Move Speed:** `2.0`
   * **Stopping Distance:** `3.0`
   * **Final Animation Delay:** `2.0`
   * **Move Animation:** `Walking`
   * **Punch Animation:** `Attack 1` (Assign your melee attack clip via the Animation Setup Tool).

---

#### Step 2: Environment Object Setup (`Breakable Object`)

For an object to be breakable by the AI, it must meet the following structural requirements:

1. **Tag:** Set GameObject tag to `BreakableObject`.
2. **Trigger Collider:** Add a `Box Collider` with **Is Trigger** enabled (✓).
3. **Script:** Attach the `Breakable Object` script.
4. **Child Objects:**
   * **Static Object:** Active by default; contains the clean `Mesh Renderer`.
   * **Destructible Object:** Inactive by default; contains individual fractured mesh pieces, each with a `Rigidbody` and `Collider` attached.
5. Assign both references in the `Breakable Object` script and set **Break Delay** to `1.0` second.

> **Warning (Weapon Collider Requirement):** The enemy's weapon (or attacking body part) must have an active collider (e.g., a `Capsule Collider` attached to a child `Damage Point` object). If no collider triggers the object's hit area, the break action will fail to initiate.

---

#### Step 3: Mesh Fracturing Tool (Optional)

To create custom destructible models directly inside Unity:

1. Open **Tools** < **Boss AI Toolkit** < **Mesh Fracture**.
2. Drag and drop your static mesh (e.g., `Stone Pillar`) into the window.
3. Set **Number of Pieces**:
   * **Mobile Platforms:** Recommended `8` – `10` pieces max to maintain physics performance.
   * **PC / Console:** Higher piece counts allowed.
4. Click **Start Fracture Process**.
5. Click **Save as Mesh** and choose your target directory.

---

### 4. Execution Logic & Testing Workflow

#### Sequential Execution Flow

When multiple abilities are added with `Sequential` enabled:

```
┌────────────────────────────────────────────────────────────────────────┐
│                        PRE-COMBAT RUNTIME FLOW                         │
├────────────────────────────────────────────────────────────────────────┤
│  1. Game Start ──► Wait [Initial Pre-Combat Delay: 2s]                 │
│  2. Execute Ability 1 (e.g., Break Object 1)                          │
│  3. Wait [Pre-Combat Delay: 5s]                                        │
│  4. Execute Ability 2 (e.g., Strafing for Max 6s)                      │
│  5. Wait [Pre-Combat Delay: 5s]                                        │
│  6. Execute Ability 1 (Target next closest Breakable Object, if any)   │
│  7. If no breakable objects remain ──► Fall back to Strafing            │
└────────────────────────────────────────────────────────────────────────┘
```

#### Testing Checklist

- [x] Verify enemy switches from **Left**, **Right**, and **Backward** strafings dynamically as the player shifts positions around the enemy.
- [x] Ensure weapon `Capsule Collider` properly contacts the object trigger zone.
- [x] Adjust **Break Delay** value per object to sync the physical break effect precisely with the impact frame of the attack animation.