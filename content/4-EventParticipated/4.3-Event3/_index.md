---
title: "AWS FCAJ Agent Forge - Deepdive"
date: 2026-08-01
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Summary Report: "AWS FCAJ Agent Forge - Deepdive"

### Event Objectives

- Provide advanced **L300 (Advanced Level)** technical training designed to guide AI Engineers, Cloud Architects, and Developers in transitioning Generative AI applications from Proof of Concept (PoC) to Production-ready enterprise environments.
- Address the 4 major pillars of enterprise AI implementation: **Performance**, **Scalability**, **Security**, and **Governance**.
- Deep dive into Agentic AI architecture, the Amazon Bedrock Agent Core ecosystem (Runtime, Identity, Gateway), and modern inter-agent communication protocols (MCP, A2A).
- Deliver hands-on experience with **Vibe Coding** using **Kiro IDE**, configuring Steering Rules, and deploying a serverless AI Agent on AWS using just 3 `agentcore CLI` commands.

### Speakers

- **Anh Nghia** – Speaker (Theory & Architecture)
- **Hai Anh** – Speaker (Hands-on Lab)
- **AWS Study Group** – Host Organization

---

### Key Highlights

#### 1. Agentic AI Philosophy & Spectrum of Autonomy
- **Agentic AI Definition:** Unlike basic LLMs that merely predict the next token, Agentic AI represents autonomous software capable of executing an iterative workflow: **Reasoning → Planning → Executing** complex, multi-step tasks.
- **Spectrum of Autonomy:**
  - *Simple Assistant:* Basic Q&A models driven directly by LLM prompts.
  - *Deterministic Workflow:* Developer-defined fixed workflows with continuous Human-in-the-loop control.
  - *Fully Autonomous Multi-Agent Systems:* Interconnected agents that autonomously delegate sub-tasks, run long-running background jobs, and synthesize results for end users.

#### 2. Basic Agent Architecture
- **5 Core Building Blocks of a Production Agent:**
  - **Brain:** Foundation Large Language Models (LLMs) handling reasoning. Examples include Anthropic Claude (Haiku for speed/cost, Sonnet for complex tasks, Opus for advanced technical/coding tasks), Amazon Nova, or Google Gemini.
  - **System Prompt & Role:** Defines identity, objective parameters, and operational guardrails.
  - **Knowledge Base / Context:** Enterprise internal data connected via RAG, Vector Databases, or File Systems.
  - **Tools / Actions:** External interaction capabilities (sending emails via Gmail API, querying databases, triggering webhooks).
  - **Memory & Observability:** Session memory management (Short-term/Long-term Memory) and operational logging via Amazon CloudWatch.

#### 3. Modern Protocols & Development Frameworks
- **Protocol Paradigm Shift:**
  - Transitioning from legacy HTTP REST APIs to dedicated AI agent protocols:
    - **MCP (Model Context Protocol):** Standardized protocol enabling agents to communicate with external tools and plugins seamlessly.
    - **A2A (Agent-to-Agent Protocol):** Protocol allowing autonomous agents to communicate and delegate sub-tasks directly to each other.
- **AWS Strands SDK Framework:** An open-source SDK developed by AWS tailored for building AI agents on AWS Cloud, offering superior optimization over LangChain or LangGraph within AWS ecosystems.
- **Design Pattern:** Utilizing the **Factory Design Pattern** to instantiate agents using a clean 3-part blueprint: `Model + System Prompt + Tools`.

#### 4. Amazon Bedrock Agent Core - Runtime Environment
- **Serverless Managed Runtime:** Managed serverless infrastructure enabling secure, scalable agent execution on a Pay-as-you-go model.
- **Firecracker MicroVM Isolation Technology:**
  - Each agent user session runs inside a completely isolated MicroVM.
  - Dedicated hardware compute, memory, and file system boundaries guarantee absolute zero data leakage across user sessions (User Data Isolation).
- **Flexible Deployment Methods:** Supports code packaging via Strands Templates, Docker Container Images registered on Amazon ECR, or compressed ZIP archives uploaded to Amazon S3.
- **Endpoint & Rollout Strategy:**
  - Endpoint ARN identifiers coupled with Alias management (`default`, `prod`, `v1`, `v2`).
  - Supports **Canary Rollouts** (gradually shifting 5% - 10% of live traffic) with instant zero-downtime Rollbacks.
- **Async Jobs & Bidirectional Streaming:**
  - *Async & Long-running Jobs:* Offloads intensive background tasks to dedicated asynchronous worker agents.
  - *Bidirectional Streaming:* Real-time two-way data streaming for Multi-modal applications handling voice, audio, and text simultaneously.

#### 5. Security & Identity Layer
- **Inbound & Outbound Authentication & Authorization:**
  - **5-Step Security Flow:**
    1. *Inbound:* Client submits a request with JWT or AWS Cognito credentials.
    2. *Token Exchange:* Agent Core exchanges the incoming JWT for a **Workload Access Token (WAT)**, combining user and agent privileges without exposing the user's raw JWT.
    3. *Outbound Exchange:* Converts WAT into downstream tool credentials (OAuth Tokens, API Keys).
    4. *Token Vault:* Stores credentials securely in an encrypted token vault.
    5. *Execution:* Executes the action and returns response safely to the user.
  - **Supported Authentication Standards:** Basic Auth, OAuth 2-legged, OAuth 3-legged (SSO), and native AWS Cognito integration.

