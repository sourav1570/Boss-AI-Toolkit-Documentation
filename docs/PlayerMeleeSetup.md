# <span font-weight:bold;">Melee Attack</span>

<div class="video-container">
    <iframe width="700" height="405" src="https://www.youtube.com/embed/hVD0wtHb4UM?si=PUNwfF04UUhETk_2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Introduction
This video will help you understand how to setup the player melee.

### Player Melee Setup

Go to Tools < Mobile Action Kit < Player < Melee < Player Melee Setup and assign the necessary gameObjects and components like shown in the video above. Your setup should look like this [See the image below].

<img src="Images/PlayerMeleeSetup.png" alt="alt text" width="460" height="360">

### Melee Attack Script

This script is responsible for player Melee attack actions.

<img src="Images/MeleeAttack.png" alt="alt text" width="460" height="360">

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
<td>MeleeType</td>
<td>Indicates the type of melee attack. 'Instant Attack' is the default.</td>
</tr>
<tr>
<td>RequiredComponents</td>
<td>Container for all the required components for the melee attack system.</td>
</tr>
<tr>
<td>MeleeUIButtons</td>
<td>List of buttons in the UI that trigger melee attacks.</td>
</tr>
<tr>
<td>MeleeAnimatorComponent</td>
<td>Animator component used to play melee animations.</td>
</tr>
<tr>
<td>MeleeIcon</td>
<td>Icon that represents melee functionality in the UI.</td>
</tr>
<tr>
<td>AudioSourceComponent</td>
<td>Audio source used to play melee-related sounds.</td>
</tr>
<tr>
<td>Animations</td>
<td>Container for all melee attack animations and their configurations.</td>
</tr>
<tr>
<td>AttackAnimations</td>
<td>List of melee attack animations available for this system.</td>
</tr>
<tr>
<td>MeleeDamageScripts</td>
<td>Scripts that handle melee damage for this attack.</td>
</tr>
<tr>
<td>AttackAnimationClip</td>
<td>Animation clip to play for this melee attack.</td>
</tr>
<tr>
<td>AttackAudioClip</td>
<td>Audio clip to play during this melee attack.</td>
</tr>
<tr>
<td>DelayDamage</td>
<td>Delay before applying damage after the animation starts.</td>
</tr>
<tr>
<td>Delays</td>
<td>Delays for different actions within the melee attack system.</td>
</tr>
<tr>
<td>KnifeActivationDelay</td>
<td>Time to wait before activating the knife in a melee attack.</td>
</tr>
<tr>
<td>InstantAttackAnimationDelay</td>
<td>Delay before starting an instant attack animation.</td>
</tr>
<tr>
<td>UIInteraction</td>
<td>Handles interactions and UI changes during melee actions.</td>
</tr>
<tr>
<td>UIDisableColor</td>
<td>Color to apply to disabled UI elements (e.g., gray).</td>
</tr>
<tr>
<td>BeforeSelection</td>
<td>UI images to disable while melee hands are activated (e.g., during weapon removal animation).</td>
</tr>
<tr>
<td>UIToDisableBeforeAttack</td>
<td>UI images to disable while the melee attack animation is playing.</td>
</tr>
</table>
