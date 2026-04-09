# The Age of Agentic AI

The software paradigm shifted. Yours should too.

**Matej Lukášik** · April 2026

---
<!-- .slide: class="center" -->

## Part I
# The Big Picture

Note: I will start really wide and then zoom in step by step. In this way, your reasoning will be grounded in the big picture and you can make your decisions with more confidence.

---

### We Live in an Information Age

Every company is a software company

Note: Your competitive advantage is determined by how effectively you can leverage software.

---
### The Evolution of Software Distribution

| Era | Medium | Model |
|-----|--------|-------|
| 1980s - 2000s | 💾,💿 Floppy disks, CDs, DVDs  | Physical distribution |
| 2000s - 2025 | 🌐 Web & SaaS | Cloud subscriptions |
| 2025+ | 🤖 Agents | On-demand generation |


Note: Developing and distributing software was difficult and expensive.

First, we had to write it, compile it and then physically distribute it.

Then came the SaaS revolution, when we could distribute the software via the browser. You might not remember, but the fact that companies did not have to contractually commit to a set version of software but instead could sign up, in comparison pay a very low monthly fee and start using the software on every computer that had a browser was revolutionary.

Today, we are entering a new software paradigm, a paradigm of Agentic AI. It is still very early, but this might be the biggest revolutions of all.

---


### The Cost of Software is Collapsing

Instead of:

`
Research tools → Compare pricing →
Sign contract → Learn UI
`
<!-- .element: style="font-size: 0.5em" -->
You can:

```bash
$ claude "build me a tool that does X"
# → Working software in minutes
```


Note: You used to:
- identify a problem in the company
- research tools
- judge whether they are compatible with what you are already using 
- decide on the tier and the number of seats
- onboard everyone in the company to use them.

__AND STILL HOWEVER MUCH you tried, the software never did everything you needed, and you always thought "If only it could do X"__

With the advent of capable coding agents like claude code or codex you can sit down and write the exact software you need in minutes.

---
<!-- .slide: class="center" -->

### KEY TAKEWAY

change your thinking from:

#### "What tool should I subscribe to next to solve my problem?"

to:

#### "How do I specify this well enough so that my coding agent can build it in one shot?"


Note: Because the cost of software creation is collapsing, it no longer makes sense to subscribe to services that does not fit you very well and you can build them to fit your needs exactly.

**HOWEVER** our thinking has not adjusted yet. We are looking at new AI powered products and comparing how much each costs on a monthly basis and whether the service has all the bells and whistles we are looking for. This is an old paradigm thinking applied to new paradigm. In the new paradigm, intelligence is on tap via API and you use this intelligence in a sovereign manner to suit your needs exactly.

---
<!-- .slide: class="center" -->

## Part II

# What is an AGENT?

---

### Brain + Tools + Memory + Agency =
## Agent 

---

BRAIN -> reasons about the next best step

---
<!-- .slide: class="compact-code" style="padding: 0; top: 0 !important; height: 700px" -->
```python
# Step 1: ask for a plan
planning_response = client.messages.create(
    model="claude-opus-4-6",
    system="You are an operations agent. When given a task, first output a numbered plan. Be specific.",
    messages=[{"role": "user", "content": "Assess whether our mining is profitable right now."}]
)

# model returns:
# "1. Fetch current BTC price
#  2. Fetch current network difficulty
#  3. Fetch our hashrate and power cost
#  4. Calculate revenue vs cost
#  5. Return a verdict"

plan_steps = parse_plan(planning_response)  # split on numbered lines

# Step 2: execute each step, feeding results back as context
for step in plan_steps:
    response = client.messages.create(
        model="claude-opus-4-6",
        system="Execute this single step. Use tools if needed. Be concise.",
        messages=conversation + [{"role": "user", "content": f"Current step: {step}"}]
    )
    conversation.append({"role": "assistant", "content": response.content[0].text})
```
<!-- .element: style="font-size: 0.44em; line-height: 1.04; white-space: pre-wrap; max-height: none; margin: 0; width: 100%; height: 700px; padding: 1em 1.05em" -->

---

TOOLS -> lets it browse the web, call APIs, edit files, send messages and execute code

---
<!-- .slide: class="compact-code" style="padding: 0; top: 0 !important; height: 700px" -->
```python
# What YOU write (clean API call):
response = client.messages.create(
    model="claude-opus-4-6",
    tools=tools,
    messages=[{"role": "user", "content": "Is mining profitable right now?"}]
)

# What the model ACTUALLY sees (roughly — Anthropic injects this into the context):
"""
You have access to the following tools:

<tools>
  <tool>
    <name>get_btc_price</name>
    <description>Fetch the current Bitcoin price in USD</description>
    <input_schema>{"type": "object", "properties": {}}</input_schema>
  </tool>
  <tool>
    <name>get_hashrate</name>
    <description>Fetch current hashrate from the mining dashboard</description>
    <input_schema>{"type": "object", "properties": {"rig_id": {"type": "string"}}}</input_schema>
  </tool>
</tools>

If a tool is appropriate, respond with a tool_use block.
If no tool is needed, respond directly.

User: Is mining profitable right now?
"""

# Model responds with:
# {"type": "tool_use", "name": "get_btc_price", "input": {}}
# — your code executes it, result goes back into context, loop continues
```

