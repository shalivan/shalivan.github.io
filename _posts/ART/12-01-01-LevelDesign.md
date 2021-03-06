---
title: Level Design
description: Navigation, Space, Visuals, Gameplay, Combat
categories:
 - ART
tags:
- Design
- Game Dev
- Gameplay
- Architecture
permalink: /leveldesign/
---



Control environment instead of camera like in movies. Contain: aesthetic + functionality
LD driven by mechanics. Books imagine, movie see, games act.


# Concept

- Restrictions, goals, context.   
- Scale, mertics and proportions .  
- Blockout, and props  
- form follow function   
- backdrop (non-playable area  
- Giving the player depth cues by  reference   
- obj with fixed size = car, without = tree    
- Readability  
- Signposting  
.
- **Critical path** = The quickest and most direct route to beating the level.
- **Golden path** = The designers ‘preferred’ route. It’s the one you expect most players to take and the one which will offer the optimal experience.


- minimize cognitive load. to avoid struggle with processing information's . to much details sensory overload


##### Intentionality
Afford present player options and goals > formulate plan > act with intentionality
Linearity feels bad could be caused by week intentionality
what to do but not how to do it


## Production Constraints & Direction   
(ograniczenia wynikajće z pipelinów)

### Pattern analysis
- grid base props (modular) vs. oprocz funkcji musza byc rzeczy ktore sprawią ze lvl jest naturalny a nie jak w girsach auromatycznym skinem. obvious.

### Recycling
Power shift / Reversal  
Playing the level backwards  
Revisit
---

# Navigation

Players action loop: Typicaly in a vantage point area, where we can survey, orient ourselfs  and plan our approach.

1. Observe
2. Plan
3. Act
4. React




## Guidance
- UI - UI, Maps, ...
- In game visuals - Signifires, Signs, Lighting,.... (not beraking fourth wall)  
- Narrative - Narrator, AI, ...


## Saliency
**Where to look** - Attention garbing. Control where player and cam look.  

  - **Bottom up Saliency** - Contrast, movement  (Stronger in cinema cause we are chilling)
  - **Top-Down Saliency** - Humans (meaning), NowSilent (We care now) (Stronger in goal/task orient mode) Human faces, people, things associated with our current task/goal (attentional goals).  

**Attentional goals**  help players notice and pay attention to things  - (which can mean you become more ‘blind’ to other things). a locked gate they might assume the goal forward is to open the gate (even though the solution is to climb out a window).It’s also worth noting that if players are already focused on something  else


## Affordances
**Where to go / what are possible actions** provide strong clues to the operations of things. Control what players believe is usable -  Windows afford to looking through.  Doors for enter, slots for inserting, knobs for turning, buton for press, flips for switch.      

.

- **Positive** - Afford to be used   
- **Negative** - Doesn’t afford to be used and can’t be  / Nope zone
- **False** - ! looks like it affords to be used but can’t

.

- **Objects** - Machines, doors...
- **Surface**  - floor. we walk to affordance surface to walk. along longest sight lights. (or somewhere else if there could be price)


### Encourage

- **Mystery** - If there is information to learn `Wniees` - landmark with mystery element
- **Teasing** - Show what you can get yet.
- **Colectables/**
- high level long term goals. not pull a leaver.


---


# Space

## Composition
Composing 3d to view in 2d (flat monitor) like composition rules  

- Clarity and flow vs confusion
- Vary silhouettes of the skyline  
- Lines of sight  
- Depth perception vs. real space

## Orientation

**where I am**  In games Perceptual pattern to create Orientation  
- Signposting (oznaczenia charakterystyczne dla areny)
- Divide to district / zroznicuj areny (to distinc in map and mind )


- `Landmarks` - individual objects
- `District` - with unique fulvous
- `Linear elements` - Path, rivers.
- `Edges` - Walls, rivers (temporary / depended)  
- `Nodes` - moments of decisions - train station
- `Point of interest` -  
Way finding elements:
dont lead player where to go but how move through space





## Function

[Architecture](/arch/)

- Differentiate by usage: `stelth` / `combat` / `traversal` / public `interaction` (opportunities for different playstyles  )
- `public space` / `purpose spaces`
- `primary target` (no deadends) vs. `illusory targets` vs. `escalating` (everywhere), vs `bonus missions`
- beginning and end


### Pacing

linear vs. non-linear ### non linear - Pacing    
 moving through a level more fluid and intuitive
- intensity  
- variety  
- time  


### Prospect & Refuge
**Prospect** is a view, and **Refuge** is Safety place. This kept our ancestors safe from enemies/predators and the elements, meet basic human psychological needs.  (evolutionary heritage). provide people with the capacity to observe (prospect)

- **Primary**  - you have now both
- **Secondary** - we have only one and see second far away is only promise)



### Secrets

- **Breadcrumbing** -  sending brief and sporadic messages. Trail of something (usually pickups or information) that leads the player in the right direction or towards  
- **Hints** - Slight or indirect indication or suggestion. (notes on paper, maps, signs)

## Traversing  Action Space > is skill based ?  


## Combat Spaces
Design for multiple options and strategies. viable/intended ranges of the combat space. pieces of cover should be available to the player at the start of combat Preventing teams from being able to spawn camp
- Vintage point - Show off the combat space (or area the player needs to sneak through),
- Fronts
- Flanks (he bridge(s) in the neutral zone between the combating sides)
- No man’s land. Hard to defence (can add colectable at center)
- Entrances (Enemy reinforcements enter from different positions or in new ways)
- Covers Can
  - durability:
    - Static - Hard cover
    - Moveable / Dynamic - can be moved / destroyed  . temporary
    - Moving - have a predictable movement
    - Concealment - no ptrotection like bush.  Soft cover  
  -  high 2m+ / low ~1m (you don’t want to make Low cover look like High cover and potentially mess up things)
  -  block
    - vision
    - damage
- Line of sight
- Vertical arangement

### Level arangement
- Flow in general is about keeping players forward momentum going. (not to hardcor cornes )
- Conmnectivity

E.g.
- circle (ring)
- 8 (2 circles)
- Clash points - places wher efight (Double Clash)
- Tug of War  - liner teams oposite sites. (vartiation with 2 paths )
types: For 'Capture the flag' CTF / therytory take over   
Offence / defence differencess      

### Graph theory
for multiplayers


https://www.raphkoster.com/games/presentations/small-worlds-competitive-and-cooperative-structures-in-online-worlds/
### Line of sight
- Horizontal LoS
- Vertical LoS
- Tight angles
- Ramps
- Corner angles & verticality



### Multiplayer

mastery mapy vs nowa mapa .
- balance
- asymetry  


---

# Visuals
- Generally more effective when it makes contextual narrative sense  
- Must be part of gameplay mechanics

## Signifiers
**Clues to how to use/discover** - Gameplay related. Physics, usable & reactivity. show Affordances (signals that help find that sth is usable (signs / colors))
Apply signifires to reflect affordances.

[Design](/graphicdesign/)

## Visual Language
Gradient of visual complexity where the play space has less visual complexity and then as the space transitions to where players/enemies can no longer traverse (or where something visually important is) we increase it.
- develop & maintain visual language consistency in style: aesthetic.
- `Optimum complexity` - redability


##### Atmosphere
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

[Lore](/lore/)


---

# Gameplay

[Game Design](/gamemechanics/)   
[Game Mechanics](/gamemechanics/)   


### Gating
Revealing level slowly, in tiers.

|  |  |
| ---|  ---|
gates hard | Halts progress until something is completed,  
gates soft | Intended to briefly slow the player down.   
valves | one way,  keep pushing players forward  





---------


# Procedural
[Procedural](/procedural/)



---------


(dieter rams: minimalist product design)  
(book: design of normal things don norman)  
(roberto rengel: shaping interior space)    
[doc](https://docs.google.com/document/d/1fAlf2MwEFTwePwzbP3try1H0aYa9kpVBHPBkyIq-caY/preview?pru=AAABcubYTrs*65ZuXXMNJriddYR6IXE8Ag#), [pod](https://www.psychologyofgames.com/2020/01/podcast-55-the-psychology-of-level-design/)   
