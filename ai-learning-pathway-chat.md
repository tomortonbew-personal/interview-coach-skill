# Conversation Transcript

*Tom Orton-Bew & Claude · March 2026*

-----

**Tom:** Hey Coach! I want to run a full, research level `prep` to produce a highly detailed, focused AI learning pathway. I am focused specifically on the JD (attached) for the Rightmove Technical Product Manager role (AI Enablement), and I’ve also attached the brief prep I did for the screening interview. You have access to my latest, updated `coaching-state.md.md` file in the project files, as well as the CV for this specific role that I submitted.

Your task is to:

1. scrutinise the job description
1. really understand what it is that they are asking for/looking for in a Technical Product Manager
1. take the insights the Talent Acquisition interviewer gave me about what Rightmove are looking for

and produce a highly detailed, focused AI learning pathway that targets every single item on the JD. If you think that there are tangential topics that I would benefit from studying, please include these.

Is my ask clear, before you undertake the full research-level preparation to craft the AI learning pathway?

-----

**Claude:** Your ask is crystal clear. Before I launch, let me pull the relevant project files so the research is grounded in your actual context rather than working from scratch.

*[research and document generation]*

Your AI Enablement Interview Mastery Pathway is ready. It’s a sequenced study plan mapped to every requirement in the Rightmove Technical PM (AI Enablement) job description, organized across three priority tiers. Tier 1 covers AI coding tools (Copilot vs. Cursor vs. JetBrains), DORA metrics and the AI productivity paradox, engineering productivity measurement frameworks (SPACE/DX Core 4), platform engineering principles, and adoption/change management strategies. Tier 2 dives into MCP and agentic AI architectures, AI governance and SSDLC frameworks, LLMOps and observability infrastructure, and Rightmove-specific context. Tier 3 includes differentiating topics like LLM evaluation, AIOps, responsible AI, prompt engineering, and ROI frameworks. The report includes specific resources to study, proof-of-understanding practice questions, guidance on what Andrew and Benny will want to hear, and a consolidated 7-day study schedule.

-----

**Tom:** *[shares LinkedIn post showing an n8n workflow for e-commerce video automation]*

Claude…wow! Incredible! Does it include tools like n8n in there, or can we explore that on a tangent?

I ask as I see posts like this popping up, and I want to understand more about agentic flows.

-----

**Claude:** Good spot — n8n isn’t explicitly in the pathway, but it absolutely belongs in your mental model, and that post is actually a great illustration of why.

What you’re looking at in that LinkedIn post is a multi-agent orchestration pipeline — exactly what the JD references. The n8n canvas in the screenshot is the visual representation of what in the pathway I called an “orchestrator-worker” architecture: one node triggers the flow, specialised nodes handle discrete tasks (scrape, fetch, convert, generate, upload), and the whole thing runs without human intervention. That’s agentic AI in practice — not a chatbot, but a workflow that perceives inputs, executes tools, and produces outputs autonomously.

**Where n8n fits in the learning pathway:**

It’s the practitioner’s route into concepts covered in Tier 2 (MCP, agentic AI architectures) and Tier 3 (prompt engineering for production systems). Rather than reading about orchestration patterns, you *build* them. n8n is particularly relevant to Rightmove because:

- It supports MCP natively (you can wire Claude or other LLMs to internal tools via MCP servers)
- It has a self-hosted option — relevant for governance and data residency discussions
- It’s the closest free tool to what enterprise agentic platforms (like Microsoft’s Agent Framework or Google’s Vertex AI Pipelines) do at scale

**The post itself is a useful case study for interview prep.** The pipeline does five things: scrape → transform → generate → validate → deliver. That structure — trigger, process, generate, check, output — is the skeleton of almost every agentic workflow pattern Andrew Ng describes.

Given that n8n was already on your hands-on shortlist, I’d suggest making your first project something with a direct Rightmove narrative. Rather than the coffee shop finder (which is good for Lovable/maps API but harder to connect to AI enablement), consider building a small developer onboarding flow in n8n — something like: new GitHub repo created → n8n fetches the README → Claude summarises it and suggests documentation gaps → pushes a comment back to the PR. That’s a concrete demonstration of an agentic workflow that maps directly to the “documentation automation” use case in the JD.

Want me to sketch out what that n8n workflow would look like, so you can build it and then reference it in the interview?

-----

