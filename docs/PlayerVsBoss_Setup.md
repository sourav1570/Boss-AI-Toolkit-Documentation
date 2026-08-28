# Player Vs Boss Setup

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/LM3s3qRj_-U"  
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>


This setup provides a comprehensive guide to setting up a full boss battle using the Boss AI Toolkit. It covers configuring global tracking parameters, distance-based ability groups, combo chain attacks, multi-phase combat scaling, camera state switching, global sound hooks, and batch-utility tools.

---

## 1. Global Tracking & Rotation Controls

Configure the boss's rotation response to avoid continuous tracking and give the player fair opportunities to land hits during combat.

### Steps
1. Select the **Bull Boss New** GameObject in your scene hierarchy.
2. In the Inspector, expand **Global Settings**:
   * **Smooth Look Rotation Delay**: Set to `2` seconds.
     * *Purpose:* Delaying target tracking keeps the boss from turning instantly toward the player constantly, opening up damage windows. Setting this to `0` makes tracking instantaneous.
   * **Rotation Speed**: Set to `200`.
   * **Spine Rotation**: Set to `20`.
   * Enable all directional/rotation checkboxes as required.
   * **Non-Combat Behavior**: Set to `Idle`.

---

## 2. Pre-Combat Configuration

Control whether the boss engages in pre-combat routines or directly transitions into battle.

### Steps
1. Expand the **Pre-Combat Settings** on the **Bull Boss New** GameObject.
2. Set **Minimum Pre-Combat Distance** to `20` meters.
3. **Enable Pre-Combat**: Uncheck to bypass pre-combat delays and allow immediate battle initiation when within engagement range.

---

## 3. Distance-Based Ability Groups (Phase 0)

Organize attack choices based on how far the player is from the boss using distance groups.

### Step 3.1: Close Range Group (`0 - 5` meters)
1. Expand **Combat Attack System**.
2. Set **Initial Attack Delay** to `3` seconds and **Combat Distance** to `100`.
3. Set **Phase 0 Health Range**: `Min Health = 50`, `Max Health = 100`.
4. Set **Group 0 Distance**: `0` to `5` meters.
5. Configure ability flags & selection memory:
   * **Do Not Repeat Last**: Checked *(Prevents repeating the single most recent ability)*.
   * **Recent Ability Memory**: Set to `3` *(Keeps track of recently used abilities to ensure random variance)*.
6. Set Probability Sliders to `100%` for:
   * **Melee Attack**
   * **Ground Slam**
   * **Spit Attack**
   * **Teleportation**

### Step 3.2: Mid Range Group (`6 - 30` meters)
1. Click **Add Distance Group**.
2. Set Distance to `6` to `30` meters.
3. Set **Min/Max Attack Delay** to `2` seconds.
4. Adjust Ability Probabilities:
   * **Melee Attack**: `80%`
   * **Ground Slam**: `30%`
   * **Flamethrower**: `80%`
   * **Charging Attack**: `100%` *(Highest Priority)*
   * **Teleportation**: `70%`
   * **Spit Attack**: `0%` *(Disabled for mid-range)*

### Step 3.3: Long Range Group (`31 - 100` meters)
1. Click **Add Distance Group**.
2. Set Distance to `31` to `100` meters (or `7` to `100`).
3. Enable **Summon Minions** and adjust ranged parameters (e.g., Meteor Strike, Projectiles).

---

## 4. Setting Up Combo Chain Attacks

Chain attacks trigger follow-up abilities automatically without waiting for combat selection cycles.

[ Primary Attack (Melee) ]
│ (0.6s Transition Delay)
▼
[ Chain Attack 1 (Ground Slam) ]
│ (0.6s Transition Delay)
▼
[ Chain Attack 2 (Flamethrower) ]

### Steps
1. Under **Group 0 (0-5m)**, expand **Melee Attack**.
2. Check **Enable Chain Attack**.
3. Expand **Chain Attack 1**:
   * **Chain Transition Delay**: `0.6` seconds.
   * **Target Ability**: Select **`Ground Slam`**.
4. Expand **Ground Slam** parameters and check **Enable Chain Attack**:
   * **Chain Attack Count**: `1`.
   * **Chain Transition Delay**: `0.6` seconds.
   * **Target Ability**: Select **`Flamethrower`**.
5. Under **Group 1 (6-30m)**, expand **Teleportation**:
   * Check **Enable Chain Attack**.
   * **Chain Transition Delay**: `0.5` seconds.
   * **Target Ability**: Select **`Meteor Strike`** with `100%` probability.

---

## 5. Multi-Phase Combat (Phase 1 Layer)

Scale aggressiveness when the boss drops below half health.

### Steps
1. In the **Enemy Ability System**, click **Add Phase Layer**. This copies all existing distance groups into Phase 1.
2. Configure Phase 1 Health Range:
   * **Min Health**: `0`
   * **Max Health**: `50`
3. Decrease **Min/Max Attack Delay** across all Phase 1 groups to `1` second to accelerate attack frequency.

---

## 6. Camera States & Sound Hooks Setup

Bind boss lifecycle events to camera modes and global sound effects.

### Step 6.1: Boss Camera Tracking Activation
1. Select **Bull Boss New** and expand **Global Event Hooks**.
2. Add two new global events:
   * **Event 1 (On Start)**: Drag **Camera Rig** -> Select `MouseCameraRotation.ActivateBossCamera`.
   * **Event 2 (On Dying)**: Drag **Camera Rig** -> Select `MouseCameraRotation.DeactivateBossCamera`.

### Step 6.2: On-Hit Universal Audio Player Setup
1. Select **Boss Voice Controller** and remove the `on hit` entry from categories.
2. Select **Bull Boss New** -> expand **Universal Sound Player**.
3. Create an action entry named **`hit sounds`** and populate it with hit audio clips.
4. Under **Global Event Hooks**:
   * Map **On Take Damage** to **Universal Sound Player** -> Select `UniversalSoundPlayer.PlayAudioCategory`.
   * Pass string parameter: **`hit sounds`**.
5. Under **Boss Voice Controller**, set `in combat` voice clip cooldown to `8` seconds.

---

## 7. Workflow Efficiency & Utility Tools

### Batch Animator Transition Tool
1. Navigate to **Tools -> Boss AI Toolkit -> Animator Transition Tool**.
2. Drag the boss's Animator Controller into the field.
3. Set **New Duration** to `0.3` seconds.
4. Click **Apply Transition Duration** to smooth out transitions across all states.

### Ability Copy-Paste Feature
1. Modify ability parameters (e.g., adjust **Ground Slam Range** or **Flamethrower Rotation Speed**).
2. Right-click the modified ability context header and select **Copy Ability**.
3. Expand target distance groups/phases, right-click, and select **Paste Ability**.

---

## 8. Verification Checklist

Before testing in Play Mode, check the following configuration settings:

- [ ] **Rotation Delay**: `Smooth Look Rotation Delay` set to `2` seconds.
- [ ] **Pre-Combat State**: `Enable Pre-Combat` toggled off for immediate engagement.
- [ ] **Distance Groups**: Proper distance brackets (`0-5m`, `6-30m`, `31-100m`) configured under Phase 0.
- [ ] **Combo Connections**: `Enable Chain Attack` verified for Melee -> Ground Slam -> Flamethrower.
- [ ] **Phase 1 Settings**: Health limits (`0-50 HP`) set with attack delay dropped to `1` second.
- [ ] **Global Events**: Camera activation bound to `On Start`/`On Dying` and hit sounds bound to `On Take Damage`.
- [ ] **Animator Transitions**: Transition duration updated to `0.3` seconds across states.