# CM12003 Haskell Coursework

## Overview

This repository contains my coursework submission for Programming 1 (CM12003). The implementation consists of a small interactive text adventure game written in Haskell, contained in `Coursework.hs`.

The project demonstrates:
- a functional game world representation
- dynamic dialogue trees and event handling
- an interactive command loop with input validation
- a solver for exploring game actions and finding a path to the end state
- a compact and readable Haskell style consistent with the course style guide

Additional supporting materials include:
- `Coursework.pdf` — assignment description
- `Style_guide.pdf` — course-specific style guidance
- `Style Guide Analysis.md` — notes on presentation, naming, commenting, and technique

## Files

- `Coursework.hs` — main source code and complete implementation
- `Coursework.pdf` — coursework supporting document
- `Style Guide Analysis.md` — self-review notes on code style and structure (derived from `Style_guide.pdf`)
- `Style_guide.pdf` — reference style guide for the course

## Implementation Summary

### Core types

- `Character` and `Party` model characters and party membership.
- `Node`, `Location`, and `Map` model a graph of rooms or locations.
- `Game` represents either an `Over` state or a running game with:
  - `Map` of connected nodes
  - current `Node`
  - current party at the player's location
  - a list of parties at all locations
- `Event` is a pure function from `Game -> Game`.

### Game world operations

The first assignment implements the world model and party management:
- `connected` discovers neighbours in the map
- `connect` and `disconnect` manage edges between nodes
- `add`, `addAt`, `addHere`, `remove`, `removeAt`, `removeHere` manipulate party membership and location-specific parties

### Dialogue system

The second assignment defines a dialogue structure and interpreter:
- `Dialogue` supports `Action`, `Branch`, and `Choice`
- `dialogue` executes nodes, prints text, and applies game events
- `findDialogue` selects dialogue based on the current party
- `testDialogue` and `theDialogues` model sample quests, NPC conversations, and choice trees

### Game loop

The third assignment implements the interactive loop:
- `step` prints the current location, travel options, party members, visible characters, and prompt text
- input handling supports:
  - `0` to end the game
  - a single travel choice to move
  - indexes to select one or more characters and trigger dialogue
- invalid input is handled safely with a retry loop and a warning message

### Puzzle solver

The fifth assignment adds a solver to automatically explore possible actions:
- `Command` defines `Travel`, `Select`, and `Talk`
- `talk` traverses dialogue branches and records choices
- `select` builds all non-empty visible-party combinations
- `travel` performs BFS over the map to locate reachable nodes and paths
- `allSteps`, `solve`, and `walkthrough` perform search for a sequence of moves to reach `Over`

## How to run

This is a single-file Haskell program. Use one of the following methods:

### Using `ghc`

```sh
ghc -o Coursework Coursework.hs
./Coursework
```

### Using `ghci`

```sh
ghci Coursework.hs
```

### Using `runhaskell`

```sh
runhaskell Coursework.hs
```

### Using `stack`

If you have `stack` installed:

```sh
stack runghc Coursework.hs
```

## How to interact with the game

1. The game prints the current location description.
2. It lists travel destinations and visible characters.
3. It prompts the user with `>>`.
4. Input options:
   - `0` ends the game immediately
   - a single number selects one of the listed locations to travel there
   - one or more index numbers selects characters for dialogue

Dialogue options may also present numbered choices. More detailed instructions can be found in `Coursework.pdf`.

## Notes and design decisions

- The game state is intentionally immutable; all actions return a new `Game` state.
- The dialogue system uses pure data and a small interpreter, which keeps story logic separate from input/output.
- The solver is implemented with breadth-first search and avoids revisiting repeated `Game` states.
- `Game` stores party lists and location parties in a simple `List` structure, which is easy to reason about for coursework purposes.
- The implementation uses `sort`, `nub`, and list comprehensions to preserve deterministic ordering and simplify comparisons.
- Input parsing uses `readMaybe` to safely interpret user input and reject invalid commands.

## Coursework features by assignment

- Assignment 1: world map, travel graph, party management, and event application
- Assignment 2: branching dialogue system, choices, and event-triggered story progression
- Assignment 3: interactive game loop with detailed scene output and command parsing
- Assignment 4: safety upgrades for invalid input handling and clear error messaging
- Assignment 5: automated solver and walkthrough generator to explore game completion paths

## Known limitations

- The game uses zero-based internal node indices, while user-facing travel options are numbered from 1.
- Dialogue selection currently assumes exact party membership matching for `theDialogues` lookup.
- The solver is breadth-first but does not explicitly limit the search depth; this is acceptable for the small map in this coursework.
- The game relies on static lists for descriptions, locations, and characters, so new content must be added manually.

## License and attribution

This repository is coursework submitted for CM12003. The implementation is original to this assignment and is intended for academic evaluation.
