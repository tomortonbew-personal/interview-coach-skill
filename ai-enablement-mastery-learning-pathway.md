# Tom’s AI enablement interview mastery pathway

**This is not a reading list — it is a sequenced study plan mapped to every requirement in the Rightmove Technical PM (AI Enablement) job description.** Each topic includes what “surface-level” versus “interview-credible depth” looks like, specific resources to study, proof-of-understanding questions, and guidance on what Andrew and Benny (senior engineering stakeholders) will want to hear. Topics are ordered by priority: Tier 1 items are non-negotiable for the competency interview; Tier 2 items are essential for the case study; Tier 3 items differentiate you from other candidates.

Rightmove’s context is critical throughout: they run on **Google Cloud Platform (GCP)** with Vertex AI and Gemini, operate **~160 microservices** on GKE,  have **~200+ engineers across ~17 product teams**,   deploy **~2,000 releases per year**,  and have **31 live AI projects** as of early 2026. Their Head of Technology Operations, **Andrew Tate**, leads infrastructure, SRE, platforms, and tooling  — and is likely one of your interviewers. The company just committed **~£12m in additional AI investment** for 2026,  and the market is watching closely for ROI. Your job is to be the person who makes that investment pay off for engineering teams.

-----

## TIER 1: Study these first — the core of every answer you give

### 1. AI coding tools: the product you’re enabling adoption of

**JD requirements addressed:** Customer-Centric AI Enablement, AI Platform & Capability Decision, AI-assisted code generation and review, Enablement & Adoption

**Why it matters for THIS role:** AI coding assistants are the single most visible AI enablement surface for engineering teams. You will own the strategy for which tools Rightmove adopts, how they’re configured, and how adoption is measured. Andrew and Benny will expect you to have opinions — not just awareness — about Copilot vs. Cursor vs. JetBrains AI, and about what “good” looks like for enterprise deployment.

**Surface-level awareness** sounds like: “Copilot suggests code completions and has a chat feature.” **Interview-credible depth** sounds like: “Copilot Enterprise gives us codebase-aware chat via repository indexing, knowledge bases tied to internal Markdown docs, a coding agent that can autonomously handle GitHub issues, and AI-powered code review that integrates CodeQL and ESLint. The Metrics API went GA in February 2026 — it gives organization-level data on acceptance rates, lines of code contributed, PR lifecycle metrics, and agent adoption, broken down by IDE and model. The average acceptance rate across the industry is ~30%,  but the real signal is whether AI-generated code survives review — Accenture found an 88% retention rate.  I’d advocate tracking acceptance rate alongside PR revert rate and change failure rate, because the 2025 DORA report found that AI adoption correlates with faster delivery but also higher instability.” 

**The competitive landscape you must know:**

**GitHub Copilot Enterprise** ($39/user/month) is the incumbent with **20M+ users**  and 90% of Fortune 100 adoption.  Key enterprise features: multi-model support (GPT-4o, Claude 3.5/3.7, Gemini 2.0 Flash),  Copilot Spaces for curated context, IP indemnity, SOC 2/ISO 27001 compliance, content exclusion controls,  and the new Copilot Coding Agent (1,000 premium requests/month for Enterprise).  It works across VS Code, JetBrains, Xcode, Vim, and CLI. 

**Cursor** ($20/month individual, $40/user/month teams) is the AI-native IDE challenging Copilot’s dominance. Its Composer mode enables multi-file editing from a single prompt. It indexes entire repositories for cross-file context. Agent mode handles autonomous multi-step refactoring. It reached **$300M ARR** by late 2025 and ~25-30% professional developer adoption. The trade-off: IDE lock-in (it’s a VS Code fork, not a plugin) and weaker enterprise compliance features.

**JetBrains AI Assistant** is the natural choice for teams already in the JetBrains ecosystem (and Rightmove uses Java heavily — IntelliJ is likely prevalent). Key differentiator: **local/offline model support** via Mellum (JetBrains’ own code completion model) and Ollama/LM Studio connectors, enabling air-gapped deployment.  MCP support is built in.  Enterprise features include .aiignore files and zero data retention by default. 

**What you should also know about:** AI code review tools (CodeRabbit, Qodo, Copilot Review — none caught a severe S3 configuration bug in independent testing;  human review remains essential for architectural decisions) and AI test generation tools (Diffblue achieves **50-69% code coverage** via reinforcement learning vs. Copilot’s 5-29%;  Qodo’s multi-agent architecture handles 11+ languages). 

**Resources to study:**

- GitHub Copilot Metrics documentation: docs.github.com/en/copilot/concepts/copilot-usage-metrics/copilot-metrics
- GitHub Copilot rolling out at scale: docs.github.com/en/copilot/rolling-out-github-copilot-at-scale
- Accenture enterprise study: github.blog/news-insights/research/research-quantifying-github-copilots-impact-in-the-enterprise-with-accenture/
- ZoomInfo enterprise case study (paper): arxiv.org/html/2501.13282v1
- Cursor official site: cursor.com
- JetBrains AI Assistant features: jetbrains.com/ai-assistant/
- BlueDot AI code review evaluation: bluedot.org/blog/best-ai-code-review-tools-2025
- Diffblue benchmark: diffblue.com/resources/diffblue-cover-vs-ai-coding-assistants-benchmark-2025/

