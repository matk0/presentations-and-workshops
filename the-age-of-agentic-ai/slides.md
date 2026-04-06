# The Age of Agentic AI

The software paradigm shifted. Yours should too.

**Matej Lukášik** · April 2026

---
<!-- .slide: class="center" -->

## Part I

# The Big Picture

---

## We Live in an Information Age

###### Every company is a software company

Your competitive advantage is determined by how effectively you can leverage software.

---

## The Evolution of Software Distribution

| Era | Medium | Model |
|-----|--------|-------|
| 1980s - 2000s | 💾,💿 Floppy disks, CDs, DVDs  | Physical distribution |
| 2000s - 2025 | 🌐 Web & SaaS | Cloud subscriptions |
| 2025+ | 🤖 Agents | On-demand generation |

Note: You're awesome!

---

## The Old Model

**Physical Era**
- Company builds software
- Packages it on media
- Ships to customers

**SaaS Era**
- Company builds software
- Hosts in the cloud
- Customers access via browser

**Common thread:** You depend on someone else to build it.

---

## The Paradigm Shift

> "We see a future where intelligence is a utility like electricity or water and people buy it on a meter."

*— Sam Altman, 2026 Infrastructure Summit*

The barrier to software creation has collapsed.

---

## It's Always Been About Cost

**Before:**
- $15K–$150K+ for custom software
- 4–6 month development cycles
- Specialized talent required
- Research → Evaluate → Pay → Wait

**Now:**
- LLM API costs dropped 80% YoY
- Inference costs falling 10x annually
- 30–50% developer productivity gains
- Describe → Generate → Use

---

## The New Reality

Instead of:

```
Research tools → Compare pricing → Sign contract → Wait → Learn UI
```

You can:

```bash
$ claude "build me a tool that does X"

→ Working software in minutes
```

---

<!-- .slide: class="center" -->

## Part II

# Mindset Shifts

---

## Pull, Don't Push

**Old Way** — You go out to find information:
- Check dashboards
- Read email newsletters
- Browse news sites
- Query databases

**New Way** — Agents pull information to you:
- Summarized and prioritized
- Delivered when relevant
- In formats you prefer
- With context attached

---

## Everything Becomes Data

Transform all company functions into formats agents can consume:

- **Meetings** → Transcripts + action items in `.md`
- **Decisions** → Documented rationale with context
- **Processes** → Structured workflows agents can execute
- **Knowledge** → Indexed, searchable, agent-accessible

**If it's not machine-readable, it doesn't exist to your agents.**

---

## Intelligence on Tap

# ⚡ = 🧠

Just as you don't think about how electricity reaches your outlet:

- Intelligence becomes infrastructure
- Available instantly, billed by usage
- Abstracted complexity
- Commodity pricing

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
