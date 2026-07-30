# First Boss Setup & NavMesh Configuration

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/YIS3VQp4ASg"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>


This guide demonstrates how to clone and set up a new Boss AI entity from scratch using the **Boss AI Cloner**, attach custom weapons, install AI Navigation dependencies, and correctly bake NavMesh surfaces while resolving mesh carving artifacts.

---

## 1. Cloning a Boss Entity

Use the Boss AI Cloner window to duplicate an existing boss setup and apply it to a new model.

### Step 1: Prepare the Model in the Scene
1. Open your project, navigate to your model directory (e.g., `Assets` > `Models`), and drag the new boss model (e.g., **Bull**) into the **Scene View**.
2. Align the new model's position, rotation, and scale to match your reference boss.
3. Assign the appropriate material to the new model's renderer.

### Step 2: Configure the Boss AI Cloner
1. Go to the top menu: `Tools` > `Boss AI Toolkit` > `Duplicate Enemy`.
2. In the **Boss AI Cloner** window, configure the following fields:

| Field | Action |
| :--- | :--- |
| **Source Boss** | Drag and drop the reference boss object (e.g., `Bull Boss`). |
| **Target Boss** | Drag and drop your newly placed model from the Scene View. |
| **New Boss Name** | Enter a unique name (e.g., `Bull Boss New`). |
| **Target Avatar** | Expand the model asset in the Project tab and assign its Avatar (e.g., `Bull Avatar`). |
| **Animator Controller** | Create and assign a new Animator Controller (e.g., `Bull Boss New Animator Controller`). |

### Step 3: Attach a Weapon
1. Click **Add Weapon** in the cloner window.
2. Select your weapon prefab (e.g., `Spiky Weapon / Mace`) and assign it to the **Weapon Object** slot.
3. Expand the **Target Boss** transform hierarchy, locate the right hand bone (or preferred joint), and drag it into the **Weapon Socket** slot.
4. Click **Start Cloning Configuration**. 
5. Click **OK** on the success pop-up and close the cloner tab.

> **NOTE**: Deactivate the old/reference boss object. Adjust the new weapon's Transform (Position, Rotation, Scale) and Material as needed to fit the new model correctly. All core scripts (`Enemy Ability System`, `Capsule Collider`, `NavMesh Agent`, etc.) are automatically duplicated to the new entity.

---

## 2. NavMesh & AI Navigation Setup

### Step 1: Install AI Navigation Package
If your `NavMesh Agent` displays a prompt requiring the navigation package:
1. Go to `Window` > `Package Manager`.
2. Set the registry to **Unity Registry**.
3. Search for **AI Navigation** and click **Install**.

### Step 2: Bake Navigation Mesh
1. Select the environment ground object containing the `NavMesh Surface` component.
2. Click **Bake** to generate navigation data for the scene.

---

## 3. Resolving NavMesh Holes & Carving Issues

Dynamic or complex prop geometry (such as equipped weapons, stones, or player gear) can unintentionally carve unwanted holes into the baked NavMesh.

### Ignore Non-Walkable Geometry
To prevent items from punching holes in the ground navigation mesh, attach a **NavMesh Modifier** component to each prop/weapon:

1. Select the weapon or prop (e.g., `Spiky Weapon`, `Stone`, `Pillar`, `Player Shield`, `Player Sword`).
2. Click **Add Component** > search for **NavMesh Modifier**.
3. Set **Mode** to **Remove Object**.
4. Select the environment ground object containing the `NavMesh Surface` component.
5. Click **Bake** to generate new navigation data for the scene.
