# <span font-weight:bold;">Weapon Firing Behaviour Part-3</span>

<div class="video-container">
    <iframe width="700" height="405" src="https://www.youtube.com/embed/hVD0wtHb4UM?si=PUNwfF04UUhETk_2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Introduction
This is the Part-3 of Humanoid AI Weapon Firing Behaviour and in this part we have covered the topic called Distance based shooting.

### Humanoid AI Weapon Firing Behaviour 

<img src="Images/DistanceBasedShooting_Screenshot.png" alt="alt text" width="460" height="360"> 

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
        <td>Enable Distance Based Shooting</td>
        <td>If enabled then Ai agent will fire this weapon based on values of 'DistanceBasedShooting' paragraph which is designed for Ai agent to perform more realistic shooting style to increase efficiency of killing the enemy at various ranges.</td>
    </tr>
    <tr>
        <td>Min Target Distance Check Interval</td>
        <td>Minimal time interval between distance to target checks for performing shooting style based on that distance.</td>
    </tr>
    <tr>
        <td>Max Target Distance Check Interval</td>
        <td>Maximal time interval between distance to target checks for performing shooting style based on that distance.</td>
    </tr>
    <tr>
        <td>Distance Based Shooting</td>
        <td>This list defines DistanceBasedShooting and sets various shooting parameters for each distance that is set in each element of this list. It is set by default to increase volume of fire as the distance to target gets shorter.</td>
    </tr>
    <tr>
        <td>Max Distance</td>
        <td>Sets the maximal distance limit for the range within which this burst type will be performed.</td>
    </tr>
    <tr>
        <td>Min Distance</td>
        <td>Sets the minimal distance limit for the range within which this burst type will be performed.</td>
    </tr>
    <tr>
        <td>Min Burst Size</td>
        <td>Minimum number of shots in a burst when firing at a target that is between min and max limits of this range.</td>
    </tr>
    <tr>
        <td>Max Burst Size</td>
        <td>Maximum number of shots in a burst when firing at a target that is between min and max limits of this range.</td>
    </tr>
    <tr>
        <td>Min Time Between Bursts</td>
        <td>Minimal time interval between bursts.</td>
    </tr>
    <tr>
        <td>Max Time Between Bursts</td>
        <td>Maximal time interval between bursts.</td>
    </tr>
</table>








