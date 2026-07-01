# <span font-weight:bold;">Emergency State(Fleeing Behaviour) Part-4</span>

<div class="video-container">
    <iframe width="700" height="405" src="https://www.youtube.com/embed/hVD0wtHb4UM?si=PUNwfF04UUhETk_2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Introduction
This is the Part-4 of AI Emergency State and in this part you will learn about how the AI react in emergency state and perform 'Flee behaviour' when there are no covers around him to take.

### Enable Emergency Alert

To enable emergency alert behaviour on AI agent you need to check the checkbox 'Enable Emergency Alerts' and enabling this checkbox will show the paragraph below called 'AI Emergency State'.

<img src="Images/EmergencyAlert.png" alt="alt text" width="460" height="360">

#### AI Emergency State

This paragraph is responsible for Ai agent behaviour in life threatening situations where he cannot detect the source of the threat and takes several measures to save his life and locate the threat. Most common emergency state triggering situations are when Ai agent will hear bullet impacts near him or will hear dying sound of friendly Ai agent or when he will see another friendly Ai agent in emergency state.All those conditions will result in Emergency behaviour that Ai agent will execute in a various forms depending on two major conditions.When Ai agent gets into Emergency state he will be provided with the coordinate of the supposed enemy position. After that Navmesh path is calculated towards this coordinate.If navmesh path is complete then Ai agent will hide behind available emergency covers for specified time and when this hiding time is expired then Ai agent will advance between emergency covers towards supposed enemy position.If there are no more available emergency covers left for Ai agent on his way to supposed enemy position then Ai agent will start run in a zigzag pattern towards those coordinates to increase survival chances.If navmesh path is incomplete towards supposed enemy position(i.e if supposed enemy coordinate is on the roof of a different building or on the other side of the river etc.) then Ai agent will perform Emergency hiding and shooting in a general direction of the supposed enemy position.This behaviour can be set up that way so that Ai agent could switch emergency covers or stay at the first occupied emergency cover without ever leaving it.

<img src="Images/EmergencyPara.png" alt="alt text" width="460" height="360">

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
        <td>Emergency Cover Finder Component</td>
        <td>Drag and drop Emergency covers finder game object with 'Find Emergency Covers' script attached to it from this Ai agent's hierarchy.</td>
    </tr>
    <tr>
        <td>Emergency Alert Radius Component</td>
        <td>Drag and drop Emergency covers finder game object with 'Emergency Alert Radius' script attached to it from this Ai agent's hierarchy.</td>
    </tr>
    <tr>
        <td>Choose Closest Emergency Covers</td>
        <td>In case this checkbox is active then Ai agent will find closest emergency covers during emergency state.</td>
    </tr>
    <tr>
        <td>Min Range To Find Emergency Cover</td>
        <td>Specifies the minimum emergency covers detection radius.</td>
    </tr>
    <tr>
        <td>Max Range To Find Emergency Cover</td>
        <td>Specifies the maximum emergency covers detection radius.</td>
    </tr>
    <tr>
        <td>Min Time Behind Emergency Cover</td>
        <td>Minimum time to hide behind emergency cover before beginning but not during advancing towards supposed enemy position.</td>
    </tr>
    <tr>
        <td>Max Time Behind Emergency Cover</td>
        <td>Maximum time to hide behind emergency cover before beginning but not during advancing towards supposed enemy position.</td>
    </tr>
    <tr>
        <td>Min Emergency Cover Occupation Distance</td>
        <td>Minimal Emergency Cover occupation distance reaching which Ai agent will stop moving towards it and start hiding behaviour.</td>
    </tr>
    <tr>
        <td>Max Emergency Cover Occupation Distance</td>
        <td>Maximum Emergency Cover occupation distance reaching which Ai agent will stop moving towards it and start hiding behaviour.</td>
    </tr>
    <tr>
        <td>Min Emergency Alert Radius Activation Delay</td>
        <td>Minimum amount in seconds of Ai agent's Emergency Alert Radius Trigger Activation delay.</td>
    </tr>
    <tr>
        <td>Max Emergency Alert Radius Activation Delay</td>
        <td>Maximum amount in seconds of Ai agent's Emergency Alert Radius Trigger Activation delay.</td>
    </tr>
    <tr>
        <td>Pose Transition Duration</td>
        <td>The duration, in seconds, it takes for the AI agent to rotate and focus on emergency cover or shooting points during emergency state. A lower value indicates a faster rotation, while a higher value results in a slower rotation.</td>
    </tr>
    <tr>
        <td>Post First Emergency Cover Behaviour Activity</td>
        <td>Select any of the options from this drop down list that contains various behaviours for Ai agent to perform after expiration of the initial Emergency cover occupation timer.</td>
    </tr>
    <tr>
        <td>Ai Fleeing Behaviour</td>
        <td>This Subsection regulates the parameters of fleeing behaviour when Ai agent sprints away from danger zone when find himself in the emergency situation.</td>
    </tr>
    <tr>
        <td>Advancing Between Covers</td>
        <td>Fields of this subsection are regulating various aspects of Ai agent's advancing between covers towards enemy supposed coordinates.</td>
    </tr>
    <tr>
        <td>ZigZag Advancing</td>
        <td>This subsection sets the coordinate for the final destination of zigzag sprinting and regulates the amplitude of the zigzag sprinting pattern.</td>
    </tr>
    <tr>
        <td>Emergency Shooting</td>
        <td>This subsection regulates various aspects of Emergency Shooting behaviour which if activated will make Ai agent to fire his weapon in general direction of the enemy situated outside of enemy detection parameters of this Ai agent.</td>
    </tr>