**Proof-of-understanding questions:**

1. “If Rightmove’s engineers primarily use IntelliJ for Java development, what would your tool selection and rollout strategy be — and how would you handle the fact that some teams might prefer Cursor’s multi-file editing capabilities?”
1. “Copilot’s acceptance rate metric just went GA. Walk me through how you’d use it alongside other signals to determine whether the tool is actually making engineers more productive, not just more prolific.”

**What good looks like in the interview:** Andrew and Benny want to hear that you understand the *tool landscape is a portfolio decision, not a winner-take-all choice*. Show you can articulate trade-offs: Copilot’s breadth of IDE support vs. Cursor’s depth of AI integration vs. JetBrains’ privacy controls. Demonstrate awareness that **~40% of AI-generated code contains vulnerabilities** and that quality guardrails (code review, SAST scanning) must scale alongside adoption. Reference specific metrics (acceptance rate, retention rate, PR revert rate) rather than vague “productivity gains.”

-----

### 2. DORA metrics and the AI productivity paradox

**JD requirements addressed:** Data-Driven Decision Making, Clear Business Alignment & Visibility, Accelerated Time-to-Value

**Why it matters for THIS role:** DORA metrics are the lingua franca of engineering leadership. When Andrew asks “how will you measure whether AI enablement is working?” your answer must be grounded in DORA. But you also need to know why DORA alone is insufficient — and why the 2025 findings fundamentally complicate the AI productivity narrative.

**Surface-level awareness** sounds like: “DORA tracks deployment frequency, lead time, change failure rate, and time to restore.” **Interview-credible depth** sounds like: “The 2025 DORA report surveyed nearly 5,000 professionals  and found that **AI is an amplifier, not a solution in a box**.  90% of technology professionals now use AI, spending a median of 2 hours daily with AI tools. AI adoption positively correlates with software delivery throughput  — teams ship faster. But it also correlates with **higher instability**: more change failures, increased rework, and longer recovery cycles.  The report replaced the old elite/high/medium/low performance tiers with seven team archetypes,  and critically, each archetype experiences AI differently. For teams in the ‘Harmonious High-Achiever’ profile, AI amplifies excellence.  For ‘Legacy Bottleneck’ teams, AI accelerates chaos.  This means a one-size-fits-all AI rollout strategy would be counterproductive — you need to diagnose where each team falls and tailor interventions.”

**The DORA AI Capabilities Model** identifies seven foundational capabilities that determine whether AI amplifies or undermines your organization: clear AI stance with psychological safety for experimentation,  healthy data ecosystems, AI-accessible internal data, strong version control,  **high-quality internal developer platforms**, user-centric product focus, and fast feedback loops with loosely coupled architectures. The finding that **platform quality directly correlates with AI amplification**  is your strongest argument for why AI enablement must be built on solid platform engineering foundations.

**The AI Productivity Paradox (Faros AI):** Telemetry from 10,000+ developers found AI coding assistants boost individual output  — **21% more tasks completed, 98% more PRs merged** — but organizational delivery metrics (DORA) stay flat. Developers using AI interact with 9% more task contexts and 47% more pull requests daily,  shifting the bottleneck to code review and testing. This is the most important finding for your role: AI doesn’t eliminate bottlenecks, it moves them downstream.

**The 2025 report also evolved the metrics themselves.** “Mean Time to Restore Service” became “Failed Deployment Recovery Time” (reclassified as throughput).  A new fifth metric — **Rework Rate** (ratio of unplanned deployments due to production issues) — was added as a stability measure.

**Tom’s existing knowledge to deepen:** You noted surface-level DORA prep. Go deeper on the seven team archetypes, the AI Capabilities Model, and the Productivity Paradox specifically. These are the insights that separate a prepared candidate from someone who just knows the four metrics.

**Resources to study:**

- 2025 DORA Report: dora.dev/research (read the full report, not just summaries)
- Google Cloud blog on DORA AI capabilities: cloud.google.com/blog/products/ai-machine-learning/from-adoption-to-impact-putting-the-dora-ai-capabilities-model-to-work
- Faros AI Productivity Paradox analysis: faros.ai/blog/ai-software-engineering
- CD Foundation on the five metrics: cd.foundation/blog/2025/10/16/dora-5-metrics/
- Pragmatic Engineer on measuring AI impact: newsletter.pragmaticengineer.com/p/how-tech-companies-measure-the-impact-of-ai
- METR randomized controlled trial (experienced devs were 19% slower with AI): metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/

**Proof-of-understanding questions:**

1. “The 2025 DORA report says AI is ‘an amplifier, not a solution in a box.’ What does that mean practically for how you’d sequence AI tool rollout across Rightmove’s ~17 product teams?”
1. “Faros AI found individual developer output increased 21% but organizational DORA metrics stayed flat. Where’s the bottleneck, and how would you address it as the AI Enablement PM?”

