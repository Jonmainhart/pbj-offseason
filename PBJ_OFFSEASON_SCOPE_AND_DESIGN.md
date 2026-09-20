# PBJ Offseason Bar — Scope & Design Document (Revised)

## 1. Purpose

The PBJ Offseason Bar is a separate, lightweight browser project that replaces or receives traffic from the main PBJ football dashboard during the offseason.

It is **not** intended to become a full game. It is a small, interactive, faux-SNES bar diorama: recognizable characters come and go, occupy familiar spots, perform simple actions, react to props and Easter eggs, and occasionally speak.

The guiding goal is:

> **Make the bar picture move.**

The project should feel alive and personal without becoming a third job to maintain.

---

## 2. Repository and Deployment

- Separate GitHub repository from the PBJ football dashboard
- Main PBJ URL may redirect here during the offseason
- Static hosting only (preferably GitHub Pages)
- No backend, database, logins, or accounts

### Preferred technical direction

- Vanilla JavaScript
- HTML Canvas
- HTML/CSS for shell UI
- Static assets
- No framework or game engine by default

Pygame/Pygbag is technically possible in the browser, but Canvas + JavaScript is preferred because the browser is the real deployment target.

---

## 3. Scope Guardrails

This project is an **animated diorama with NPC behavior**, not a traditional game.

### In scope

- One primary bar scene
- Faux-SNES visual style
- Named and generic sprites
- Simple arrival/departure behavior
- Node-based movement
- Simple idle/action animations
- Speech bubbles
- Click/tap interactions
- Character-specific behavior configured in character data
- Node-specific Easter eggs
- Reusable costume overlays
- TV state and TV-related events
- Time-of-day lighting
- Indoor background activity
- Deterministic simulation tests before graphics
- Static deployment

### Out of scope unless deliberately added later

- Quests
- Inventory system
- Player avatar
- Physics
- Free-form navigation
- General-purpose pathfinding
- Combat
- Scoring
- Accounts or saved user profiles
- Backend services
- Database persistence
- Multiplayer
- Real weather
- Real sunrise/sunset calculations
- Dynamic shadow simulation
- Large inheritance hierarchies
- A general-purpose game engine

### Explicit simplifications

- No visible parking lot
- No bikes
- No cars
- No POS station
- No picnic tables
- Minimal visible seating clutter

---

## 4. Visual Direction

### Style

The visual target is **faux-SNES** rather than strict hardware-authentic SNES art.

The project should evoke 16-bit console games while selectively cheating for recognizability and readability.

### Art rules

- Hard pixel edges
- Deliberately low apparent pixel density
- Environment may use a coarser pixel grid than named characters
- Named sprites may selectively use extra detail where it helps recognition
- Limited-feeling palette without enforcing true historical hardware limits
- Simple pixel shadows rather than realistic lighting
- Short, economical animations
- No photographic smoothing
- No overly polished or modern vector-like character rendering

---

## 5. Perspective and Orientation

The earlier parking-lot perspective has been dropped in favor of a simpler, more top-down view that stays closer to the original rough diagram.

### Final working perspective

- More top-down than the earlier parking-lot concept
- Still slightly angled, not perfectly overhead
- Designed to keep sprites readable while simplifying the environment
- The visible scene stays almost entirely within the outside bar area

### Real-world orientation

If viewed on a map:

- The street runs **east/west**
- The main parking lot is **south** of the outside area
- Additional parking is **west** past the top wall
- The **glass wall** separating outside from inside is **north**
- The scene perspective shifts to look toward the **west wall**, where the **TV** is located

### Gameplay-facing implication

This gives a compact, self-contained scene with entry from:

- **East**
- **North** (interior)
- **South**

The parking lot exists conceptually, but it is **not drawn**.

---

## 6. Clean Scene Layout

### Scene philosophy

The scene should be a simplified, recognizable version of the real outside bar, not an architectural recreation.

The entire visible scene should live inside the bar area itself. The environment should read immediately as the outside bar, but with clutter reduced to improve readability, movement, and maintainability.

### Major visible features

