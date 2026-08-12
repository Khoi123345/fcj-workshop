---
title: "Proposal"
date: 2026-06-22
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Project Proposal: AI Dungeon RPG Adventure Game

## 1. Executive Summary

The **AI Dungeon RPG Adventure Game** is a modern Role-Playing Game (RPG). This project combines Generative Artificial Intelligence (AI) with a scalable and cost-effective AWS Serverless system.

Players can create characters and start their own open adventures. Stories, quests, and turn-based Boss battles are not fixed. Instead, the game creates them in real time based on player choices using **AWS Bedrock** with the **Amazon Nova Pro (`amazon.nova-pro-v1:0`)** model. Players play the game on a **Unity 2D Client** that connects to a **.NET 8 Backend** on AWS.

## 2. Problem Statement

### Problems with Traditional RPG Games
*   **Fixed Storylines:** Traditional RPG games use fixed scripts. Players quickly finish all content, making the game boring to replay.
*   **High Server Costs:** Running traditional game servers costs a lot of money for unused hardware. It is also hard to handle when many new players join at once.

### Our Solution
*   **Real-Time AI Stories:** By using Large Language Models (LLMs) on **AWS Bedrock (`amazon.nova-pro-v1:0`)**, the game creates new stories, worlds, and results instantly when players make choices.
*   **Flexible Serverless System:** Core game features (login, inventory, battle logic) run on **AWS Lambda**, and data is saved in **Amazon DynamoDB**. This helps the game automatically handle many players while keeping costs very low.

## 3. Solution Architecture

The project uses a 100% Serverless system on AWS (Singapore Region: ap-southeast-1). It separates the Game Client and Cloud Backend to keep the game fast and secure.

![AWS Architecture Diagram](images/aws-architect-project.jpg)
*(System Architecture Overview)*

*   **Amazon API Gateway & Cognito:** Receives requests safely, manages user login/register, and checks JWT Tokens with Cognito Authorizer.
*   **Object Storage + CDN (Amazon CloudFront & Amazon S3):**
    *   **Amazon CloudFront (CDN + OAC):** Delivers game files quickly to the Unity 2D Client.
    *   **Amazon S3 (Game Assets & Templates):** Stores game files and story prompt templates safely.
*   **Compute Tier (AWS Lambda - .NET 8):** Uses **13 Lambda functions** split into 5 main groups:
    *   `AuthFunction` (4 functions): Handles Login, Register, Refresh Token, and User check.
    *   `CharacterHandler` (2 functions): Manages Player Profile and Stats.
    *   `InventoryManager` (3 functions): Manages Items and Equipment.
    *   `BattleSystem` (2 functions): Handles turn-based battle logic.
    *   `StoryGenerator` (2 functions): Connects to AI Bedrock using `StoryActionFunction` to create stories.
*   **Database Tier (Amazon DynamoDB):** A fast NoSQL database with **10 main tables**:
    *   `Users`, `Characters`, `Inventory`, `StorySessions`, `Battles`, `Bosses`, `BossEncounter`, `LootDrops`, `StoryActions`, and `DefeatBosses`.
*   **Generative AI (AWS Bedrock):** The AI brain of the game. It calls **Amazon Nova Pro (`amazon.nova-pro-v1:0`)** to generate new stories and choices.
*   **Monitoring & Logging (Amazon CloudWatch):** Automatically records system logs and performance data for Lambda and Bedrock.

### How a Game Request Works (Example: Story Action Request)
1. **Send Request:** Unity 2D Client sends a POST request to `/story/action` with a JWT Token.
2. **Check Token:** API Gateway checks the JWT Token with Cognito Authorizer.
3. **Run Lambda:** API Gateway calls `StoryActionFunction` (AWS Lambda).
4. **Get Template:** `StoryActionFunction` gets story prompt templates from Amazon S3 via CloudFront CDN.
5. **Call AI:** `StoryActionFunction` calls Bedrock **Amazon Nova Pro (`amazon.nova-pro-v1:0`)** to create stories and choices.
6. **Save Data:** `StoryActionFunction` saves the new story and choices into DynamoDB (`StoryActions`, `StorySessions`).
7. **Record Logs:** CloudWatch automatically records execution logs and system metrics.

## 4. Technical Implementation

The project uses a **Monorepo** structure. This allows sharing C# models and data objects (DTOs) between Unity Client and Lambda Backend easily.
*   **Frontend (Game Client):** Built with Unity (C#) and 2D URP. It connects to the backend using HTTPS REST API and downloads assets via CloudFront.
*   **Backend & Infrastructure as Code (IaC):** The AWS infrastructure is written in **AWS CDK (C#)**. Developers run `cdk deploy` to update AWS resources automatically using **AWS CloudFormation**.
*   **Security:** Uses a Server-Authoritative design. Important calculations (health points, damage, loot drops) are done inside AWS Lambda to prevent player cheating.

## 5. Timeline & Milestones

*   **Milestone 1 (22/06/2026 - 05/07/2026):** Finish core system design, setup AWS CDK, deploy Amazon Cognito (Auth), S3/CloudFront CDN, and 10 DynamoDB tables.
*   **Milestone 2 (06/07/2026 - 19/07/2026):** Connect AWS Bedrock (`amazon.nova-pro-v1:0`), build prompt generators with S3 templates, and write a JSON parser for AI data.
*   **Milestone 3 (20/07/2026 - 02/08/2026):** Build backend logic for turn-based battles, Boss fights, loot drops, and inventory management.
*   **Milestone 4 (03/08/2026 - 15/08/2026):** Connect Unity Client to Backend API, run full End-to-End (E2E) testing, and reduce AI waiting time.

## 6. Budget Estimation

Using Serverless helps keep costs very low during testing:
*   **AWS Cognito / Lambda / DynamoDB / S3 & CloudFront:** $0.00 (Free under AWS Free Tier limits).
*   **AWS Bedrock (`amazon.nova-pro-v1:0`):** Pay per token (About $1.00 - $5.00/month for testing).
*   **Amazon API Gateway & CloudWatch:** About $0.50 - $1.00/month.
*   **Estimated Total Cost:** **~$1.50 - $6.00 / month**. This is very cheap for a scalable game backend.

## 7. Risk Assessment

| Risk | Impact | How to Fix |
| :--- | :--- | :--- |
| **AI Response Time (Latency)** | High | Show loading animations on Unity Client while waiting for AI responses. |
| **Wrong AI JSON Format** | Medium | Backend uses validator tools and auto retry if AI returns bad JSON format. |
| **High AI Token Cost** | Low | Set strict `max_tokens` limits and use AWS Budget alerts. |

## 8. Expected Outcomes

*   **Great Player Experience:** Players get a unique story every time they play.
*   **Standard Architecture Framework:** A clean, reusable template combining Unity 2D and AWS .NET 8 Serverless for future game projects.
*   **Low Cost & Easy Operation:** Proves that we can build and run a smart online game with almost zero server cost at the start.