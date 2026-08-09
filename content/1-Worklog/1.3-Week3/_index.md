---
title: "Week 3 Worklog"
date: 2026-07-06
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

* Learn Unity UI Presenter architectural pattern (MVP / Presenter separation).
* Study asynchronous API communication using `UnityWebRequest` and `Task`/`UniTask` in C#.
* Build HTTP client helper class (`ApiClient`) to call REST API endpoints from Unity.
* Implement error handling, loading spinners, and alert modal UI components in Unity.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Learn Unity UI Canvas layout, Anchors, Layout Groups & UI Event Listeners <br> - Study MVP (Model-View-Presenter) design pattern for Unity | 07/06/2026 | 07/06/2026 | Unity UI Documentation |
| Tue | - Research `UnityWebRequest` for sending HTTP POST/GET requests <br> - Learn async/await programming model in Unity C# | 07/07/2026 | 07/07/2026 | UnityWebRequest Manual |
| Wed | - Write reusable `ApiClient.cs` utility class <br> - Implement JSON payload serialization using `GameShared` DTOs | 07/08/2026 | 07/08/2026 | Async C# in Unity |
| Thu | - Build UI Loading Spinner component to block UI during API waiting <br> - Create Error Popup Modal component for network timeout notifications | 07/09/2026 | 07/09/2026 | Unity UX Design |
| Fri | - Test mock API calls using `ApiClient` to test HTTP request/response flow <br> - Refactor UI Presenter code to keep View components clean of networking logic | 07/10/2026 | 07/10/2026 | Refactoring UI Code |

### Week 3 Achievements:

* Mastered Unity UI layout design and the UI Presenter architectural pattern.
* Successfully built an asynchronous `ApiClient` capable of communicating with HTTP REST APIs.
* Implemented proper user feedback mechanisms (loading overlay & error modals) for smooth UX.