- L-shaped outside bar
- Two 4-person high-top tables
- North-side glass wall separating outside from inside
- Limited visible interior just beyond the glass wall
- A more prominent TV on the west wall
- A small amount of open floor space for movement
- Very limited interior furniture:
  - maybe one inside seat or bar spot
  - possibly a tiny amount of floor space
  - no need for a full interior recreation

### Removed features

- POS station
- Picnic tables
- Visible parking lot
- Bike/car staging
- Most incidental chairs/stools

### Layout intent

The interactive focus is tightly concentrated on:

- The L-bar
- The two high tops
- The TV
- A very small number of props/Easter eggs
- Moving named characters

### Clean conceptual layout

```text
                NORTH / INTERIOR
        ┌─────────────────────────────┐
        │  limited visible interior   │
        │  (small background area)    │
        └────── glass wall / entry ───┘

        ┌──────────── L-BAR ─────────┐
        │ B7  B6  B5                 │
WEST    │ B1  B2  B3  B4             │   EAST / BOTTOM
TV ---> │                            │   customer entry
        └────────────────────────────┘

              H1A   H1B
              H1C   H1D

              H2A   H2B
              H2C   H2D

           SOUTH entry (offscreen origin)
```

This diagram is conceptual only. Exact node placement can shift after better reference photos and a cleaner scene blockout.

### Intended visible feel

- The bar remains the obvious focal point
- The TV is prominent enough to matter
- The interior is visibly present but not dominant
- The scene is compact, readable, and easy to route

---

## 7. Scene Scope

### Primary visible elements

- L-shaped outside bar
- Two 4-person high-top tables
- North glass wall separating outside from inside
- Limited interior beyond the glass wall
- TV on the west wall
- A few carefully chosen props
- Open walking space

### Interior

The indoor area is:

- Visible
- Animated
- Non-interactive
- Small in scope
- A source/destination for some sprites
- Home to both generic and specific inside-only sprites

The interior should act as a background layer, not a second playable area.

---

## 8. Entrances and Movement

### Customer entry/exit

Customers may enter or leave from:

- **East**
- **North / interior**
- **South**

### Staff movement

Staff may use any plausible route, especially the north/interior side.

### Navigation model

Movement is **node-based**, not free-form.

There is no need for general-purpose pathfinding. Routes between entries, transit points, and destination nodes can be explicitly defined.

Logical movement can be discrete even if rendered movement is smoothed visually.

---

## 9. Interactive Node Model

The main interactive area contains **15 destination nodes**.

### Bar nodes

- B1
- B2
- B3
- B4
- B5
- B6
- B7

### High-top 1

- H1A
- H1B
- H1C
- H1D

### High-top 2

- H2A
- H2B
- H2C
- H2D

### Occupancy

- A primary node normally supports one occupant
- Characters choose among valid open nodes
- Character preferences may weight certain nodes
- Node-specific events may become available depending on who is present and what props exist

---

## 10. John B3

John B3 is a special recurring character, but his special behavior should be configured **inside his character definition**, not scattered across separate special-rule files.

### Character identity

Finalized visual traits:

- Older man, roughly in his 60s but not overly old-looking
- Flat cap
- Short grey buzzed hair on back/sides
- No facial hair
- Longer pointed nose
- Lighter brows
- Mole on left jaw
- Slight beer belly
- Light chambray short-sleeve button-downs or polos
- Cargo shorts

Catchphrase:

> **“This is a Family Restaurant!”**

### B3 behavior

- B3 is **not permanently reserved**
- Any character may occupy B3 while John is absent
- When John arrives:
  - If B3 is empty, he takes B3
  - If another character occupies B3, that character gets up and moves to the next valid available node
  - John then occupies B3

### Bike note

The bike concept has been **removed from scope**.

---

## 11. Character Model Philosophy

Character-specific policy belongs with the character.

If someone wants to change how John behaves, they should be able to open John’s data file and change it there.

### Character files should contain

- Identity
- Display name
- Preferred nodes
- Phrase pool
- Action weights
- Traits
- Costume interest
- TV preferences
- Arrival/departure preferences
- Other character-specific behavior configuration

### Engine responsibility

The engine implements generic verbs such as:

