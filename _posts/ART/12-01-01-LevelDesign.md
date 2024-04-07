---
title: Level Design
description: Navigation, Space, Visuals, Gameplay, Combat
categories:
  - ART
tags:
  - Design
  - Gameplay
  - Architecture
  - GameDev
  - 3D
  - CG
permalink: /leveldesign/
aliases:
  - leveldesing
---
> related [[13-01-01-Architecture|arch]] [[12-01-01-Lore|lore]] [[10-01-01-U_World|uworld]]

[Game Design](/gamemechanics/)   
[Game Mechanics](/gamemechanics/)   

# Concept
- **Show don't tell**
- **Minimize cognitive load**. to avoid struggle with processing information's . to much details sensory overload.
- **Readability**  
- **Form follow function**. Restrictions, goals, context.   
- **Scale**,** metrics** and **proportions** .  Object with fixed size (car), and without (tree).    
- Giving the player **depth cues** by  reference.   

LD driven by mechanics.
  - High level: - [Environmental storytelling](/ludology/)
  - Medium level: - Level Design
  - Low level: - [World Building / Lore](/lore/)

- Control environment instead of camera like in movies.  
- Contain: aesthetic + functionality



##  Constraints & Direction   
- Design constraints
- Pipeline tools constraints


# Navigation

## Intentionality
Afford present player. Tell what to do but not how to do it.  Typically from a vantage point area where we can survey, orient ourselves  and plan our approach. Linearity feels bad could be caused by week intentionality.

##### Players action loop:
- **Observe** options and goals (Learn) > formulate **Plan**  (Play) > **Act** with intentionality (Challenge) > Reaction (Surprise)

## Guidance
We can guide player with: 
- UI - UI, Maps, ...
- In game visuals - Signposting: Signifiers, Signs, Lighting,.... (not breaking fourth wall)  
- Narrative - Narrator, AI, …

##### Paths
- **Critical path** = The quickest and most direct route to beating the level.
- **Golden path** = The designers ‘preferred’ route (generic path). It’s the one you expect most players to take and the one which will offer the optimal experience. Hardest to create. 

##### Circulation


## Saliency
**Where to look**  Attention garbing. Control where player and cam look.  

#### Bottom up
- Contrast, movement  (Stronger in cinema cause we are chilling)

#### Top Down
- Humans (meaning), NowSilent (We care now) (Stronger in goal/task orient mode) Human faces, people, things associated with our current task/goal (attentional goals).  

**Attentional goals**  help players notice and pay attention to things  - (which can mean you become more ‘blind’ to other things). a locked gate they might assume the goal forward is to open the gate (even though the solution is to climb out a window).It’s also worth noting that if players are already focused on something else ...


## Affordances
**Where to go** Possible of potential actions. Provide strong clues to the operations of things. Control what players believe is usable.  
- **Objects** -  Windows afford to looking through.  Doors for enter, slots for inserting, knobs for turning, buton for press, flips for switch, Machines to use
- **Surface**  - floor. we walk to affordance surface to walk. along longest sight lights. (or somewhere else if there could be price)
- **Lights**

#### Positive
Afford to be used

Way of Encourage player to take action
- **Mystery** - If there is information to learn `Whining` - landmark with mystery element
- **Teasing** - Show what you can get yet.
- **Collectables**
- high level long term goals. not pull a leaver.

#### Negative
Doesn’t afford to be used and can’t be  / Nope zone

#### False
looks like it affords to be used but can’t



## Progression 
 
Progression type
- Game as a progression od levels
- circle / bottlenecks / dead -ends
- Verticality !!!!! important  
- sandbox / multiplayer / boss arenas / lineasr


#### Linear 

