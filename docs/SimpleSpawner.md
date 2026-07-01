# <span font-weight:bold;">Simple Spawner</span>

<div class="video-container">
    <iframe width="700" height="405" src="https://www.youtube.com/embed/hVD0wtHb4UM?si=PUNwfF04UUhETk_2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Introduction

In this tutorial you will learn how to setup simple spawner and spawn AI agents and any other gameObjects within a spawn point and collider volume. 

### Simple Spawner

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
        <td>ShowGizmosInTheScene</td>
        <td>Draw the spawning area gizmo in the Unity scene view.</td>
    </tr>
    <tr>
        <td>GizmoColor</td>
        <td>Set the color of the spawning area gizmos in the Unity scene view.</td>
    </tr>
    <tr>
        <td>TriggeringGameObject</td>
        <td>Drag & drop the game object (usually player) from the hierarchy into this field to trigger spawn events.</td>
    </tr>
    <tr>
        <td>SpawnOnlyOnTriggerEnter</td>
        <td>If checked, then the Spawnables will be spawned only if the player enters the trigger collider attached to the 'GeneralSpawner' game object.</td>
    </tr>
    <tr>
        <td>SpawnableType</td>
        <td>Choose one of the types of the Spawnable objects.</td>
    </tr>
    <tr>
        <td>Spawnables</td>
        <td>Assign game entities to be spawned by this spawner.</td>
    </tr>
    <tr>
        <td>MinSpawnDelay</td>
        <td>Minimum time between spawns.</td>
    </tr>
    <tr>
        <td>MaxSpawnDelay</td>
        <td>Maximum time between spawns.</td>
    </tr>
    <tr>
        <td>SpawnWithinVolume</td>
        <td>If checked, then AI agents or game objects will spawn within the volume of the trigger collider attached to the child game object of this 'GeneralSpawner' named 'SpawnVolume.' You will have to create it, add a trigger collider to it, and set up its dimensions to ensure that agents or game objects spawn only within certain rooms or other enclosed spaces.</td>
    </tr>
    <tr>
        <td>SpawnVolume</td>
        <td>Drag and drop 'SpawnVolume' child game object with the trigger collider attached to it into this field.</td>
    </tr>
    <tr>
        <td>SpawnPoint</td>
        <td>Drag and drop child game object named 'SpawnPoint' into this field.</td>
    </tr>
    <tr>
        <td>AmountOfSpawnables</td>
        <td>Number of agents this spawner script can spawn.</td>
    </tr>
    <tr>
        <td>MinNonAiSpawnablesOffset</td>
        <td>Minimal offset of non-AI 'Spawnables' from the spawn point along x, y, and z axis to space them out from each other.</td>
    </tr>
    <tr>
        <td>MaxNonAiSpawnablesOffset</td>
        <td>Maximal offset of non-AI 'Spawnables' from the spawn point along x, y, and z axis to space them out from each other.</td>
    </tr>
    <tr>
        <td>AiSpawnPointRadius</td>
        <td>Radius within which AI agents will be spawned.</td>
    </tr>
    <tr>
        <td>AiUpdaterComponent</td>
        <td>Drag and drop AI Updater game object from the hierarchy with 'AiUpdater' script attached to it into this field in case Spawnables of this spawner will be AI agents.</td>
    </tr>
</table>

<img src="Images/SimpleSpawner.png" alt="alt text" width="460" height="360">