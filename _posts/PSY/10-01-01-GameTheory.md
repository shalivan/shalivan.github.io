---
title: Game Theory
description: Rules, Strategies
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


# Game Theory
Mathematical study of optimizing agents strategies in games with more than one player where outcome depend on other agents actions. (payoff is affected by the decisions made by others)model as players are perfect  every agent must play with GT rules. (but its rational to behave time to time irrational)


1. Make assumptions - thought process came from Assumptions. Can dispute, criticize ect... (Carefully with assumptions)
2. Do math  - can not dispute
3. Reach conclusion


Game theory to work need rational actors 

[Human Behavioral Biology](/humbio1/)   
[Personality](/personality/)  
[Game Mechanics](/gamemechanics/)  


- In lot of species there is no cognitive strategy
- In real live multiple goals and multiple games

### Number of Players  
- Two
- More players

### Progression
- Turn based   
- Simultaneous move    

### Number of Rounds
- Infinite
- Repeated

Repeated play increase cooperation

### Information availability
- Perfect -  known information
- Incomplite  -> Bayesian Nash equilibrium, perfect Bayesian equilibrium
- Depth limited search.

### Zero Sum Game
 - Interest is not overlapping. `win-lose`

---
# Cooperative
**How to be fair** - Group best effort, coalition and benefit and contribution type in coalition

### Shapley Value
- method of dividing gains  or costs  among players according to value of individual contribution

### Marginal Contribution
- Determined by what is gain or lost  by removing them from the game
- Dummy player have 0 value

If 2 parties bring same things to coalition, they should have to contribute  the same amount &  should  be rewarded  for their contributions equal.



### Pareto efficiency
Outcome is Pareto optimal if there is no outcome that makes at least one player better off without making any player worse off.


# Competitive
**How to be smart**  - Actor best interest - sub optimal solution in the long run


### Nash equilibrium
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



## Probability distributuin
- advancced strategies games, more revarding

---

# Strategies


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


#####  Jeopardy! Strategy



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


# War
(international relations)
- war inefficiency puzzle, preverntive war, preemptive war

```
r/K selection theory
 trade off between quantity and quality of offspring.
r (left), K (right) strategies.
```


---


# Games





#### Poisoner Dilemma
number show years in jail if Cooperate or Defect

||Cooperate|Defect |
|--|--|--|
**Cooperate**|-1, -1 |0 , -10
**Defect** | -10, 0 | 5, 5

Defect strategy dominate cooperate
Better of Defecting regardless what other player does  

#### Stag Hunt

neither player deviate

||Stag|Rabbit|
|--|--|--|
**Stag**|3, 3 |  0 , 2
**Rabbit** | 2, 0 | 1, 1

Stag/Stag (pareto efficient) and Rabit/Rabit (pareto inefficient) are equilibrias.

- if no lies


#### Matching Pennies
Zero sum game.  No pure strategy nash equilibrium.  
If no pure nash exist in mix strategies.  



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



---

# Poker


## Basics



||Letter to act - better.|||
|-|-|-|-|
Small Blind | "out of position" | Early position | wide open-rise range. all figures, all suited and sudoconnectors  
Big Blind | defending range calling range 40%  (no AA KK QQ - because it wuld be rerange )  play garbage hands (range advantage) | Early position
Under The Gun | | Act first  
Under The Gun +1  | | Mid positions
LoJack ||| Tide pairs and Figure + high
HiJack
Cutoff  |  second-best position in a hand of poker. |  Late Positions
Button / Dealer | strongest - 50% opening range / button river betting range (only 57 combos) |  Act last

Bet   
Check   
Fold    
Call  
Check-raise


- **Ante** - Ante and Blinds are forced bets
- **Bounty** -

## GTO
Game theory optimal - is not enough agressive.



U MUST EXPLOIT OPPONENTS AND LOOK WEAKNES IN THEM
kombninatoryka wazna

Optimize decisions and  
build strategies to put opponents in place where they have hard time with optimization their decisions.
relation of hands u have to opponent hand
- your percived range. Whaty they expected u to have


--
jak zapobiegać wojnie.
- kraje chandlujące ze sobą mniej wojen (world with trade consume more )
- koszty




SOMETIMES: burning money help to increes payof !!!!!!!!!

## Limping
comon blind vs blind action
Limper is calling in Big Blind

Playing minimum bet when u  last to act.

button klimpoing (specific)
## Tels

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