- move
- speak
- idle
- interact with node
- interact with prop
- pick up prop
- use prop
- change TV channel
- wear costume
- return to preferred node

The character definition decides **when and why** those behaviors are favored.

---

## 12. Current Character Roster

### Strongly established / anchor designs

- Mr. Angie
- Angie
- Eli
- Black James
- Will
- John B3
- Mafia
- D-Real

### Still subject to more visual refinement

- Big Red
- Beth
- Kelley
- Shauna
- Keri (Staff)
- Karlee (Staff)
- Steff (Staff)
- Kass (Staff)
- Shorty (Staff)
- Sweary (Staff)
- Jeff (Staff)
- Junior (Staff)
- APJ (with appropriate reactive behavior from certain characters when present)
- Boss Don
- Tom

### Generic characters

The project may include generic inside-only patrons and staff whose purpose is ambience rather than recognizability.

---

## 13. Character Interaction Model

### Main rule

> **Tap/click a character → request that character to do one valid interesting thing.**

Possible responses include:

- Move to another node
- Say a character-specific canned phrase
- Say a phrase from a general pool
- Perform an idle/special animation
- Perform a node-specific action
- Interact with a nearby prop
- React to another nearby character
- React to repeated clicking

### Interaction constraints

- Protected or uninterruptible actions should finish before a queued click response begins
- Repeated clicking should not stack uncontrolled commands
- Use a short interaction cooldown
- No visible action menu
- No player inventory
- No traditional game UI required

---

## 14. Action Selection

Action choice should be context-sensitive and weighted.

A character builds a set of currently valid actions, then selects one by weight.

Possible categories:

- Character-specific phrase
- General phrase
- Move
- Idle animation
- Node-specific interaction
- Prop interaction
- Character reaction

Each action should be able to answer a simple eligibility question such as:

```js
canRun(character, scene)
```

Invalid actions are filtered out before selection.

---

## 15. Easter Eggs and Props

### Persistent Easter egg

**B7** always contains a **mini-xylophone**.

### Random Easter eggs

Some props may appear randomly at eligible nodes.

Examples:

- TV remote
- Hotdog costume
- Hat
- Sunglasses
- Mystery drink
- Football

Props should be lightweight scene data, not a new subsystem.

---

## 16. TV and Remote System

The TV should have a very small state model.

### TV channels

Plan for approximately **2–3 looping TV animations**.

Possible channel categories:

- John’s preferred channel
- Alternate channel
- Weird/wildcard channel

### Remote behavior

If a character other than John finds the remote:

1. They may change the TV channel
2. If John is present and the new channel is not his preferred channel:
   - John notices
   - John leaves B3
   - John retrieves the remote
   - John switches the TV back
   - John returns to B3
3. If John is absent:
   - The changed channel remains
4. If John arrives later and the TV is on the wrong channel:
   - John may immediately or soon trigger the restore sequence

The remote does not require a full inventory system.

---

## 17. Hotdog Costume

A hotdog costume is an Easter egg that can be found and worn by **any eligible character**.

Angie should have a much higher interest weight because she has always wanted to be a mascot.

### Behavior

- Any eligible character can find it
- Angie is strongly weighted toward noticing/finding it
- Once worn, it remains for the rest of that character’s visit
- No persistent wardrobe or inventory system is needed

---

## 18. Lighting and Time of Day

Lighting is in scope, but only as a lightweight visual layer.

### Goal

Visible sky and scene lighting should change according to the visitor’s local clock.

### Initial states

- Day
- Golden hour / dusk
- Night
- Late night

Transitions should blend rather than hard-switch.

### Effects may include

- Sky color shift
- Overall scene tint
- Interior becoming relatively brighter after dark
- Bar practical lights switching on
- TV/sign glow
- Simple pre-rendered glow overlays

### Explicit non-goals

Do not initially implement:

- Real weather
- Location lookup
- Sunrise/sunset API
- Seasonal solar calculations
- Dynamic real-time shadows
- Per-sprite physically based lighting

Working principle:

> **clock → palette blend → practical lights**

---

## 19. Simulation Before Graphics

The first implementation milestone should be **headless**.

Before Canvas, sprites, or animation, the project should prove the simulation rules through data models and automated tests.

