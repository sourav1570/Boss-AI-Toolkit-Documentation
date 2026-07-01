# <span font-weight:bold;">Non Combat Chatter Part-3</span>

<div class="video-container">
    <iframe width="700" height="405" src="https://www.youtube.com/embed/hVD0wtHb4UM?si=PUNwfF04UUhETk_2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Introduction
In this tutorial you will how to setup Non combat chatter script for AI agent.

### Non Combat Chatter

Select the Non Combat Chatter gameObject which is the child of the AI agent. Within this gameObject by default you will find following components attached- Ai Non Combat Chatter Scipt, Sphere Collider and Audiosource Component.[See the image below]

<img src="Images/NonCombatChatter.png" alt="alt text" width="460" height="360">

### Ai Non Combat Chatter

This script is responsible for playing back AudioClips(usually conversations or radio chatter) whenever Player gets within a certain range that is defined by the sphere collider attached to this gameobject. Audio clips from the 'ChatterAudioClips' list and will be played sequentially in the order they are listed. If player will get outside of the trigger and then will re-enter it then the Chatter playback sequence will resume from the next clip in the list. The list of chatter audio clips is played only once for the duration of the player`s presence within the trigger. 

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
        <td>CoreAiBehaviourScript</td>
        <td>Drag&Drop root gameobject of this AI agent with CoreAiBehaviour script attached to it into this field.</td>
    </tr>
    <tr>
        <td>ChatterTriggerObject</td>
        <td>Drag&Drop gameobject (usually the Player) that will trigger the playback of the AiNonCombatChatter audio clips.</td>
    </tr>
    <tr>
        <td>MinChatterDelay</td>
        <td>Minimum delay before playing the chatter audio clips.</td>
    </tr>
    <tr>
        <td>MaxChatterDelay</td>
        <td>Maximum delay before playing the chatter audio clips.</td>
    </tr>
    <tr>
        <td>AudioSourceComponent</td>
        <td>Drag&Drop Audio Source component attached to this gameobject into this field.</td>
    </tr>
    <tr>
        <td>NoElementReplayOnTriggerReEnter</td>
        <td>If checked, the audio clip will continue playing until all clips have finished, even if the player exits the trigger collider. If unchecked, the audio clip will stop and resume from where it left off if the player re-enters the trigger collider. This ensures the player hears all audio clips in the list properly.</td>
    </tr>
    <tr>
        <td>ChatterAudioClips</td>
        <td>List of Audio clips to play sequentially in the order they are listed.</td>
    </tr>
    <tr>
        <td>MinTimeIntervalBetweenChatterClips</td>
        <td>Minimal time interval between playback of the Audio Clips from the list.</td>
    </tr>
    <tr>
        <td>MaxTimeIntervalBetweenChatterClips</td>
        <td>Maximal time interval between playback of the Audio Clips from the list.</td>
    </tr>
</table>

### Speaker

When there are more than one AI agent in the game and you may want only one agent to playback assigned audio clips while other agents to listen to the playing audio clips for this case you need to add a script called 'Speaker' to only one of the agent and drag and drop the other Ai agents in the field name 'Listeners'.[See the image below] This will allow all the AI agent to wait playing the default behaviour until the 'Speaker' has completed the playback of all assigned audio clips.

### Speaker Script

This script is assigned to Ai agent to make him a speaker for the duration of NonCombatChatter. So that other AI agents that are assigned to the list of Listeners would not be able to speak and thus interrupt the speaker. This is achieved by preventing the AiNonCombatChatter script on those listeners agents from playing back any audio clips from their 'ChatterAudioClips' lists. And after the 'Speaker' Ai agent will finish playback of all the audio clips from his list then Speaker as well as all his Listeners will begin performing their default behaviours and playback audio clips from 'DefaultBehaviourAudioClips' list located inside 'HumanoidAiAudioPlayer' script.

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
        <td>Listeners</td>
        <td>Drag and drop all the 'AI agents' listening to this AI agent.</td>
    </tr>
</table>