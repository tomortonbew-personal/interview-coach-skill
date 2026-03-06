+———————————————————————–+
| **n8n**                                                               |
|                                                                       |
| A Complete Deep Dive                                                  |
|                                                                       |
| *What it is · How it works · Why it matters for Rightmove AI          |
| Enablement*                                                           |
+———————————————————————–+

+———————————————————————–+
| **📌 How to use this document**                                       |
|                                                                       |
| This is a sequenced deep dive: start at the top and work down. Each   |
| section builds on the one before it. The final section contains your  |
| hands-on workflow — a practical n8n build you can reference in your |
| Rightmove interviews to demonstrate real agentic AI experience.       |
+———————————————————————–+

**1. What is n8n?**

n8n (pronounced 'nodemation') is an open-source workflow automation
platform that lets you connect applications, services, and APIs to build
automated pipelines — without writing code for every integration.
Think of it as the infrastructure layer that makes services talk to each
other.

The name is a numeronym: n + 8 letters + n = 'nodemation'. It sits in
the same category as Zapier and Make (formerly Integromat), but with
critical differences that make it significantly more powerful for
technical users and enterprises.

+———————————————————————–+
| **🎯 One-sentence definition**                                        |
|                                                                       |
| n8n is a workflow automation tool where you visually connect nodes    |
| — each node being a trigger, action, or transformation — to build |
| automated pipelines that run with zero manual intervention.           |
+———————————————————————–+

**2. Origin and History**

**Who built it**

n8n was founded by Jan Oberhauser, a German developer who built the
first version over a weekend in 2019 and open-sourced it immediately.
The name came from him thinking about 'node automation' and shortening
it. He ran it as a solo project for several months before it gained
traction.

-----

**Milestone**         **Detail**

Founded               2019 — solo project by Jan Oberhauser

Open-sourced          2019 — immediately on launch, hosted on GitHub

Company formed        n8n GmbH, Berlin, Germany

Series A              $12M led by Sequoia Capital (2021)

Series B              $35M led by Felicis Ventures (2023)

Series C              $60M led by Highland Europe (2024)

Current valuation     ~$220M (2024)

GitHub stars          ~50,000+ (one of the fastest-growing automation
tools)

Self-hosted installs  500,000+

Cloud users           100,000+

-----

**Licensing model — the important nuance**

n8n uses a 'fair-code' licence called the Sustainable Use Licence.
This means:

- Free to self-host for internal use (including commercial use inside
  your own organisation)
- Cannot be offered as a hosted service to third parties without a
  commercial licence
- All source code is always available — no black boxes

