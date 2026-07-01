# <span font-weight:bold;">Grenade Alerts Part-3</span>

<div class="video-container">
    <iframe width="700" height="405" src="https://www.youtube.com/embed/hVD0wtHb4UM?si=PUNwfF04UUhETk_2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Introduction
This is the Part-3 of AI Grenades and in this part you will learn about how the AI agent get alerted when the grenade lands near him.

### Enable Grenade Alerts

To make Humanoid AI agent to be alerted by a grenade. You need to enable grenade alert checkbox by going to 'Core AI Behaviour' script and than under 
'Combat state behaviours' check the checkbox 'Enable Grenade Alerts'.

<img src="Images/GrenadeAlerts.png" alt="alt text" width="460" height="360">

#### Humanoid Grenade Alerts

Set of AI agent`s properties for grenade alert behaviour.

<img src="Images/GrenadeAlertParagraph.png" alt="alt text" width="460" height="360">

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
        <td>Grenade Detector</td>
        <td>Drag and drop grenade detector gameObject from the hierarchy of this AI agent into this field.</td>
    </tr>
    <tr>
        <td>Visible Layers</td>
        <td>Specify which layers will be visible when detecting incoming grenades.</td>
    </tr>
    <tr>
        <td>Choose Alert Type</td>
        <td>Choose one of the options from the list provided below. If 'MoveAwayFromLandedGrenades' is selected then the AI agent will 100% move away from the grenades if he is within the trigger area. In case the second option is chosen 'RandomizeMoveFromLandedGrenades' then the AI agent will have a 50/50 chance to decide whether to move away from landed grenades or not.</td>
    </tr>
    <tr>
        <td>Retreat Points</td>
        <td>Drag and drop retreat point child game objects of AI agent in this list.</td>
    </tr>
    <tr>
        <td>Retreat Point Radius</td>
        <td>After getting world coordinates of a retreat point another second world coordinate is created within the retreat point radius. AI agent runs towards this second world coordinate instead of the initial world coordinate of a retreat point. The bigger this value is the more unpredictable the resulted retreat direction and distance will get.</td>
    </tr>
    <tr>
        <td>Retreat Timer</td>
        <td>Value in this field is defining allowed time for the AI agent to perform retreat behavior. When this value is expired the AI agent will get back to the previous behavior. In case the fight was over while AI agent was performing retreat behavior then the AI agent will get back to whatever state he was in before this fight started.</td>
    </tr>
</table>

