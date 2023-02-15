---
title: Game Theory
description: Players, Strategy, Payoff.
categories:
 - PSY
tags:
- Cognition
- Science
- Game Dev
- Gameplay
- Math

permalink: /gametheory/

---



# Game Types
Mathematical modeling at strategic interaction between rational agents.
 - action of one player influence other players (concept of strategic interdependence)
- assumption that agents act rationally. (rational bah not always conform to reality)


Players, strategy, payoff.    

process:
1. Make assumptions - thought process came from Assumptions. Can dispute, criticize ect... (Carefully with assumptions)
2. Do math  - can not dispute
3. Reach conclusion


Game theory to work need rational actors

[Human Behavioral Biology](/humbio1/)   
[Personality](/personality/)  
[Game Mechanics](/gamemechanics/)  


- In lot of species there is no cognitive strategy
- In real live multiple goals and multiple games

## Number of Players  
- Two
- More players

## Progression
- Turn based   
- Simultaneous move    

## Number of Rounds
- Infinite
- Repeated

Repeated play increase cooperation

## Information availability
- Perfect -  known information
- Incomplite  -> Bayesian Nash equilibrium, perfect Bayesian equilibrium
- Depth limited search.

## Zero Sum Game
 - Interest is not overlapping. `win-lose`


## Approaches to Conflict
### Cooperative
**How to be fair** - Group best effort, coalition and benefit and contribution type in coalition

#### Shapley Value
- method of dividing gains  or costs  among players according to value of individual contribution

#### Marginal Contribution
- Determined by what is gain or lost  by removing them from the game
- Dummy player have 0 value

If 2 parties bring same things to coalition, they should have to contribute  the same amount &  should  be rewarded  for their contributions equal.



#### Pareto efficiency
Outcome is Pareto optimal if there is no outcome that makes at least one player better off without making any player worse off.


### Competitive
**How to be smart**  - Actor best interest - sub optimal solution in the long run


#### Nash equilibrium
optimal outcome of a game is where no player have incentives to deviate from initial strategy.  
(decide to be better off no matter what opponent will do) (rational play when more then one player. not only define start but always believes) Every player play `best response`  strategy  to what other doing. Knowing other strategies and have no incentives to cheat. Everyone want to keep it without policing

Most games have odd number of equilibria

no player have profitable deviations

---





# Terms

### Risk Aversion
how much u willing to pay for insurance



### Tragedy of the Commons
Some public good lot of persons contribute no one want to pay cause take a small parts of contribution only.( there is mat trough to compensate )   


there are certain optimal strategies and no other GT solution


### Commitment problems
You must commit but not sure what B will chose



**Ultimatum** Game Assumptions - single ultimatum, Take or leave it  



### Probability distributuin
- advancced strategies games, more revarding

---

# Strategies

#### Dominant strategy
- best payoff no matter other players moves.
ITS EXTENTION IS NASH EQQUILIBRIUM (and more)

#### MinMax  
- minmimize maximum lose. ensure you guarded by worst scenario. (use in zero sum)

#### Mix Strategy
- play only if there are indifferences in few strategies



#### Backward Induction
Base on assumption that all future play will be rational. Whenever I'm making move now I should focus on what opponent will do after that. maximizing

#### Forward Induction
Based on assumption that all past play was rational


#### Tic Tac Toe


#### Pavlov strategy
 - switch if not working (you can exploit)

#### TfT
-  `Tit for tat` drove other strategies to extinction and formalize optimal strategy  may lose battles but win wars. (Vulnerable of signal error). Start nice cooperating > forgiving > cooperate when you can   

#### FTfT
- `forgiving tit for tat`  witch is more vulnerable for exploitation TfT -> jezeli zaufanie to switch to forgiven TFTF Trust  

#### Madness
- possibility of changes   
Strategies to survive forgiving tic for tat (vulnerable to exploit) > forgiven tic for tat after while  
- counterintuitive moves could help with strength opponents.


#### Game Theory Optimal
- assumes opponent is always countering with the perfect strategy
- can have lower yield EV then exploitative play

pkr > fint highest EV lines routes possible for have best formulatetd strategy. + balance it to dont be exploited.
but can be not profitable as exploit.  
balance stratedy  

##### Exploitative
-humans make a lot errors  exploit mistakes
exploitative strategy is valuable in the short run after new entry,

##### Explorative
while explorative strategy is significant in the long run only after new entry.

#####  Jeopardy! Strategy


---

transitivity-in-game-theory
# Games





#### Poisoner Dilemma


| | A Cooperate | A Defect |
|--|--|--|
**B Cooperate**| A 0 / B 0 | A 0 / B -2
**B Defect** |  A  -2 / B 0 | A -1 / B -1

For player A - Always defect to GTO ( Dominant strategy ) best outcome regardless what other player does.

