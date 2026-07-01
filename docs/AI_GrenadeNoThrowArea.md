# <span font-weight:bold;">Grenade No Throw Area Part-4</span>

<div class="video-container">
    <iframe width="700" height="405" src="https://www.youtube.com/embed/hVD0wtHb4UM?si=PUNwfF04UUhETk_2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Introduction
This is the Part-4 of AI Grenades and in this part you will learn about how the AI agent refrain from throwing grenades upon entering the trigger area of the firing points.

### Setup No Throw Area

1.Right-click in the Hierarchy window.Select Create Empty.Rename the GameObject to something like NoGrenadeZone for clarity.

2.With the NoGrenadeZone GameObject selected, go to the Inspector window Click Add Component.Type Box Collider in the search bar and select Box Collider from the list.Set the Box Collider is Trigger to be checked

3.In the Inspector, find the Layer dropdown (usually located near the top).Click the dropdown and select IgnoreRaycast.If Ignore Raycast is not available, you can add it by selecting Add Layer..., then creating a new layer named IgnoreRaycast.

4.With the NoGrenadeZone GameObject still selected, click Add Component again.Select New Script and name the new script Humanoid_AI_NoGrenadeThrowArea.Click Create and Add.

<img src="Images/NoThrowArea.png" alt="alt text" width="460" height="360">

#### Humanoid_AI_No Grenade Throw Area

This script enables Humanoid AI agents to refrain from throwing grenades upon entering the trigger area of this collider.

<img src="Images/AINoThrowArea.png" alt="alt text" width="460" height="360">