#### Open world 
Problems with open worlds: [YT Open worlds essey](https://youtu.be/-O3oe8sSRhQ), [YT Open worlds essey 2](https://youtu.be/7Rmqx6mHz-g) quick transport / objectives hud 





# Space


## Orientation
**where I am**    
In games Perceptual pattern to create Orientation  
- Signposting (characteristic to area, or showing way)
- Divide to district /  (to distinct at map and mind )

- `Landmarks` - individual objects
- `District` - with unique fulvous
- `Linear elements` - Path, rivers.
- `Edges` - Walls, rivers (temporary / depended)  
- `Nodes` - moments of decisions - train station
- `Point of interest` -  
Way finding elements:
don't lead player where to go but how move through space


### Callouts

Places on level you can call by name.  Areas are distingue enough that player can identify them by feature (space, light, color). Should be thought through different scales (arena, district, level).


## Composition
Composing 3d to view in 2d (flat monitor) like composition rules  

- Clarity and flow vs confusion
- Vary silhouettes of the skyline  
- Lines of sight  
- Depth perception vs. real space

- players typ spectator go to the edge, traveler to center
- more comfortable in positive space not so in negative.

### Spatial empathy
- twist to confusion
- open of isolation and epic scale
- narrow to large space and other way
- vertycality - persecution
- vertigo / rewad if stnding on top   


## Function

[Architecture](/arch/)
manage how players are able to take risk !!

- melee vs range
- mobility vs stability
- bruteforce vs Ingenuity (create own timing windows , distract enemy) (code braking - open paths)
- combar vs stelth (wait for oportunity time window)


- Differentiate by usage: `stealth's` / `combat` / `traversal` / public `interaction` (opportunities for different playstyles  )
- `public space` / `purpose spaces`
- `primary target` (no dead-ends) vs. `illusory targets` vs. `escalating` (everywhere), vs `bonus missions`
- beginning and end

.

- primary circulation routes . connect primary nodes of activity
- secondary roots to increase mobility  
- no dead ends
- only pedestrian routes

### Pacing

linear vs. non-linear ### non linear - Pacing    
 moving through a level more fluid and intuitive
- intensity  
- variety  
- time  

### Traversing  

### Action Space
Skill based

### Prospect & Refuge
**Prospect** is a view, and **Refuge** is Safety place. This kept our ancestors safe from enemies/predators and the elements, meet basic human psychological needs.  (evolutionary heritage). provide people with the capacity to observe (prospect)

- **Primary**  - you have now both
- **Secondary** - we have only one and see second far away is only promise)


### Gating
Revealing level slowly, in tiers.

|  |  |
| ---|  ---|
| gates hard | Halts progress until something is completed,  
|gates soft | Intended to briefly slow the player down.   
|valves | one way,  keep pushing players forward  

###  Exploration 

### Secrets

- **Breadcrumbing** -  sending brief and sporadic messages. Trail of something (usually pickups or information) that leads the player in the right direction or towards  
- **Hints** - Slight or indirect indication or suggestion. (notes on paper, maps, signs)





# Combat

Design for multiple options and strategies. viable/intended ranges of the combat space. pieces of cover should be available to the player at the start of combat Preventing teams from being able to spawn camp
- Vintage point - Show off the combat space (or area the player needs to sneak through),
- Fronts
- Flanks (he bridge(s) in the neutral zone between the combating sides)
- No man’s land. Hard to defense (can add collectable at center)
- Entrances (Enemy reinforcements enter from different positions or in new ways)
- Covers Can
  - durability:
    - Static - Hard cover
    - Moveable / Dynamic - can be moved / destroyed  . temporary
    - Moving - have a predictable movement
    - Concealment - no protection like bush.  Soft cover  
  -  high 2m+ / low ~1m (you don’t want to make Low cover look like High cover and potentially mess up things)
  -  block
    - vision
    - damage
- Line of sight
- Vertical arrangement

### Level arrangement
- Flow in general is about keeping players forward momentum going. (softer corners )
- Connectivity