#### 6. Enterprise Gateway Layer
- **Middleware Infrastructure:** Manages system complexity as operations scale to hundreds of agents and thousands of tool endpoints/MCP servers.
- **Key Gateway Features:**
  - **Human-in-the-Loop (HITL):** Allows administrators to manually approve or deny actions exceeding policy thresholds (e.g., auto-approving refunds ≤ $100, while routing refunds > $100 to human admins).
  - **Semantic Tool Search:** Automatically searches and routes agent requests to relevant tools using Vector Indexing without hardcoding API endpoints.
  - **Interceptors / Hooks:** Automatic safety filters inspecting inbound/outbound flows to redact Personally Identifiable Information (PII).
  - **Diverse Targets & Enterprise Topology:** Supports Lambda, REST API, API Gateway, and MCP Server targets, connecting on-premises enterprise systems securely via AWS PrivateLink and NAT Gateways.

#### 7. Hands-on Labs: Build & Deploy AI Agents
- **Lab 1: Kiro and Its Features**
  - **Environment Setup:** Flexible setup via *Local Kiro IDE* (`aws configure` targeting region `ap-southeast-1`) or pre-configured *AWS Hosted Remote Desktop (Amazon DCV)* equipped with Kiro, Python, AWS CLI, and AgentCore CLI.
  - **Kiro Steering Configuration:** Setting up `.kiro/steering.md` directive files to guide the Kiro AI assistant in adhering to AWS Strands SDK coding standards and exception handling. Validating output via **Vibe Coding**.
- **Lab 2: Build & Deploy AI Agents via AgentCore CLI (3 Commands)**
  - *Command 1 (Project Init):* `agentcore init my-first-agent` → Generates standard project files (`agent.py`, `config.yaml`, `requirements.txt`).
  - *Command 2 (Runtime Config):* `agentcore configure --model anthropic.claude-3-5-sonnet --prompt "You are a helpful AWS assistant."` → Connects the LLM brain and configures system prompts.
  - *Command 3 (Deploy & Invoke):* `agentcore deploy --env dev` → Packages and deploys to Bedrock AgentCore Runtime (MicroVM), followed by `agentcore invoke --prompt "..."` to stream live responses.

---

### Key Takeaways

#### Design Mindset
- **PoC-to-Production Mindset:** Mastering the 4 essential pillars (Performance, Scalability, Security, Governance) required for enterprise GenAI deployments.
- **Strict User Isolation:** Leveraging Firecracker MicroVM technology to enforce micro-level hardware and memory boundaries for every session.
- **WAT-Based Delegation:** Utilizing Workload Access Tokens (WAT) to protect end-user identity credentials during third-party tool execution.

#### Technical Architecture
- **AI Protocol Standardization:** Understanding the central role of MCP and A2A protocols in orchestrating multi-agent systems and tool ecosystems.
- **Bedrock Agent Core Mastery:** Deep understanding of the 3 core layers: **Runtime** (Serverless microVMs), **Identity** (AuthN/AuthZ), and **Gateway** (Middleware & HITL).
- **Vibe Coding Paradigm:** Utilizing Kiro IDE and Steering Directives to steer AI coding assistants toward cloud-native architectural patterns.

#### Operations & Deployment
- **Canary Deployment Strategies:** Utilizing Bedrock Agent Core Alias ARNs to conduct safe 5-10% canary traffic releases with zero-downtime rollbacks.
- **Human-in-the-Loop Governance:** Embedding admin approval mechanisms at the Gateway level to control high-risk enterprise actions.

---

### Applying to Work

- **Develop Agents using Strands SDK:** Implement the AWS Strands SDK and Factory Design Pattern to build highly modular, cloud-optimized AI agents.
- **Establish Project Steering Directives:** Create `.kiro/steering.md` files within repositories to standardize AI-assisted code generation across engineering teams.
- **Streamline Deployments via AgentCore CLI:** Accelerate agent lifecycle management using the 3-command CLI workflow (`agentcore init`, `agentcore configure`, `agentcore deploy`).
- **Enforce Data Sovereignty & Security:** Configure Bedrock Gateway Interceptors to filter sensitive PII data and establish AWS PrivateLink for secure hybrid network traffic.

---

### Event Experience

Attending **AWS FCAJ Agent Forge - Deepdive** provided profound technical knowledge and invaluable insights into building enterprise-grade Agentic AI systems.

- **High-Impact L300 Content:** Speaker Anh Nghia skillfully condensed over 350 slides of advanced content into intuitive architectural models, clarifying the roadmap for moving AI agents to production.
- **Interactive Vibe Coding:** Speaker Hai Anh's hands-on lab demonstrated how Kiro IDE and AgentCore CLI make initializing, configuring, and deploying serverless AI agents achievable in just minutes.
- **Demystifying Security Barriers:** Learning how Firecracker MicroVMs, Workload Access Tokens (WAT), and Enterprise Gateways work together eliminated lingering concerns regarding enterprise data privacy and access governance.

#### Some event photos
![AWS FCAJ Agent Forge - Deepdive](hinh-anh-sk-3/IMG_20260801_091335.webp)
![AWS FCAJ Agent Forge - Deepdive](hinh-anh-sk-3/IMG_20260801_110623.webp)

> The AWS FCAJ Agent Forge - Deepdive was a landmark workshop that completely reshaped my approach to designing autonomous Agentic AI architectures, equipping me with the skills to leverage Bedrock Agent Core and build production-ready Cloud-native AI solutions.