**What good looks like in the interview:** Don’t just recite the four (now five) metrics. Show you understand the *paradox*: AI makes individuals faster but organizations aren’t necessarily better. Articulate that your job is to identify and unblock the downstream constraints (code review capacity, test coverage, deployment pipeline throughput) that absorb individual productivity gains. Reference the seven archetypes to show you wouldn’t treat all teams the same.

-----

### 3. Engineering productivity measurement beyond DORA

**JD requirements addressed:** Data-Driven Decision Making, Internal Customer Insights

**Why it matters for THIS role:** You need a multi-dimensional measurement framework. DORA measures delivery outcomes; you also need to measure developer experience, satisfaction, and the human dimensions of AI adoption.

**The SPACE Framework** (Forsgren, Storey et al., 2021) measures five dimensions: **Satisfaction & Well-being** (surveys — developer happiness, burnout), **Performance** (quality outcomes connected to business value), **Activity** (commits, PRs, reviews — most common AND most misused metric), **Communication & Collaboration** (code review quality, knowledge discoverability), and **Efficiency & Flow** (uninterrupted focus time, friction).   The key principle: **measure at least 3 of 5 dimensions simultaneously**  across individual, team, and system levels. Nicole Forsgren, who developed both DORA and SPACE, describes them as complementary: “DORA = the signal (how we are doing); SPACE = action required (how to improve).” 

**DX Core 4** (evolved from SPACE by the same team, used by 300+ organizations) unifies measurement into four dimensions: Speed, Effectiveness, Quality, and Impact. Its **Developer Experience Index (DXI)** is a composite score from 14 survey items — each 1-point DXI improvement saves ~13 minutes per developer per week. This is the framework that connects developer experience directly to quantifiable business value.

**Resources to study:**

- SPACE paper: queue.acm.org/detail.cfm?id=3454124
- DX Core 4 research: getdx.com/research/measuring-developer-productivity-with-the-dx-core-4/
- Nicole Forsgren on AI productivity measurement (podcast): lennysnewsletter.com/p/how-to-measure-ai-developer-productivity
- Jellyfish 2025 AI metrics review: jellyfish.co/blog/2025-ai-metrics-in-review/

**Proof-of-understanding questions:**

1. “Why is acceptance rate a better proxy for AI tool effectiveness than lines of code, and what would you pair it with?”
1. “How would you design a measurement framework for Rightmove’s AI enablement program that satisfies both engineering leadership (who care about delivery speed) and the CFO (who cares about the £12m investment ROI)?”

-----

### 4. Platform engineering and “platform as a product”

**JD requirements addressed:** AI Platform & Capability Decision, Internal Customer Insights, Product Roadmaps & Delivery

**Why it matters for THIS role:** Rightmove already practices platform-as-a-product thinking (their Project Factory, self-service GCP provisioning via PRs, and Terraform/Terragrunt pipelines prove this).  Your role is to extend this mindset to AI capabilities — making AI tools, models, and patterns available through a self-service internal platform. This is possibly the single most important conceptual frame for the role.

**Surface-level awareness** sounds like: “Platform engineering means building internal tools for developers.” **Interview-credible depth** sounds like: “Platform engineering, informed by Team Topologies, structures organizations into stream-aligned teams (delivering user value), platform teams (accelerating stream-aligned teams), enabling teams  (temporarily boosting capabilities), and complicated-subsystem teams.  The platform team’s job is to reduce cognitive load on stream-aligned teams by providing self-service golden paths — the approved, easiest way to do something. The ‘Thinnest Viable Platform’ principle  says start with the smallest useful set of APIs, docs, and tools, then iterate based on developer feedback. Gartner predicts 80% of large engineering organizations will have platform teams by 2026.   The 2025 DORA report found that **90% of organizations now have platform engineering capabilities**, with platform quality directly correlating to AI’s positive amplification effect.” 

**Backstage** (Spotify, CNCF Incubation) is the dominant open-source developer portal framework: Software Catalog (central registry of all services with ownership), Software Templates (standardized scaffolding), TechDocs (“docs like code”), and a plugin ecosystem. Spotify’s internal data: frequent Backstage users are **2.3x more active in GitHub**, create **2x code changes in 17% less cycle time**, and deploy **2x as often**.

**For Rightmove specifically:** They already have platform-as-a-product DNA (Project Factory, embedded platform product owner).  Your AI enablement platform would extend this with: an AI service catalog (centralized access to approved models and APIs), AI golden paths (standardized patterns for common AI use cases), prompt/template libraries, model governance controls, and observability dashboards.

**Resources to study:**

- Team Topologies key concepts: teamtopologies.com/key-concepts
- Martin Fowler’s Team Topologies bliki: martinfowler.com/bliki/TeamTopologies.html
- Backstage documentation: backstage.io/docs
- DX on platform engineering in the AI era: getdx.com/blog/platform-engineering/
- CNCF platform engineering definition: cncf.io/blog/2025/11/19/what-is-platform-engineering/
- Rightmove’s own cloud journey (understand their existing platform): rightmove.blog/rightmoves-journey-to-cloud/

**Proof-of-understanding questions:**

