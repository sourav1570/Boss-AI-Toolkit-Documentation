# PC Controls

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/JNCCtthvTq8"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This setup provides a guide on configuring keyboard and mouse input controls for PC gameplay using the **Boss AI Toolkit** in Unity. It covers enabling PC controls, configuring keybindings, syncing UI joystick animations for PC inputs, and configuring mouse look parameters on the camera.

## 1. Enabling & Configuring PC Input Settings

Enable the PC control scheme on the player controller and configure keybindings and UI joystick synchronization.

### Steps
1. Select the main player GameObject (e.g., `Player New`) in the scene hierarchy.
2. In the Inspector, locate and expand the **PC Controls** section on the player controller script.
3. Check **Use PC Controls**.

### Key Parameter Settings

| Parameter | Recommended Value | Description |
| :--- | :--- | :--- |
| **Use Joystick Sync To Child** | `Checked` | Automatically moves the UI joystick handle visual when pressing PC movement keys (useful for recording gameplay footage). |
| **Joystick Handle UI** | Drag Joystick Handle | Reference to the UI Joystick Handle transform. |
| **Joystick Handle Radius** | `120` | Defines the movement distance limit of the UI joystick handle. |
| **Smooth Speed** | `30` | Smoothness speed of joystick transition when keys are pressed. |

---

## 2. Setting Up Action & Movement Keybindings

Configure the keyboard and mouse key bindings under **Action Key Bindings** and **Movement Controls**:

* **Movement Controls**:
  * **Forward**: `W`
  * **Backward**: `S`
  * **Left**: `A`
  * **Right**: `D`
* **Sprint Settings**:
  * **Sprint Key**: `Left Shift` *(Pressing `W` + `Left Shift` enables forward sprint)*.
* **Combat Actions**:
  * **Melee Attack Key**: `Mouse Left` (Left Click)
  * **Dodge Key**: `Space`
  * **Shield Key**: `X`

---

## 3. Configuring Camera Mouse Look & Cursor Locking

Configure camera rotation using the mouse and set cursor lock parameters on the camera rig.

### Steps
1. Select the **Camera Rig** GameObject in the scene hierarchy.
2. In the Inspector, locate the camera controller component.
3. Check **PC Mouse Look** to enable mouse-driven camera orientation.
4. Check **Lock Cursor On PC** to automatically lock and hide the mouse cursor during gameplay.
5. *(Optional)* 
   * **Mouse Rotation Speed X / Y**: Tweak mouse sensitivity.
   * **Mouse Min Y / Max Y**: Set vertical tilt limits.

---

## 4. Verification Checklist

Before running tests in Play Mode, check the following settings:

- [ ] **PC Controls Enabled**: `Use PC Controls` is checked on the player controller.
- [ ] **Keybindings Verified**: Key assignments for attack (`Left Click`), dodge (`Space`), shield (`X`), and sprint (`Left Shift`) are mapped.
- [ ] **Camera Settings**: `PC Mouse Look` and `Lock Cursor On PC` are enabled on the `Camera Rig`.
- [ ] **Joystick Sync**: `Joystick Handle UI` transform assigned if UI synchronization is enabled.