# <span font-weight:bold;">Post Combat Scan</span>

<div class="video-container">
    <iframe width="700" height="405" src="https://www.youtube.com/embed/hVD0wtHb4UM?si=PUNwfF04UUhETk_2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Introduction
This video will help you understand about the 'Post Combat Scanning' behaviour of the Humanoid AI agent.

### Enable Post Combat Scan

To enable the post combat scan behaviour select the Core AI Behaviour script and than expand the combat behaviour and check the checkbox 'Enable Post Combat Scan'.Checking this checkbox will display a sub section below called as 'Post Combat Aimed Scan Behaviour' where you can tweak the values to achieve the desired behaviour.

<img src="Images/ChooseEnemyPursueType.png" alt="alt text" width="460" height="360">

You can tweak values in this sub section to achieve the desired behaviour.

<img src="Images/PostCombatScanPara.png" alt="alt text" width="460" height="360">

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
        <td>Post Combat Aimed Scan Behaviour</td>
        <td>Set of AI agent`s properties for post combat scan behaviour after the combat state.</td>
    </tr>
    <tr>
        <td>Min Time Between Aimed Turns</td>
        <td>Minimum time to keep aimed look in the direction that resulted after playing previous aimed animation turn clip, before starting playback of the new turn animation clip.</td>
    </tr>
    <tr>
        <td>Max Time Between Aimed Turns</td>
        <td>Maximum time to keep aimed look in the direction that resulted after playing previous aimed animation turn, before starting playback of the new one.</td>
    </tr>
    <tr>
        <td>Min Scan Completion Time</td>
        <td>Minimum time to keep aimed scanning before switching to non combat state.</td>
    </tr>
    <tr>
        <td>Max Scan Completion Time</td>
        <td>Maximum time to keep aimed scanning before switching to non combat state.</td>
    </tr>
    <tr>
        <td>Play Animations Sequentially</td>
        <td>If checked scan animations will playback sequentially. In case unchecked, the scan animations will playback randomly.</td>
    </tr>
    <tr>
        <td>Aimed Turning Animations</td>
        <td>Create up to 4 turning directions for AI agent to perform during aimed scanning.</td>
    </tr>
      <tr>
        <td>Turn Direction</td>
        <td>Choose one of 4 turning directions from this list. AI agent will play corresponding animation clip from the animation tree that is assigned to this direction.</td>
    </tr>
    <tr>
        <td>Min Aimed Turn Animation Speed</td>
        <td>Minimal playback speed of the the turn animation clip.</td>
    </tr>
    <tr>
        <td>Max Aimed Turn Animation Speed</td>
        <td>Maximal playback speed of the the turn animation clip.</td>
    </tr>
</table>