1. “Rightmove already has a Project Factory for self-service GCP provisioning. How would you design an equivalent ‘AI Factory’ — what would be in the self-service catalog and what would require platform team involvement?”
1. “What does the ‘Thinnest Viable Platform’ concept mean for an AI enablement initiative in its first quarter?”

**What good looks like in the interview:** Show you understand that AI enablement IS platform engineering. You’re not just rolling out tools — you’re building a self-service AI platform that reduces cognitive load. Reference Team Topologies directly. Mention golden paths. Demonstrate you’d treat engineering teams as your customers and run user research, surveys, and feedback loops exactly as you would for an external product. This directly mirrors how Rightmove already thinks about their infrastructure platform. 

-----

### 5. AI adoption, change management, and champion programs

**JD requirements addressed:** Enablement & Adoption, Internal Customer Insights, Customer-Centric AI Enablement

**Why it matters for THIS role:** The hardest part of this job isn’t choosing tools — it’s getting 200+ engineers to actually change their workflows. The data is sobering: **only 2% of Microsoft 365 subscribers use Copilot** despite 70% of Fortune 500 purchasing licenses. Only 28% of employees know how to use their company’s AI applications.  93% of executives say culture and readiness block AI progress. 

**Tom’s existing knowledge to deepen:** You’ve been an AI Champion at The Economist and participated in the Copilot pilot. This is a strong foundation — but go deeper on structured adoption frameworks and quantified outcomes.

**The evidence-based playbook:**

- **Champion programs** increase adoption by up to 40%. Optimal ratio: 1 champion per 100-200 employees.  Champions must be technically strong, respected by peers, and genuinely enthusiastic (not just senior).
- **Embedding AI in workflows** (not making it optional) is the key lever. CIBC achieved **90% adoption and 10-14% productivity lift** by embedding Copilot directly into developer workflows rather than offering it as an opt-in tool.
- **Tiered training**: AI Fundamentals (all) → AI in Practice (active users) → AI Expertise (power users).
- **Phased rollout**: Pilot (25-30 people) → evaluate with quantified metrics → expand gradually. GitHub recommends 2-3 developers for 30 days as initial pilot. 
- Microsoft research shows **11 weeks** for developers to fully realize productivity gains  — set expectations accordingly.
- Real adoption rates plateau around **60%** even in leading organizations (DX Research). Plan for this.

**AI adoption maturity stages** (Larridin): AI Curious → AI Enabled → AI Scaling → AI Embedded → AI-Native.  Most organizations are at Enabled/Scaling. Your job is to move Rightmove toward Embedded.

**Key adoption barriers to address**: Fear of replacement (53% worry using AI makes them look replaceable), skills gap (38% of challenges), no training (77% of organizations offer none), middle management resistance, and the knowing-doing gap (understanding AI but not using it consistently).

**Resources to study:**

- Faros AI enterprise adoption scaling guide: faros.ai/blog/enterprise-ai-coding-assistant-adoption-scaling-guide
- HBR on organizational barriers to AI adoption: hbr.org/2025/11/overcoming-the-organizational-barriers-to-ai-adoption
- GitHub’s AI governance and policy framework: resources.github.com/learn/pathways/copilot/essentials/empower-developers-with-ai-policy-and-governance/
- Prosci ADKAR model applied to AI: prosci.com/blog/ai-adoption
- WalkMe SODA 2025 report: walkme.com/blog/enterprise-ai-adoption/

**Proof-of-understanding questions:**

1. “You’re rolling out AI coding tools to 200+ Rightmove engineers. 60% is a realistic active adoption ceiling. How do you design interventions to push past that — and when do you decide that 60% is actually good enough?”
1. “An engineering manager tells you their team tried Copilot for two weeks and ‘didn’t see the point.’ What’s your diagnostic framework and what interventions would you propose?”

**What good looks like in the interview:** Reference your Economist AI Champion experience but show you’ve systematized the approach. Mention specific metrics: activation rate, weekly active users, feature utilization depth, time-to-first-value. Talk about treating adoption as a product problem (user research, friction mapping, iterative improvement) rather than a rollout problem. Show awareness that adoption barriers are primarily cultural and organizational, not technical.

-----

## TIER 2: Essential for case study depth and technical credibility

### 6. MCP (Model Context Protocol) and agentic AI architectures

**JD requirements addressed:** AI Platform & Capability Decision, Internal AI agents supporting SSDLC tasks, managing multi-agent systems

**Why it matters for THIS role:** MCP is the protocol layer that makes enterprise AI integration scalable. Agentic AI is the architectural paradigm shift from “AI as autocomplete” to “AI as autonomous collaborator.” Both are central to what this role will be building toward.

**Tom’s existing knowledge to deepen:** You noted conceptual familiarity with MCP and agents. Go from “I know what MCP is” to “I can explain how we’d use MCP servers to connect AI tools to Rightmove’s internal systems.”