This is why n8n is the right choice for enterprise AI enablement: you
can self-host it on GCP (Rightmove's cloud provider), keep all data
internal, and never worry about sensitive internal data transiting a
third-party SaaS platform.

**3. Core Concepts — How n8n Works**

**The fundamental building blocks**

-----

**Concept**        **What it is**             **Analogy**

Workflow           A complete automation —  A recipe
a connected graph of nodes
that executes a process

Node               A single step in a         A step in the recipe
workflow — a trigger,  
action, or transformation

Trigger node       The starting node —      The alarm clock that
watches for an event       starts the recipe
(webhook, schedule, file  
change, etc.)

Action node        Does something — calls   An instruction in the
an API, queries a          recipe
database, sends a message

Data               Reshapes or filters data   Adjusting the recipe
transformation     passing between nodes      mid-cook
node               (Set, Function, IF,  
Switch, etc.)

Execution          A single run of a workflow One completed dish
— triggered once,  
produces a result

Credential         Stored authentication (API The pantry — stored
keys, OAuth tokens) used   ingredients
by nodes securely

-----

**How data flows**

n8n passes data between nodes as JSON objects called 'items'. Each
node receives items, processes them, and passes items to the next node.
Multiple items can be processed in parallel (batch mode) or one by one.

+———————————————————————–+
| **💡 Key principle**                                                  |
|                                                                       |
| Every node in n8n receives input items and outputs items. The shape   |
| of the data can change at every step — a trigger node might output  |
| a single JSON object with a GitHub webhook payload; a transformation  |
| node might split it into 10 items (one per file changed); an action   |
| node might send all 10 to Slack as individual messages. Data          |
| transformation is first-class.                                        |
+———————————————————————–+

**Trigger types — how workflows start**

- Webhook trigger: an external service sends an HTTP POST to n8n's
  URL (e.g., GitHub sends a pull request event)
- Schedule trigger: runs on a cron schedule (e.g., every day at 9am)
- File/directory watch: watches for changes in a folder
- Manual trigger: you click 'Execute' — useful for testing and
  one-off runs
- Event trigger: listens to a specific event from a connected service
  (e.g., 'new row in Airtable', 'new email in Gmail')
- Sub-workflow trigger: called by another n8n workflow

**The node library — what you can connect**

n8n has 400+ built-in integrations. The ones most relevant to developer
enablement and AI workflows:

-----

**Category**       **Examples**               **Relevance to AI
Enablement**

Version control    GitHub, GitLab, Bitbucket  Trigger workflows on PR
events, code changes, repo
creation

AI / LLMs          OpenAI, Anthropic, Google  Call LLMs within workflows
Gemini, Ollama,            for generation,
HuggingFace                summarisation, analysis

Communication      Slack, Teams, Gmail,       Send notifications,
Outlook                    reports, alerts to
engineering teams

Project management Jira, Linear, Asana,       Create issues, update
Notion                     tickets, pull context for
AI prompts

Data / storage     Google Sheets, Airtable,   Read/write data, log
Postgres, MySQL, Redis     results, maintain state

HTTP / API         HTTP Request node          Call any REST API —
(generic)                  including internal
Rightmove APIs

Code               JavaScript Function node,  Write custom logic when no
Python node                native node exists

Files              Read/Write files, Google   Handle file
Drive, S3                  inputs/outputs, store
artefacts

Scheduling         Cron node                  Run workflows on any
schedule

-----

**4. n8n vs Zapier vs Make — The Key Differences**

-----

**Dimension**      **n8n**                    **Zapier**

Pricing model      Free self-hosted; cloud    $20–$799/month (per
from ~$20/month          task volume)

Self-hosting       Yes — Docker,            No — SaaS only
Kubernetes, bare metal

Code support       Full JavaScript/Python     Very limited (Zapier Code
nodes                      step)

Data privacy       All data stays in your     Data transits Zapier's
infrastructure             servers

AI integration     Native LLM nodes, MCP      Basic — Zapier Central
support, AI agents         is immature

Complexity ceiling Very high — loops,       Medium — linear flows,
branches, sub-workflows,   complex branching is
error handling             clunky

Community          Large open-source          Large but closed ecosystem
community, 50K+ GitHub  
stars

Best for           Technical teams,           Non-technical users,
enterprises, AI pipelines  simple integrations

-----

+———————————————————————–+
| **🏢 Why n8n is the right tool for enterprise AI enablement**         |
|                                                                       |
| n8n's self-hosting capability is the deciding factor for enterprise  |
| use. An organisation like Rightmove cannot send internal code,        |
| incident data, or engineering telemetry through Zapier's cloud. n8n  |
| deployed on GCP (Rightmove's cloud) keeps everything inside the      |
| security perimeter — and integrates with the same IAM, VPC, and     |
| logging infrastructure the engineering team already manages.          |
+———————————————————————–+

**5. n8n's AI and MCP Capabilities**

**Why n8n matters specifically for AI workflows**

n8n added first-class AI support in 2024, making it one of the few
automation platforms that treats AI as a native primitive — not an
afterthought integration.

**Built-in LLM nodes**

- Anthropic Claude node: call any Claude model with custom system
  prompts and user messages
- OpenAI node: GPT-4o, GPT-4o mini, o1 — completions, function
  calling, image analysis
- Google Gemini node: Gemini 2.0 Flash, Gemini Pro — especially
  relevant given Rightmove's GCP partnership
- Ollama node: run open-source models locally (Llama 3, Mistral,
  Phi-3) for zero-cost, air-gapped inference
- HuggingFace node: access 300,000+ open models

**MCP integration**

n8n added native MCP support in 2024. This is critically important for
this interview context — it means n8n can act as an MCP client,
connecting AI models within your workflows to any MCP server.

In practice, this means: *an n8n workflow can trigger Claude (via the
Anthropic node), pass it a task, and Claude can use MCP tools to query
your internal Jira board, fetch documentation from Confluence, run a
code search against GitHub, and return a structured result — all
within a single automated workflow.* This is the exact pattern the
Rightmove JD describes as 'internal AI agents supporting SSDLC tasks'.

**AI agent node**

n8n has a dedicated 'AI Agent' node that implements the ReAct
(Reasoning + Acting) pattern: the agent can use tools, observe results,
and loop until it completes the task. You connect it to a language model
and a set of tools (which can include other n8n nodes). This is the
simplest path to agentic workflows without writing custom agent
frameworks like LangGraph.

**6. n8n Architecture — Self-Hosted on GCP**

**Deployment options**

- Docker Compose: simplest setup, single server, suitable for small
  teams
- Kubernetes (GKE): production-grade, auto-scaling, high availability
  — Rightmove's natural choice
- n8n Cloud: managed SaaS — not suitable for enterprise sensitive
  data
- Queue mode: Redis + worker nodes for high-volume parallel execution

**Components in a production deployment**

-----

**Component**         **Role**

n8n main process      API server, UI, workflow management, scheduling

Worker processes      Execute workflow runs in parallel (queue mode)

PostgreSQL            Stores workflows, credentials, execution history

Redis                 Queue for job distribution between workers

Reverse proxy         TLS termination, URL routing
(nginx/Traefik)

Persistent volume     Stores files, binary data

-----

+———————————————————————–+
| **🔒 Security note for the interview**                                |
|                                                                       |
| In an enterprise deployment, n8n credentials (API keys for GitHub,    |
| Slack, LLMs, etc.) are stored encrypted in PostgreSQL. Access to the  |
| n8n instance itself is controlled via SSO/LDAP integration. Workflows |
| can be version-controlled in Git. For Rightmove, this means n8n slots |
| neatly into the existing platform engineering model — GKE           |
| deployment, Terraform-managed infrastructure, GCP IAM for access      |
| control, and Cloud Logging for execution observability.               |
+———————————————————————–+

**7. The Hands-On Workflow — Documentation Gap Detector**

+———————————————————————–+
| **🎯 What this workflow does**                                        |
|                                                                       |
| When a new GitHub repository is created at Rightmove, this workflow   |
| automatically: fetches the README, passes it to Claude for analysis,  |
| identifies documentation gaps, and posts a structured comment back to |
| the repository as a GitHub issue. It demonstrates AI-assisted         |
| documentation automation — one of the five use cases listed in the  |
| Rightmove JD.                                                         |
+———————————————————————–+

**Why this workflow is interview gold**

It maps directly to three JD requirements: **documentation automation**
(AI generating docs from code), **AI-assisted SSDLC tasks** (improving
engineering workflow quality), and **agentic workflows** (a multi-step
autonomous pipeline). It also demonstrates MCP-adjacent thinking and is
something you actually built — which is worth ten times more than
reading about it.

**Workflow architecture overview**

The workflow has 7 nodes, each doing a discrete job. Data flows top to
bottom.

+—+——————————————————————+
| * | **⚡ GitHub Webhook Trigger**                                    |
| * |                                                                  |
| 1 | Listens for 'repository.created' events from Rightmove's      |
| * | GitHub organisation. When a new repo is created, GitHub sends a  |
| * | webhook POST to n8n with the repository metadata (name,          |
|   | description, owner, URLs).                                       |
+—+——————————————————————+

↓

+—+——————————————————————+
| * | **🌐 HTTP Request — Fetch README**                             |
| * |                                                                  |
| 2 | Makes a GET request to the GitHub Contents API: GET              |
| * | /repos/{owner}/{repo}/contents/README.md. Returns the raw README |
| * | content (base64-encoded). If no README exists, this node returns |
|   | a 404 — handled by the next node.                              |
+—+——————————————————————+

↓

+—+——————————————————————+
| * | **⚙️ IF Node — README exists?**                                |
| * |                                                                  |
| 3 | Branches the workflow: if the HTTP request returned a 200,       |
| * | proceed to analysis. If 404 (no README), route to a separate     |
| * | branch that creates a 'Missing README' issue immediately,      |
|   | skipping the AI analysis step.                                   |
+—+——————————————————————+

↓

+—+——————————————————————+
| * | **🔄 Function Node — Decode README**                           |
| * |                                                                  |
| 4 | The README content arrives base64-encoded from the GitHub API.   |
| * | This JavaScript Function node decodes it:                        |
| * | Buffer.from(item.json.content, 'base64').toString('utf8').   |
|   | Also extracts repo name, description, and primary language from  |
|   | the webhook payload.                                             |
+—+——————————————————————+

↓

+—+——————————————————————+
| * | **🤖 Anthropic Claude Node — Analyse Gaps**                    |
| * |                                                                  |
| 5 | Sends the decoded README to Claude with a structured system      |
| * | prompt. The prompt instructs Claude to act as a senior developer |
| * | reviewing internal documentation and to return a JSON object     |
|   | with four fields: overall_score (1–10), missing_sections (array |
|   | of strings), improvement_suggestions (array of strings), and     |
|   | priority (high / medium / low). Temperature set to 0 for         |
|   | consistent, deterministic output.                                |
+—+——————————————————————+

↓

+—+——————————————————————+
| * | **⚙️ Function Node — Format Issue Body**                       |
| * |                                                                  |
| 6 | Takes Claude's JSON response and formats it into a Markdown     |
| * | GitHub issue body. Creates a structured comment with a score     |
| * | badge, a checklist of missing sections, and prioritised          |
|   | suggestions. Keeps the output human-readable, not raw JSON.      |
+—+——————————————————————+

↓

+—+——————————————————————+
| * | **📋 GitHub Node — Create Issue**                              |
| * |                                                                  |
| 7 | Creates a GitHub issue on the new repository with the formatted  |
| * | Markdown body. Labels it 'documentation' and 'ai-generated'. |
| * | Assigns it to the repository owner. The engineering team sees it |
|   | in their normal GitHub workflow — no new tool to learn.        |
+—+——————————————————————+

**The Claude prompt (Node 5)**

+———————————————————————–+
| **SYSTEM PROMPT**                                                     |
|                                                                       |
| You are a senior software engineer reviewing internal repository      |
| documentation. Your job is to identify gaps, missing sections, and    |
| improvement opportunities in README files. You must return ONLY valid |
| JSON — no prose, no markdown fences.                                |
|                                                                       |
| Return this exact structure:                                          |
|                                                                       |
| { "overall_score": <1-10>, "missing_sections": ["section1",  |
| ...], "improvement_suggestions": ["suggestion1", ...],       |
| "priority": "high|medium|low" }                                 |
|                                                                       |
| **USER MESSAGE**                                                      |
|                                                                       |
| Repository: {{$json.repo_name}} | Language:                         |
| {{$json.language}}\n\nREADME content:\n{{$json.readme_content}}  |
+———————————————————————–+

**What the output looks like**

The workflow creates a GitHub issue that looks like this in the
repository:

+———————————————————————–+
| **📋 [AI] Documentation Review — payment-service**                |
|                                                                       |
| *Labels: documentation · ai-generated | Priority: HIGH*              |
|                                                                       |
| **Documentation Score: 4 / 10**                                       |
|                                                                       |
| **Missing sections:**                                                 |
|                                                                       |
| -   [ ] Installation and local setup instructions                   |
|                                                                       |
| -   [ ] API endpoint documentation                                  |
|                                                                       |
| -   [ ] Environment variable reference                              |
|                                                                       |
| -   [ ] Contributing guidelines                                     |
|                                                                       |
| **Suggestions:**                                                      |
|                                                                       |
| -   Add a quickstart section — the repo has no onboarding path for  |
|     new engineers                                                     |
|                                                                       |
| -   The architecture section exists but references services that no   |
|     longer exist                                                      |
|                                                                       |
| *Generated automatically by the AI Documentation Reviewer workflow ·  |
| Rightmove AI Enablement*                                              |
+———————————————————————–+

**How to build this in n8n**

1. Sign up for n8n Cloud (free tier: 5 workflows, 2,500
   executions/month) at app.n8n.cloud. No installation needed — you
   can run this entirely in the browser.
1. Create a new workflow and name it 'Documentation Gap Detector'.
1. Add a Webhook node as the trigger. Set the HTTP method to POST. Copy
   the webhook URL that n8n generates — you will register this with
   GitHub.
1. In your GitHub account or organisation settings, go to Webhooks and
   add a new webhook. Paste the n8n URL. Set Content type to
   application/json. Under events, select Repositories (which includes
   repository.created events).
1. Add an HTTP Request node connected to the Webhook. Set method to
   GET. Set URL to:
   https://api.github.com/repos/{{$json.body.repository.full_name}}/contents/README.md
   — this uses n8n's expression syntax to pull the repo name from
   the incoming webhook data.
1. Add an IF node. Set the condition to: {{$json.status}} equals 200.
   Connect the true branch forward and the false branch to a separate
   GitHub issue node that creates a 'Missing README' issue.
1. Add a Function node (JavaScript). Paste the decoding logic: const
   content = Buffer.from($input.item.json.content,
   'base64').toString(); return [{json: {readme_content: content,
   repo_name: $('Webhook').item.json.body.repository.name, language:
   $('Webhook').item.json.body.repository.language}}];
1. Add an Anthropic node. Select the Claude Sonnet model. Paste the
   system prompt from Section 7 above. In the user message field, use
   n8n expressions to pull in the repo name, language, and decoded
   README content.
1. Add a second Function node to format the GitHub issue body from
   Claude's JSON response. Parse the JSON, build a Markdown string
   with the score, missing sections checklist, and suggestions.
1. Add a GitHub node. Select the 'Create Issue' operation. Set the
   owner and repo fields using n8n expressions from the original
   webhook payload. Set the title, body, and labels fields.
1. Test end-to-end by creating a test repository in GitHub with a
   minimal README. You should see the workflow execute in n8n's
   Executions view and a new issue appear in your repository within
   seconds.

**8. Extending the Workflow — Ideas for Deeper Exploration**

Once the base workflow is working, these extensions add significant
interview value:

- Add a Slack notification node in parallel with the GitHub issue —
  post a message to #engineering-enablement summarising the score and
  top gaps for visibility across teams
- Add a Google Sheets / Airtable logging node to build a documentation
  health dashboard — track scores over time and identify teams/repos
  that consistently score low
- Extend the IF branch to handle different repository types (service
  vs. library vs. tooling) — adjust the Claude prompt and scoring
  criteria per type
- Add a second workflow that triggers when the issue is closed —
  re-runs the analysis to confirm the gaps were addressed and updates
  the score in the dashboard
- Replace the static Anthropic node with an n8n AI Agent node and give
  it GitHub tools via MCP — the agent can then proactively fetch the
  actual code files to cross-check whether the README matches reality

**9. The Interview Narrative — How to Talk About This**

+———————————————————————–+
| **💬 When asked about hands-on AI experience**                        |
|                                                                       |
| "I've been actively hands-on with two tools specifically to build   |
| concrete experience I can bring into this role. The first is Lovable, |
| which I used to vibe-code a functional web app — that gave me       |
| direct experience of AI-assisted generation and understanding where   |
| the human judgment layer is still essential. The second is n8n, where |
| I built a documentation gap detection workflow: when a new GitHub     |
| repository is created, the workflow fetches the README, passes it to  |
| Claude with a structured prompt, and creates a formatted GitHub issue |
| listing documentation gaps and a quality score. It runs completely    |
| autonomously — trigger to output with no manual intervention. That  |
| maps directly to the documentation automation and AI-assisted SSDLC   |
| use cases in your JD. What I found most interesting building it       |
| wasn't the AI part — it was designing the governance layer:        |
| deciding what temperature to set for deterministic output, how to     |
| handle the case where no README exists, and how to make the output    |
| actionable for an engineer rather than just informative."            |
+———————————————————————–+

+———————————————————————–+
| **💬 When asked about agentic workflows**                             |
|                                                                       |
| "n8n gave me a very practical understanding of what 'agentic'      |
| actually means in a production context. The workflow I built is a     |
| simple agent: it has a goal (assess documentation quality), it uses   |
| tools (GitHub API, Claude), and it produces a structured output       |
| without human intervention at each step. What it taught me is that    |
| the interesting design decisions aren't the AI model choice —      |
| they're the branching logic, error handling, and output formatting   |
| that make the workflow reliable and the output genuinely useful to    |
| the engineer who sees it."                                           |
+———————————————————————–+

**10. Quick Reference — n8n Concepts Glossary**

-----

**Term**              **Definition**

Workflow              A saved automation — a directed graph of nodes
with a trigger and one or more action paths

Node                  A single step: trigger, action, transformation,
or logic branch

Item                  A JSON data object that flows between nodes —
the unit of data in n8n

Expression            Dynamic value using n8n syntax:
{{$json.fieldName}} or
{{$('NodeName').item.json.field}}

Credentials           Stored, encrypted authentication (API keys,
OAuth) — reusable across workflows

Execution             One complete run of a workflow — visible in the
Executions tab with full input/output per node

Sub-workflow          A workflow called by another workflow — enables
modularity and reuse

Error workflow        A dedicated workflow that runs when another
workflow fails — handles alerting and recovery

Queue mode            Production deployment mode: Redis queues jobs,
multiple worker processes execute them in
parallel

AI Agent node         Built-in node implementing ReAct pattern — uses
tools, observes results, loops until task
complete

MCP node              n8n node that connects to an MCP server —
exposes MCP tools as n8n actions within a
workflow

Pinned data           Fixture data saved on a node for
development/testing — lets you build without a
live trigger

Wait node             Pauses workflow execution — waits for time,
webhook callback, or form submission before
continuing

-----

*Prepared for Tom Orton-Bew · Rightmove Technical PM (AI Enablement)
Interview Preparation · March 2026*