### Early behaviors to prove

- Spawn
- Depart
- Move to node
- Occupy node
- Vacate node
- Idle
- Speak
- Click/tap requests action
- Node-specific event
- Prop interaction
- Costume state
- TV state
- Event queue
- John reclaiming B3
- TV remote chain
- Hotdog costume discovery

---

## 20. Determinism and Testing

Randomness and time must be isolated from the rest of the code from the beginning.

### Do not call directly throughout the project

- `Math.random()`
- `Date.now()`

Instead use wrappers such as:

- `simulation/random.js`
- `simulation/clock.js`

### Test priorities

- B3 occupancy and John reclaim behavior
- Remote discovery and TV restore behavior
- Hotdog suit spawning and wearing behavior
- Click-requested action selection and filtering

---

## 21. Architectural Seams

Structure code around responsibilities that change independently.

### Domain

What exists.

Examples:

- Character
- Node
- Prop
- TV

### Actions

Generic verbs/mechanics.

Examples:

- move
- speak
- idle
- interact with node
- interact with prop
- change TV
- wear costume

### Simulation

Runtime behavior.

Examples:

- engine/tick
- scene state
- event queue
- random source
- clock

### Content

Project-specific personality and scene configuration.

Examples:

- character files
- node definitions
- general dialogue
- props
- TV channels

### Rendering

Presentation only.

Examples:

- Canvas renderer
- Sprite renderer
- Lighting renderer
- Speech bubble renderer

### Input

User interaction only.

Example:

- Pointer/tap handling

### Core rules

> **The simulation should know nothing about graphics.**

> **Character files own personality. Engine files own mechanics.**

---

## 22. Proposed Project Structure

```text
pbj-offseason-bar/
├── index.html
├── style.css
├── package.json
├── README.md
├── docs/
│   └── PROJECT_SCOPE_AND_DESIGN.md
├── src/
│   ├── domain/
│   │   ├── character.js
│   │   ├── node.js
│   │   ├── prop.js
│   │   └── tv.js
│   ├── actions/
│   │   ├── move.js
│   │   ├── speak.js
│   │   ├── idle.js
│   │   ├── interactWithNode.js
│   │   ├── interactWithProp.js
│   │   ├── changeTv.js
│   │   └── wearCostume.js
│   ├── simulation/
│   │   ├── engine.js
│   │   ├── scene.js
│   │   ├── eventQueue.js
│   │   ├── random.js
│   │   └── clock.js
│   ├── content/
│   │   ├── characters/
│   │   ├── nodes.js
│   │   ├── props.js
│   │   ├── generalDialogue.js
│   │   └── tvChannels.js
│   ├── rendering/
│   │   ├── canvasRenderer.js
│   │   ├── spriteRenderer.js
│   │   ├── lightingRenderer.js
│   │   └── speechBubbleRenderer.js
│   ├── input/
│   │   └── pointerInput.js
│   └── main.js
├── assets/
│   ├── scene/
│   ├── sprites/
│   ├── costumes/
│   ├── props/
│   └── tv/
└── tests/
    ├── domain/
    ├── actions/
    ├── simulation/
    └── integration/
```

---

## 23. Development Principle

> **No abstraction until the need appears at least twice.**

Do not build:

- a general-purpose entity-component system
- a full behavior tree
- general pathfinding
- a large character inheritance model

---

## 24. Milestones

### Milestone 0 — Project Definition and Repository Setup

- Create GitHub repository
- Add this scope/design document
- Add README
- Add `.gitignore`
- Pick test/lint/format tooling
- Create labels and milestones
- Create initial issues
- Define v1 done

### Milestone 1 — Scene Reference and Final Layout

- Confirm final camera/perspective
- Confirm simplified scene crop
- Confirm L-bar geometry
- Confirm B1–B7 placement
- Confirm H1A–H1D and H2A–H2D placement
- Confirm north glass wall / interior entry
- Confirm east and south entries
- Confirm TV prominence
- Confirm reduced interior band
- Produce clean scene blockout

### Milestone 2 — Headless Domain Model

- Node model
- Character model
- Prop model
- TV model
- Scene state
- Character content files
- Node content data
- Prop definitions
- TV channel definitions
- Random abstraction
- Clock abstraction