**MCP in 90 seconds:** Anthropic open-sourced MCP in November 2024 as an open protocol standardizing how AI systems integrate with external tools. Before MCP, connecting M AI applications to N data sources required M×N custom integrations.  MCP collapses this to M+N.  Architecture: **Hosts** (LLM apps like Claude/Cursor), **Clients** (connectors within hosts), **Servers** (services exposing tools/data).  Three primitives: **Tools** (functions AI can execute), **Resources** (data for context), **Prompts** (templated workflows).   Transport: stdio for local, Streamable HTTP for remote (added March 2025 with OAuth 2.1).  It was **donated to the Linux Foundation’s Agentic AI Foundation** in December 2025, co-founded by Anthropic, Block, and OpenAI, supported by AWS, Google, Microsoft.  It now has **97 million monthly SDK downloads** and 10,000+ servers. 

**Agentic AI patterns** (Andrew Ng’s canonical framework): **Reflection** (agent critiques and improves its own output), **Tool Use** (calling external functions/APIs), **Planning** (decomposing goals into sub-tasks), **Multi-Agent Collaboration** (specialized agents working together).  The spectrum of autonomy runs from autocomplete (Level 1) through supervised agents (Level 3, like Cursor) to autonomous agents (Level 4, like Claude Code/Devin). Most production tools cluster at Level 3-4 in 2025.

**Multi-agent frameworks to know:** LangGraph (graph-based state machine,  production at 400+ companies — LangChain’s team says “use LangGraph for agents, not LangChain”), CrewAI (role-based teams, YAML-driven),  Microsoft Agent Framework (merged AutoGen + Semantic Kernel, GA Q1 2026), OpenAI Agents SDK (replaced Swarm). Architecture patterns: orchestrator-worker (supervisor delegates), sequential pipeline, peer-to-peer (decentralized).

**Critical enterprise challenge:** Gartner reports an **85% failure rate** in multi-agent implementations.  Start with single agents; add complexity only when justified. Coordination overhead, error propagation, and observability are the key engineering problems.

**Resources to study:**

- MCP specification: modelcontextprotocol.io/specification/2025-11-25
- Anthropic’s MCP announcement: anthropic.com/news/model-context-protocol
- Anthropic MCP course: anthropic.skilljar.com/introduction-to-model-context-protocol
- Andrew Ng’s Agentic AI course: deeplearning.ai/courses/agentic-ai/
- ByteByteGo agentic patterns: blog.bytebytego.com/p/top-ai-agentic-workflow-patterns
- Deloitte Agentic AI Strategy: deloitte.com/us/en/insights/topics/technology-management/tech-trends/2026/agentic-ai-strategy.html
- LangGraph documentation: langchain-ai.github.io/langgraph/

**Proof-of-understanding questions:**

1. “Explain how you’d use MCP to connect an AI coding assistant to Rightmove’s internal service catalog, Jira board, and monitoring dashboards — what MCP servers would you need and what primitives would they expose?”
1. “When would you recommend Rightmove build a multi-agent system versus a single agent with tool use? What’s the decision framework?”

**What good looks like in the interview:** Show you understand MCP as infrastructure, not just a protocol — it’s how you’d build a composable AI platform where AI tools can access internal systems. For agents, demonstrate you know the spectrum of autonomy and would start conservative (human-in-the-loop) and expand based on trust and evaluation data. Reference the 85% failure rate to show you’re not a hype-driven PM.

-----

### 7. AI governance, SSDLC, and safety frameworks

**JD requirements addressed:** Governance, Safety & Scalability, Internal AI agents supporting SSDLC tasks, Experimentation with risk-aware governance

**Why it matters for THIS role:** You’ll partner with security, compliance, data, and architecture teams to translate emerging risks into product decisions. Andrew and Benny will test whether you can balance velocity with safety — this is the “risk-aware governance” skill the JD explicitly calls out.

**Tom’s existing knowledge to deepen:** You mentioned familiarity with SSDLC and participation in the Copilot pilot from a governance perspective. Go deeper on specific frameworks and the OWASP LLM Top 10.

**Three governance frameworks to know:**

**NIST AI RMF** (AI 100-1, January 2023): Four functions — **Govern** (establish policies), **Map** (contextualize risks), **Measure** (quantify via TEVV), **Manage** (act on risks).  The **GenAI Profile (NIST AI 600-1)** extends this with 12 risk categories specific to generative AI: confabulation/hallucination, data privacy, information security, IP concerns, and others,  with 200+ suggested actions.  Use NIST AI RMF to *structure governance conversations* — it provides the shared vocabulary.

**EU AI Act** (Regulation 2024/1689): Risk-based classification — Unacceptable (banned), High (conformity assessments required), Limited (transparency obligations), Minimal (no requirements). Key dates: prohibitions effective February 2025;  majority of rules August 2026.  As a UK company, Rightmove is not directly subject, but should align as a de facto global standard. Penalties up to **€35M or 7% global turnover**. 

**ISO 42001** (December 2023): The only *certifiable* AI management system standard.  PDCA cycle with  38 specific controls.  Microsoft achieved certification for M365 Copilot.  Use NIST AI RMF for initial risk assessment → ISO 42001 for formal governance maturity.

**OWASP LLM Top 10 (2025)** — the security risks you must know: **Prompt Injection** (LLM01), **Sensitive Information Disclosure** (LLM02), **Supply Chain vulnerabilities** (LLM03), **Excessive Agency** (LLM06 — critical for agentic AI), **System Prompt Leakage** (LLM07), **Vector/Embedding Weaknesses** (LLM08), **Unbounded Consumption** (LLM10 — cost/resource risks).  

