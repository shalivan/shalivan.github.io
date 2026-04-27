---
title: Game Mechanics Shooting
description: Systems, Progression, Economy, Balance
categories:
  - PSY
tags:
  - Design
  - Gameplay
  - GameDev
  - Narration
permalink: /gamemechanicsmulti/
aliases:
  - gamemechanicsmulti
---
Related notes: [Ludology](/ludology/)  [Game Design](/gamedesign/)    [Game Mechanics](/gamemechanics/)    [Game Theory](/gametheory/)   [Level Design](/leveldesign/)  [Taxonomy](/puzzle/)

 
 {% comment %}  [[08-01-01-GameDesign]]  [[10-01-01-GameTheory]]   [[Classic_Mechanics]]  [[05-01-01-MechanicsSingle]] [[09-01-01-Ludology]] [[10-01-01-GameTheory]]  [[12-01-01-Lore]]  {% endcomment %}
 
```
# Enemies
  types and classes .
  - short long distance and speed
  - difficulty

## Encounters
Events with NPCs

###### Waves
Increase and manipulate amounts / strength

- combat types
- obrona manewrowa
- raidy

# Combat
non combat - combat loop
fighhting games are rock paper scisors (advanced with reading opponents pre anims to read next move )   

Melee > projectiles > hitscan
Charge > stay back

szybkosc projectaili - wpływa na dystancs w ktorym jest walka. !



## Combat loop
pasing / important elements
- doom dropp all what slow down actions (like aming)
peak priorities
how much weapons / how get new and ammo ...
upgread trees
pase - of new tools and mechanics  2.


## AI

[YT rainworld 2d ai](https://youtu.be/hOsYTzd0yeA) -

### .
- pathfinding
- behaviur trees - selector node / sequence node (queque)


## Mele  

https://threadreaderapp.com/thread/1358654321303277568.html


### Timed
not instant. 3 phases
1. anticipation - speed  
2. contact
3. recovery

tacticly distinct !!!!!!!!!!!!!!!!!!!!!!!!!! - could be subtle -
Advantages / Disadvantage - (heavy damage slow)

- fast /slow  -  light 14 frames - heavy 28 frames and u are vonurable beform hit
- wide/ range
- push away/ knock down /air
- work on distance
- stunt  - watch for stunt lock (get enemy in loop )
- culdown to not spawning
- player vornuable after use
- required sth
- animation canceling. (no in darksouls)  carfeul and commiting
- range distance/snaping  (depend how sticky ) in batman lot of snaping (and in other flow quick )- not in dark souls
- distnace - tip of blade more crit than full close.
- charge

combos and controls.
- seq of keys or gesture
- chain of same keys in rythm

parry / counter - block exackly when u block in same time of attack  .
  - efortless vs
  - only in slmall time slot - can damage if not done in time


tactic:
- piking targts - kill the hiller


## Shooting  

#### Bullets

|     |             |          |     |
| --- | ----------- | -------- | --- |
|     | Projectiles | stayback |     |
|     | Hit scan    | charging |     |

Projectiles are predictable

#### Recoil     

#### Reloads


fast assault rifle   
shotgun at close   
rocket launch - deadly but risky   

### Aiming

auto aim   

https://twitter.com/Fading_Shadow_/status/1540095904643895296
- The Accuracy Cone (= Error Angle) defines an area where your bullet can land. The placement of your bullet within this area is entirely random.
- The Aim Assist Cone defines an area around your reticle where the game will look for enemy targets. Once an enemy enters this area (or you move your reticle close to them) Aim Assist will kick in. What Aim Assist does is it snaps your accuracy cone to a target. [cont]...] What's important about this is that the Aim Assist is factored in first which means that the randomness introduced by the Accuracy Cone will not be corrected for by Aim Assist.
So TLDR: Accuracy doesn't care what's in front of you, it's purely RNG

First on that list is the in-air accuracy penalty. ⏬
Fading Shadow

Each archetype of weapon has an intrinsic penalty to accuracy that is activated as soon as your boots leave the ground.
This penalty cuts the remaining cone you have in half again leaving you with 1/4 of the original size of your Aim Assist cone.



### Types 


 SMG - Spora szybkostrzelność , pojemny magazynek , niewielki zasięg że mogę się z nimi dość sprawnie poruszać i przez mniejszy DMG per Pocik ale zwiększoną szybkostrzelność powinienem raczej pakować we wroga długie serie ( Spray and pray Jako broń o małym zasięgu ( wydaje mi się mająca pełnić role SMG ) powinna mieć w miarę skuteczny hipfire
 snip - 
 shotg - 
 pistol - 






----


### Enemies

queue of killing. Archer healer, normals
dela with me first
deal wieh me last
high hp low famage

Attribute differentiation
timing. of damage. sometimes take
close/ long range attack
movement

immune to some actions
local vulnerability  


## AI

good AI let u know what is intended to do
 p- predictable > player can plan  
predictable actions / unpredictable consequences. (someone run but u never  know where)   

personal AI's that have RNG stats (na stałe wylosowane) - & remembering interactions with player
ecosystems for ai

---
[Rafał Tyl - Uncommon sense: a systemic approach to beliefs of AI agents](https://youtu.be/hoHE2QhMMuk)

AI
cheating AI
lack of situational awareness

perception > belief building (reasoning about inf from past) its hard  cause data is heterogenious >  decision makeing > action

barbara dunin-kęplicz Andrzej Szałas  MIMUW
- epistemic profiles
= rule-based resoning with belied structure
- 4QL language
- Group beliefs



- lack of data  (hidden)
- wrong answer  
https://youtu.be/hoHE2QhMMuk?list=PLqUbLv3b1v3cDIo9LCgcsZ3A0whWixGe6
differences (,1. false, 2. unknown (false or true), 3. inconsistent (false and true), 4. true)

----


dynamic organization building and repairing   
villains with procedural goals

```