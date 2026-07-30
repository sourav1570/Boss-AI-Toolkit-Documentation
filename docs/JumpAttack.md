# Jump Attack Ability (Boss AI Toolkit)

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/laIUHSCSlVI"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>


This guide details how to configure the **Jump Attack** combat ability for the `Bull Boss` AI entity. It covers ability parameter configuration, root motion setup, animation binding, collider assignments for landing impacts, and camera shake event integration.

---

## 1. Overview & Ability Configuration

Add the Jump Attack ability to the boss ability entries and configure its physical movement parameters.

### Steps
1. Select the **Bull Boss** GameObject in the hierarchy.
2. Open the **Enemy Ability System** component.
3. Set the probability of other previously created abilities to `0%` so you can focus exclusively on testing the Jump Attack.
4. Add or expand an ability entry group and set the ability type/name to **Jump Attack Ability**.
5. Set **Probability** to `100%`.
6. Check **Apply Root Motion**.
7. Configure vertical movement and timing parameters:
   * **Jump Height** *(Vertical Height)*: `5`
   * **Jump Duration**: `1.1` seconds

---

## 2. Animation Setup

Import and bind the Jump Attack animation to the boss animator component.

### Steps
1. Expand the **Animation Setup Tool** on the `Bull Boss` inspector.
2. Click **Add Animation**.
3. Locate the `Jump Attack` animation clip in the `Animations` folder in your **Project** panel.
4. Drag and drop `Jump Attack` into the field and set its name to **`Jump Attack`**.
5. Click **Add to Animator**.
6. Scroll back up to the **Enemy Ability System** component and set **Jump Animation** to `Jump Attack`.

---

## 3. Land Attack Collider & Activation Setup

Configure attack colliders that trigger when the boss lands. You can reuse an existing charging collider or create a dedicated jump attack collider.

### 3.1 Reusing or Creating a Landing Collider
1. Locate your attack collider object in the hierarchy (e.g., the charging collider).
2. Rename the object to **`Charging and Jump Attack Collider`** if using it for both abilities.
   > **Note:** If you prefer a unique hit volume for the jump attack, duplicate the object, adjust its collider shape/size in the inspector, and ensure a **Knockback Trigger** component is attached.

### 3.2 Binding Collider to Ability Activation
1. Select `Bull Boss` and locate the **Jump Attack Ability** parameters in the inspector.
2. Under **Objects to Activate on Land**, add an entry:
   * Drag and drop `Charging and Jump Attack Collider` into this field.
3. Set the remaining operational timing values:
   * **Objects Deactivation Time**: `1` second *(Deactivates the collider automatically after 1s)*.
   * **Idle Animation Delay**: `2` seconds *(Plays the idle animation after a 2-second delay)*.

---

## 4. Camera Shake Event Setup

Add landing feedback by triggering a camera shake when the boss impacts the ground.

### 4.1 Configuring the Camera Shaker Trigger Object
Ensure you have a `Camera Shake Trigger Automatic` GameObject in your scene configured with the following properties:
* **Script**: `Camera Shake Trigger` component attached.
* **Looping Duration**: `0.5` seconds.
* **Oscillation Speed**: `10`.
* **Offset/Z-Axis**: Set to your desired impact value.

### 4.2 Adding the Event Listener
1. Select `Bull Boss` and scroll to the event listener section of the **Enemy Ability System**.
2. Remove any previous event listeners that were used for other abilities (e.g., charging).
3. Click **Add Event Listener**.
4. Set the event callback type to **`On Landing Impact`**.
5. Click the **`+`** icon to add an action:
   * **Target Object**: Drag and drop `Camera Shake Trigger Automatic`.
   * **Function**: Select `CameraShakeTrigger -> TriggerShake`.

---

## 5. Testing & Verification Checklist

- [ ] **Probability**: Jump Attack set to `100%`, other abilities set to `0%` for testing.
- [ ] **Root Motion**: `Apply Root Motion` is enabled.
- [ ] **Animation**: `Jump Attack` clip is assigned in the ability system.
- [ ] **Landing Collider**: Object assigned under `Objects to Activate on Land` with a `Deactivation Time` of `1` second.
- [ ] **Camera Shake Event**: `On Landing Impact` listener set to call `TriggerShake`.
- [ ] **Play Mode Check**: Verify the jump arc height, landing impact timing, collider bounds, and camera shake in Play Mode.