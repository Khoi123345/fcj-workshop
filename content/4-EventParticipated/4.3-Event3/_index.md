---
title: "FCAJ - Agentic AI Build Week"
date: 2026-07-25
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Summary Report: "FCAJ - Agentic AI Build Week & Agent Forge"

### Event Objectives

- Understand the paradigm shift from basic LLM prompts to autonomous Agentic AI systems (`Reasoning → Planning → Execution`).
- Master the 5 production architecture layers of an AI Agent on AWS Cloud: Brain, System Prompt, Knowledge Context, Tools, and Memory/Observability.
- Explore modern AI protocols (Model Context Protocol - MCP, and Agent-to-Agent - A2A) for seamless tool and inter-agent communication.
- Deep dive into Amazon Bedrock Agent Core security features, including Firecracker MicroVM isolation, Workload Access Tokens (WAT), and Human-in-the-Loop (HITL) Gateways.
- Practice hands-on Vibe Coding using Kiro IDE with Steering Rules and deploy AI Agents via `agentcore CLI`.

### Speakers

- **Nghia Nguyen** – Principal Speaker (Covering Enterprise Agentic AI Architecture & L300 Theory)
- **Hai Anh** – Hands-on Speaker (Leading Live Vibe Coding with Kiro IDE & AgentCore CLI)
- **AWS Study Group** – Host & Community Organizer

---

### Key Highlights

#### 1. Agentic AI Philosophy & The Spectrum of Autonomy (Nghia Nguyen)
- **Beyond Standard LLMs:** Traditional LLMs act as token predictors. Agentic AI represents a new class of autonomous software that performs an iterative loop: **Reasoning → Planning → Execution**.
- **Spectrum of Autonomy:** Categorized into a 4-level spectrum:
  - *Simple Assistant:* Basic Q&A prompt interfaces.
  - *Deterministic Workflow:* Fixed developer-coded workflows with human oversight.
  - *Human-in-the-Loop Workflow:* Autonomous agent planning requiring mandatory human approval for critical actions.
  - *Fully Autonomous Multi-Agent Systems:* Specialized agents autonomously collaborating and handling long-running background tasks.

#### 2. Core 5-Layer AI Agent Production Architecture (Nghia Nguyen)
- **Decoupling Production Agents:** Building resilient production AI Agents requires decoupling five essential components:
  1. *Brain (LLM Reasoning):* Core cognitive models like Anthropic Claude 3.5 Sonnet, Claude 3 Haiku, or Amazon Nova.
  2. *System Prompt & Steering Rules:* Defining identity, role boundaries, and strict response formatting.
  3. *Knowledge Base / Context:* Connecting enterprise data via RAG and Vector Databases (e.g., OpenSearch Serverless).
  4. *Tools & Action Invocation:* Exposing external capabilities (executing SQL queries, calling REST Webhooks, Gmail API).
  5. *Memory & Observability:* Maintaining short-term/long-term session context and monitoring telemetry via Amazon CloudWatch.

#### 3. Next-Generation AI Protocols & Frameworks (Nghia Nguyen)
- **Model Context Protocol (MCP):** An open standard protocol replacing traditional REST APIs for agent-to-tool communication, making plugin integration seamless across different LLM models.
- **Agent-to-Agent (A2A) Protocol:** Standardizing inter-agent communication, allowing a Master Agent to delegate specialized sub-tasks to Worker Agents autonomously.
- **AWS Strands SDK & Factory Pattern:** Utilizing open-source Strands SDK alongside the Factory Design Pattern to instantiate agents cleanly (`Agent = Model + System Prompt + Tools`).

#### 4. Amazon Bedrock Agent Core Infrastructure & Security Topology (Nghia Nguyen)
- **Firecracker MicroVM Isolation:** Amazon Bedrock Agent Core executes each user session inside a dedicated Firecracker MicroVM, guaranteeing zero cross-tenant data leakage.
- **5-Step Security Flow with Workload Access Token (WAT):**
  1. *Inbound Request:* Client submits request with a JWT or AWS Cognito Credential.
  2. *Token Exchange:* Agent Core exchanges user JWT for a scoped Workload Access Token (WAT).
  3. *Outbound Delegation:* WAT is converted into tool-specific credentials (OAuth/API Key) stored in an encrypted Token Vault.
  4. *Execution:* Tools execute without ever exposing the user's primary credentials.
  5. *Safe Response:* Filtered response is returned securely to the client.