<!-- .element: style="font-size: 0.44em; line-height: 1.04; white-space: pre-wrap; max-height: none; margin: 0; width: 100%; height: 700px; padding: 1em 1.05em" -->
---

MEMORY -> keeps context across time

---
```python
import anthropic
import numpy as np

client = anthropic.Anthropic()

# --- WRITE: storing a memory ---
fact = "Rig #12 was replaced on 2025-11-03 due to a failed PSU."

embed_response = client.messages.create(  # in practice: use a dedicated embeddings API
    model="claude-opus-4-6",              # e.g. OpenAI embeddings or a local model
    ...
)
vector = get_embedding(fact)   # → [0.021, -0.843, 0.374, ...]  (1536 floats)
vector_db.store(vector, metadata={"text": fact, "date": "2025-11-03", "rig": 12})

# --- READ: at the start of every agent run ---
query = "Is rig #12 behaving normally?"
query_vector = get_embedding(query)

# fetch the top 3 most semantically similar memories
results = vector_db.search(query_vector, top_k=3)
# → ["Rig #12 was replaced on 2025-11-03 due to a failed PSU.",
#    "Rig #12 average hashrate: 98 TH/s",
#    "Rig #12 flagged for elevated temp on 2025-10-28"]

# inject only the relevant memories into the system prompt
system_prompt = f"""You are an operations agent.

Relevant context from memory:
{chr(10).join(results)}

Use this context when answering. Do not hallucinate hardware history."""
```

---

AGENCY -> means it can decide and act in a loop

---

```python
messages = [{"role": "user", "content": user_input}]

while True:
    response = client.messages.create(
        model="claude-opus-4-6",
        system=system_prompt,
        tools=tools,
        messages=messages
    )

    if response.stop_reason == "end_turn":
        print(response.content[0].text)
        break                                    # agent is done

    if response.stop_reason == "tool_use":
        tool_call = response.content[0]
        result = execute_tool(tool_call.name, tool_call.input)  # your code runs here

        messages.append({"role": "assistant", "content": response.content})
        messages.append({"role": "user", "content": [{
            "type": "tool_result",
            "tool_use_id": tool_call.id,
            "content": str(result)
        }]})
        # ↑ loop continues — model sees the result and decides next step
```

---


### Agentic AI FOMO

Note: One of the reasons we are having this workshop right now is that there is so much hype and almost a sense of FOMO around agents.

There is also the counternarrative of AI being useless, slop machines and stories of agentic worklflows gone terribly wrong.


## Part III
# The Use Cases

Note: The truth is somewhere in the middle. Let's go through some of the ways agents are being used right now.

---

## Pull, Don't Push

Old software makes humans poll systems for updates.

Agentic software flips the flow:
- Watches inboxes, dashboards, feeds, and databases
- Pulls out what changed
- Summarizes what matters
- Routes it to the right person
- Takes the next step when allowed

**The interface matters less. The outcome matters more.**

Note: Software used to be something you had to go check. With agents, the software starts working in the background and brings you the delta, not the raw stream.

---

## Everything Becomes Data

To work well, agents need machine-readable context:

- **Meetings** → Transcripts, owners, deadlines
- **Decisions** → Rationale, tradeoffs, approvals
- **Processes** → States, triggers, handoffs
- **Knowledge** → Indexed docs and searchable repositories
- **Systems** → APIs, exports, and event streams

**If agents cannot read it and write back to it, the workflow stays manual.**

Note: This is why data readiness matters so much. If important context only lives in people's heads, scattered screenshots, or closed interfaces, your agents stay blind.

---

## Intelligence on Tap

# ⚡ = 🧠

Reasoning starts to look like infrastructure:

- On-demand
- Metered
- Embedded into every workflow
- Swappable by price, speed, or privacy
- Expected everywhere, noticed nowhere

You will not buy software for every edge case.

You will route intelligence into the process.

Note: This is the bridge into the next section. Once intelligence becomes infrastructure, the obvious questions become who controls it, where it runs, and what happens to your data.

---

<!-- .slide: class="center" -->

## Part III

# Sovereignty

---

## Why Sovereignty Matters

- **Data privacy** — Your data never leaves your infrastructure
- **Compliance** — Meet regulatory requirements (GDPR, industry-specific)
- **Control** — No vendor lock-in, no API changes breaking workflows
- **Cost predictability** — Own your compute, control your costs
- **Censorship resistance** — No content policies blocking legitimate use cases

