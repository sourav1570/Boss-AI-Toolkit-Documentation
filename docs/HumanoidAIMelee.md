# <span font-weight:bold;">Melee Behaviour</span>

<div class="video-container">
    <iframe width="700" height="405" src="https://www.youtube.com/embed/hVD0wtHb4UM?si=PUNwfF04UUhETk_2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Introduction
This video will help you understand how the AI Agent perform Melee Attack against his enemies.


### AI Melee 

To Enable the Melee Attack on AI agent you need to select the Humanoid AI agent and inside the 'Core AI Behaviour' expand the Combat state behaviour and Enable Melee Attack.
[See the image below]

<img src="Images/enableMelee.png" alt="alt text" width="460" height="360">

This will show you a section below called as Ai Melee Attack.

<img src="Images/AIMelee.png" alt="alt text" width="460" height="360">

<style>
    .custom-table {
        border-collapse: collapse;
        width: 100%;
    }
    .custom-table th, .custom-table td {
        border: 1px solid grey;
        padding: 8px;
        text-align: left;
    }
</style>

<table class="custom-table">
    <tr>
        <th>Fields</th>
        <th>Info</th>
    </tr>
    <tr>
        <td>Enable Time Between Melee Attacks</td>
        <td>Activate this checkbox to enable time intervals between Melee attacks.</td>
    </tr>
    <tr>
        <td>Min Time Interval Between Melee Attack</td>
        <td>Minimum Time interval between Melee Attacks.</td>
    </tr>
    <tr>
        <td>Max Time Interval Between Melee Attack</td>
        <td>Maximum time interval between Melee Attacks.</td>
    </tr>
    <tr>
        <td>Min Distance To Attack Player</td>
        <td>Minimum required distance to attack player.</td>
    </tr>
    <tr>
        <td>Max Distance To Attack Player</td>
        <td>Maximum required distance to attack player.</td>
    </tr>
    <tr>
        <td>Min Distance To Attack Enemy Ai Agent</td>
        <td>Minimum required distance to attack enemies Ai agents.</td>
    </tr>
    <tr>
        <td>Max Distance To Attack Enemy Ai Agent</td>
        <td>Maximum required distance to attack enemies Ai agents.</td>
    </tr>
    <tr>
        <td>Animations To Play</td>
        <td>Use slider to decide how many animations to play for Melee attack.</td>
    </tr>
    <tr>
        <td>Melee Animation</td>
        <td>Set of fields to create melee animations for the Ai agent.</td>
    </tr>
    <tr>
        <td>Melee Attack</td>
        <td>Choose melee attack animation to be played during the melee attack. If melee attack 1 is selected, check which animation will be used by going to the scene and then clicking on the Tools <> MobileActionKit < HumanoidAi < EditHumanoidAiAnimations. After clicking 'EditHumanoidAiAnimations', you can drag and drop this Humanoid Ai agent into the field named 'Humanoid Ai animator controller' and click import animations. This way, you will be able to see which animation is used in melee attack 1.</td>
    </tr>
    <tr>
        <td>Melee Animation Clip</td>
        <td>Provide the same melee attack animation clip that you have used for this Humanoid AI agent. You can check which animation you have used by going to the tools < MobileActionKit < HumanoidAi < EditHumanoidAiAnimations. After clicking 'EditHumanoidAiAnimations', you can drag and drop this Humanoid Ai agent into the field named 'Humanoid Ai animator controller' and click import animations. This way, you will be able to see which animation is used for melee attack.</td>
    </tr>
    <tr>
        <td>Melee Damage Scripts Activation Delay</td>
        <td>Set the delay time for activating the melee damage scripts.</td>
    </tr>
    <tr>
        <td>Ai Melee Damage Scripts</td>
        <td>Drag and drop the Ai melee damage scripts attached with the child gameObject of this Ai agent.</td>
    </tr>
</table>




