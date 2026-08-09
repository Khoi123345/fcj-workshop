---
title: "FCAJ - Agentic AI Build Week & Agent Forge"
date: 2026-08-01
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Detailed Summary Report: "AWS FCAJ Agent Forge & Agentic AI Build Week"

### 1. General Event Overview & Speakers

* **Event Name:** AWS FCAJ Agent Forge - Deepdive & Agentic AI Build Week
* **Date & Time:** 09:00 AM – 12:30 PM, August 1, 2026
* **Location:** 26th Floor, Bitexco Financial Tower, 02 Hai Trieu Street, Ben Nghe Ward, District 1, Ho Chi Minh City
* **Target Audience:** AI Engineers, Cloud Architects, Developers, and AWS Tech Enthusiasts
* **Organizers (Host):** AWS Study Group & First Cloud AI Journey (FCAJ)
* **Distinguished Speakers:**
  * **Nghia Nguyen** – Principal Speaker (Covering Enterprise Agentic AI Architecture & L300 Theory)
  * **Hai Anh** – Hands-on Speaker (Leading Live Vibe Coding with Kiro IDE & AgentCore CLI)

---

### 2. Event Purpose & Objectives

The primary mission of **AWS FCAJ Agent Forge - Deepdive** was to transition Generative AI solutions from initial Proof-of-Concept (PoC) experiments to production-ready enterprise deployments on AWS Cloud. 

The event dissected the **four critical pillars** of enterprise AI adoption:
1. **Performance:** Minimizing latency and enabling real-time streaming responses.
2. **Scalability:** Managing multi-agent workloads with serverless architecture.
3. **Security:** Guaranteeing strict multi-tenant data isolation and token privacy.
4. **Governance:** Enforcing policy compliance with Human-in-the-Loop (HITL) gateways.

---

### 3. Detailed Technical Content & Core Takeaways

#### A. Agentic AI Philosophy & The Spectrum of Autonomy
Unlike traditional Large Language Models (LLMs) that function primarily as token predictors or simple conversational chatbots, **Agentic AI** represents a paradigm shift toward autonomous software entities. An Agent operates through an iterative loop:

$$\text{Reasoning} \longrightarrow \text{Planning} \longrightarrow \text{Execution}$$

The event categorized AI autonomy into a 4-level spectrum:
* **Level 1 (Simple Assistant):** Single-prompt Q&A interfaces relying on raw LLM completion.
* **Level 2 (Deterministic Workflow):** Hardcoded developer workflows where LLMs perform structured extraction.
* **Level 3 (Human-in-the-Loop Workflow):** Autonomous agent planning with mandatory human approval gates for critical actions.
* **Level 4 (Fully Autonomous Multi-Agent Systems):** Specialized agents autonomously collaborating, delegating long-running background tasks, and synthesizing multi-modal results.

#### B. The 5 Core Production Architecture Layers of an AI Agent
To build a resilient AI Agent on AWS, the architecture must decouple five essential components:

1. **Brain (Reasoning Engine):** Large Language Models acting as the central cognitive unit. Common choices include **Anthropic Claude 3.5 Sonnet** (for complex logic and coding), **Claude 3 Haiku** (for rapid, cost-effective responses), and **Amazon Nova**.
2. **System Prompt & Steering Rules:** Defining identity, persona, domain limits, and strict output schemas.
3. **Knowledge Base / Context Layer:** Enterprise internal knowledge connected via Retrieval-Augmented Generation (RAG) and Vector Databases (e.g., OpenSearch Serverless).
4. **Tools & Action Invocation Layer:** Exposing external execution capabilities (executing SQL queries, calling REST Webhooks, sending emails via Gmail API).
5. **Memory & Observability Layer:** Maintaining session state across short-term and long-term memory while logging execution telemetry to **Amazon CloudWatch**.

