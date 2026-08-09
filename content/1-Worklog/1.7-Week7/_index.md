---
title: "Week 7 Worklog"
date: 2026-08-03
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Connect Amazon Bedrock AI Story generation service with Unity Story UI.
* Integrate complete End-to-End game loop: Story AI -> Player Choice -> Battle -> Level Up -> Item Drop -> Next Story.
* Perform comprehensive system testing, handling network latency, AI timeout edge cases, and UI bugs.
* Polish UI/UX with smooth screen transitions, damage numbers floating text, and audio effects.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Connect backend `/story/next` API powered by Amazon Bedrock (Claude LLM) <br> - Pass player story history and character state into Bedrock prompt | 08/03/2026 | 08/03/2026 | Bedrock Context Management |
| Tue | - Test dynamic branching in Unity UI (selecting choice 1 vs choice 2 vs choice 3) <br> - Trigger random encounter combat scenes based on AI story choices | 08/04/2026 | 08/04/2026 | Unity Event Flow |
| Wed | - Execute full End-to-End game loop test (Story node -> Choice -> Battle mode -> Victory/Defeat -> Reward drop -> Story continuation) | 08/05/2026 | 08/05/2026 | End-to-End Game Testing |
| Thu | - Handle API timeout & Bedrock fallback mechanisms when AI generation exceeds 5 seconds <br> - Add floating damage text & health bar fill animations in Unity UI | 08/06/2026 | 08/06/2026 | Unity UI Polish & DOTween |
| Fri | - Add button sound effects, background ambient music, and defeat screen UI <br> - Fix minor UI text wrapping & button positioning bugs across different resolutions | 08/07/2026 | 08/09/2026 | Game Polish Checklist |

### Week 7 Achievements:

* Successfully integrated Amazon Bedrock (Claude LLM) for context-aware interactive RPG storytelling.
* Verified seamless full gameplay loop from story decisions to combat and reward progression.
* Polished Unity Client UI with animations, sound effects, and robust error handling.
