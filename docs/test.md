# Setting Up and Configuring a Zombie AI Agent in Unity

This documentation provides a detailed, step-by-step guide on setting up a zombie model, configuring its AI, downloading and integrating animations from Mixamo, and optimizing them within your Unity project.

---

## 1. Preparing the Zombie Model

Before you begin, ensure you have your zombie model ready. This tutorial uses a pre-rigged Mixamo model.

1.  **Locate the Model:**
    * In your **Project** window, navigate to `Mobile Action Kit` > `Art` > `Zombie`.
    * Select the zombie model (e.g., "zombie"). You can preview it in the Inspector window.
2.  **Configure Animation Type:**
    * With the zombie model selected in the Project window, go to its **Rig** tab in the Inspector.
    * Set **Animation Type** to **Humanoid**.
    * Set **Avatar Definition** to **Create From This Model**.
    * Click **Apply**.
3.  **Place in Scene and Unpack Prefab:**
    * Drag and drop the zombie model from the Project window into your **Scene View**.
    * Adjust its position and rotation (e.g., rotate 90 degrees on the Y-axis) so it faces a suitable direction.
    * In the Hierarchy, **right-click** on the newly placed zombie model.
    * Go to **Prefab** > **Unpack Completely**. This allows you to modify the instance without affecting the original prefab.
4.  **Rename Sub-Objects (Optional but Recommended):**
    * If your model has default naming, you might want to rename parts for clarity. For instance, rename a child object like "cylinder.002" to **Zombie Skin**.

---

## 2. Setting Up Humanoid AI Agent

The Mobile Action Kit provides a tool to quickly set up AI agents.

1.  **Open Setup Humanoid AI Agent Window:**
    * Go to **Tools** > **Mobile Action Kit** > **Humanoid AI** > **Setup Humanoid AI Agent**.
    * Position this window conveniently.
2.  **Configure AI Agent Properties:**
    * **Humanoid AI Type:** Select **Zombie**.
    * **Reference AI Prefab:**
        * In your **Project** window, navigate to the `Prefabs` folder (within `Mobile Action Kit` or your designated prefabs location).
        * Locate the **Zombie Reference Prefab** model.
        * Drag and drop this `Zombie Reference Prefab` into the **Reference AI Prefab** field in the `Setup Humanoid AI Agent` window. This prefab contains pre-configured components that will be copied to your new zombie instance.
    * **Humanoid Model:**
        * Drag and drop the **zombie model** that's located in your **Hierarchy** into this field.
    * **Human Model Avatar:**
        * In the **Project** window, select your **zombie model**.
        * Expand its hierarchy in the Project Inspector (if necessary).
        * Locate the **Avatar** asset (usually named after your model, e.g., "zombieAvatar").
        * Drag and drop this **zombieAvatar** into the **Human Model Avatar** field.
    * **My Body Part To Target:**
        * In the Hierarchy, expand your **zombie model** until you find the **mixamohips** and then its child bones.
        * Locate the **headbone**.
        * Drag and drop the **headbone** into the **My Body Part To Target** field. This specifies the target for other AI entities (like soldiers) to aim at.
3.  **Configure AI Agent:**
    * Click the **Configure Humanoid AI Agent** button.
    * This action automatically adds all necessary components and game objects to your zombie model based on the reference prefab, making it functional as an AI.

---

## 3. Adjusting Materials and Hierarchy

1.  **Reorganize Hierarchy (Optional but Recommended):**
    * In the Hierarchy, select the **Zombie Skin** and **mixamohips** GameObjects.
    * Drag them to the top level of your **zombie model's** hierarchy for easier access and clarity.
