# <span font-weight:bold;">Player Footstep Sounds Based On Surfaces</span>

<div class="video-container">
    <iframe width="700" height="405" src="https://www.youtube.com/embed/hVD0wtHb4UM?si=PUNwfF04UUhETk_2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Introduction
This video will guide you on how to setup different footstep sounds at different surfaces i.e - Grass,Metal. There are two ways using which you can create footstep sounds at different surfaces. You can detect at which collider the player is moving by using Trigger based collider Or by using Raycast.

### Player Surfaces (Collider Detection)

You can create any collider example: A Box collider and check its is Trigger Checkbox and add a component to that gameObject called 'PlayerSurfaces'. [See The Image below]

Script Info: This Script is Responsible To Change the Player Walk and Run Sounds Within the Surface Area For Example : Metal Surface , Grass Surface etc... 

<img src="Images/FootStepSound_Image1.png" alt="alt text" width="460" height="360">                                     
 
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
        <td>PlayerManagerScript</td>
        <td>Reference to the PlayerManager script for player-related functions.</td>
    </tr>
    <tr>
        <td>FirstPersonControllerScript</td>
        <td>Reference to the FirstPersonController script for movement-related functions.</td>
    </tr>
    <tr>
        <td>AudioSourcesProperties.WalkAudioSourceComponent</td>
        <td>Audio source for the walking sound.</td>
    </tr>
    <tr>
        <td>AudioSourcesProperties.RunAudioSourceComponent</td>
        <td>Audio source for the running sound.</td>
    </tr>
    <tr>
        <td>AudioSourcesProperties.JumpStartAudioSourceComponent</td>
        <td>Audio source for the jump start sound.</td>
    </tr>
    <tr>
        <td>AudioSourcesProperties.JumpLandAudioSourceComponent</td>
        <td>Audio source for the jump landing sound.</td>
    </tr>
    <tr>
        <td>AudioClipProperties.WalkAudioClip</td>
        <td>Audio clip to be played when walking.</td>
    </tr>
    <tr>
        <td>AudioClipProperties.RunAudioClip</td>
        <td>Audio clip to be played when running.</td>
    </tr>
    <tr>
        <td>AudioClipProperties.JumpStartAudioClip</td>
        <td>Audio clip to be played when starting a jump.</td>
    </tr>
    <tr>
        <td>AudioClipProperties.JumpLandAudioClip</td>
        <td>Audio clip to be played when landing after a jump.</td>
    </tr>
    <tr>
        <td>TimeStepsProperties.TimeBetweenStandRunSteps</td>
        <td>Time interval between each footstep sound while standing and running.</td>
    </tr>
    <tr>
        <td>TimeStepsProperties.TimeBetweenCrouchRunSteps</td>
        <td>Time interval between each footstep sound while crouching and running.</td>
    </tr>
    <tr>
        <td>TimeStepsProperties.TimeBetweenStandWalkSteps</td>
        <td>Time interval between each footstep sound while standing and walking.</td>
    </tr>
    <tr>
        <td>TimeStepsProperties.TimeBetweenCrouchWalkSteps</td>
        <td>Time interval between each footstep sound while crouching and walking.</td>
    </tr>
    <tr>
        <td>TimeStepsProperties.TimeBetweenAimedStandSteps</td>
        <td>Time interval between each footstep sound while aiming and standing.</td>
    </tr>
    <tr>
        <td>TimeStepsProperties.TimeBetweenAimedCrouchSteps</td>
        <td>Time interval between each footstep sound while aiming and crouching.</td>
    </tr>
    <tr>
        <td>AudioSourceComponents</td>
        <td>Contains references to the audio sources for different movement sounds.</td>
    </tr>
    <tr>
        <td>AudioClips</td>
        <td>Contains references to the audio clips for different movement sounds.</td>
    </tr>
    <tr>
        <td>TimeSteps</td>
        <td>Stores footstep time intervals based on different movement states.</td>
    </tr>
</table>

### Player Surface Detector (Raycast Detection)

You can create an empty gameObject and make it to be the child of 'Player' and rotate it's X Axis at 90 degree and position it little bit above from the ground and add the component to it called 'PlayerSurfaceDetector' and using the script you can tweak different values and decide which audio clip to playback when the player walk/run/jump on a certain surface with a unique tag.[See The Image below]

