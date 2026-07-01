# <span font-weight:bold;">Weapon Firing Behaviour Part-1</span>

<div class="video-container">
    <iframe width="700" height="405" src="https://www.youtube.com/embed/hVD0wtHb4UM?si=PUNwfF04UUhETk_2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Introduction
This is the Part-1 of Humanoid AI Weapon Firing Behaviour and in this part we have covered following topics - full automatic fire,Semi automatic fire,Reloading,Supression fire,
Dropped Weapon lifetime and basic setup required for the weapon to function properly.

### Humanoid AI Weapon Firing Behaviour 

<img src="Images/Part1_HumanoidAIWeaponFiringBehaviour.png" alt="alt text" width="460" height="360">

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
        <td>Raycast Bullet Range</td>
        <td>This field is applicable to raycast and projectile shooting determining how far this humanoid AI agent weapon can shoot.</td>
    </tr>
    <tr>
        <td>Muzzle Flash Particle</td>
        <td>Drag and drop Muzzleflash particles from the hierarchy (child of the Shooting Point gameobject attached to AI agent`s weapon).</td>
    </tr>
    <tr>
        <td>Use Muzzle Flash Mesh</td>
        <td>Use mesh instead of particles for muzzle flash effect.</td>
    </tr>
    <tr>
        <td>Muzzle Flash Mesh</td>
        <td>Drag and drop MuzzleFlashMesh gameobject from the hierarchy (child of the Shooting Point gameobject attached to AI agent`s weapon).</td>
    </tr>
    <tr>
        <td>Auto Deactivate Muzzle Flash Mesh</td>
        <td>Deactivates 'MuzzleFlashMesh' right after weapon shot animation clip playback. Otherwise it will get deactivated after set number of seconds specified in the 'TimeToDeactivateMuzzleMesh' field.</td>
    </tr>
    <tr>
        <td>Muzzle Flash Duration</td>
        <td>Muzzle Flash mesh deactivation delay.</td>
    </tr>
    <tr>
        <td>Min Muzzle Flash Mesh Z Rotation</td>
        <td>Set the minimal rotational offset angle value for MuzzlFlashMesh to add variations of its appearance with each new shot.</td>
    </tr>
    <tr>
        <td>Max Muzzle Flash Mesh Z Rotation</td>
        <td>Set the maximal rotational offset angle value for MuzzlFlashMesh to add variations of its appearance with each new shot.</td>
    </tr>
    <tr>
        <td>Fire Rate</td>
        <td>Shots per second parameter of this weapon.</td>
    </tr>
    <tr>
        <td>Optimize Raycast Shooting</td>
        <td>If checked, will decrease performance hit by doing raycast shot only once for the first shot at the current closest enemy and after that performing set number of consecutive shots inside field below named 'OptimizedRaycastShots' without actual raycasting until target is killed or another enemy becomes closest target in which case raycast optimization will reset itself for that new closest enemy.</td>
    </tr>
    <tr>
        <td>Optimized Raycast Shots</td>
        <td>Specifies how many consecutive shots after first raycast shot (not including it) Ai agent will do at its current target before resuming OptimizeRaycastShooting cycle.</td>
    </tr>
    <tr>
        <td>Damage To Target</td>
        <td>Amount of damage points of each raycast shot of this weapon (Does not affect projectiles).</td>
    </tr>
    <tr>
        <td>Impact Effect Name</td>
        <td>Enter the exact name of the default impact effect from the object pooler that will be applied to surfaces which do not have their own impact effects specified in 'HitImpactEffect' script attached to them.</td>
    </tr>
    <tr>
        <td>Semi Automatic Fire</td>
        <td>If checked, then this weapon will only do single shots and would not be able to do burst (automatic) firing.</td>
    </tr>
    <tr>
        <td>Min Time Between Semi Auto Shots</td>
        <td>Minimal time interval between semi-automatic shots.</td>
    </tr>
    <tr>
        <td>Max Time Between Semi Auto Shots</td>
        <td>Maximal time interval between semi-automatic shots.</td>
    </tr>
    <tr>
        <td>Should Eject Bullet Shell</td>
        <td>If enabled, then bullet shells will be ejected when firing this weapon.</td>
    </tr>
    <tr>
        <td>Bullet Shell Name</td>
        <td>Name of the bullet shell effect inside object pooler.</td>
    </tr>
    <tr>
        <td>Bullet Shell Spawn Point</td>
        <td>Drag and drop child gameobject of this weapon named 'BulletShellSpawnPoint' from the hierarchy into this field. Bullet shells particle prefabs will then be spawned at the origin of this gameobject and will along the local Z axis of this game object.</td>
    </tr>
    <tr>
        <td>Projectile Name</td>
        <td>Copy and paste name of the projectile to be used with this weapon from the 'ObjectPooler' script into this field.</td>
    </tr>
    <tr>
        <td>Projectiles Per Shot</td>
        <td>Enter the number of the projectiles of the single shot of this weapon if you want this weapon to be shotgun. The spread of those projectiles is specified in 'BulletSpread' paragraph.</td>
    </tr>
    <tr>
        <td>Shooting Option</td>
        <td>Select one of the three available options for the kind of shooting that this weapon will utilise. RaycastShootingWithTracers is an option where those tracers are not dealing damage to targets and are there only for visuals.</td>
    </tr>
    <tr>
        <td>Min Open Fire Delay</td>
        <td>Minimum time delay before commencement of the weapon firing behavior.</td>
    </tr>
    <tr>
        <td>Max Open Fire Delay</td>
        <td>Maximum time delay before commencement of the weapon firing behavior.</td>
    </tr>
    <tr>
        <td>Suppression Fire Probability</td>
        <td>Sets the probability for AI agent to continue firing his weapon (for some time specified in the fields below) at the targets that became hidden behind covers.</td>
    </tr>
    <tr>
        <td>Min Suppression Fire Duration</td>
        <td>Specify the minimum duration of the suppressing fire.</td>
    </tr>
    <tr>
        <td>Max Suppression Fire Duration</td>
        <td>Specify the maximum duration of the suppressing fire.</td>
    </tr>
    <tr>
        <td>Min Reload Delay Time</td>
        <td>Minimal delay time before reloading the weapon after shooting last bullet from magazine or in cases that require manual reload after each single shot.</td>
    </tr>
    <tr>
        <td>Max Reload Delay Time</td>
        <td>Maximal delay time before reloading the weapon after shooting last bullet from magazine or in cases that require manual reload after each single shot.</td>
    </tr>
    <tr>
        <td>Max Ammo</td>
        <td>Maximum amount of rounds for this weapon that Ai agent will have.</td>
    </tr>
    <tr>
        <td>Magazine Size</td>
        <td>Amount of rounds in the magazines for this weapon.</td>
    </tr>
    <tr>
        <td>Match Reload Time With Animation</td>
        <td>If checked then duration of the reload will match the duration of the used reload animation clip. If unchecked then it will be possible to set the durations of reload for Crouched and Standing positions regardless of the reload animation clip playback time.</td>
    </tr>
    <tr>
        <td>Stand Reload Duration</td>
        <td>The time it will take to reload this weapon in stance position.</td>
    </tr>
    <tr>
        <td>Crouched Reload Duration</td>
        <td>The time it will take to reload this weapon in crouched position.</td>
    </tr>
    <tr>
        <td>Weapon Mesh</td>
        <td>Drag&Drop this weapon mesh from this AI agent`s hierarchy into this field.</td>
    </tr>
    <tr>
        <td>Core Ai Behaviour Script</td>
        <td>Drag and drop 'CoreAiBehaviourScript' component attached with the root gameobject of this Ai agent from the hierarchy into this field.</td>
    </tr>
    <tr>
        <td>Animator Component</td>
        <td>Drag and drop 'Animator' component attached with the root gameobject of this Ai agent from the hierarchy into this field.</td>
    </tr>
    <tr>
        <td>Weapon Sounds</td>
        <td>Drag&drop 'WeaponSounds' gameobject with 'AlertingSoundActivator' script attached to it from this AI agent`s hierarchy into this field.</td>
    </tr>
    <tr>
        <td>Stand Reload Clip</td>
        <td>Drag and drop the stand reload animation clip from the project window into this field.</td>
    </tr>
    <tr>
        <td>Crouch Reload Clip</td>
        <td>Drag and drop the crouch reload animation clip from the project window into this field.</td>
    </tr>
    <tr>
        <td>Stand Fire Clip</td>
        <td>Drag and drop the stand fire animation clip from the project window into this field.</td>
    </tr>
    <tr>
        <td>Crouch Fire Clip</td>
        <td>Drag and drop the crouch fire animation clip from the project window into this field.</td>
    </tr>
    <tr>
        <td>Dropped Weapon Life Time</td>
        <td>Specify for how long this weapon will stay active after Ai agent that carried it was killed.</td>
    </tr>
</table>






