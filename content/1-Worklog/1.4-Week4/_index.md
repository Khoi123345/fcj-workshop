---
title: "Week 4 Worklog"
date: 2026-07-13
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

* Learn Serverless backend programming with .NET 8 on AWS Lambda.
* Study Amazon Bedrock Runtime API and Claude LLM prompt engineering.
* Write a prototype .NET 8 Lambda function that invokes Amazon Bedrock API.
* Test generating dynamic story text and branching choices for RPG adventures.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Study AWS Lambda architecture for C# .NET 8 runtime <br> - Learn `Amazon.Lambda.Core` & `Amazon.Lambda.APIGatewayEvents` packages | 07/13/2026 | 07/13/2026 | AWS Lambda C# Docs |
| Tue | - Research Amazon Bedrock Service and Claude LLM foundation models <br> - Learn IAM permissions required for `bedrock:InvokeModel` | 07/14/2026 | 07/14/2026 | Amazon Bedrock Developer Guide |
| Wed | - Install `AWSSDK.BedrockRuntime` NuGet package in .NET 8 backend <br> - Design prompt templates for generating RPG dungeon scenarios and 3 player choices | 07/15/2026 | 07/15/2026 | AWS SDK for .NET Docs |
| Thu | - Implement AI Story Generator service calling Bedrock Runtime API <br> - Write JSON parser to map AI output into `StoryNodeResponse` DTO | 07/16/2026 | 07/16/2026 | Prompt Engineering Best Practices |
| Fri | - Test local execution of .NET 8 Lambda handler invoking Bedrock <br> - Verify generated story nodes and choices formatting consistency | 07/17/2026 | 07/17/2026 | AWS Mock Testing |

### Week 4 Achievements:

* Understood .NET 8 Serverless architecture on AWS Lambda.
* Successfully integrated Amazon Bedrock Runtime API into C# backend.
* Created working AI story prompt templates generating structured RPG adventure choices.
