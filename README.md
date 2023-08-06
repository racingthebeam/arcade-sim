# arcade-sim

The game is an arcade simulator, based on Theme Park. Player manages an 80-90s style arcade, installing gaming cabinets and other attractions, hiring staff, managing policies and financial concerns; customers come in and play the games, eat, drink - basically spend their money until they're bored, then they leave.

## Key Concepts

  - Any static object placed in the world (except for walls and doors) is a Thing
  - Each Thing placed in the world has a _build time_ and _cost_.
  - Five types of autonomous agents: Customer, Customer Service Rep (CSR), Janitor, Security Guard, Technician

## Arcade Metrics

At any given time, the player's arcade can be represented by a metrics vector that includes e.g. popularity, safety cash reserves, running cost. This vector is used to determine a) how the arcade is performing against its competitors and b) whether potential customers decide to come to this arcade.

  - [ ] decide exact list of metrics

## Competitor Arcades

For each level there are a number of competitor aracdes. These are not fully simulated; instead, the options are:

  1. predetermined functions are used to model competitors metrics over time
  2. lightweight simulation function

In the first instance we will implement (1) since this is easy to implement; each level simply needs to have pregenerated per-competitor metrics curves. For harder levels these curves could even be related/react to the player's own metrics.

The advantage of (2) is that competitors would be able to react to each other's decisions at a macro level, but this is far more complicated to implement, and there's no guarantee there will be a good outcome from a gameplay PoV. A poor implementation could even cause competitors to become insurmountably better that the player's arcade.

Since an arcade's metric vector is ultimately all that matters, the method by which it is calculated is not important insofar as it relates to implementing all game features. So let's just do (1) until there's a proven need for (2).

## Customer Attraction

At regular intervals, a random cohort of potential customer agents is generated. Each of these agents ranks the active arcades (players + competitors) based on its own preferences and decides which arcade to visit. Those customers that choose the player's arcade are spawned as agents at the entrance point.

## Customer Model

Customer attributes:

  - age: fixed at creation time; used to scale how much certain activities interest them, and to limit access to certain things
  - money: used to pay for games, food, drink etc.
  - skill vector: one entry for each game type
  - hunger: increases over time; once it hits a threshold, customer will prioritise finding food
  - thirst: increases over time; once it hits a threshold, customer will prioritise finding drink
  - rage: increases as customer spends time playing games they are not good at (multiplied by games intrinsic frustration-factor). Once rage exceeds threshold, customer may lash out (damage/destroy cabinets, attack people)
  - boredom: increases if customer cannot find/play games they enjoy
  - happiness: increases when "good" things happen, and vice-versa
  - fame: fixed at creation time; famous players will attract crowds. This could be flags rather than a single value, e.g. "pinball wizard", "beat-em-up king"
  - tickets won: total number of tickets won
  - ticket balance
  - prizes won: total number of prizes won
  - prize value won: value of all prizes won

TODO: need a list of things that affect these attributes

## IDEA: Customer Groups

Players could form groups (either at time of arrival, or spontaneously during their visit). Customers in a group would try to act together, or at least stay roughly in the same vicinity. Groups make it easier to support games that require 2+ players (e.g. bowling, air hockey), since there's an implicit pool of partners.

---

## Implementation Details

### Game Access

Every game has a participation rule:

  - single player: only one player can play at a time
  - group multi player: min/max number of players, all of whom must come from the same group (examples: air hockey, bowling, 2-4 player cabinet)
  - open multi player: min/max number of players, any visitor is a candidate (example: go karts)
  - continuous multi player: max number of players, any visitor is a candidate, no fixed duration (example: soft-play)

When a game becomes free, it is added to the free list of games. We need an algorithm to decide which visitor does what. Questions:

  - can agents fight/compete over access to games? sounds like a fun mechanic
  - if there's a multi-player game that someone wants to play, but they have no friends, can they claim a spot and wait for someone else to hopefully join them? This could be a cool mechanic for forming ad-hoc groups

---

Everything below here is just rambling...

## Random Ideas

  - Age policies - set min/max ages for activities. Allowing kids to play things too old for them might, e.g. scare them away, or be too dangerous (e.g. go-karting). Allowing older kids on soft-play might cause the younger ones to get injured



## Win Conditions

Arcade is judged on a bunch of metrics:

  - turnover/profit
  - popularity
  - safety
  - tech-level

...any others?

## Resources to Manage

### Outgoings

  - Rent
  - Staff wages
  - Electricity
  - Stock

## Map

  - 2D, tile-based
  - each cell has a floor type (determines its draw-style, and zoning - e.g. public/staff area)
  - wall may be placed on cell, which makes it impassable
  - Things can be placed on cell, which makes it impassable
  - Doors join zone and can be denoted as staff-only

## Attractions

### Food/Drink

  - Drink stand
  - Food stand
  - Vending machine (food, drink, coffee)
  - Bar

### Games

Types of games:

  - Various arcade cabinets
  - Air Hockey (needs 2 players)
  - DDR
  - Pinball
  - Prize-games: each has configurable difficulty/win-rate/payout
    - Basketball hoops
    - Punch strength
    - Punch reaction time
    - Grabber
    - Coin drop

Metrics we could use to rate games:

  - wow-factor
  - difficulty
  - novelty
  - prestige
  - cost
  - length
  - fairness
  - player count
  - type

### Entertainment

  - Bowling alley
  - Dancefloor (with DJ booth)
  - Laser combat game?
  - Go-karts?
  - Soft-play

### Other

  - Prize kiosk: allows prize tickets to be exchanged for prizes. Can add prize stock, set # of tickets required for each price

## Agent

Agent types:

  - Customer
  - Technician
  - Janitor
  - Security Guard
  - Customer Service

### Brains

Each agent type has its own brain implementation.

Brains:

  - have a current active task (possibly hierarchical - e.g "move to location" is a composite action comprising "find-path" and "follow-path" sub-actions)
  - once the active task completes, brain selects a new task
  - additionally, brains can react to external events - which may cause the current action to be cancelled and replaced with a new one. For example, fire alarm causes agents to locate exit and flee map.

#### Customer

Agent stats:

  - skill level (do we need a skill level per game type?)
  - happiness
  - boredom
  - rage
  - fame
  - hunger
  - thirst
  - money

#### Technician Brain

#### Janitor Brain

#### Security Brain

## Thing

Any permanent fixture on the map is called a Thing; examples:

  - Arcade game
  - Shop
  - Decorative fixture

## Scenarios

### Unruly Customer

### Celebrity Player

Player comes in 

### 
