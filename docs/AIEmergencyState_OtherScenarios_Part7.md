# <span font-weight:bold;">Emergency State(Other Scenarios) Part-7</span>

<div class="video-container">
    <iframe width="700" height="405" src="https://www.youtube.com/embed/hVD0wtHb4UM?si=PUNwfF04UUhETk_2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Introduction
This is the Part-7 of AI Emergency State and in this part you will learn about some other scenarios during emergency state. These scenarios are the following that are mentioned in the video:

1.What happen If you uncheck choose closest covers?

2.What happen if there is only 1 cover but 2 AI agents?

3.How the enemy AI agent can provoke emergency state on other AI agents?

4.Which emergency Behaviour AI agent overrites in case when the path to the player position is incomplete and impossible to reach? 

### What happen If you uncheck choose closest covers?

#### ANSWER

The AI agents in such a situation move to any random cover which are within the Min/Max range to find the covers. 

### What happen if there is only 1 cover but 2 AI agents?

#### ANSWER

Only 1 Agent will be allowed to take the cover (in case only one valid cover point is available) while the other AI agent will be performing the flee behaviour and as soon as the cover becomes vacant the AI agent who is performing the flee behaviour will take that available cover and will perform emergency shooting from that cover.

### How the enemy AI agent can provoke emergency state on other AI agents.

#### ANSWER

Just by creating a Team1 Soldier and placing it as mentioned (in the video above) with one shot of Team1 AI agent towards its enemies can provoke the emergency state on Team2 agents.


### Which emergency Behaviour AI agent overrites in case when the path to the player position is incomplete and impossible to reach? 

#### ANSWER

When the path to the player position is considered as incomplete as well as path to the closest coordinate to the player is also invalid/incomplete in such a case when there is no way to reach the player. the enemies will overrite there 'Post First Emergency Behaviour Activity' to only with 'Emergency Shooting' and will be performing 'Emergency Shooting' until the combat behaviour starts.