**Tom:** I think that sounds amazing, yes please! And yes — please go ahead and create that n8n workflow, **but** as part of a deep dive into n8n itself. I know nothing about it, so an explainer beforehand (what it is, what it’s used for, who created it, so on and so forth) and then yes, the n8n workflow itself.

Also, did I tell you I ended up vibe coding that app with Lovable?

-----

**Claude:** You did NOT tell me about Lovable — that’s brilliant, I want to hear all about it. Drop the details when you’re ready (what you built, how it went, what surprised you) because that’s a concrete hands-on AI story you can use in the interview.

Now — n8n. Let me build this properly.

*[document generation]*

Ten sections, fully formatted. Here’s what’s inside:

What the document covers:

1. What n8n is (including the name origin)
1. Full history — Jan Oberhauser, founding story, funding rounds, licence model
1. Core concepts — nodes, items, triggers, data flow — all explained from scratch
1. n8n vs Zapier vs Make — the comparison table that matters for interviews
1. AI and MCP capabilities — LLM nodes, the AI Agent node, MCP integration
1. Architecture for GCP self-hosting — why it matters for Rightmove specifically
1. **The full 7-node workflow** — Documentation Gap Detector — with the complete Claude prompt, a mock GitHub issue output, and step-by-step build instructions
1. Workflow extension ideas for deeper exploration
1. Two pre-written interview narrative scripts for when you’re asked about hands-on experience
1. Full glossary of n8n concepts

The workflow maps to three JD requirements by name (documentation automation, AI-assisted SSDLC, agentic workflows) and the interview narrative scripts in Section 9 tie your Lovable experience in alongside n8n — so you have two concrete hands-on stories rather than one.

Now — tell me about the Lovable app. What did you build, how did it go, and what surprised you?

-----

**Tom:** *[shares Röster first draft document]*

Amazing Claude, thank you! Well — I have a question for you, but first, as requested, attached is the first draft of my little Lovable project!

-----

**Claude:** Brilliant — let me read it!

*[reads document]*

Tom. This is *genuinely* excellent. Not “good for a non-engineer” excellent — actually excellent, full stop.

Let me tell you what stands out and why it matters for the interview.

**What you built is more impressive than you probably realise.** A PWA with live API integration, custom map markers, deep linking with query parameter detection, a service worker, dark mode, accessibility pass, and a sharable deploy — in under 24 hours. That’s not a toy. That’s a working product.

**The engineering memo is interview gold.** It’s the most useful thing in the document because it shows exactly the mindset Rightmove’s engineering interviewers want to see from a TPM. Specifically:

The section on *what AI-assisted development is actually like* — unreliable for multi-component state changes, subtle CSS bugs require iteration, quality of output is proportional to prompt specificity — is precisely the nuanced, honest take that separates someone who has actually used these tools from someone who has read about them. Andrew and Benny will have seen plenty of candidates claim “AI coding experience.” Almost none of them will have debugged a `beforeinstallprompt` iOS edge case or hit the Places API (New) vs legacy endpoint mismatch.

Your three closing observations are the sharpest part of the whole document:

> *“The distance between idea and working prototype is now measured in hours, not sprints. That changes how we should validate before writing a spec.”*

> *“PMs who can prompt effectively can now run technical experiments independently. That’s a risk if it bypasses architectural review for anything beyond throwaway prototypes.”*

> *“AI-generated code still needs reading.”*

That last one in particular — said plainly, without hedging — is exactly the kind of thing a Head of Technology Operations wants to hear from an AI Enablement PM. It’s not evangelism. It’s judgment.

**The product breakdown is strong too.** The walking time vs distance reasoning, the Favourites/Visited distinction, the location bias implementation — these are genuine product thinking examples, not just feature lists. The *decisions deliberately not made* section is particularly good and directly mirrors how Rightmove thinks about their own product prioritisation.

**Now — your question.** You said you had one before sharing this. What is it?

-----

**Tom:** Thank you Claude! That’s very kind 🙂 I also say it’s my first draft as I think I could share more details out of Lovable into the separate Claude conversation where I pulled this doc together; more on that another time!

The question was…I seem to have caught the Lovable bug 🤣 and I wondered if I could turn your “AI Enablement Interview Mastery Pathway” doc into a personal learning app via Lovable? Don’t do anything about that yet — I simply want to discuss the feasibility and efficacy first 😊

-----

**Claude:** Love that you’ve caught the bug — and love even more that you’re asking the feasibility question first rather than just diving in. That’s the product instinct showing.

