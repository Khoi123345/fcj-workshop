---
title: "Week 2 Worklog"
date: 2026-06-29
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

* Learn advanced C# data structuring and class library separation in Monorepo.
* Design and implement shared DTOs (Data Transfer Objects) and Domain Models in `GameShared`.
* Define game data contracts for Character, Battle, Inventory, and AI Story responses.
* Test library compilation across .NET 8 runtime and Unity Engine C# runtime environment.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Research C# class library target frameworks (.NET Standard 2.1 vs .NET 8) <br> - Configure `GameShared.csproj` settings for cross-platform compatibility | 06/29/2026 | 06/29/2026 | Microsoft .NET Standard Docs |
| Tue | - Design Character & Player State DTOs: `PlayerStats`, `CharacterProfile`, `LevelProgress` <br> - Implement C# data contracts with JSON serialization attributes | 06/30/2026 | 06/30/2026 | System.Text.Json Docs |
| Wed | - Design Battle System DTOs: `BattleRequest`, `BattleResult`, `TurnAction`, `BossStats` <br> - Add enum definitions for Damage Types & Combat Actions | 07/01/2026 | 07/01/2026 | Game Architecture Patterns |
| Thu | - Design Inventory DTOs: `ItemModel`, `EquipRequest`, `InventoryState` <br> - Design AI Story DTOs: `StoryPromptRequest`, `StoryNodeResponse`, `ChoiceOption` | 07/02/2026 | 07/02/2026 | Clean Code C# |
| Fri | - Build `GameShared.dll` and test importing into Unity project <br> - Verify JSON serialization & deserialization compatibility | 07/03/2026 | 07/03/2026 | Unity C# Scripting |

### Week 2 Achievements:

* Built a clean `GameShared` library providing strong typing and unified data contracts.
* Avoided code duplication between backend and frontend by sharing DTO classes.
* Successfully tested `GameShared.dll` compatibility in Unity C# and .NET 8 Lambda environment.
