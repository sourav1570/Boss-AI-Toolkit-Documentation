# Smart Turning Behaviour


<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/fEh2SKWaURc"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This guide demonstrates how to configure turning animations and target detection parameters on the **Bull Boss** enemy using the Boss AI Toolkit

---

## 1. Overview & Key Concepts

* **Team Member System:** Manages target detection and determines hostile vs. friendly entity relationships based on Team IDs
* **Enemy Vision Angle:** Sets the field-of-view threshold (e.g., 45, 60) required to trigger turn animations
* **Mixamo Animation Workflow:** Importing, configuring Humanoid rigs, and assigning root motion turning clips

---

## 2. Setup Guide

### Step 1: Target & Team Setup

1. Select the `Bull Boss New` GameObject in your Unity hierarchy
2. In the Inspector, navigate to **Enemy Ability System**.Expand Global Settings to locate the `Team Member` script
3. Configure team relationships:
   * **Bull Boss:** Set `Team Name` to `Team2`
   * **Player:** Set `Team Name` to `Team1`

!!! **NOTE** "Team Relationship Rule"
    If both entities share the same team name (e.g., `Team 2`), they are treated as friendly and will not attack each other Differing team names establish hostility

4. Assign target body parts (`My Body Part to Target`) for hit registration
5. Set `Target Detection Range` to `100`
6. Check **Auto Update Target** (scans for nearby targets every 0.5–2.0 seconds)
7. Uncheck **Log Sorted Enemies** 

---

### Step 2: Rotation Settings

Under **Global Settings**, configure the following properties:

* **Detection Range:** Set to `100` (matches the Team Member script)
* **Enemy Vision Angle:** Set to `45`
* **Initial Search Delay:** Min `1`, Max `2` seconds
* **Rotation Check Interval:** `2`
* **Rotation Speed:** `1000`

Enable the following checkboxes:
- [x] **Control Rotation**
- [x] **Use Rotation Animation**
- [x] **Always Look at Target**
- [x] **Rotate Spine Bone**

---

### Step 3: Mixamo Animation Setup

1. Search [Mixamo](https://www.mixamo.com) for **"Mutant Turn"**
2. Download **Mutant Right Turn 90** (`Unity format`, `With Skin`)
3. Toggle the **Mirror** checkbox on Mixamo to flip the clip, then download the **Left Turn** animation
4. Drag both `.fbx` files into your Unity project
5. Select both animation files and configure their Inspector settings:
   * **Rig Tab:** Set **Animation Type** to `Humanoid` and Click **Apply**
   * **Animation Tab:**
     * Rename clips to `Right Turn` and `Left Turn`
     * Set **Based Upon (Root Transform Rotation)** to `Original`and Click **Apply**

---

### Step 4: Link Clips to Animator & Script

1. Select `Bull Boss New` and expand **Animation Setup Script** and **Add Animation**
2. Drag `Right Turn` and `Left Turn` into their respective slots
3. Assign parameter names:
   * Right Animation `Right Turn`
   * Left Animation `Left Turn`
4. Click **Add to Animator Controller** and **Optimize Animation Clips**
5. Under **Rotation Animations**, map the directions as follows:

| Setting | Right Direction | Left Direction |
| :--- | :--- | :--- |
| **Direction** | Right | Left |
| **Rotation Animation** | Right Turn | Left Turn |
| **Idle Animation** | Idle | Idle |
| **Use Root Motion** | Enabled | Enabled |
| **Animation Duration** | 2 seconds | 2 seconds |

!!! Tip "Auto Duration"
    Click **Auto Get Length** to automatically populate the animation duration from the clip

---

## 3. Testing Vision Angles

| Vision Angle | Behaviour Summary |
| :--- | :--- |
| **45 Degrees** | **Tight Response:** The boss turns rapidly as soon as the player leaves its 45 Degrees, triggering quick micro-adjustments |
| **60 Degrees** | **Forgiving Margin:** The player has a wider arc to maneuver without triggering turn animations, reducing overall turn frequency |