**AI-generated code security:** ~40% of AI-generated code contains vulnerabilities.  ~80% of developers *mistakenly believe* AI-generated code is more secure. Key risks: SQL injection, hardcoded credentials, insecure dependencies, missing input validation. This is why SAST/DAST scanning of AI-generated code is non-negotiable.

**Guardrails tools to reference:** NVIDIA NeMo Guardrails (programmable safety rails using Colang DSL),  Guardrails AI (Pydantic-style output validation),  Anthropic’s Constitutional AI approach (training AI with explicit ethical principles).

**Resources to study:**

- NIST AI RMF: airc.nist.gov/AI_RMF_Knowledge_Base/AI_RMF
- NIST AI 600-1 GenAI Profile: doi.org/10.6028/NIST.AI.600-1
- OWASP LLM Top 10 (2025): genai.owasp.org/llm-top-10/
- EU AI Act timeline: artificialintelligenceact.eu/implementation-timeline/
- ISO 42001 overview: iso.org/standard/42001
- GitHub AI governance pathway: resources.github.com/learn/pathways/copilot/essentials/empower-developers-with-ai-policy-and-governance/
- NeMo Guardrails: github.com/NVIDIA-NeMo/Guardrails

**Proof-of-understanding questions:**

1. “A team wants to deploy an AI agent that can autonomously modify production configuration files based on monitoring alerts. Walk me through how you’d assess and govern this using NIST AI RMF’s four functions.”
1. “What are the top three OWASP LLM risks that are most relevant to Rightmove’s AI enablement use cases, and how would you mitigate each?”

**What good looks like in the interview:** Show you can translate abstract governance frameworks into concrete product decisions. Don’t just list NIST functions — show how you’d apply them to a real scenario (e.g., “For an AI code review agent with write access to PRs, I’d Map the risks of incorrect auto-merges, Measure the error rate through a shadow-mode pilot, and Manage by requiring human approval above a confidence threshold”). Reference the OWASP LLM Top 10 to demonstrate security literacy. Frame governance as an enabler of faster adoption (“clear guardrails give teams confidence to experiment”), not a blocker.

-----

### 8. LLMOps, observability, and AI platform infrastructure

**JD requirements addressed:** AI Platform & Capability Decision, Data-Driven Decision Making, Log/metric analysis and incident assistance

**Why it matters for THIS role:** You need to understand the infrastructure beneath AI features — how models are served, monitored, evaluated, and optimized. This is the “how” behind the “what” of AI enablement.

**LLMOps differs from traditional MLOps** in fundamental ways: you start with foundation models rather than training from scratch; the key technique is prompt engineering and RAG rather than feature engineering; evaluation requires human feedback and hallucination detection rather than just accuracy/F1; and cost management is per-token at inference rather than per-GPU at training. Three maturity levels: operating LLM APIs → fine-tuning pre-trained models → training from scratch (rare).

**AI Gateways are emerging critical infrastructure.** They sit between applications and LLM providers, handling unified API access, model routing (latency/cost/quality-based), fallbacks during outages, rate limiting, budget enforcement, observability, guardrails, and semantic caching. Key tools: **Portkey** (enterprise governance, 1,600+ models), **LiteLLM** (open-source, OpenAI-compatible), **Kong AI Gateway** (enterprise API management). For Rightmove on GCP, Vertex AI provides native model serving with built-in governance.

**LLM Observability** is non-negotiable. Key tools: **Langfuse** (MIT open-source, self-hostable, 50K free events/month), **Helicone** (proxy-based, 2 lines of code integration, <1ms latency), **LangSmith** (deep LangChain integration). Capabilities needed: end-to-end request tracing, token/cost tracking per team/app, latency monitoring, hallucination detection, and session-level agent workflow visualization.

**RAG (Retrieval-Augmented Generation)** is the default enterprise AI architecture. It augments LLMs with real-time retrieval from knowledge bases before generating responses. Critical for Rightmove’s **4 petabytes of proprietary data**. But naive RAG has only **10-40% success rates** in enterprise environments. Production requires hybrid search (vector + keyword), cross-encoder reranking, and semantic chunking as baseline. Decision framework: start with prompt engineering → add RAG for knowledge grounding → fine-tune only when behavior modification is needed.

**Resources to study:**

- Databricks LLMOps guide: databricks.com/glossary/llmops
- Langfuse documentation: langfuse.com
- Helicone guide to LLM observability: helicone.ai/blog/the-complete-guide-to-LLM-observability-platforms
- Portkey AI Gateway: portkey.ai/features/ai-gateway
- Enterprise RAG architecture: applied-ai.com/briefings/enterprise-rag-architecture/
- Google Cloud Vertex AI (Rightmove’s partner): cloud.google.com/vertex-ai

**Proof-of-understanding questions:**

1. “If Rightmove wants to offer multiple LLM models to engineering teams (e.g., Gemini for some tasks, Claude for others), how would you architect the access layer? What concerns would you need to address?”
1. “How would you use RAG to make an internal AI assistant that helps Rightmove engineers query their own service documentation and incident history?”

