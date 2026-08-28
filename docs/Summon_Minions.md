# Summon Minions

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/P7isgiH3x_8"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This setup provides a comprehensive guide for setting up the **Summon Minions Ability** on the **Bull Boss** using the Boss AI Toolkit in Unity. It covers core ability settings, VFX and teleport spawn location configurations, ground and aerial summoning modes, predefined spawn point setups, and ability sequence management.


## 1. Initial Ability & Proximity Setup

Configure the Summon Minions ability inside the **Enemy Ability System** and adjust probability settings to isolate the ability during testing.

### Steps
1. Select the **Bull Boss New** GameObject in your scene hierarchy.
2. In the **Enemy Ability System**, expand the active Phase group.
3. Adjust proximity parameters:
   * Set **Min Distance** to `0` and **Max Distance** to `100` meters.
4. Set existing ability probabilities (e.g., Spit Attack) to `0%`.
5. Click **Add Ability Entry to Group**.
6. Set **Ability Type** to **Summon Minions**.
7. Set **Summon Minions Probability** to `100%` for isolated testing.
8. Set **Look Mode** to `Target`.

---

## 2. Core Ability & Visual Effects Setup

Configure the casting animation, aura effects, and delay settings for spawning minion entities.

### Steps
1. **Skip Check**: Enable **Skip If Spawned Enemies Exist** to prevent summoning a new wave if previous minions are still active in the arena.
2. **Begin Animation**: Assign the **`magic area`** animation clip.
3. **Casting Effect**: Assign the **`Lightning Aura`** GameObject (active particle system during casting) to the **Effect To Activate** field:
   * Set **Effect Fade Out Duration** to `3` seconds.
4. **Spawn Effect Prefab**:
   * Search for the `Teleport` effect prefab (`Hovl Studio Magic Effects`) in the Project folder.
   * Assign `Teleport` to **Spawn Location Effect Prefab**.
   * Set **Spawn Location Effect Offset** to `0.7` (elevates the effect slightly above ground level).
5. **Timing Delays**:
   * Set **Spawn Effect Delay** to `3` seconds (delay before showing teleport visual indicators).
   * Set **Delay Enemies Spawn After Effects** to `0.5` seconds (delay between visual effect appearance and actual entity instantiation).
   * Set **Idle Delay** to `1` second.

---

## 3. Minion Prefab & Placement Settings

Specify the enemy prefabs to spawn and define their target proximity or sequential spawning options.

### Ground Spawn Configuration Options

| Parameter | Recommended Value | Description |
| :--- | :--- | :--- |
| **Enemies Prefab** | `Knight` Prefab | Melee minion entity instantiated by the ability. |
| **Number of Enemies to Spawn** | `3` | Total count of minion entities spawned per cast. |
| **Spawn Enemies Sequentially** | Unchecked | If enabled, spawns assigned enemy prefabs one after another. |
| **Spawn Range From Target** | `20` meters | Maximum radius around the player where minions spawn. |
| **Distance Between Each Spawned Enemy** | `5` meters | Minimum spatial separation between individual spawned minions. |

---

## 4. Predefined Spawn Points (Optional)

Specify exact positional markers for minion spawning instead of using dynamic target-range spawning.

### Steps
1. Right-click in the Hierarchy -> **Create Empty** and name it **`Predefined Enemy Spawn Points`**.
2. Create three child empty GameObjects inside it:
   * `Predefined Enemy Spawn Point 1` (positioned left of the boss)
   * `Predefined Enemy Spawn Point 2` (positioned right of the boss)
   * `Predefined Enemy Spawn Point 3` (positioned behind the boss)
3. *(Optional)* Parent `Predefined Enemy Spawn Points` under the **Bull Boss New** GameObject.
4. Select **Bull Boss New** and locate the **Summon Minions** settings:
   * Lock the Inspector window.
   * Enable **Spawn At Predefined Points**.
   * Drag all three point transforms into the **Predefined Points** array.
   * Unlock the Inspector window.

---

## 5. Aerial Summoning Setup (Optional)

Enable aerial capabilities to make the boss fly to a designated point before casting the summoning spell.

### Steps
1. Navigate to **Summon Minions** settings on the **Bull Boss New** GameObject.
2. Check **Fly At Certain Point**.
3. **Fly Target Point**: Drag an existing elevated transform (e.g., `Fly Point`) into this slot.
4. Set **Fly Speed** to `3`.
5. Set **Fly Animation** to `Idle` (or a dedicated hover animation).

---

## 6. Execution Sequencing

Combine the Summon Minions ability with other combat abilities (e.g., Melee Attack) using sequential execution.

### Steps
1. Under the active Phase group, set probabilities to `100%` for both **Summon Minions** and **Melee Attack**.
2. Check **Play In Sequence**.
3. Reorder the ability list in the Inspector so **Summon Minions** is positioned at the top above **Melee Attack**.
4. Upon execution, the boss will perform the **Summon Minions** ability first and transition into a **Melee Attack** once the spawn cycle completes.

---

## 7. Verification Checklist

Before running tests in Play Mode, verify the following configuration settings:

- [ ] **Proximity Limits**: Group Min/Max distance set appropriately (`0 - 100` meters).
- [ ] **Probabilities**: `Summon Minions` set to `100%` (and `Play In Sequence` checked if chaining abilities).
- [ ] **Prefabs & Effects**: Teleport effect assigned to **Spawn Location Effect Prefab** and minion asset (`Knight`) assigned to **Enemies Prefab**.
- [ ] **Skip Check**: `Skip If Spawned Enemies Exist` checked if single-wave spawning is desired.
- [ ] **Spawn Points**: If `Spawn At Predefined Points` is enabled, verify all transform slots are populated.