#### C. Next-Generation AI Protocols & Frameworks
* **Model Context Protocol (MCP):** A open standard protocol replacing traditional REST APIs for agent-to-tool communication, making plugin integration seamless across different LLMs.
* **Agent-to-Agent (A2A) Protocol:** Standardizing inter-agent communication, allowing a Master Agent to delegate specialized sub-tasks to Worker Agents.
* **AWS Strands SDK & Factory Pattern:** Utilizing AWS's open-source Strands SDK alongside the **Factory Design Pattern** to instantiate agents cleanly by encapsulating:

$$\text{Agent} = \text{Model} + \text{System Prompt} + \text{Tools}$$

#### D. Amazon Bedrock Agent Core & Enterprise Security Topology
* **Firecracker MicroVM Isolation:** Amazon Bedrock Agent Core executes each user session inside a dedicated **Firecracker MicroVM**. This provides absolute hardware, memory, and filesystem isolation between user sessions, ensuring zero cross-tenant data leakage.
* **5-Step Security Flow with Workload Access Token (WAT):**
  1. *Inbound Request:* Client submits request with a JWT or AWS Cognito Credential.
  2. *Token Exchange:* Agent Core exchanges the user JWT for a scoped **Workload Access Token (WAT)**.
  3. *Outbound Delegation:* WAT is converted into tool-specific credentials (OAuth/API Key) stored in an encrypted Token Vault.
  4. *Execution:* Tools execute without ever exposing the user's primary credentials.
  5. *Safe Response:* Filtered response is returned securely to the client.
* **Enterprise Gateway & Human-in-the-Loop (HITL):** Acts as a middleware proxy. For example, financial refund requests under \$100 are automatically executed by the Agent, whereas requests over \$100 trigger an administrative approval workflow before execution.
* **PII Interceptors:** Gateway filters automatically redact Personally Identifiable Information (PII) from both incoming prompts and outgoing LLM completions.

#### E. Hands-on Vibe Coding Lab with Kiro IDE & `agentcore CLI`
* **Kiro IDE & Steering Rules:** Configured `.kiro/steering.md` rules to instruct the AI assistant inside Kiro IDE to generate C# and Python code following AWS Strands SDK best practices.
* **3-Command Deployment Workflow:**
  1. `agentcore init my-first-agent` — Automatically scaffolds project structure (`agent.py`, `config.yaml`, `requirements.txt`).
  2. `agentcore configure --model anthropic.claude-3-5-sonnet` — Links the LLM brain and system persona.
  3. `agentcore deploy --env dev` — Packages and deploys the agent onto Amazon Bedrock Agent Core Firecracker MicroVMs in seconds.

---

### 4. Direct Application to My Internship Project (AI Dungeon RPG)

Participating in **FCAJ Agent Forge** directly impacted the architectural design of my internship project, the **AI Dungeon RPG Adventure Game**:

1. **Serverless AI Backend Integration:** Applied Amazon Bedrock Runtime API calls inside the .NET 8 AWS Lambda backend (`/story/next` endpoint) to dynamically generate story choices based on player character state.
2. **Structured JSON Output Constraints:** Utilized system prompt steering techniques learned at the event to enforce strict JSON schemas on Claude LLM responses, allowing seamless deserialization into C# `StoryNodeResponse` DTOs.
3. **Resilience & Fallback Handling:** Implemented timeout protection (5-second fallback buffer) and error interceptors to handle AI service latency without breaking the Unity UI game loop.

---

### 5. Event Gallery

![AWS FCAJ Agent Forge Event Session](hinh-anh-sk-3/event3.png)

---

### 6. Final Conclusion & Reflections

The **AWS FCAJ Agent Forge - Deepdive** event was a landmark learning milestone during my internship. It provided a complete blueprint for moving Generative AI from simple prompt demos to robust, secure, and production-ready Cloud architectures. The technical knowledge and hands-on experience gained from this event significantly elevated the quality and reliability of my **AI Dungeon RPG** project implementation!
