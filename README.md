# arcade-sim

The game is an arcade simulator, based on Theme Park.

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