E.g.
- circle (ring)
- 8 (2 circles)
- Clash points - places where fight (Double Clash)
- Tug of War  - liner teams opposite sites. (variation with 2 paths )
types: For 'Capture the flag' CTF / territory take over   
Offence / defence differencess      


https://andrewyoderdesign.blog/2019/08/04/the-door-problem-of-combat-design/   
 fight for territory is one aspect of map control, but there are other aspects to consider. In an abstract sense, map control is about a player developing their options while limiting the options available to their opponent


### Graph theory
for multiplayers

https://www.raphkoster.com/games/presentations/small-worlds-competitive-and-cooperative-structures-in-online-worlds/

### Line of sight
- Horizontal LoS
- Vertical LoS
- Tight angles
- Ramps
- Corner angles & verticality
	- angle advantage: if you step away from corener you get corner advatage wiev.  https://youtu.be/FbeTevpBQPc

### Multiplayer

mastery mapy vs nowa mapa .
- balance
- asymetry  


# Visuals
- Generally more effective when it makes contextual narrative sense  
- Must be part of gameplay mechanics + Backdrops - non-playable areas

ELements:
- Architecture   
- Geography
- Biology
- Chemistry / Mechanics
- Culture History Geo Politics






## Signifiers
**Clues to how to use/discover** - Gameplay related. Physics, usable & reactivity. show Affordances (signals that help find that sth is usable (signs / colors))
Apply signifires to reflect affordances.

[Design](/graphicdesign/)

## Visual Language
Gradient of visual complexity where the play space has less visual complexity and then as the space transitions to where players/enemies can no longer traverse (or where something visually important is) we increase it.
- develop & maintain visual language consistency in style: aesthetic.
- `Optimum complexity` - readability

schemes and symbols
color coding / names / shapes (waypoints/orientation)

### Atmosphere
- `Depth`  - Atmosphere, Repeating same elements in space
- `Light` - but we not evolve to going directly to light.

## Visual Storytelling
let content of story to draw image  (not style ! )
evaluating story:
- what matter from the story point of view (no details)
- what is interesting for story
- summary important details


### Environmental narrative (mise-en-scene)
- universal themes understood by all cultures > honor freedom lib injustice vengin survival
- `Symbolism` (ascending desc.) > stairs up (create narrative),
- `Expression`. world; Historical and cultural, inhabitant (znaki zamieszkania)
- `Mystery` (scene enrichment)
- `Novelty`
- `Foreshadowing` - showing goals
- Emotions and history
- Architecture  https://vol.co/product/anime-architecture/

### Ecosystem
How level elements interacts in world.
http://tmdag.com/ptakun/eco_system/makeofplants_en_htm.htm


[Lore](/lore/)


# Pipelines 

## Pipelines
- Blockouts, and props  

## Procedural
[Procedural](/procedural/)



### Pattern analysis
Grid base props (modular) - need lot of custom work to break pattern recognition, and don't feel unnatural and obvious.
https://www.patternlanguage.com/

##### Recycling

Make a change when recycling:
- Power shift / Reversal  
- Playing the level backwards  
- Revisit

# . 

> Minimalist product design - Dieter Rams

> Design of normal things Don Norman

> Shaping interior space. Roberto Rengel

> A Practical Guide to Level Design From Theory to Practice, Diplomacy, and Production"  https://youtu.be/8wEt8bCNvg8    

[doc](https://docs.google.com/document/d/1fAlf2MwEFTwePwzbP3try1H0aYa9kpVBHPBkyIq-caY/preview?pru=AAABcubYTrs*65ZuXXMNJriddYR6IXE8Ag#)
[pod psychology of games podcast](https://www.psychologyofgames.com/2020/01/podcast-55-the-psychology-of-level-design/)   
https://www.youtube.com/c/LevelDesignLobby/videos  
https://www.youtube.com/watch?v=CpOoTAVeEcU  
https://www.worldofleveldesign.com/categories/cat-level-design.php

