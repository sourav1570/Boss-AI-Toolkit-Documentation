# Chase & Attack

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/o9PGm-zczII"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>

This part details how to set up both **Ground Projectile Attacks** and **Aerial Projectile Attacks** for the **Bull Boss** using the Boss AI Toolkit in Unity. It covers ability configuration, animation bindings, custom projectile prefab setup, timing logic, and flying point parameters.

---

## 1. Initial Ability & Spawn Point Setup

Configure the core Projectile Attack parameters inside the Enemy Ability System and set up the origin point for projectile instantiation.

### Step 1.1: Projectile Spawn Point Creation
1. Right-click in the Hierarchy and select **Create Empty**.
2. Name the object **`Projectile Spawn Point`**.
3. Position the object near the boss's hand or spine (where projectiles should originate).

### Step 1.2: Core Ability Configuration
1. Select the **Bull Boss** GameObject in the scene hierarchy.
2. Expand the **Enemy Ability System** component.
3. Set previous ability probabilities (e.g., Throw Weapon) to `0%` and click **Add Ability Entry to Group**.
4. Set **Ability Type** to **Projectile Attack**.
5. Set **Projectile Attack Probability** to `100%` for isolated testing.
6. Configure timing and targeting settings:
   * **Look Mode**: `Target`
   * **Powerup Animation Duration**: `3` seconds
   * **Projectile Throw Animation Duration**: `3` seconds
   * **Look At Target While Spawning**: Checked
   * **Projectile Spawn Delay**: `1` second
   * **Initial Projectile Move Delay**: `3` seconds
   * **Parent Spawn Projectile**: Checked (ensures the projectile rotates with the boss before launching).
   * **Idle Delay**: `1` second
7. Assign the **`Projectile Spawn Point`** GameObject to the **Spawn Point** field.

---

## 2. Animation Setup

Import and bind the power-up charge animation and projectile release animation via the **Animation Setup Tool**.

### Steps
1. Open the **Animation Setup Tool** on the **Bull Boss**.
2. Locate the animations in the project folder (`Boss AI Toolkit -> Animations`):
   * **Powerup Animation** (`power up`)
   * **Spellcast / Throw Animation** (`projectile throw`)
3. Click **Add Animation** and assign both clips:
   * Set parameter name for the powerup clip to `Power Up`.
   * Set parameter name for the throw clip to `Projectile Throw`.
4. Click **Add to Animator**.
5. Select **Bull Boss** and set:
   * **Powerup Animation**: `Power Up`
   * **Projectile Throw Animation**: `Projectile Throw`

---

## 3. Projectile Prefab Configuration

Create a custom projectile asset containing physics colliders, trajectory scripts, team detection, and damage hitboxes.

### Step 3.1: Constructing the GameObject Structure
1. Search for `VFX Projectile 01` in the Project tab and drag it into the scene.
2. Unpack the prefab completely and rename/nest it under an empty parent named **`Projectile`**.
3. Unparent `Projectile` to place it at the scene root.

### Step 3.2: Component & Physics Setup
Select the root **`Projectile`** object and add the following three components:
1. **Sphere Collider**:
   * Adjust radius size to fit the visual effect.
   * Check **Is Trigger**.
2. **Projectile Component**:
   * **Moving Delay**: `0`.
   * **Move Speed**: `10`.
   * **Rotation Mode**: `Face Moving Direction`.
   * **Unparent On Move**: Checked (detaches projectile from boss transform upon release).
   * **Offset From Target Position**: Checked.
   * **Min / Max Offset**: X=`0`, Y=`1`, Z=`0`.
3. **Team Member Component**:
   * **Team Name**: Set to match the boss's team (e.g., `Team2`).
   * **My Body Part Target**: Drag `Projectile` into this slot.
4. **Hitbox Component**:
   * **Owner**: Drag `Projectile` into this slot.
   * **Compare Enemy**: Checked.
   * **Script Team Member**: Drag the attached **Team Member** component here.
   * **Activation Mode**: `Auto Activate On Start`.
   * **Activation Delay**: `1` second.
   * **Deactivate Hitbox On Hit**: Checked.
   * **Deactivate Hitbox After Time**: Checked (`5` seconds lifetime).

### Step 3.3: Link Prefab to Ability
1. Drag the configured **`Projectile`** object into your `Prefabs` folder to create a reusable asset.
2. Delete the instance from the Hierarchy.
3. Select **Bull Boss** and drag the new `Projectile` prefab into the **Projectile Prefab** field under ability settings.

---

## 4. Multi-Projectile Cycles & Firing Modes

Configure how multiple projectiles are spawned and cycled during an attack sequence.

### Steps
Set **Projectile Count** to `3`. Choose one of the following cycle modes based on desired behavior:

#### Firing Cycle Modes Comparison

| Cycle Mode | Description | Typical Settings |
| :--- | :--- | :--- |
| **`Restart Cycle`** | Plays the full Powerup and Throw animation sequence individually for **each** spawned projectile. | Delay range: `0.1` to `0.3` seconds. |
| **`Ignore Cycle Restart`** | Plays the charge sequence **once**, then launches all projectiles sequentially within the same continuous cycle. | Projectiles Delay: `1` second between launches. |

---

## 5. Aerial Projectile Attack Setup

Convert the ground attack into an aerial projectile attack where the boss leaps into the air before firing.

### Steps
1. Right-click in Hierarchy -> **Create Empty** and name it **`Fly Point`**.
2. Position `Fly Point` in the air.
3. Select **Bull Boss** and navigate to the **Projectile Attack** settings:
   * Check **Fly To Point**.
   * **Fly Point**: Drag and drop the `Fly Point` GameObject.
   * **Fly Speed**: Set to `3`.
   * **Stay In Air Post Shoot**: Set to `2` seconds (duration boss hovers after completing all projectile cycles before landing).
   * **Return Animation**: Set to `Idle`.

---

## 6. Verification Checklist

Before running tests in Play Mode, verify all parameters against this list:

- [ ] **Spawn Point Assigned**: `Projectile Spawn Point` is linked to the ability.
- [ ] **Unparent On Move**: Enabled on the `Projectile` component so launched projectiles detach from the boss.
- [ ] **Team Name Match**: `Team Member` string on the projectile matches the boss (`Team2`).
- [ ] **Hitbox Setup**: `Compare Enemy` is enabled and linked to the projectile's `Team Member` script.
- [ ] **Aerial Fly Point**: `Fly To Point` is checked and assigned to a valid elevated target point (if setting up aerial attacks).