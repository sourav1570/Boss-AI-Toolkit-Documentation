# Boss Health System

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/s97eahDNhhU"  
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This setup provides a comprehensive guide for setting up hit reaction animations, health/UI systems, and death behaviors (Animation vs. Ragdoll physics) for the **Bull Boss** using the Boss AI Toolkit in Unity.

---

# Setting Up Boss Health, Hit Reactions & Death System  


## 1. Hit Reaction Setup & Parameter Tuning

Configure hit reaction animations and cooldown intervals to prevent hit-stun locking during combat.

### Step 1.1: Interval Configuration
1. Select the **Bull Boss** GameObject in your scene hierarchy.
2. In the Inspector, expand the **Hit Reactions** section.
3. Set **Min Hit Interval Time** to `5` seconds and **Max Hit Interval Time** to `7` seconds.
   * *Note:* Keeping interval times longer ensures the boss has adequate time to perform combat behaviors without constantly interrupting its own attacks with hit reactions.
4. **Do Not Wait For Animation Completion**: Keep **Unchecked** so hit reaction animations play out smoothly.

### Step 1.2: Animation Registration via Animation Setup Tool
1. Expand the **Animation Setup Tool** component on the **Bull Boss**.
2. Register the following hit reaction animations using **Add Animation**:
   * `face punch reaction` -> Parameter Name: **`hit reaction 1`**
   * `hit reaction to the waist` -> Parameter Name: **`hit reaction 2`**
   * `hit reaction third` -> Parameter Name: **`hit reaction 3`**
3. Click **Add to Animator**.

### Step 1.3: Hit Reaction Entry Settings
In the **Hit Reactions** settings panel, add 3 hit animation entries and configure them:

| Animation Entry | Parameter Name | Animation Duration (Override) | Root Motion |
| :--- | :--- | :--- | :--- |
| **Element 0** | `hit reaction 1` | `1.2` seconds | Checked |
| **Element 1** | `hit reaction 2` | `2.2` seconds | Checked |
| **Element 2** | `hit reaction 3` | `1.0` second | Checked |

> **Tip:** Click **Auto Get Length** to fetch default animation durations. You can manually trim the duration to cut hit animations short and make combat feel more responsive.

---

## 2. Health & UI System Setup

Configure boss health points, dynamic UI bar settings, and auto-destruction parameters.

### Steps
1. Select the **Bull Boss** GameObject and expand **Health & UI**.
2. Configure general health settings:
   * **Max Health**: Set initial maximum health (e.g., `100`).
   * **Enemy Name**: Type `Bull Boss`.
   * **Enemy Name Text**: Drag the TextMeshPro UI element reference.
3. Configure dual-bar visual depletion settings:
   * **Damage Speed**: `0.7`
   * **White Bar Speed**: `0.5`
   * *Mechanism:* The white bar decreases first, followed by the red trailing bar after a short delay for smooth visual feedback.
4. Cleanup & Despawn:
   * **Destroy On Die**: Checked
   * **Delay Destroy On Die**: `10` seconds (removes the boss entity 10 seconds post-death).

---

## 3. World-Space Overhead Health Bar (Optional)

If you prefer a floating health bar above the boss entity rather than fixed screen UI, configure these options:

* Check **Spawn Health Bar Prefab**.
* **Spawn Offset**: Adjust the Y-axis position to hover over the boss's head.
* **Follow Target By Rotation**: Checked (ensures the floating health bar continuously faces towards the active player camera).

---

## 4. Death Modes: Animation vs. Ragdoll Physics

Choose between animated death sequences or physics-driven ragdoll collapses upon reaching 0 HP.

### Mode 1: Animated Death Setup
1. Open the **Animation Setup Tool** on the boss.
2. Register the death clip (e.g., `dying backwards`) under parameter name **`dying animations`** and click **Add to Animator**.
3. Under **Health & UI -> Death Settings**, set **Death Mode** to **`Die Using Animations`**.
4. Select the `dying animations` from the given list. Enable **Root Motion** if required.

### Mode 2: Ragdoll Physics Setup
1. Go to Unity Top Menu: **GameObject -> 3D Object -> Ragdoll...**
2. Assign the **Bull Boss** Animator component into the wizard and click **Autofill** to auto-assign limb bones.
3. Click **Create** to build physical colliders and Rigidbodies across the body hierarchy.
4. Adjust generated colliders (e.g., fine-tune head bone sphere collider).
5. Under **Health & UI -> Death Settings**, set **Death Mode** to **`Die Using Ragdoll Physics`**.
   * *Mechanism:* Disables the Animator component on death and enables physics simulation across all child Rigidbodies.

---

## 5. Combat Timing Troubleshooting: Attack Delay vs. Hit Reactions

If the boss fails to play hit reaction animations when taking damage during testing:

* **Problem**: Setting **Min/Max Attack Delay** to `0` seconds forces continuous attack animation loops. The engine cannot find a free state window to trigger a hit reaction.
* **Solution**: In **Combat Attack System**, set **Min and Max Attack Delay** to at least `2` seconds. This creates idle windows between attacks, allowing hit reactions to interrupt the boss when damaged.

---

## 6. Verification Checklist

Before running combat tests in Play Mode, verify the following configuration settings:

- [ ] **Hit Cooldown**: `Min/Max Hit Interval` set (`5-7` seconds) to prevent constant stagger locking.
- [ ] **Combat Gaps**: `Min/Max Attack Delay` set to `2` seconds or higher to allow reaction windows.
- [ ] **Animator Sync**: Hit reaction parameters registered via the Animation Setup Tool.
- [ ] **Death Mode Selected**: `Death Mode` set explicitly to either Animation or Ragdoll Physics.
- [ ] **Despawn Timer**: `Destroy On Die` enabled with `Delay Destroy On Die` set (e.g., `10` seconds).