### Milestone 3 — Core Simulation and Movement

- Tick/update loop
- Spawn/departure behavior
- Node occupancy
- Node movement
- Entry/exit handling
- Character action selection
- Weighted actions
- Action eligibility
- Click/action request model
- Event queue
- Text-mode scene snapshot
- Event logging

### Milestone 4 — Signature Behavior Tests

- John B3 arrival behavior
- B3 displacement
- John return-to-B3 behavior
- B7 xylophone behavior
- TV channel state
- Remote spawning
- Remote discovery
- Non-John TV channel change
- John TV reaction sequence
- John late-arrival TV correction
- Hotdog suit spawning
- Generic costume wearing
- Angie hotdog weighting
- Repeated-click reaction

### Milestone 5 — Basic Canvas Renderer

- Canvas setup
- Responsive scaling
- Logical scene coordinates
- Placeholder background
- Placeholder characters
- Node-to-screen coordinate mapping
- Character movement interpolation
- Basic depth ordering
- Speech bubbles
- Tap/click hit detection
- Reduced-motion behavior

### Milestone 6 — Faux-SNES Scene Art

- Final environment art direction
- Background layers
- L-bar artwork
- High tops
- North glass wall/interior treatment
- TV
- Selected props
- Final scene crop and scaling

### Milestone 7 — Character Sprite Production

Initial production-ready sprite work for:

- John B3
- Angie
- Mr. Angie
- Eli
- Black James
- Will
- Mafia
- D-Real

Then:

- Big Red
- Beth
- Generic patrons/staff

### Milestone 8 — Props, TV, and Costume Art

- Mini-xylophone
- TV remote
- Hotdog costume overlay
- TV channel loops
- Any required prop interaction frames

### Milestone 9 — Time-of-Day Lighting

- Day palette
- Dusk palette
- Night palette
- Late-night palette if useful
- Smooth blending
- Practical-light overlays
- Interior illumination shift

### Milestone 10 — Content Pass

- Character-specific phrase pools
- General phrase pool
- Node-specific actions
- Character action weights
- Generic indoor characters
- Spawn weighting
- Arrival/departure tuning
- Rare events
- Additional low-cost Easter eggs

### Milestone 11 — Mobile, Accessibility, and Performance

- iPhone/mobile testing
- Desktop testing
- Touch hit-target tuning
- Responsive scaling
- Reduced-motion support
- Performance profiling
- Basic accessibility review

### Milestone 12 — Offseason Release

- Final static build
- GitHub Pages deployment
- PBJ redirect/offseason routing plan
- README cleanup
- Release tag
- Maintenance notes

---

## 25. v1 Definition of Done

A successful v1 should have:

- Recognizable outside-bar scene
- 15 interactive nodes
- Working entrances/exits
- At least several named characters
- John B3 behavior
- B7 xylophone
- TV with multiple channels
- Remote event chain
- Hotdog costume
- Click/tap interaction
- Speech bubbles
- Basic indoor background activity
- Time-of-day lighting
- Static hosting
- Automated tests for major behavior rules

Everything else is optional expansion.

---

## 26. Future Ideas — Not Commitments

Ideas that may be revisited later:

- More costumes
- More props
- More TV channels
- Character-to-character conversations
- Rare seasonal events
- Holiday lighting
- Additional ambient sound
- More indoor-only named sprites
- Additional click reactions
- More node-specific gags

These should not be allowed to block v1.

---

## 27. Final Design Principles

1. **Keep it small enough to remain fun to maintain.**
2. **The scene is an animated diorama, not a full game.**
3. **Character files own personality; engine files own mechanics.**
4. **Simulation logic must not depend on rendering.**
5. **Randomness and time must be injectable and testable.**
6. **Use explicit nodes and routes instead of general pathfinding.**
7. **Prefer data-driven Easter eggs over new subsystems.**
8. **Do not generalize until the same need appears multiple times.**
9. **Art may cheat for recognizability while preserving a faux-SNES feel.**
10. **Prove the world in text before drawing it.**
11. **Ship the recognizable, funny core before adding more cleverness.**