2.  **Apply Materials:**
    * Select the **Zombie Skin** GameObject in the Hierarchy.
    * In the Project window, navigate to the `Materials` folder (within your zombie model's assets).
    * Drag and drop your desired material (e.g., **Zombie Variant 3**) onto the `Zombie Skin` GameObject in the Scene View or directly onto its Material slot in the Inspector.

---

## 4. Setting Up the Ragdoll

Ragdoll physics allow for realistic death animations.

1.  **Open Setup Humanoid AI Agent Window:**
    * Go back to **Tools** > **Mobile Action Kit** > **Humanoid AI** > **Setup Humanoid AI Agent**.
2.  **Create Ragdoll:**
    * Click the **Create Ragdoll** button. This opens the Ragdoll Wizard.
3.  **Assign Bones:**
    * **Pelvis Bone:** Drag and drop **mixamohips** from the Hierarchy to the **Pelvis** field.
    * **Left Hip:** Drag and drop **LeftUpLeg**.
    * **Left Knee:** Drag and drop **LeftLeg**.
    * **Left Foot:** Drag and drop **LeftFoot**.
    * Repeat for **Right Hip**, **Right Knee**, and **Right Foot** using their respective bones.
    * **Middle Spine:** Drag and drop the **spine** bone.
    * Assign other required bones as indicated by the Ragdoll Wizard (e.g., chest, head, arms).
4.  **Finalize Ragdoll Creation:**
    * Click **Create Ragdoll**.
5.  **Adjust Colliders:**
    * After creating the ragdoll, expand the `mixamohips` GameObject in the Hierarchy.
    * Select individual colliders (e.g., Capsule Colliders, Box Colliders) attached to the bones.
    * In the Scene View, adjust their size, position, and rotation to accurately encompass the body parts of your zombie model.

---

## 5. Configuring Layers and Tags

1.  **Enable Gizmos:**
    * In the Scene View, click the **Gizmos** button to ensure you can see colliders and other components.
2.  **Set Tag and Layer for Zombie Root:**
    * Select the **zombie model** (root GameObject) in the Hierarchy.
    * In the Inspector, set its **Tag** to **AI**.
    * Set its **Layer** to **AI**.
3.  **Set Layers for Children GameObjects:**
    * Observe that some child GameObjects within your zombie model might not have their layers changed.
    * For each child GameObject that needs its layer changed:
        * Select the GameObject.
        * Click on its **Layer** dropdown in the Inspector (it might show "Default").
        * Select **AI**.
        * A prompt "Do you want to apply changes to children?" will appear. Click **Yes, change children**. Repeat this for any other necessary child GameObjects.

---

## 6. Managing Ragdoll Kinematics

When setting up a ragdoll for an animated character, you need to manage its kinematic state to avoid conflicts between animations and physics.

1.  **Select Rigidbodies:**
    * In the Hierarchy, select all GameObjects that have a **Rigidbody** component attached (these are typically the bones of your ragdoll). You can multi-select them.
2.  **Enable Is Kinematic:**
    * In the Inspector, locate the **Rigidbody** component.
    * Check the **Is Kinematic** checkbox.
    * *Explanation:* Enabling `Is Kinematic` means the Rigidbody will be controlled by animations rather than physics simulation (like gravity). This prevents the ragdoll from collapsing while the animation is playing. When the zombie "dies," the `Is Kinematic` checkbox will be automatically unchecked via script (by enabling the "Enable Ragdoll" checkbox in the Humanoid AI Health script), allowing physics to take over for a realistic fall.

---

## 7. Preparing Animator Controller

To integrate animations, you'll work with an Animator Controller.

1.  **Duplicate Base Animator Controller:**
    * In the Project window, navigate to `Mobile Action Kit` > `Humanoid AI` > `Animator Controllers`.
    * Locate the **Zombie AI Base Animator Controller**.
    * Select it and press **Ctrl+D** (Windows) or **Cmd+D** (Mac) to duplicate it.
    * Rename the duplicated controller to something like **Zombie AI Animator Controller**. This ensures you don't modify the base asset.
2.  **Assign New Animator Controller:**
    * Select your **zombie model** in the Hierarchy.
    * In the Inspector, locate the **Animator** component.
    * Drag and drop your newly created **Zombie AI Animator Controller** from the Project window to the **Controller** field.

---

## 8. Downloading and Preparing Animations from Mixamo

You'll need various animation clips for your zombie's behavior.

1.  **Open Edit Humanoid AI Animations Window:**
    * Go to **Tools** > **Mobile Action Kit** > **Humanoid AI** > **Edit Humanoid AI Animations**.
    * Position this window conveniently.
2.  **Assign Humanoid AI Animator Controller:**
    * Drag and drop your **zombie model** from the Hierarchy to the **Humanoid AI Animator Controller** field in the `Edit Humanoid AI Animations` window.
    * Set **Character Type** to **Zombie**.
3.  **Download Animations from Mixamo:**
    * Go to [Mixamo.com](https://www.mixamo.com/) in your web browser.
    * Search for and select a **zombie character** if you haven't already.
    * For each animation listed below, search on Mixamo, download it, and save it to your project's assets (e.g., in a new `Animations` folder).
    * **Crucial Download Settings:**
        * **Format:** FBX for Unity
        * **Skin:** With Skin (for initial download, this will be optimized later)
        * **In Place:** Check this for movement animations (Idle, Walk, Run, Sprint, Turn). Uncheck for attacks and death.
        * **Mirror:** Check/uncheck as needed for turn animations (e.g., mirror for turn left if using a turn right animation).

    Here's a list of animations you'll need:
    * **Stand Idle:** Search for "idle" (e.g., "Full Post Idle").
    * **Turn Left:** Search for "zombie turn," download, and **mirror** it.
    * **Turn Right:** Search for "zombie turn," download, and **unmirror** it.
    * **Turn Forward/Turn Backward:** You can use the same "zombie turn" animations or find specific forward/backward turn animations.
    * **Walk Forward:** Search for "zombie walk" (choose an "in place" animation).
    * **Run Forward:** Search for "zombie run" (choose an "in place" animation).
    * **Sprinting:** You can use the same "run forward" animation or a dedicated "sprinting" animation.
    * **Melee Attack 1:** Search for "zombie attack" (e.g., "Kick").
    * **Melee Attack 2:** Search for "zombie attack" (e.g., another "Punch" or "Swing").
    * **Melee Attack 3:** Search for "zombie bite" (e.g., "Neck Bite").
    * **Upper Body Hit 1, 2, 3:** Search for "zombie hit" (download 2-3 different hit reactions).
    * **Lower Body Hit 1, 2, 3:** You can use the same "zombie hit" animations or different ones.
    * **Death Animations (Dying 1, 2):** Search for "zombie dying" (download 2 distinct death animations).

---

## 9. Renaming and Modifying Animation Clips

Mixamo FBX files often contain multiple animation clips and unnecessary data. You need to clean them up.

1.  **Import All Downloaded Animations:**
    * Select all the downloaded FBX animation files in your operating system's file explorer.
    * Drag and drop them into an `Animations` folder within your Unity project's Project window.
2.  **Open Rename and Modify Animations Window:**
    * Go to **Tools** > **Mobile Action Kit** > **Humanoid AI** > **Rename and Modify Animations**.
3.  **Process Each Animation FBX:**
    * Drag and drop *one* of your imported animation FBX models from the Project window into the field in the `Rename and Modify Animations` window.
    * Provide a **New Name** for the animation clip (e.g., "MilliAttackOne", "ZombieIdle", "DyingAnimationOne").
    * Click **Rename Game Object and Animation Clip**.
    * *Result:* The FBX file will be renamed, and it will now contain only one animation clip with the specified name.
    * Repeat this process for *all* your downloaded animation FBX files, giving them clear, descriptive names. (e.g., "MilliAttackTwo", "BodyHitAnimationOne", "ZombieRun", "TurnLeft", "DyingAnimationTwo", etc.)

---

## 10. Optimizing Animation Clips and Assigning to Animator

After renaming, you'll optimize the animation files to reduce project size and prepare them for the Animator Controller.

1.  **Open Edit Humanoid AI Animations Window:**
    * Go to **Tools** > **Mobile Action Kit** > **Humanoid AI** > **Edit Humanoid AI Animations**.
2.  **Assign Animation Clips to Fields:**
    * Drag and drop the appropriate **animation clips** (not the FBX models, but the clips *within* the FBX models, now that they are clean) from your Project window to their respective fields in the `Edit Humanoid AI Animations` window.
    * For `Turn Forward` and `Turn Backward`, you can use `Turn Left` and `Turn Right` animations if you don't have separate ones.
    * For `Sprinting`, you can use the `Zombie Running` animation.
    * Assign `Body Hit Animation 1` and `Body Hit Animation 2` to the `Upper Body Hit` and `Lower Body Hit` slots as you see fit.
    * **Do not assign the Death Animations yet.**
3.  **Duplicate and Modify Import Settings:**
    * Click the **Duplicate Animation Clip and Modify Import Settings** button.
    * *Process:* This step optimizes each assigned animation clip. It creates separate instances for shared animations (like "Sprinting" using "Run Forward") and adjusts their import settings (e.g., **Loop Time**, **Loop Pose**, **Root Transform Position**, **Bake into Pose**) to match the project's requirements for seamless looping and root motion.
    * This may take a few seconds.
4.  **Delete Redundant FBX Files:**
    * After the optimization, you will notice that the `Edit Humanoid AI Animations` window now uses the optimized animation clips directly.
    * You can now select and **delete** all the original FBX animation models from your `Animations` folder in the Project window, *except* for the Death Animation FBX files (`Dying Animation 1` and `Dying Animation 2`). This significantly reduces project size.

---

## 11. Finalizing Death Animations

Death animations require a slightly different import process.

1.  **Convert Death Animation FBX to Humanoid:**
    * Select `Dying Animation 1` and `Dying Animation 2` FBX models in the Project window.
    * Go to the **Rig** tab in the Inspector.
    * Set **Animation Type** to **Humanoid**.
    * Set **Avatar Definition** to **Create From This Model**.
    * Click **Apply**.
2.  **Extract Death Animation Clips:**
    * Expand `Dying Animation 1` in the Project window.
    * Select the animation clip inside (it will likely have the FBX file's name).
    * Press **Ctrl+D** (Windows) or **Cmd+D** (Mac) to **duplicate** the animation clip. This extracts it as a separate `.anim` asset.
    * Rename the extracted clip to `Dying Animation 1`.
    * Repeat this for `Dying Animation 2`.
3.  **Configure Extracted Death Clips:**
    * Select the extracted `Dying Animation 1` and `Dying Animation 2` `.anim` assets in the Project window.
    * In the Inspector, ensure the following are set for both:
        * **Loop Time:** Unchecked (death animations typically don't loop).
        * **Bake into Pose (Rotation):** Checked, **Based Upon:** Original
        * **Bake into Pose (Position):** Checked, **Based Upon:** Original
4.  **Assign Death Animations to Animator:**
    * Go back to the **Edit Humanoid AI Animations** window.
    * Drag and drop the extracted `Dying Animation 1` and `Dying Animation 2` `.anim` assets to their respective **Death Animation Clip** fields.
    * Click **Add Death Animation Clips to Animator**. This will integrate them into your `Zombie AI Animator Controller`.
5.  **Save Changes:**
    * Click **Save New Animations to Animator**. This finalizes all animation assignments and settings in your Animator Controller.
6.  **Delete Original Death FBX Files:**
    * You can now safely delete the original `Dying Animation 1` and `Dying Animation 2` FBX models from your Project window, as their animation clips have been extracted.

---

## 12. Assigning Missing GameObjects and Final Checks

Before running the game, some fields in your zombie's components need to be assigned.

1.  **Create Helper GameObjects:**
    * In the Hierarchy, expand your **zombie model** > **mixamohips** > **headbone**.
    * **Right-click** on **headbone** > **Create Empty**.
    * Rename this new GameObject to **Field of View GameObject**. Position it slightly in front of the headbone.
    * Duplicate **Field of View GameObject** (Ctrl+D/Cmd+D).
    * Rename the duplicate to **Hide To Unhide Enemy Switcher**. Position it similarly.
    * Duplicate **Hide To Unhide Enemy Switcher**.
    * Rename the duplicate to **Vision Obstacle Checker**. Position it similarly.
2.  **Assign GameObjects to Zombie Components:**
    * Select your **zombie model** in the Hierarchy.
    * In its Inspector, scroll through the various components until you find the following fields and drag and drop the corresponding GameObjects:
        * **Humanoid AI Controller:**
            * **Field Of View Game Object:** Drag and drop **Field of View GameObject** (the one you just created).
            * **Hide To Unhide Enemy Switcher:** Drag and drop **Hide To Unhide Enemy Switcher**.
        * **Humanoid Visibility Checker:**
            * **Vision Obstacle Checker:** Drag and drop **Vision Obstacle Checker**.
        * **Head Bone For Detection Validator:**
            * **Headbone For Detection Validator:** Drag and drop the original **headbone** (the actual bone in the rig, not the helper GameObjects).
3.  **Set Agent Role and Default Behavior:**
    * In the **Humanoid AI Controller** component (on your zombie model):
        * **Agent Role:** Ensure this is set to **Zombie**.
        * **Default Behavior:** For testing, set this to **Stationary**. Keep other settings as default for now.
4.  **Save Your Scene and Project.**

---

## 13. Testing the Zombie AI

1.  **Run the Game:**
    * Click the **Play** button in Unity.
    * The zombie should now appear in the scene and, with `Default Behavior` set to `Stationary`, it might start moving towards the player if they are within its detection range.

2.  **Understanding Team IDs (Important for AI Interaction):**
    * Exit Play Mode.
    * Select your **zombie model** in the Hierarchy.
    * In the **Humanoid AI Controller** component, locate **My Team ID**.
    * **Default Behavior (Team 2):** By default, zombies are usually on "Team 2" and will attack "Team 1" (which typically includes the player).
    * **Changing Team (Team 1):** If you set the **My Team ID** of the zombie to **Team 1** (the same as the player), the zombie will **not** attack the player, as it now perceives the player as an ally. This is useful for testing different AI interactions without immediate combat.