Honest answer: **feasible, yes. Efficacious — it depends on what you actually want it to do.**

Let me break that down properly.

**The case for doing it**

The pathway document is long and dense. A learning app could genuinely improve how you consume it — progress tracking (which topics you’ve studied), spaced repetition prompts, a way to surface the “proof of understanding” questions interactively rather than just reading them, a study session timer, a checklist against the 7-day schedule. Those are all things a document can’t do but an app can. And the act of building it in Lovable is itself another hands-on AI story for the interview — you’d be demonstrating that you can identify a personal friction point and build a tool to solve it, which is literally the job description.

**The case for pausing**

The interview timeline is the constraining factor. If the competency interviews with Andrew and Benny are imminent, the time spent prompting, iterating, and debugging Lovable might be better spent actually working through the Tier 1 content. A beautiful learning app that you built instead of studying is a worse outcome than a plain document you actually read.

**The sweet spot**

If you build it, keep the scope ruthlessly narrow. The highest-value version isn’t a full learning platform — it’s something very simple: a card-based question drill app. You paste in the proof-of-understanding questions from the pathway, and the app surfaces them one at a time, lets you rate your confidence (red/amber/green), and tracks which ones you’ve nailed vs. need to revisit. That’s maybe 2-3 hours in Lovable, directly useful for interview prep, and a genuinely good Lovable story in itself.

**The question I’d ask you back:** do you have a date for the next interview stage yet? That’s the variable that determines whether this is a good use of your prep time or a fun distraction.

-----

**Tom:** Thank you Claude for an insightful view of it! I think what I was thinking was:

- the app takes the exact document contents and renders them in “lessons”, or sessions, that I can easily read and consume. The document is incredible, but as you say, it is dense (not a bad thing), but I wonder if I’d find it easier to read the content in the format I just described?
- at the end of each section, I could have a “pop quiz” style learning reinforcer (or whatever medium/format you think best)

What do you reckon?

-----

**Claude:** Honestly? That’s a much better scoped idea than I initially anticipated, and I think it’s worth doing. Here’s my thinking.

**Why this specific concept works**

The document as written is a reference — it’s designed to be comprehensive, not to be consumed linearly in one sitting. What you’re describing is essentially converting it from a *textbook* into a *course*. That’s a genuine UX improvement, not a vanity project. Chunked lessons with a quiz at the end of each one is literally how spaced repetition learning works — you’re not just making it prettier, you’re making the learning more effective.

The pop quiz format is particularly well-suited to this material because most of the Tier 1 and Tier 2 topics require you to be able to *recall and articulate* under pressure — which is exactly what an interview is. Passive reading doesn’t train that. A quiz does.

**What I’d suggest for the app structure**

Keep it brutally simple in Lovable. Ten lessons mapped to the ten sections of the pathway. Each lesson is: a clean, readable rendering of the section content — broken into short scrollable chunks rather than one wall of text — followed by 2-3 quiz questions. Question format matters: I’d go with a mix of multiple choice (fast, confidence-building) and one open-ended “say it out loud” prompt per section — something like *“In one sentence, explain the AI Productivity Paradox to a sceptical engineering director.”* No correct answer to check against; just a prompt that forces you to articulate rather than passively recognise.

Progress state is the other must-have: a simple dashboard showing which lessons are done, which quizzes you’ve passed, and which you’ve flagged for review.

**The one honest caveat**

Lovable will render the text fine, but the quiz logic — tracking scores, flagging weak areas, persisting state across sessions — is exactly the multi-component state management territory you identified in your engineering memo as where Lovable gets unreliable. So: be specific in your prompts, build the content rendering first before touching quiz logic, and don’t try to do both in the same session.

**My suggestion on sequencing**

Before you open Lovable, spend 20 minutes writing out the prompts you’d use. Define the lesson structure, the quiz question formats, and the progress tracking behaviour in plain English first. That document becomes your spec *and* your Lovable prompt sequence. Given what you learned building Röster, you know that prompt specificity is everything — and this app is more stateful than Röster was.

Want me to draft that spec and prompt sequence for you? That way you open Lovable with a plan rather than a vague idea, which based on your own experience is the difference between a clean build and a 3-credit revert.

-----

**Tom:** Thank you so much Claude! Before we continue; could you please put **all** of the text we’ve typed to each other (i.e. my message, your response) — *not* any attachments, artifacts or suchlike — into a simple .md file?

-----

**Claude:** *[this file]*
