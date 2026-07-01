# <span font-weight:bold;">Weapon Firing Behaviour Part-5</span>

<div class="video-container">
    <iframe width="700" height="405" src="https://www.youtube.com/embed/hVD0wtHb4UM?si=PUNwfF04UUhETk_2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Introduction
This is the Part-5 of Humanoid AI Weapon Firing Behaviour and in this part we have covered the topic called 'Optimize Raycast Shooting'.

### Humanoid AI Weapon Firing Behaviour 

<img src="Images/OptimiseRaycastShooting.png" alt="alt text" width="460" height="360"> 

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
        <td>Optimize Raycast Shooting</td>
        <td>If checked, will decrease performance hit by doing raycast shot only once for the first shot at the current closest enemy and after that performing set number of consecutive shots inside field below named 'OptimizedRaycastShots' without actual raycasting until target is killed or another enemy becomes closest target in which case raycast optimization will reset itself for that new closest enemy.</td>
    </tr>
    <tr>
        <td>Optimized Raycast Shots</td>
        <td>Specifies how many consecutive shots after first raycast shot (not including it) Ai agent will do at its current target before resuming OptimizeRaycastShooting cycle.</td>
    </tr> 
</table>







