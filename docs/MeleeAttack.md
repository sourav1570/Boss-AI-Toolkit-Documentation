# Melee Combat Behavior

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/RpfasK9Hi5A"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>


This guide walks through configuring the melee attack combat behavior for an AI boss entity (`Bull Boss New`), including setting up pre-combat delays, distance range groups, weapon hitboxes, weapon trail effects, audio triggers, and animation events.

---

## 1. Overview & General Parameters

Before configuring specific attack abilities, set the overarching combat timings and distance rules for the boss.

### Steps
1. Select the **Bull Boss New** GameObject in the hierarchy.
2. In the inspector, expand **Pre-Combat Behaviors**:
   * Change **Initial Pre-Combat Delay** to `4`.
3. Expand the **Combat Attack System**:
   * Set **Initial Attack Delay** to `2` seconds.
   * Set **Combat Forget Distance** to `100`. 

> **Note:** If the target/player moves further than `100` meters away, the boss will drop combat and enter the **Non-Combat Behavior State**.

---

## 2. Phase Layers & Distance Range Setup

Configure the health range and distance parameters under which the melee attack triggers.

### Steps
1. Click **Add Phase Layer**:
   * Set **Min Health** to `0`.
   * Set **Max Health** to `100`.
2. Click **Add Distance Range Subgroup**:
   * Set **Min Distance** to `0`.
   * Set **Max Distance** to `20`.
   * Ensure **Play in Sequence** and **Do Not Repeat Last** are **unchecked**.
   * Set **Min Attempt Delay** to `3` seconds.
   * Set **Max Attempt Delay** to `4` seconds.

---

## 3. Configuring the Melee Ability Entry Group

Define the specific properties for the melee attack sequence.

### Steps
1. Click **Add Ability Entry Group** and name it `Melee Attack`.
2. Set the **Melee Attack Probability Slider** to `100%` (ensures this ability always plays during this combat phase).
3. Adjust the movement and engagement parameters:
   | Parameter | Recommended Value | Description |
   | :--- | :--- | :--- |
   | **Look Mode** | `Target` | Boss faces the target during the attack. |
   | **Move Speed** | `2` | Movement speed while engaging target. |
   | **Move Animation** | `Walking` | Animation state while moving toward player. |
   | **Stopping Distance** | `2` | Distance at which the boss stops moving toward the target. |
   | **Re-Engage Distance** | `5` | If target moves > 5m away, boss resumes chasing until 2m away. |
   | **Attack Duration** | `10` | Duration (in seconds) the boss continues attacking before re-evaluating state. |
   | **Sequential** | Checked | Plays animations in order (uncheck for random selection). |
   | **Min/Max Attack Delay** | `1` | Delay between consecutive attack animations (plays full animation clip first). |

---

## 4. Animation Setup

Add the required attack animations to the boss's animator component.

### Steps
1. Scroll down to the **Animation Setup Tool** and expand it.
2. Under your project assets (`Animations` folder), locate `Attack 4` and `Attack 5`.
3. Drag and drop `Attack 4` and `Attack 5` into the tool:
   * Rename them to `Attack 2` and `Attack 3` for clarity (assuming `Attack 1` is already present).
4. Click **Add to Animator**.
5. Scroll back up to the **Melee Attack Ability Entry Group**, click the **`+`** icon, and assign the attack animations:
   * Slot 1: `Attack 1`
   * Slot 2: `Attack 2`
   * Slot 3: `Attack 3`
6. Set **Idle Delay** to `0` (or `1`) and select `Idle` as the fallback animation state.

---

## 5. Hitbox Setup & Animation Events

Set up damage dealing by attaching a Hitbox component to the weapon and triggering it via Animation Events.

### 5.1 Setting up the Hitbox Component
1. Select the weapon object (e.g., `Spiky Weapon -> Damage Point`).
2. Click **Add Component** and search for `Hit Box`.
3. Configure the **Hit Box** settings:
   * **Damage**: `5`
   * **Owner**: Drag and drop `Bull Boss New`.
   * **Compare Enemy**: Checked (Drag `Bull Boss New` into the Team Member script slot if prompted).
   * **Activation Mode**: `Manual`
   * **Deactivate Hitbox on Hit**: Unchecked
   * **Deactivate Hitbox after Time**: Unchecked
   * **Destroy Mode on Hit**: `Do Not Destroy`
4. Select `Bull Boss New` again, expand the **Hitbox Controller**, click **`+`**, and assign the `Damage Point` object.

### 5.2 Binding Hitbox via Animation Events
1. Open **Window -> Animation -> Animation**.
2. Select the `Attack 1` animation clip.
3. Scrub the timeline to where the strike begins:
   * Click **Add Event** -> Choose `Hitbox Controller -> ActivateHitbox`.
4. Scrub to where the strike ends:
   * Click **Add Event** -> Choose `Hitbox Controller -> DeactivateHitbox`.
5. Repeat these steps for `Attack 2` and `Attack 3`.

---

## 6. Weapon Trail Effects (Slash Manager)

Create visual slash trails for weapon swings using the `Trail Renderer` and `Slash Manager`.

### 6.1 Trail Object Creation
1. Right-click on the weapon object (`Spiky Weapon`) -> **Create Empty** and name it `Trail`.
2. Add a **Trail Renderer** component:
   * **Width**: Set curve ending at `0` (Top value: `1`).
   * **Time**: `2`
   * **Min Vertex Distance**: `0.01`
   * **Corner Vertices / End Cap Vertices**: `16`
   * **Material**: Assign `/Material` (located under `My Models -> Bull -> Materials`).
   * **Position**: Adjust local transform (e.g., `Y = 6`) to align with the weapon edge.

### 6.2 Slash Manager Configuration
1. Select `Bull Boss New` and expand the **Slash Manager** script.
2. Click **Add New Configuration** for each attack:

| ID And Animation String ID | Wind Up Delay | Swing Active Duration | Weapon Trail Object |
| :--- | :--- | :--- | :--- |
| `Attack 1` | `0.7` | `0.5` | `Trail` |
| `Attack 2` | Default | Default | `Trail` |
| `Attack 3` | Default | Default | `Trail` |

3. Open **Window -> Animation -> Animation**.
4. On frame `0` of each attack animation clip (`Attack 1`, `Attack 2`, `Attack 3`):
   * Add Event -> Select `SlashManager.ActivateSlashWithID`.
   * Pass the string parameter matching the ID (`Attack 1`, `Attack 2`, or `Attack 3`).
5. Disable/Deactivate the `Trail` GameObject in the hierarchy by default.

---

## 7. Sound Effects Configuration

Add audio triggers using the **Universal Sound Player**.

### Steps
1. Select `Bull Boss New` and open the **Animation** window.
2. Select each attack clip (`Attack 1`, `Attack 2`, `Attack 3`).
3. Position the playhead on the frame where the swing sound should play.
4. Click **Add Event**:
   * Function: `UniversalSoundPlayer -> PlayAudioAction`.
   * String Parameter: Pass the corresponding audio action ID (e.g., `Attack Sound 1`, `Attack Sound 2`, `Attack Sound 3`).

---

## 8. Testing & Troubleshooting Checklist

Before entering Play Mode, verify the following setup steps:

- [ ] **Trail Object**: Disabled in the hierarchy.
- [ ] **Game Audio**: Unmuted in the Game Window.
- [ ] **Idle Delay**: Set to `0` in the Enemy Ability System (for instant transitions back to idle after combat ends).