-----

### 9. Rightmove-specific context — know your customer

**JD requirements addressed:** All — this is context that should permeate every answer

**Study this thoroughly.** You’re interviewing with engineers who live this context daily.

**Key facts to internalize:**

- **GCP, not AWS.** Multi-year Google Cloud collaboration announced November 2025 spanning cloud, platform, data, and AI — including Vertex AI and Gemini models.
- **Scale:** 50M daily page views, 14M daily searches, 125M+ monthly visitors, ~160 microservices on GKE, ~2,000 releases/year, ~200+ engineers, ~17 product teams.
- **31 live AI projects** as of early 2026 (up from 4 in November 2025). Consumer-facing: AI Keywords, Style with AI, Renovation Cost Estimator, AI Conversational Search (Gemini-powered), ChatGPT app. Partner-facing: Vendor Prediction Model (powering Discover — 40% conversion increase), AI writing tools for agents.
- **Architecture:** Java (primary backend), React.js frontend, Kafka for event streaming, Spring Boot, contract testing with Pact, Resilience4J for circuit breaking.
- **Platform engineering maturity:** Project Factory (self-service GCP provisioning via PRs), Terraform/Terragrunt pipelines, policy-as-code, “you build it, you run it” culture.
- **Culture:** 10% time for learning, hackathons, RFC process for proposals, T-shaped engineers encouraged, continuous delivery.
- **Business tension:** £12m additional AI investment for 2026, operating margin expected to drop from 70% to 67%. Share price dropped 28% intraday when announced. **You must be able to articulate ROI clearly.**
- **Andrew Tate** (likely interviewer) = Head of Technology Operations, leads infrastructure, SRE, platforms, and tooling.
- **Competitive urgency:** CoStar Group acquired OnTheMarket, AI-native startups like Jitty emerging, Google AI Overviews potentially disintermediating portal search.

**Resources to study:**

- Rightmove tech blog: rightmove.blog (read all recent posts)
- Rightmove tech stack: rightmove.blog/our-tech-stack/
- Cloud journey: rightmove.blog/rightmoves-journey-to-cloud/
- Event-driven architecture: rightmove.blog/from-legacy-to-resilience-how-event-driven-systems-improved-efficiency-at-rightmove/
- AI innovations: hub.rightmove.co.uk/latest-ai-innovations/
- FY2025 results: rightmove.co.uk/press-centre (read the latest press release)
- FY2025 investor presentation (search for the Trading Update PDF)

**Proof-of-understanding questions:**

1. “Rightmove has ~17 product teams and 200+ engineers. Given their existing platform engineering maturity and GCP/Vertex AI partnership, what would your first-quarter AI enablement roadmap look like?”
1. “The market penalized Rightmove’s share price for AI investment costs. How would you structure your enablement program to demonstrate ROI within the first two quarters?”

-----

## TIER 3: Differentiating topics that set you apart

### 10. LLM evaluation frameworks

**Why it differentiates:** Most PM candidates can’t discuss how to evaluate model quality beyond “we’d test it.” Knowing LMSYS Chatbot Arena (crowdsourced pairwise battles, Bradley-Terry rating, 6M+ votes), HELM (Stanford’s holistic multi-metric evaluation), and the concept of building proprietary eval sets (100-500 production-representative examples) shows engineering-level rigor. Key insight from Andrew Ng: *“The single biggest predictor of whether someone executes well is their ability to drive a disciplined process for evals and error analysis.”*

**Resources:** lmarena.ai (Chatbot Arena), crfm.stanford.edu/helm/ (HELM), github.com/openai/evals

### 11. AIOps and AI-assisted incident response

**JD requirement:** Log/metric analysis and incident assistance

**Why it differentiates:** This is a specific use case called out in the JD. AI-powered incident management platforms save an average of **4.87 hours per incident**. Tools like incident.io reduced MTTR by 37% for Favor. The CoSAI framework (October 2025) provides AI-specific incident response playbooks covering prompt injection, data poisoning, model drift, and unauthorized tool execution. Knowing the progression from read-only AI (observe and summarize) → advised (recommend actions) → assisted (execute reversible actions with approval) → autonomous (handle known scenarios) shows maturity.

**Resources:** incident.io/blog/5-best-ai-powered-incident-management-platforms-2026, CoSAI framework: coalitionforsecureai.org

### 12. Responsible AI and Anthropic’s approach

**Why it differentiates:** Shows you think beyond tools to principles. Anthropic’s **Responsible Scaling Policy (v3, February 2026)** defines AI Safety Levels (ASL-1 through ASL-4+) — graduated safeguards that scale with model capabilities. Their Constitutional AI approach trains AI with explicit ethical principles rather than relying solely on human feedback. The January 2026 constitution introduced a **4-tier priority hierarchy: safety > ethics > compliance > helpfulness**. Knowing this shows you understand the philosophical foundations behind guardrails, not just the technical implementation.

**Resources:** anthropic.com/news/responsible-scaling-policy-v3, anthropic.com/research/constitutional-ai-harmlessness-from-ai-feedback

### 13. Prompt engineering for production systems