---

## Running on Your Hardware

The sovereign AI stack:

| Layer | Options |
|-------|---------|
| Models | Llama 3, Mistral, Qwen — open weights |
| Inference | Ollama, llama.cpp, vLLM, LM Studio |
| Orchestration | OpenClaw, LangChain, CrewAI |
| Routing | LiteLLM, Routstr |

---

## Routstr: Decentralized AI Routing

- **Permissionless** — No accounts, no sign-ups
- **Private** — Pay with Cashu eCash tokens via Bitcoin Lightning
- **OpenAI-compatible** — Drop-in replacement for existing code
- **Monetize your hardware** — Run the proxy, earn from inference

```python
# Point your OpenAI SDK at any Routstr provider
# Use a Cashu token as your API key
client = OpenAI(base_url="https://routstr-provider.com")
```

---

<!-- .slide: class="center" -->

## Part IV

# Agentic AI Deep Dive

---

## The Spectrum of Autonomy

| Type | Control | Use Case |
|------|---------|----------|
| **Single LLM** | User-driven, stateless | One prompt → one response |
| **Agentic Workflows** | Predefined paths, managed state | Structured multi-step processes |
| **Autonomous Agents** | LLM-directed, memory | Open-ended goal pursuit |

A smaller model in an agentic workflow hit **95.1%** on HumanEval — vs 67% for the best model alone.

**Architecture beats model size.**

---

## OpenClaw

**247K+ GitHub stars in 60 days** — fastest-growing OSS project ever

- Runs locally on Mac, Windows, Linux
- 100+ built-in skills
- Multi-channel inbox (WhatsApp, Telegram, Slack, Discord...)
- Browser control, file system access, shell commands
- Works with Claude, GPT, or local models

> "Probably the single most important release of software, probably ever."

*— Jensen Huang, March 2026*

---

## OpenClaw Alternatives

| Tool | Focus | Codebase | RAM |
|------|-------|----------|-----|
| **OpenClaw** | Full-featured | 430K lines | 390 MB |
| **Nanobot** | Simplicity | 4K lines | 50 MB |
| **ZeroClaw** | Edge, security | Rust | 5 MB |
| **PicoClaw** | Ultra-light, IoT | Go | <10 MB |
| **CrewAI** | Multi-agent | Python | Varies |

---

## Autoresearch

Andrej Karpathy's experiment: **let AI conduct ML research overnight**

- Agent modifies `train.py`, runs 5-min experiments
- Evaluates results, keeps improvements, discards failures
- ~12 experiments/hour → 100+ iterations overnight
- Wake up to improved models + detailed logs

**This is the future: AI agents that improve themselves.**

[github.com/karpathy/autoresearch](https://github.com/karpathy/autoresearch)

---

<!-- .slide: class="center" -->

## Part V

# Actions You Can Take Now

---

## Start Tomorrow

**1. Spin up a VPS with Docker**

One container per employee with OpenClaw (or ZeroClaw for lower overhead)

**2. Give each employee a token budget**

$100/month is enough to explore — tracks usage and builds intuition

**3. Start small, find the friction**

Look for repetitive tasks: reports, data extraction, formatting, scheduling

---

## What to Automate First

- **Meeting summaries** → Transcribe, extract actions, send follow-ups
- **Report generation** → Pull data, format, distribute on schedule
- **Email triage** → Categorize, draft responses, flag urgent items
- **Research tasks** → Gather info, summarize, present findings
- **Code review prep** → Initial pass, flag issues, suggest improvements

**ROI: 300–500% within 6 months** is typical for well-chosen use cases.

---

<!-- .slide: class="center" -->

## Part VI

# How I Can Help

---

## Services

**🎯 Consulting & Advisory**

Assess workflows, identify high-impact automation opportunities, build adoption roadmap. Avoid the 40% of AI projects that fail due to poor data readiness.

**🔧 Implementation**

Design and deploy custom AI agents tailored to your processes. From single-task automations to multi-agent orchestration.

**📚 Training & Workshops**

Hands-on sessions for your team. From prompt engineering to production agent workflows. Build internal capability, not dependency.

---

## Engagement Options

| Format | Duration | Outcome |
|--------|----------|---------|
| **Discovery Session** | Half-day | Top 3 automation candidates |
| **Pilot Project** | 2–4 weeks | Working agent for one workflow |
| **Team Workshop** | 1–2 days | Hands-on skills for engineers |
| **Full Implementation** | 1–3 months | Production-ready infrastructure |

---

<!-- .slide: class="center" -->

## The Bottom Line

# Software is becoming instant.

The companies that adapt fastest will have an insurmountable advantage.

The barrier isn't technology — it's mindset.

---

<!-- .slide: class="center" -->

# Thank You

**Matej Lukašík**

Questions?

*Slides and resources available after the talk*
