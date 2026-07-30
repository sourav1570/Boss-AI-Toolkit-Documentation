# Getting Started

<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px;">
    <iframe
        src="https://www.youtube.com/embed/csamf61JHGY"
        title="Boss AI Toolkit Tutorial"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen>
    </iframe>
</div>


Welcome to the **Boss AI Toolkit** setup guide. This part will walk you through importing the core toolkit, installing all required dependency assets, and configuring your project's render pipeline (Built-in Render Pipeline vs. Universal Render Pipeline).


## 1. Initial Setup & Demo Scene

Follow these steps to set up the toolkit within your Unity project:

1. **Import the Package**: Open the **Package Manager** in Unity and import the **Boss AI Toolkit** package.
2. **Open the Demo Scene**: 
    - In the **Project** tab, navigate to `Boss AI Toolkit` > `Scenes`.
    - Double-click to open the **Demo Scene**.
3. **Open Setup Wizard**:
    - Go to the top menu bar: `Tools` > `Boss AI Toolkit` > `Getting Started`.

---

## 2. Installing Required Dependency Assets

The Boss AI Toolkit relies on four free dependency assets for visual effects and enemy models. 

| Asset Name | Source | Description |
| :--- | :--- | :--- |
| **Magic Effects Free** | Unity Asset Store | Visual effects for magic abilities |
| **Free Quick Effects** | Unity Asset Store | General visual & particle effects |
| **War Effects** | Unity Asset Store | Combat and impact effects |
| **Mobile Spider and Worm Pack** | Unity Asset Store | Free monster model pack |

### Step-by-Step Installation

1. **Magic Effects Free**
   - Click **Magic Effects Free** inside the *Getting Started* window.
   - The Package Manager will open automatically and search for the asset.
   - *Note:* If you haven't added it to your Unity account yet, click **Download** to open the Asset Store page, add it to **My Assets**, then return to Unity and click **Import**.

2. **Free Quick Effects**
   - Click **Free Quick Effects** in the setup wizard.
   - In Package Manager (under *My Assets*), click **Download** and then **Import**.

3. **War Effects**
   - Click **War Effects** in the setup wizard.
   - Download and click **Import**.

4. **Mobile Spider and Worm Pack**
   - Click the link in the setup wizard.
   - **Troubleshooting**: If the Package Manager shows an error or cannot find the asset name directly, remove a few trailing words from the search query in the top-right search bar of the Package Manager.
   - Click **Import** once located.

> **Note**: After installing all four required assets, close the Package Manager, clear your Unity Console log, and close the *Getting Started* tab.

---

## 3. Render Pipeline Configuration

By default, the Boss AI Toolkit materials are configured for the **Built-in Render Pipeline (BIRP)**. You can easily switch between **BIRP** and **Universal Render Pipeline (URP)** using the included automated converter tool.

---

### Option A: Converting to Universal Render Pipeline (URP)

#### Step 1: Install URP Package
1. Open `Window` > `Package Manager`.
2. Change the package filter dropdown from *In Project* to **Unity Registry**.
3. Search for **Universal RP** (Universal Render Pipeline) and click **Install**.

#### Step 2: Create & Assign URP Asset
1. In your **Project** window, right-click and select `Create` > `Rendering` > `URP Asset (with Universal Renderer)`.
2. Press `Enter` to confirm creation.
3. Open `Edit` > `Project Settings` > `Graphics`.
4. Drag and drop your newly created **URP Asset** into the **Scriptable Render Pipeline Settings** field.
5. Click **Confirm**.

> **Note on Pink Shaders**: Standard materials in the scene will render bright pink at this stage because their shaders belong to BIRP. Custom shaders (such as the Bull enemy's **Dissolve Shader** used for teleportation abilities) will not turn pink as it handle custom shader rendering independently.

#### Step 3: Automated Material Conversion
1. Go to `Tools` > `Boss AI Toolkit` > `Material Pipeline Converter`.
2. In the **Project** window, locate the settings folder: `Boss AI Toolkit` > `Pipeline Settings`.
3. Drag and drop the **URP Settings** (`.json`) file into the converter window's **JSON File** slot.
4. Click **Convert Materials**.

All project materials will automatically be updated for URP.

---

### Option B: Reverting to Built-in Render Pipeline (BIRP)

If you need to switch your project back to the Built-in Render Pipeline from URP:

1. Open `Edit` > `Project Settings` > `Graphics`.
2. Click the **Scriptable Render Pipeline Settings** field, set it to **None**, and click **Confirm**.
3. Open `Tools` > `Boss AI Toolkit` > `Material Pipeline Converter`.
4. Locate the `Pipeline Settings` folder in your project.
5. Drag and drop the **BIRP Settings** (`.json`) file into the converter's **JSON File** slot.
6. Click **Convert Materials**.