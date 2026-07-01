# <span font-weight:bold;">Merge Wave Spawner & AI Maintaining Spawner</span>

<div class="video-container">
    <iframe width="700" height="405" src="https://www.youtube.com/embed/hVD0wtHb4UM?si=PUNwfF04UUhETk_2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Introduction

In this tutorial you will learn how to setup Wave spawner and AI Maintaining Spawner together and spawn consistent number of enemies and friendlies in each wave.

### AI Maintaining Spawner Global AI List

This script holds shared list of Ai agents for multiple 'AiMaintainingSpawners' to refer to. It allows keeping global count of alive Ai agents spawned by all 'AiMaintainingSpawners' throughout the mission. So that it would be possible to keep constant overall Ai agents count for a team by replenishing it without exceeding shared value of 'Ai agents to Maintain' fields of 'AiMaintainingSpawners' in case 'AiMaintainingSpawners' are used together with 'WaveSpawner' that would spawn enemy waves. 'AiMaintainingSpawners' could then respawn required amount of specified friendly Ai agents to maintain the size of player`s team. Respawning them synchronously with each new enemy wave. It is used in case game developers want player to be assisted by team of friendly Ai agents to engage enemy waves. 

<img src="Images/AIMaintainingSpawner&GlobalAIList.png" alt="alt text" width="460" height="360">
