---
title: "Week 6 Worklog"
date: 2026-07-27
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Implement core serverless game logic on .NET 8 AWS Lambda to prevent client-side cheating.
* Develop Turn-based Battle calculation engine (Damage, Critical hit, Defense reduction, Dodge).
* Develop Character Level Up system, Stat growth formulas, and Player Death System reset rules.
* Develop Inventory backend logic (Item equipping, Potion usage, Stat modifier recalculation).

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Implement `BattleService.cs` in .NET 8 backend <br> - Write turn-based combat algorithms (Physical damage, Elemental damage, Crit multiplier) | 07/27/2026 | 07/27/2026 | Game Combat Math |
| Tue | - Implement Boss AI turn logic and Skill execution engine <br> - Return structured `BattleResult` DTO after each round | 07/28/2026 | 07/28/2026 | Boss Turn State Machine |
| Wed | - Implement `LevelUpService.cs` (Experience gain calculation & Stat point allocation) <br> - Implement `DeathSystem.cs` (Revive rules & death penalty logic) | 07/29/2026 | 07/29/2026 | RPG Progression Systems |
| Thu | - Implement `InventoryService.cs` (Equip/Unequip items, recalculate character stats) <br> - Write Potion use handler (restore HP/MP instantly on server) | 07/30/2026 | 07/30/2026 | Inventory Management Patterns |
| Fri | - Write Lambda Handlers for `/battle/action`, `/character/levelup`, and `/inventory/equip` <br> - Run unit tests for battle calculation edge cases (overkill damage, 0 HP death) | 07/31/2026 | 08/02/2026 | xUnit for .NET 8 |

### Week 6 Achievements:

* Built robust serverless game logic in .NET 8 AWS Lambda functions.
* Ensured zero cheat vulnerability by calculating all battle actions and stat growths on the backend.
* Completed Battle, Level Up, Death System, and Inventory backend handlers.
