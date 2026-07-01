# <span font-weight:bold;">Player Leader and AI Followers Part-3</span>

<div class="video-container">
    <iframe width="700" height="405" src="https://www.youtube.com/embed/hVD0wtHb4UM?si=PUNwfF04UUhETk_2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Introduction
This is the Part-3 of this series and in this part you will learn about how the Player becomes the leader and the AI to be his followers.

### Player Leader

To make the Player to be the leader you need to add the component 'Player Guide' to the Player root gameObject and than drag and drop the AI Followers in the specified list.

<img src="Images/PlayerGuide.png" alt="alt text" width="460" height="360">

### Player Guide

This script makes assigned Ai agents to follow player.If Agents following the player get into combat they will stop following him for the duration of the combat and will resume player following behaviour once combat ends.

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
        <td>Follower Agents</td>
        <td>Drag and drop into this field one or multiple Ai agents from the hierarchy tab (with their role set as the 'Follower' inside the 'core Ai behaviour' script).
        This functionality is designed to work with AI agents that are preplaced in the level by  mission designer(not spawned AI agents).</td>
    </tr>
</table>