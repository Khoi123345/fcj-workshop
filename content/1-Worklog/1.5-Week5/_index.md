---
title: "Week 5 Worklog"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

* Build complete game UI Presenters for Unity Client in the AI Dungeon RPG game.
* Implement MainMenu, CharacterScreen, StoryView, BattleView, and InventoryView UI scenes.
* Connect Unity UI Views with `ApiClient` to fetch player data and post actions to backend.
* Handle dynamic UI state binding for Health bar, Mana bar, Experience progress, and Choice buttons.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Design & implement `MainMenuPresenter` & `CharacterCreatePresenter` <br> - Connect character creation UI to backend API to retrieve player stats | 07/20/2026 | 07/20/2026 | Unity UI Canvas Layout |
| Tue | - Design & implement `StoryViewPresenter` <br> - Bind dynamic AI story text and generate 3 choice buttons dynamically from API response | 07/21/2026 | 07/21/2026 | Unity Dynamic UI Instantiation |
| Wed | - Design & implement `BattleViewPresenter` <br> - Build HP/MP bars, turn action buttons (Attack, Skill, Defend, Flee), and boss avatar rendering | 07/22/2026 | 07/22/2026 | Unity UI Animation & Health Bars |
| Thu | - Design & implement `InventoryViewPresenter` <br> - Build item grid slots, equipment info tooltip modal, and item usage buttons | 07/23/2026 | 07/23/2026 | Unity Grid Layout Group |
| Fri | - Connect all UI Presenters with `ApiClient` <br> - Test full UI navigation flow from Main Menu -> Story -> Choice -> Battle -> Inventory | 07/24/2026 | 07/24/2026 | Unity Scene Management |

### Week 5 Achievements:

* Completed full set of Unity UI Presenters for the AI Dungeon RPG game.
* Bound player stats dynamically to HP/MP bars and inventory item grids.
* Successfully connected all Unity UI screens to backend API endpoints via `ApiClient`.