Script Info: The PlayerSurfaceDetector script offers a sophisticated solution for enhancing player behavior through dynamic footstep sound adjustments based on terrain/Mesh types. By employing tags and raycasting, this approach continuously checks ahead of the Player at intervals set by Min/Max timers. It provides detailed environmental responsiveness, allowing player to interact realistically with various surfaces like grass, concrete, or wood. However, due to its continuous raycasting nature, developers should consider performance implications, particularly on mobile platforms where it may slightly impact FPS. For smaller environments, alternative script like 'PlayerSurfaces' which do collider-based detection may be more performance-efficient, ensuring optimal gameplay experience across different device capabilities.

<img src="Images/RaycastBased_FootstepSoundDetection.png" alt="alt text" width="460" height="360">                                     

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
        <td>FirstPersonControllerScript</td>
        <td>Reference to the FirstPersonController script for player movement and footstep handling.</td>
    </tr>
    <tr>
        <td>AudioSourceComponents</td>
        <td>Holds references to different audio sources used for movement sounds.</td>
    </tr>
    <tr>
        <td>raycastLength</td>
        <td>Length of the raycast that detects surfaces in front of the Player. Adjust this value based on how far ahead you want the Player to detect surfaces.</td>
    </tr>
    <tr>
        <td>minTimeToRaycast</td>
        <td>Minimum time interval between consecutive raycasts. Controls how often the script performs raycast checks.</td>
    </tr>
    <tr>
        <td>maxTimeToRaycast</td>
        <td>Maximum time interval between consecutive raycasts. Controls how often the script performs raycast checks.</td>
    </tr>
    <tr>
        <td>VisibleLayers</td>
        <td>Visible layers during raycasting. Objects on these layers will trigger surface detections.</td>
    </tr>
    <tr>
        <td>debugRaycast</td>
        <td>Toggle to enable or disable visual debugging of raycasts in the Scene view. When enabled (true), the raycast is visualized with raycastColor during development and testing.</td>
    </tr>
    <tr>
        <td>raycastColor</td>
        <td>Color used to visualize the raycast in the Scene view. Helps developers see where the raycast is directed during debugging.</td>
    </tr>
    <tr>
        <td>customFootStepSounds</td>
        <td>List of custom footstep sounds for different surface tags. Populate this list with tags and corresponding audio clips to simulate realistic footstep behavior based on terrain type.</td>
    </tr>
    <tr>
        <td>WalkAudioSourceComponent</td>
        <td>Audio source for walking sounds.</td>
    </tr>
    <tr>
        <td>RunAudioSourceComponent</td>
        <td>Audio source for running sounds.</td>
    </tr>
    <tr>
        <td>JumpStartAudioSourceComponent</td>
        <td>Audio source for jump start sounds.</td>
    </tr>
    <tr>
        <td>JumpLandAudioSourceComponent</td>
        <td>Audio source for jump landing sounds.</td>
    </tr>
    <tr>
        <td>WalkAudioClip</td>
        <td>Audio clip for walking on this surface type.</td>
    </tr>
    <tr>
        <td>RunAudioClip</td>
        <td>Audio clip for running on this surface type.</td>
    </tr>
    <tr>
        <td>JumpStartAudioClip</td>
        <td>Audio clip for jump start on this surface type.</td>
    </tr>
    <tr>
        <td>JumpLandAudioClip</td>
        <td>Audio clip for jump landing on this surface type.</td>
    </tr>
    <tr>
        <td>TimeBetweenStandRunSteps</td>
        <td>Time interval between each footstep while standing and running on this surface.</td>
    </tr>
    <tr>
        <td>TimeBetweenCrouchRunSteps</td>
        <td>Time interval between each footstep while crouching and running on this surface.</td>
    </tr>
    <tr>
        <td>TimeBetweenStandWalkSteps</td>
        <td>Time interval between each footstep while standing and walking on this surface.</td>
    </tr>
    <tr>
        <td>TimeBetweenCrouchWalkSteps</td>
        <td>Time interval between each footstep while crouching and walking on this surface.</td>
    </tr>
    <tr>
        <td>TimeBetweenAimedStandSteps</td>
        <td>Time interval between each footstep while aiming and standing on this surface.</td>
    </tr>
    <tr>
        <td>TimeBetweenAimedCrouchSteps</td>
        <td>Time interval between each footstep while aiming and crouching on this surface.</td>
    </tr>
</table>


