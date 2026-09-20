# PBJ Offseason

PBJ Offseason is the offseason companion to the PBJ Football Pool dashboard.

The goal is to create a small, interactive faux-SNES bar scene where familiar characters come and go, occupy known spots, react to props and Easter eggs, and occasionally speak.

This is intentionally **not a full game**. It is an animated diorama with lightweight NPC behavior.

## Status

Planning and project setup.

Implementation has not started yet.

## Technical Direction

The current plan is:

- Vanilla JavaScript
- HTML Canvas
- Static assets
- Static hosting
- No backend
- No game engine unless a clear need emerges later

The simulation logic will be designed and tested before graphics are added.

## Design Document

Project scope, architecture, scene rules, milestones, and design decisions are documented in:

[`PBJ_OFFSEASON_SCOPE_AND_DESIGN.md`](PBJ_OFFSEASON_SCOPE_AND_DESIGN.md)

## Core Design Principles

- Keep the project small enough to remain fun to maintain
- Treat it as an animated diorama, not a full game
- Keep simulation logic independent from rendering
- Keep character-specific behavior with the character data
- Use explicit nodes and routes instead of general pathfinding
- Prefer simple, data-driven Easter eggs over new subsystems
- Prove behavior in tests before building the visual layer