</table>

#### AI Fleeing Behaviour Paragraph

This Subsection regulates the parameters of fleeing behaviour when Ai agent sprints away from danger zone when find himself in the emergency situation.

<img src="Images/AIFleePara.png" alt="alt text" width="460" height="360">

<table class="custom-table">
    <tr>
        <th>Fields</th>
        <th>Info</th>
    </tr>
    <tr>
        <td>Flee Destinations</td>
        <td>Set of points with their respective names matching their general flee directions (left, right, backward) and tweakable parametric Min/Max radius is provided for Ai agent in this subsection. Note that if Min / Max radius values are high enough then Ai agent will be able to flee to what appears as an opposite direction of chosen flee point. For example with radius value of the left flee point being bigger than the separation distance of left flee point from Ai agent will result in possibility for Ai agent to flee to the right even though left point is situated to the actual left side of the Ai agent. This is very flexible fleeing behaviour construct that allow users to achieve great deal of customisation. You can get away even with one Flee point that is located right at the origin of Ai agent and has very small value for minimal radius and very big value for maximum radius. Thus allowing Ai agent to flee in any direction or distance within 360 degrees angle.</td>
    </tr>
    <tr>
        <td>Min Flee Duration</td>
        <td>Minimum duration in seconds for Ai Agent to keep sprinting away in case no emergency cover is available to Ai agent at the beginning of Emergency State.</td>
    </tr>
    <tr>
        <td>Max Flee Duration</td>
        <td>Maximum duration in seconds for Ai Agent to keep sprinting away in case no emergency cover is available to Ai agent at the beginning of Emergency State.</td>
    </tr>
    <tr>
        <td>Min Emergency Sprint Away Radius</td>
        <td>Minimal Emergency sprint coordinate value for Ai agent to sprint towards if no Emergency cover is found at the beginning of Emergency state.</td>
    </tr>
    <tr>
        <td>Max Emergency Sprint Away Radius</td>
        <td>Maximum Emergency sprint coordinate value for Ai agent to sprint towards if no Emergency cover is found at the beginning of Emergency state.</td>
    </tr>
    <tr>
        <td>Min Time To Decide Shoot Or Flee Away</td>
        <td>Minimum time required to decide whether to flee or continue shooting.</td>
    </tr>
    <tr>
        <td>Max Time To Decide Shoot Or Flee Away</td>
        <td>Maximum time required to decide whether to flee or continue shooting.</td>
    </tr>
    <tr>
        <td>Flee Away Probability</td>
        <td>Sets the probability of Shooting and Flee away during emergency state.</td>
    </tr>
</table>