- **Enterprise Gateway & HITL:** Acts as a middleware proxy. For example, financial refund requests under \$100 are automatically executed by the Agent, whereas requests over \$100 trigger an administrative approval workflow before execution.

#### 5. Practical Vibe Coding Lab with Kiro IDE & agentcore CLI (Hai Anh)
- **Kiro IDE Steering Rules:** Configured `.kiro/steering.md` rules to instruct the AI assistant inside Kiro IDE to generate C# and Python code following AWS Strands SDK best practices.
- **3-Command Deployment Workflow:**
  1. `agentcore init my-first-agent` — Automatically scaffolds project structure (`agent.py`, `config.yaml`, `requirements.txt`).
  2. `agentcore configure --model anthropic.claude-3-5-sonnet` — Links LLM model and system persona.
  3. `agentcore deploy --env dev` — Packages and deploys the agent onto Amazon Bedrock Agent Core Firecracker MicroVMs in seconds.

---

### Key Takeaways

#### Design Mindset
- **Autonomous Agentic Loops:** Transition from static single-turn prompt interactions to autonomous Reasoning → Planning → Execution workflows.
- **Zero Tenant Data Leakage:** Leverage hardware-isolated Firecracker MicroVMs to run secure user agent sessions in multi-tenant environments.
- **Human-in-the-Loop Governance:** Enforce administrative approval gates at the Gateway layer for high-risk corporate actions.

#### Technical Architecture
- **Standardized Agent Protocols:** Adopt Model Context Protocol (MCP) and Agent-to-Agent (A2A) standards to streamline tool integration and multi-agent coordination.
- **Workload Access Token Security:** Protect user credentials by delegating external tool calls through scoped Workload Access Tokens (WAT).
- **Decoupled Agent Factories:** Use Factory Design Patterns to bundle Models, System Prompts, and Tools into modular agent instances.

#### Modernization & AI Integration
- **Vibe Coding Methodology:** Use IDE Steering Rules (`.kiro/steering.md`) to guide AI coding assistants in generating Cloud-native code.
- **Serverless CLI Deployment:** Streamline agent infrastructure management using rapid CLI toolchains (`agentcore CLI`).

---

### Applying to Work

- **Implement Bedrock Story Service:** Integrate Amazon Bedrock Runtime API into .NET 8 Lambda backend to generate dynamic adventure scenarios.
- **Enforce Output Steering Rules:** Apply system prompt constraints to force AI responses into structured JSON schemas for C# DTO parsing.
- **Build Async API Gateway Handlers:** Utilize async/await patterns in Unity `ApiClient` to handle AI response streaming without blocking UI frame rates.
- **Handle Timeout Fallbacks:** Implement fallback story nodes and 5-second timeout buffers to handle AI service latency gracefully.
- **Adopt Modular Code Generation:** Use IDE Steering Rules to standardize code formatting and architectural patterns across the Monorepo C# codebase.

---

### Event Experience

Attending the **FCAJ - Agentic AI Build Week & Agent Forge** was an extraordinary learning experience that provided deep technical insights into production-grade AI Agent development on AWS Cloud.

- **High-Quality L300 Technical Depth:** Nghia Nguyen's breakdown of Bedrock Agent Core, Firecracker MicroVMs, and WAT security solved critical doubts regarding enterprise AI safety.
- **Hands-on Vibe Coding Practice:** Hai Anh's live demonstration of Kiro IDE and `agentcore CLI` showcased how fast developers can build and deploy Serverless AI Agents.
- **Direct Relevance to Project:** Understanding AI story prompt formatting and Bedrock API integration directly shaped the architecture of my **AI Dungeon RPG** project.
- **Inspiring Developer Community:** Engaging with Cloud Architects, AI Engineers, and fellow bootcamp students reinforced my passion for Cloud-native AI innovation.

#### Some event photos

![FCAJ Agentic AI Build Week](hinh-anh-sk-3/event3.png)


> The FCAJ Agentic AI Build Week event was a landmark learning milestone during my internship, equipping me with the production-ready mindset and technical tools to build robust, secure, and scalable AI Agent applications on AWS Cloud.
