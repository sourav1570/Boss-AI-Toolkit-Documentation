# <span font-weight:bold;">Zombie Voices</span>

<div class="video-container">
    <iframe width="700" height="405" src="https://www.youtube.com/embed/hVD0wtHb4UM?si=PUNwfF04UUhETk_2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Introduction
In this tutorial you will how to setup Recurring and Non Recurring Sounds for the Zombie.

### Humanoid Ai Audio Player

The script is responsible for playback of different sounds and phrases in various situations. When Zombie is wounded or dying or reloading weapons or engaging his enemy etc.

<img src="Images/ZombieAudioPlayer.png" alt="alt text" width="460" height="360">

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
        <td>AudioSourceComponent</td>
        <td>Drag and drop audio source component which is the child of this Zombie from the hierarchy into this field.</td>
    </tr>
    <tr>
        <td>DyingAudioClips</td>
        <td>Drag and drop one or more dying sound clips from the project into this field.</td>
    </tr>
    <tr>
        <td>FireSoundAudioSourceComponent</td>
        <td>Drag and drop audio source component which is the child of this Zombie from the hierarchy into this field.</td>
    </tr>
    <tr>
        <td>ReloadSoundAudioSourceComponent</td>
        <td>Drag and drop audio source component which is the child of this Zombie from the hierarchy into this field.</td>
    </tr>
    <tr>
        <td>WeaponShotAudioClip</td>
        <td>Drag and drop 'Fire sound clip' from the project window into this field.</td>
    </tr>
    <tr>
        <td>WeaponReloadAudioClip</td>
        <td>Drag and drop the Reload Sound clip from the project window into this field.</td>
    </tr>
    <tr>
        <td>FootStepsAudioSourceComponent</td>
        <td>Drag and drop audio source component which is the child of this Zombie from the hierarchy into this field.</td>
    </tr>
    <tr>
        <td>FootStepAudioClip</td>
        <td>Drag and drop 'Footstep sound clip' from the project window into this field.</td>
    </tr>
    <tr>
        <td>AudioSourceComponent (Replayable Voices)</td>
        <td>Drag and drop the audio source component which is the child of this Zombie from the hierarchy into this field.</td>
    </tr>
    <tr>
        <td>DefaultBehaviourAudioClips</td>
        <td>Drag and drop default behavior audio clips from the project window into this field.</td>
    </tr>
    <tr>
        <td>EngagingTheEnemyAudioClips</td>
        <td>Drag and drop engaging the enemy audio clips from the project window into this field.</td>
    </tr>
    <tr>
        <td>FollowerAudioClips</td>
        <td>Drag and drop follower audio clips from the project window into this field.</td>
    </tr>
    <tr>
        <td>LeaderAudioClips</td>
        <td>Drag and drop leader audio clips from the project window into this field.</td>
    </tr>
    <tr>
        <td>MinTimeBetweenRecurringAudioClips</td>
        <td>Minimum time interval between recurring audio clips. Example: '1.0' seconds.</td>
    </tr>
    <tr>
        <td>MaxTimeBetweenRecurringAudioClips</td>
        <td>Maximum time interval between recurring audio clips. Example: '2.0' seconds.</td>
    </tr>
    <tr>
        <td>MinRecurringAudioClipsDelayAfterInterruption</td>
        <td>Minimum delay after interruption before recurring audio clips can play again. Example: '2.0' seconds.</td>
    </tr>
    <tr>
        <td>MaxRecurringAudioClipsDelayAfterInterruption</td>
        <td>Maximum delay after interruption before recurring audio clips can play again. Example: '4.0' seconds.</td>
    </tr>
    <tr>
        <td>AudioSourceComponent (OneTime Voices)</td>
        <td>Drag and drop the audio source component which is the child of this Zombie from the hierarchy into this field.</td>
    </tr>
    <tr>
        <td>OnceReloadingAudioClips</td>
        <td>Drag and drop reloading audio clips from the project window into this field.</td>
    </tr>
    <tr>
        <td>OnceMeleeAudioClips</td>
        <td>Drag and drop melee audio clips from the project window into this field.</td>
    </tr>
    <tr>
        <td>OnceEmergencyAudioClips</td>
        <td>Drag and drop emergency audio clips from the project window into this field.</td>
    </tr>
    <tr>
        <td>OnceDeadBodyInvestigationAudioClips</td>
        <td>Drag and drop dead body investigation audio clips from the project window into this field.</td>
    </tr>
    <tr>
        <td>OnceHearingInvestigationAudioClips</td>
        <td>Drag and drop hearing investigation audio clips from the project window into this field.</td>
    </tr>
    <tr>
        <td>OnceWoundedAudioClips</td>
        <td>Drag and drop wounded audio clips from the project window into this field.</td>
    </tr>
    <tr>
        <td>OnceEnemyLostAudioClips</td>
        <td>Drag and drop enemy lost audio clips from the project window into this field.</td>
    </tr>
    <tr>
        <td>OnceTargetKilledAudioClips</td>
        <td>Drag and drop target killed audio clips from the project window into this field.</td>
    </tr>
    <tr>
        <td>OnceGrenadeAlertAudioClips</td>
        <td>Drag and drop grenade alert audio clips from the project window into this field.</td>
    </tr>
    <tr>
        <td>OnceThrowingGrenadeAudioClips</td>
        <td>Drag and drop throwing grenade audio clips from the project window into this field.</td>
    </tr>
    <tr>
        <td>OnceLeaderAtHaltPointAudioClips</td>
        <td>Drag and drop leader at halt point audio clips from the project window into this field.</td>
    </tr>
    <tr>
        <td>MinNonRecurringAudioClipsDelay</td>
        <td>Minimum delay between non-recurring audio clips. Example: '1.0' seconds.</td>
    </tr>
    <tr>
        <td>MaxNonRecurringAudioClipsDelay</td>
        <td>Maximum delay between non-recurring audio clips. Example: '2.0' seconds.</td>
    </tr>
    <tr>
        <td>RecurringSounds</td>
        <td>Settings for recurring sound clips based on time intervals. Example: 'Default behavior sounds that play at random intervals while the AI is patrolling.'</td>
    </tr>
    <tr>
        <td>NonRecurringSounds</td>
        <td>Settings for non-recurring sound clips that play once under specific conditions. Example: 'Emergency state sound that plays once when the AI enters an emergency state.'</td>
    </tr>
    <tr>
        <td>DyingSounds</td>
        <td>Settings for dying sound clips that play when the Zombie dies.</td>
    </tr>
    <tr>
        <td>WeaponSounds</td>
        <td>Settings for weapon sound clips that play during firing and reloading actions.</td>
    </tr>
    <tr>
        <td>DefaultFootStepSounds</td>
        <td>Settings for footstep sound clips that play when the Zombie moves.</td>
    </tr>
</table>


