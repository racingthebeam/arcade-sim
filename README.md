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

At regular intervals, a random cohort of potential customer agents is generated. Each of these agents ranks the active arcades (players + competitors) based on its own stats and decides which arcade to visit. Any that choose the player's arcade are spawned as agents at the entrance point.



## Win Conditions

Arcade is judged on a bunch of metrics:

  - turnover/profit
  - popularity
  - safety
  - tech-level

...any others?

## Resources to Manage

### Money

### Electricity

### Stock

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
