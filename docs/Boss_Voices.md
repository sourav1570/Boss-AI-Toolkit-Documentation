# Boss Voices

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/HZRESUB22nc"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This guide provides step-by-step instructions for configuring dynamic contextual audio triggers using the **Boss Voice Controller** in Unity. This system dynamically plays category-specific audio clips (e.g., combat dialogue, taunts, damage reactions, and idle sounds) based on the boss AI's active behavior state.

## 1. GameObject & Audio Source Creation

Create the dedicated voice controller object under the boss hierarchy and attach required audio components.

### Steps
1. In the Hierarchy, right-click the **Bull Boss New** GameObject and choose **Create Empty**.
2. Rename the new child object to **`Boss Voice Controller`**.
3. Select **Boss Voice Controller** and click **Add Component** -> **Audio Source**:
   * **Play On Awake**: Uncheck.
   * **Spatial Blend**: Set to `3D` (slide completely to `1.0`).
   * **Min Distance**: `20` meters.
   * **Max Distance**: `30` meters.
4. Click **Add Component** -> **Boss Voice Controller**:
   * Drag the **Audio Source** component into the **Audio Source** field on the script.

---

## 2. Voice Controller Settings & Category Configuration

Configure voice playback behavior, delay intervals between category switches, and set up state categories.

### Steps
1. In the Inspector for **Boss Voice Controller**, verify core settings:
   * **Enable Voices**: Checked.
   * **Interrupt Current Voice**: Unchecked (ensures active dialogue lines finish playing completely without clipping).
   * **Min Category Delay**: `2` seconds.
   * **Max Category Delay**: `3` seconds.
2. In the **Add Category** section, type each category name exactly as shown below and click **Add Category** after each entry:
   * `in combat`
   * `on hit`
   * `in pre-combat`
   * `in non-combat`

> **Note:** Additional custom categories (e.g., `ground slam`) can be created following the same step.

---

## 3. Audio Clip Assignment

Assign relevant audio files to their corresponding state categories.

### Steps
Expand each generated category inside the **Boss Voice Controller** Inspector and assign audio clips:

* **`in combat`**: Assign battle lines, taunts, and attack vocalizations.
* **`in pre-combat`**: Assign pre-engagement threat clips or warning voice lines.
* **`on hit`**: Assign pain clips and damage reaction sounds (`enemy hit` audio assets).
* **`in non-combat`**: Assign idle vocalizations, ambient growls, roars, or idle mouth sounds.

---

## 4. Global Event Mapping

Hook global state changes on the main boss entity to trigger category switches in the Voice Controller.

### Steps
1. Select the main **Bull Boss New** GameObject in the hierarchy.
2. Navigate to the **Global Events** section in the Inspector and click **Add Global Event** 4 times.
3. Configure the 4 events to bind boss state changes to audio categories:

| Event Type | Target GameObject | Called Function | Category String Parameter |
| :--- | :--- | :--- | :--- |
| **In Combat** | `Boss Voice Controller` | `BossVoiceController.PlayCategory` | `in combat` |
| **On Take Damage** | `Boss Voice Controller` | `BossVoiceController.PlayCategory` | `on hit` |
| **In Pre-Combat** | `Boss Voice Controller` | `BossVoiceController.PlayCategory` | `in pre-combat` |
| **In Non-Combat** | `Boss Voice Controller` | `BossVoiceController.PlayCategory` | `in non-combat` |

---

## 5. Specific Ability Audio Triggers (Optional)

You can trigger specific voice lines for individual abilities (such as a Ground Slam or Melee attack).

### Steps
1. In **Boss Voice Controller**, create a new category (e.g., `ground slam`) and assign matching voice clips.
2. Select the **Bull Boss New** GameObject and expand the specific ability parameters inside the **Enemy Ability System** (e.g., Ground Slam ability entry).  
3. Under the ability's Event Hooks section, click **Add Event Hook** (`+`).
4. Drag `Boss Voice Controller` into the field.
5. Select function: **`BossVoiceController.PlayCategory`**.
6. Enter the category parameter name (e.g., `ground slam`).

---

## 6. Playback Logic Overview

Understanding the underlying playback mechanics ensures optimal tuning:

* **Clip Duration Protection**: The controller automatically calculates the active clip's exact playback duration before applying cooldown timers. If a clip is 10 seconds long and category cooldown is set to 3 seconds, the system waits 13 seconds total before attempting to play the next line.
* **Category Transition Delays**: When the boss state changes (e.g., transitioning from `in combat` to `in pre-combat`), the system waits for the **Min/Max Category Delay** interval (`2 - 3` seconds) before initiating clips from the new category.
* **Default Initial State**: If no state category is explicitly active at initialization, the voice system automatically picks a default category and plays back an available clip.

---

## 7. Verification Checklist

Before running tests in Play Mode, check the following configuration settings:

- [ ] **Audio Source**: `Play On Awake` is disabled and `Spatial Blend` is set to 3D (`1.0`).
- [ ] **3D Sound Range**: `Min Distance` is set to `20` and `Max Distance` to `30`.
- [ ] **No Voice Interrupts**: `Interrupt Current Voice` is unchecked to allow full line playback.
- [ ] **Category String Exact Matches**: String entries in Global Events match category names exactly (`in combat`, `on hit`, `in pre-combat`, `in non-combat`).
- [ ] **Global Event Hooks**: All 4 state events are hooked to `BossVoiceController.PlayCategory`.
- [ ] **Audio Clips**: Audio clips are populated across all active categories.