# <span font-weight:bold;">Covers Fields Explanation</span>

<div class="video-container">
    <iframe width="700" height="405" src="https://www.youtube.com/embed/hVD0wtHb4UM?si=PUNwfF04UUhETk_2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Introduction
This is the Part-5 of Humanoid AI Covers and in this part you will learn about fields in the paragraph called 'Ai Covers' located in the 'Core AI Behaviour'.

### AI Covers

Fields in this section will take effect if AI agent will be structured the way that allows him take covers during combat.i.e If Ai agent is not configured to be stationary and 'Use Covers' checkbox is checked.Ai Agent detects cover assemblies by the colliders of their child cover points.And then creates the list of all covers within specified range. And then does requests to cover assemblies of interest during the combat state.

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
        <td>Cover Finder</td>
        <td>Drag and drop the child gameObject of this Ai agent which has a script named 'FindCovers' from the hierarchy into this field.</td>
    </tr>
    <tr>
        <td>Choose Closest Covers</td>
        <td>If enabled, the Ai agent will find the closest covers from his current position. If this checkbox is disabled, the Ai agent will take a random cover within the range specified in the field 'RangeToFindCoverPoint'.</td>
    </tr>
    <tr>
        <td>Switching Covers Probability</td>
        <td>The slider value below indicates the probability of the Ai agent switching to new covers. If the value is 100, the Ai agent will switch between different covers around him. If the value is 0, the Ai agent will not switch to any new cover after taking his first cover and will stay in his first cover for the duration of combat. Depending on the probability, the Ai agent will decide whether to pick a new cover or stay at the currently picked one. If the taken cover becomes invalid, the Ai agent will switch to another valid cover.</td>
    </tr>
    <tr>
        <td>Range to Find Existing Cover Points</td>
        <td>Range within which the Ai agent will find cover points to hide behind.</td>
    </tr>
    <tr>
        <td>Enable Sprinting Between Covers</td>
        <td>If unchecked, the AI agent will perform an assault by walking and shooting its target.</td>
    </tr>
    <tr>
        <td>Min Sprinting Distance</td>
        <td>Minimal value for remaining distance to target to set the shortest limit for random value.</td>
    </tr>
    <tr>
        <td>Max Sprinting Distance</td>
        <td>Maximal value for remaining distance to target to set the longest limit for random value.</td>
    </tr>
    <tr>
        <td>Min Time to Check for Covers</td>
        <td>Minimum time the AI agent will check for cover availability. If an AI agent cannot find a suitable cover at the start of the game, he will check for free cover. If the AI agent is already behind cover, he will not consider checking for cover again, even if the cover time has expired.</td>
    </tr>
    <tr>
        <td>Max Time to Check for Covers</td>
        <td>Maximum time the AI agent will check for cover availability. If an AI agent cannot find a suitable cover at the start of the game, he will check for free cover. If the AI agent is already behind cover, he will not consider checking for cover again, even if the cover time has expired.</td>
    </tr>
    <tr>
        <td>Min Time Between Covers</td>
        <td>Minimum time the AI agent will spend behind the current cover before taking another available cover point.</td>
    </tr>
    <tr>
        <td>Max Time Between Covers</td>
        <td>Maximum time the AI agent will spend behind the current cover before taking another available cover point.</td>
    </tr>
    <tr>
        <td>Min Time at Open Fire Point</td>
        <td>Minimum time that the AI agent will stay at the Open Fire point before returning to the cover point, or leaving the cover if other combat behavior comes into effect.</td>
    </tr>
    <tr>
        <td>Max Time at Open Fire Point</td>
        <td>Maximum time that the AI agent will stay at the Open Fire point before returning to the cover point, or leaving the cover if other combat behavior comes into effect.</td>
    </tr>
    <tr>
        <td>Transition Speed to Stand Cover</td>
        <td>Speed at which the AI agent will be procedurally rotated to the stand hiding pose.</td>
    </tr>
    <tr>
        <td>Taken Cover Proximity Distance</td>
        <td>Remaining distance to cover point at which the AI agent registers himself occupying it.</td>
    </tr>
    <tr>
        <td>Enable Reloading Behind Hide Covers</td>
        <td>If enabled, the AI agent will be able to reload his weapon when behind the hide cover, e.g., Stand Hide Cover, Crouch Hide Cover.</td>
    </tr>
    <tr>
        <td>Reload Delay Behind Stand Hide Cover</td>
        <td>Delay value to allow for AI agent rotation and playback of stand hide cover animation before reloading his weapon.</td>
    </tr>
    <tr>
        <td>Reload Delay Behind Crouch Hide Cover</td>
        <td>Delay value to allow for AI agent playback of crouch hide cover animation before reloading his weapon. To prevent reloading animation from previous state (like running or walking/strafing).</td>
    </tr>
    <tr>
        <td>Reload If Ammo Left in Magazine Is Less Than</td>
        <td>Allows the AI agent to reload his weapon while he is at stand or crouch hide cover points even if the magazine is not yet empty.</td>
    </tr>
    <tr>
        <td>Min Stop and Shoot Cancel Distance to Cover</td>
        <td>Minimum distance to cancel Stop and Shoot behavior if the distance to the cover is less than or equal to the value specified in this field.</td>
    </tr>
    <tr>
        <td>Max Stop and Shoot Cancel Distance to Cover</td>
        <td>Maximum distance to cancel Stop and Shoot behavior if the distance to the cover is less than or equal to the value specified in this field.</td>
    </tr>
    <tr>
        <td>Open Fire Behaviour</td>
        <td>Fields in this subsection are setting the AI agent's weapon firing behavior while he is moving towards or between covers. This subsection is reused in three different combat-related paragraphs: Ai Charging, Ai Covers, and Ai Firing Points. In each case, this subsection defines Open Fire Behavior in relation to the parent paragraph's subject. In the 'Ai Charging' paragraph, fields will define shooting behavior in relation to enemies. In the 'AI Covers' paragraph, those fields are used in relation to covers. In the 'Ai Firing Points' paragraph, in relation to Firing points. The value in this field is related to cover instead of enemy or the Fire Point.</td>
    </tr>
    <tr>
        <td>Stop and Shoot Probability</td>
        <td>This slider sets the probability of 'Stop and Shoot' behavior while the AI agent is moving towards or between covers.</td>
    </tr>
    <tr>
        <td>Strafing Probability</td>
        <td>This slider sets the probability of 'Strafing' behavior while the AI agent is moving towards or between covers.</td>
    </tr>
    <tr>
        <td>Min Stop and Shoot Distance to Enemy or Cover</td>
        <td>Minimal distance towards the cover to activate Stop&Shoot behavior.</td>
    </tr>
    <tr>
        <td>Max Stop and Shoot Distance to Enemy or Cover</td>
        <td>Maximum distance towards the cover to activate Stop&Shoot behavior.</td>
    </tr>
    <tr>
        <td>Min Time Till Stop and Shoot Behaviour</td>
        <td>Minimum time since the AI agent decided to go towards or between covers till he starts Stop&Shoot behavior.</td>
    </tr>
    <tr>
        <td>Max Time Till Stop and Shoot Behaviour</td>
        <td>Maximum time since the AI agent decided to go towards or between covers till he starts Stop&Shoot behavior.</td>
    </tr>
    <tr>
        <td>Min Stop and Shoot Duration</td>
        <td>Minimum duration in seconds of the Stop&Shoot behavior.</td>
    </tr>
    <tr>
        <td>Max Stop and Shoot Duration</td>
        <td>Maximum duration in seconds of the Stop&Shoot behavior.</td>
    </tr>
</table>


