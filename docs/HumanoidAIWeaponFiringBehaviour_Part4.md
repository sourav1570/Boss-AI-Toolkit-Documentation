# <span font-weight:bold;">Weapon Firing Behaviour Part-4</span>

<div class="video-container">
    <iframe width="700" height="405" src="https://www.youtube.com/embed/hVD0wtHb4UM?si=PUNwfF04UUhETk_2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Introduction
This is the Part-4 of Humanoid AI Weapon Firing Behaviour and in this part we have covered the topic called - Line of fire check.
This paragraph defines the LineOfFireChecks parameters when Aiming AI agent is careful not to fire his weapon when his friendlies are within a specified distance from the line of fire.Thus minimising the chances of accidental friendly fire. Aiming Ai agent will check if any friendly AI agents are within line of fire threshold which is checked along X and Y axis from his root objects local Z axis which would be facing the enemy at the time of this check.And if separation between Ai agent`s root object local Z axis and friendly AI agent closest to the line of fire in both X and Y axis Line Of fire threshold values is less then allowed for both of those values then AI agent will cease fire until his friendly gets further away from his local Z axis along either Y or X axis so that friendly Ai agent would get outside of line of fire threshold.In case aiming Ai agent will be standing and closest friendly to the line of fire will be crouching in front of him, then X and Y proximity checks will be bypassed and  aiming Ai agent would be able to open fire.And in case aiming Ai agent is crouching then X and Y proximity checks will be done regardless of whether closest friendly to the line of fire is crouching or standing. 

### Humanoid AI Weapon Firing Behaviour 

<img src="Images/LineOfFireCheck.png" alt="alt text" width="460" height="360"> 

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
        <td>Enable Line Of Fire Checks</td>
        <td>If enabled then Ai agent will check if any of his friendlies are within LineOfFire threshold before firing his weapon and if they are then Ai agent will not shoot until they move out of his line of fire.</td>
    </tr>
    <tr>
        <td>Line Of Fire Proximity X</td>
        <td>Distance along local X axis from direct line of fire within which to do the checks for friendlies.</td>
    </tr>
    <tr>
        <td>Line Of Fire Proximity Y</td>
        <td>Distance along local Y axis from direct line of fire within which to do the checks for friendlies.</td>
    </tr>
    <tr>
        <td>Debug Proximity To Line Of Fire</td>
        <td>If checked then will display in the fields below the proximity values of the closest friendly Ai agent to LineOfFire.</td>
    </tr>
    <tr>
        <td>Display X Axis Proximity</td>
        <td>Displays the friendly Ai agent separation along X axis from direct line of fire.</td>
    </tr>
    <tr>
        <td>Display Y Axis Proximity</td>
        <td>Displays the friendly Ai agent separation along Y axis from direct line of fire.</td>
    </tr>
    <tr>
        <td>Min Time Between Line Of Fire Checks</td>
        <td>Minimal time interval between checks for friendlies within line of fire dangerous proximity.</td>
    </tr>
    <tr>
        <td>Max Time Between Line Of Fire Checks</td>
        <td>Maximal time interval between checks for friendlies within line of fire dangerous proximity.</td>
    </tr>
</table>