| | A Cooperate | A Defect |
|--|--|--|
**B Cooperate**| A 0  | **A 0**
**B Defect** |  A  -2  | **A -1**


#### Stag Hunt



||Stag|Rabbit|
|--|--|--|
**Stag**| **3, 3** |  0 , 2
**Rabbit** | 2, 0 | **1, 1**

if no lies / neither player deviate
- Stag/Stag (**pareto efficient**)
- Rabit/Rabit (**pareto inefficient**) are equilibria's.


#### Matching Pennies
Zero sum game.  No pure strategy Nash equilibrium. - If no pure nash exist in mix strategies.  



||Heads|Tails|
|--|--|--|
**Heads**|1, -1 |  -1 , 1
**Tails** | -1, 1 | 1, -1

Coin filps


#### Batle of sexes


||Heads|Tails|
|--|--|--|
**Heads**|1, 2 | 0 , 0
**Tails** | 0, 0 | 2, 1

A>B>C

||Heads|Tails|
|--|--|--|
**Heads**|B, a | C, c
**Tails** | C, c | A, b

(1,2) - are nash


-------

combinatorial games      
diferential games    
TCG - traiding card games  



---

# Poker

a game of decision-making in the face of incomplete information.
## Basics


### Betting rounds & Positions

|Button / Dealer | strongest - 50% opening range / button river betting range (only 57 combos) | **In position** (Act last)|
|-|-|-|
|Cutoff  |  second-best position in a hand of poker. |  Late Positions
|HiJack
|LoJack |Tide pairs and Figure + high||
|Under The Gun +1  | | Mid positions
|Under The Gun | only ases | (left to the BB Act first Before the flop)
|BB | defending range calling range 40%  (no AA KK QQ - because it wuld be rerange )  play garbage hands priced in (range advantage) | Early position
|SB | tight is right |  **Out of position** Act first (After flop) // in short stack when AllIn - is good (game of chicken ) |





### Moves
Bet - change   
Check - stay in game, no change   
Fold -   
Call - answer to bet    
Check-raise - The player who checked (in anticipation of others raise) then raises in the same round    
Limp - Playing minimum bet when u  last to act.   

### Chips
Chips to start: 20-40 BB for shallow tables to 250+ for deep game  


### Other rules
- **Ante** - Ante and Blinds are forced bets
- **Bounty** -

### pattern visible on table
pair - invisible
straight -
flush - visible

## Strategies
kombninatoryka wazna  
- relation of hands u have to opponent hand
- your percived range. Whaty they expected u to have

#### Combinatorics
ranges / minimum defence frequency (MDF) /  correct frequencies for calling, folding, and raising (depending on bet size) / likelihood of your opponent holding specific hands
169 different poker hands:  
 Hand Range Charts

### GTO
Game theory optimal - is not enough agressive. Optimize decisions and  build strategies to put opponents in place where they have hard time with optimization their decisions (look for weaknes).



## Tells
- How much `Engagement` in cards
- protect valuable things, close to you vs prefold (away)
- eyes,
   - quick glance on chip, thinking about value  legs
subconcious tels
concious tell> playing .. overacting > opposit what trying to convey
- feet forrward > `confidence` `strengths`
- stop chewing gum if scary , exiced chue
- disconnect
  - bad cards  from the game .
  - good cards just no focs on cards , watch for chit chat

https://www.youtube.com/c/Gametheory101/videos  
https://www.youtube.com/c/PrimerLearning/videos  



--


# Bargaining
Bargening dynamics get really complicated really quickly.


| ||
| ---| ---|
| Proposal power |  make offers to the other side (accept/reject position not good)
| Patience  | no needing a deal (**Tragedy of bargening**) 'rich get richer'
| Outside options |
| Monopoly | Unique quality
| Knowledge | knowledge of the others sides minimum value dont know choose between lesser of two evils
| Reputation|
| Credible commitment | contracts good / black market bad
| Costly signals of higher value |

---


# War
(international relations)
- war inefficiency puzzle
- preventive war
- preemptive war

jak zapobiegać wojnie.
- kraje handlujące ze sobą mniej wojen (world with trade consume more )
- koszty



# Bio
r/K selection theory
 trade off between quantity and quality of offspring.
r (left), K (right) strategies.


---
- coordination problem
- mysia utopia


SOMETIMES: burning money help to increes payof !!!!!!!!!


# Tactics
- odciecie od zaopatrzenia
- wysokość - pozycja
- nacierajacy x3 sil (latwiej bronic)
-

- pogoda gdzie sie przemieszczać
-



#
standaard deviation

https://www.google.com/search?q=standard+deviation&source=lmns&bih=786&biw=1597&hl=en&sa=X&ved=2ahUKEwiatuLygbb6AhWJAhAIHfmlCZ4Q_AUoAHoECAEQAA