**Why it differentiates:** Anthropic’s official guide (docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/claude-4-best-practices) covers six core techniques: be clear and direct, use examples (multishot), let Claude think (chain-of-thought), use XML tags for structure, give Claude a role (system prompts), chain complex prompts. The key agent-specific insight: agent prompting requires *heuristics and principles* rather than rigid few-shot examples, because traditional examples can backfire in agentic loops. Production prompt management means version control, A/B testing, evaluation suites, and prompt caching.

**Resources:** docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/, github.com/anthropics/prompt-eng-interactive-tutorial

### 14. AI product metrics and ROI frameworks

**Why it differentiates:** You need to speak the language of business value, not just engineering metrics. **Risk-Adjusted ROI** = (ΔRevenue + ΔGross Margin + Avoided Cost) − TCO, discounted by safety/reliability signals. TCO includes integration work, evaluation harnesses, data labeling, prompt/retrieval spend, infrastructure, monitoring, and change management. Target payback: <2 quarters for operations use cases; <1 year for developer-productivity platforms. Sobering context: **42% of companies abandoned most AI projects in 2025**, only 25% deliver expected ROI. Johnson & Johnson found only **10-15% of their 900 GenAI projects delivered 80% of value.** This means ruthless prioritization is the PM’s primary value-add.

**Resources:** Gartner AI value metrics: gartner.com/en/articles/ai-value-metrics, Google Cloud KPI framework: cloud.google.com/transform/gen-ai-kpis-measuring-ai-success-deep-dive

-----

## Consolidated study schedule

Given interview timeline pressure, here is the recommended sequence. Allocate approximately the indicated time per block.

**Days 1-2 (Foundation — ~8 hours total):**

- Read Rightmove’s tech blog cover-to-cover (2 hours): rightmove.blog — especially the cloud journey, tech stack, and event-driven architecture posts
- Read the 2025 DORA report executive summary and AI capabilities section (2 hours): dora.dev/research
- Read the Faros AI Productivity Paradox analysis (1 hour): faros.ai/blog/ai-software-engineering
- Study GitHub Copilot Enterprise features and Metrics API docs (2 hours): docs.github.com/en/copilot
- Read the SPACE paper (1 hour): queue.acm.org/detail.cfm?id=3454124

**Days 3-4 (Tools and Platform — ~8 hours total):**

- Deep-dive on Cursor, JetBrains AI, and code review/test generation tools (2 hours)
- Study Team Topologies key concepts and platform-as-a-product (2 hours): teamtopologies.com/key-concepts + backstage.io
- Read the GitHub AI governance pathway (1 hour): resources.github.com
- Study the AI adoption playbook — Faros guide, HBR article, Prosci ADKAR (2 hours)
- Read Rightmove’s AI innovations page and recent press releases (1 hour): hub.rightmove.co.uk

**Days 5-6 (Technical Depth — ~8 hours total):**

- MCP specification and Anthropic’s MCP course (2 hours): modelcontextprotocol.io + anthropic.skilljar.com
- Andrew Ng’s Agentic AI course (2 hours): deeplearning.ai/courses/agentic-ai/
- OWASP LLM Top 10 and NIST AI RMF overview (2 hours): genai.owasp.org + airc.nist.gov
- LLMOps and observability tools overview — Langfuse, Helicone docs (1 hour)
- RAG architecture patterns (1 hour): applied-ai.com/briefings/enterprise-rag-architecture/

**Day 7 (Synthesis and Practice — ~4 hours):**

- Practice answering every proof-of-understanding question in this document out loud
- Prepare 3-5 “Rightmove-specific” scenarios showing how you’d apply each concept
- Draft your “first 90 days” plan for the AI Enablement PM role
- Review Tier 3 differentiating topics at headline level

-----

## The narrative thread for every interview answer

Across every topic, your answers should weave together a consistent story with five beats:

**Beat 1 — Empathy for the engineer:** “I’d start by understanding the friction points engineers actually experience, not what I assume they need. Structured research: workflow shadowing, surveys, platform telemetry, direct engagement.”

**Beat 2 — Platform thinking:** “AI enablement is platform engineering. We build self-service golden paths, not mandates. Thinnest Viable Platform first, iterate based on developer feedback.”

**Beat 3 — Measurement rigor:** “I’d combine DORA metrics (delivery signal) with SPACE/DX Core 4 (developer experience) and AI-specific metrics (acceptance rate, retention rate, feature utilization depth). Leading indicators for early signal, lagging for confirmed impact.”

**Beat 4 — Governance as enabler:** “Clear guardrails give teams confidence to experiment. I’d use NIST AI RMF to structure risk assessments, OWASP LLM Top 10 for security baselines, and phased rollouts with increasing autonomy as trust is earned.”

**Beat 5 — Business alignment:** “Every initiative ties to the £12m investment ROI. I’d report adoption progress, velocity improvements, and quantified time savings at stakeholder forums, using risk-adjusted ROI that accounts for quality and safety signals.”

This narrative arc — from empathy to platform to measurement to governance to business value — is the complete story of what the AI Enablement PM does. If every answer touches at least two of these beats, you’ll demonstrate the structured, self-directed thinking the JD requires.
