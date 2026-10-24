# ColdLine.C — Game Design Document

**Version:** 1.0
**Date:** 2026-10-24
**Genre:** Top-down action
**Platform:** Web browser (desktop)
**Technologies:** TypeScript, HTML5 Canvas, CSS
**Main reference:** Hotline Miami

---

## Table of contents

1. [Technical sheet](#1-technical-sheet)
2. [Overview and pillars](#2-overview-and-pillars)
3. [Story and setting](#3-story-and-setting)
4. [Main character](#4-main-character)
5. [Gameplay loop](#5-gameplay-loop)
6. [Detailed mechanics](#6-detailed-mechanics)
7. [Enemy AI](#7-enemy-ai)
8. [Controls](#8-controls)
9. [Prototype level](#9-prototype-level)
10. [Art direction](#10-art-direction)
11. [Audio](#11-audio)
12. [Technical architecture](#12-technical-architecture)
13. [Scope, risks and next steps](#13-scope-risks-and-next-steps)

---

## 1. Technical sheet

| Item | Description |
| --- | --- |
| Title | ColdLine.C |
| Genre | Top-down action |
| Perspective | Top-down |
| Platform | Desktop web browser |
| Technologies | TypeScript + HTML5 Canvas + CSS |
| Inspiration | Hotline Miami |
| Target audience | Fast-action players and pixel art fans |
| Age rating | 16+ (stylized violence) |
| Mode | Single player |
| Scope of this version | One-level prototype |

---

## 2. Overview and pillars

**ColdLine.C** is a top-down action game in which the player controls a police officer determined to clean up the streets of his city by arresting and neutralizing criminals. Combat is fast, enemies are dangerous, and the player also goes down in a few hits, which rewards planning and precise execution.

### Design pillars

1. **Fast and lethal combat** — the player is strong but vulnerable. Every mistake is costly.
2. **Plan before acting** — observe the room, choose the route and the right weapon.
3. **Pixel art with a neon mood** — visuals inspired by Hotline Miami and synthwave.
4. **Mastery-based progression** — short, replayable levels; the player improves with practice.

---

## 3. Story and setting

The protagonist is a veteran police officer from ColdLine, a fictional city taken over by criminal factions. After years of watching criminals go unpunished, he decides to act outside the system: break into hideouts, stun suspects and dismantle the operations one by one.

- **Tone:** dark, tense and stylized; violence presented in an arcade way.
- **Setting:** alleys, warehouses, bars and abandoned buildings lit by neon.
- **Narrative:** delivered through short texts between levels (no cutscenes in the prototype).

---

## 4. Main character

| Attribute | Value |
| --- | --- |
| Name | The Officer (ColdLine) |
| Motivation | Clean the city of crime |
| Health | Low (2 to 3 hits) |
| Speed | Medium; sprinting raises noise |
| Starting weapons | Punch, baton, chokehold |
| Acquired weapons | Weapons dropped by enemies |
| Limitation | No healing; no armor |

---

## 5. Gameplay loop

```
[Level start]
       |
       v
[Observe and plan the route]
       |
       v
[Enter the area and stun the first enemy]
       |
       v
[Pick up the dropped weapon / swap weapons]
       |
       v
[Eliminate or arrest the remaining enemies]
       |
       v
[Complete the level objective]
       |
       v
[Score + next level]
```

---

## 6. Detailed mechanics

### 6.1 Movement and collision

- 8-direction movement (WASD or arrow keys).
- Collision with walls, furniture and enemies.
- Sprint (Shift) increases speed and the enemies' detection radius.

### 6.2 Melee attacks

| Attack | Range | Effect | Notes |
| --- | --- | --- | --- |
| Punch | Short | Stuns | Fast, no cost |
| Baton | Medium | Stuns or neutralizes | Officer's starting weapon |
| Chokehold | Very short | Silently neutralizes | Requires being behind the enemy |
| Firearm (enemy) | Long | High damage | Limited ammo |

### 6.3 Stunning versus neutralizing

- **Stunned:** the enemy falls and can be handcuffed (the "arrest" objective) or finished off.
- **Neutralized:** the enemy is permanently out of combat.
- The player chooses between arresting (more points) and neutralizing (faster).

### 6.4 Weapons on the ground

- Downed enemies drop their weapon on the ground.
- The player picks it up with **E**, replacing the current weapon.
- Firearms have ammo and can be discarded when empty.
- Melee weapons have no ammo.

### 6.5 Win and loss conditions

- **Win:** complete the level objective (e.g., neutralize/arrest all targets).
- **Loss:** the player's health reaches zero.
- **Restart:** instant level restart with **R**.

---

## 7. Enemy AI

| State | Behavior |
| --- | --- |
| Patrol | Walks along predefined waypoints |
| Suspicious | Investigates noise or a partial sighting of the player |
| Alert | Chases the player and calls for backup |
| Attack | Melee attacks or shoots from a distance |
| Stunned | Immobile and vulnerable |
| Out of combat | Neutralized or arrested |

Initial rules:
- Detection by vision cone and by noise (sprinting, gunshots, doors).
- Enemies cannot see through walls.
- Configurable reaction time to balance difficulty.

---

## 8. Controls

| Action | Key |
| --- | --- |
| Move | W A S D |
| Sprint | Shift |
| Aim | Mouse |
| Attack | Left mouse button |
| Interact / pick up weapon | E |
| Restart level | R |
| Pause | Esc |

---

## 9. Prototype level

**Name:** Docks Warehouse
**Objective:** neutralize or arrest 5 criminals and leave through the east door.

```
+-----------------------------------+
|  ENTRANCE       CRATES      EXIT  |
|  [P]   . . . .  [XX]  . .  [E]    |
|  . . . . . . .  [XX]  . .  .      |
|  [1]  . . [2] . . . . [3]  .      |
|  . . . . . . . . . . . .  .       |
|  [4]  . . . . [5] . . . . .       |
|  . . . . . . . . . . . .  .       |
+-----------------------------------+
P = player | 1..5 = enemies | XX = crates | E = exit
```

- **Enemies:** 5, with varied weapons (2 melee, 2 with pistols, 1 with a baton).
- **Weapons in the level:** 1 spare baton and 1 pistol with limited ammo.
- **Estimated duration:** 2 to 4 minutes per attempt.
- **Future vision:** new levels (alley, bar, building) with their own layouts and objectives.

---

## 10. Art direction

- **Style:** top-down pixel art inspired by Hotline Miami.
- **Base resolution:** 320 x 180, scaled by integer multiples to keep pixels sharp.
- **Tiles:** 16 x 16 pixels.
- **Palette:** dark blues and purples with neon highlights (pink, cyan, yellow).
- **Animations:** 4 directions, 4 to 6 frames per action (walk, attack, stunned).
- **Interface:** minimalist HUD with health, current weapon and objective.

---

## 11. Audio

- **Soundtrack:** synthwave/arcade loops per level.
- **Effects:** punch, baton, gunshot, footsteps, alarm, level complete.
- **Prototype:** free or placeholder sounds and music with a compatible license.
- **Rule:** separate volume for music and effects.

---

## 12. Technical architecture

### 12.1 Stack

- **TypeScript** for logic and typing.
- **HTML5 Canvas** for 2D rendering.
- **CSS** for page layout and HUD.
- **Vite** as the development server and build tool.

### 12.2 Proposed folder structure

```
coldline.c/
|-- index.html
|-- package.json
|-- tsconfig.json
|-- src/
|   |-- main.ts
|   |-- engine/
|   |   |-- loop.ts
|   |   |-- input.ts
|   |   |-- renderer.ts
|   |   `-- collision.ts
|   |-- entities/
|   |   |-- player.ts
|   |   |-- enemy.ts
|   |   `-- weapon.ts
|   |-- systems/
|   |   |-- combat.ts
|   |   |-- ai.ts
|   |   `-- level.ts
|   `-- levels/
|       `-- warehouse.ts
`-- assets/
    |-- sprites/
    |-- tiles/
    `-- audio/
```

### 12.3 Game loop

1. Read keyboard and mouse input.
2. Update entities based on delta time.
3. Resolve collisions.
4. Update AI and combat state.
5. Render the level, entities and HUD to the Canvas.
6. Repeat via `requestAnimationFrame`.

---

## 13. Scope, risks and next steps

### Prototype scope

- One playable level: Docks Warehouse.
- Movement, three melee attacks and weapon pickup.
- Basic AI with patrol, alert and attack.
- HUD with health, weapon and objective.
- Provisional pixel art and placeholder audio.

### Out of scope (future vision)

- Multiple levels and progression.
- Narrative between levels.
- Score ranking.
- Level editor.
- Gamepad and mobile support.

### Risks

| Risk | Impact | Mitigation |
| --- | --- | --- |
| Pixel art takes too long | High | Use provisional assets and refine later |
| AI becomes too complex | Medium | Start with 2 states and evolve |
| Development time | Medium | Deliver the one-level prototype first |
| Difficulty balancing | Medium | Tune timings and damage through testing |

### Next steps

1. Set up the project with TypeScript, Vite and Canvas.
2. Implement player movement and collision.
3. Implement attacks and weapon pickup.
4. Implement AI and win/loss conditions.
5. Build the Docks Warehouse level.
6. Apply art and audio.
7. Test, balance and publish to the browser.
