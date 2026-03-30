# Paperclip — Overview

[[Technical|← Technical]] | [[FOLIO — Venture Overview]]

**GitHub:** https://github.com/paperclipai/paperclip
**Companies repo:** https://github.com/paperclipai/companies
**License:** MIT (open-source, self-hosted)
**Last reviewed:** 2026-03-30

---

## What It Is

Paperclip is an open-source AI agent orchestration platform. It provides company-level infrastructure for running teams of AI agents (Claude Code, Codex, Gemini, etc.) toward shared business goals.

> "If Claude Code is an employee, Paperclip is the company around it."

You act as the board of directors. You set the mission, hire agents into roles, approve decisions, and monitor performance. The agents do the actual work autonomously.

**What it is NOT:**
- Not a chatbot interface
- Not an agent framework (doesn't tell you how to build agents)
- Not a workflow builder or prompt manager
- Not for single-agent use. Designed for teams of agents working together.

---

## Tech Stack

| Layer | Tech |
|---|---|
| Backend | Node.js 20+ / Express.js REST API |
| Frontend | React dashboard |
| Database | Embedded PostgreSQL (zero config locally) |
| Package manager | pnpm 9.15+ |
| Default port | localhost:3100 |

Self-hosted. No cloud services required. You bring your own AI API keys.

---

## Core Concepts

### The Heartbeat System

Agents don't run continuously. They wake up on triggers like an alarm clock:

- Scheduled interval fires (e.g. every 30 min, every hour)
- A new task gets assigned
- Someone @-mentions the agent in a comment
- Manual trigger from dashboard
- An approval decision is made

**When an agent wakes up, it follows a 9-step protocol:**
1. Check identity — who am I, what is my role, what is my budget?
2. Handle any pending approvals
3. Check inbox — what tasks are assigned to me?
4. Pick the highest-priority work
5. Checkout the task (atomic lock — only one agent can work on it)
6. Understand the full context of the task
7. Do the work using available tools
8. Update status and leave comments
9. Delegate subtasks to reports if needed

Then the agent goes back to sleep until the next trigger.

---

### Goal Cascade

Every piece of work traces back to the company mission:

```
Company Mission
  └── Project (e.g. "FOLIO Essay Processing Pipeline")
        └── Goal (e.g. "Process 50 essays within 3 business days")
              └── Issue/Task (e.g. "Run OCR on batch-2026-03-30")
                    └── Subtask (delegated work)
```

Every agent knows WHY they are doing something, not just WHAT.

---

### Org Chart & Chain of Command

Tree-based hierarchy. Every agent reports to exactly one manager. The CEO is at the top and reports to you (the board).

- Managers can create and delegate subtasks to direct reports
- Agents can escalate blockers up the chain
- Cross-team assignments are possible
- You approve all new agent hires

---

### Agent Configuration (5 Areas)

| Area | What it controls |
|---|---|
| **Instructions** | Agent's identity, role, responsibilities, domain knowledge, communication style. Think: job description + training manual. |
| **Configuration** | Adapter type (Claude Code / Codex / etc.), model, timeout, max turns per heartbeat, env variables, heartbeat interval, wake triggers |
| **Skills** | Lazy-loaded `SKILL.md` files injected at runtime when relevant to the current task |
| **Budget** | Monthly token budget. Soft warning at 80%, auto-pause at 100% |
| **Runs** | Full log of every heartbeat: what was done, token usage, cost, transcript, success/fail |

---

### Skills

Skills are reusable instruction sets that agents load dynamically. Each skill lives in its own folder:

```
skill-name/
  SKILL.md           ← required
  references/        ← optional supporting files
```

`SKILL.md` structure:
```yaml
---
name: skill-name
description: Use this skill when the agent needs to [specific trigger]
---

[Detailed instructions in markdown]
```

Agents only load a skill when it's relevant to their current task. This keeps base prompts lean. Write skills for any recurring workflow you want to standardize.

**Good skill principles:**
- Routing-focused descriptions (when to apply AND when to skip)
- Concrete instructions with code examples / API calls
- Single responsibility per skill
- Keep the SKILL.md lean; put reference material in separate files

---

## Setup

**Prerequisites:**
- Node.js 20+
- Claude Code installed and authenticated
- pnpm 9.15+

**Install:**
```bash
npx paperclipai onboard --yes
```

This configures embedded PostgreSQL, sets up auth, and walks through creating your first company. Paperclip runs at http://localhost:3100.

**Or manual:**
```bash
git clone https://github.com/paperclipai/paperclip.git
cd paperclip
pnpm install
pnpm dev
```

---

## Pre-Built Company Templates

Available at https://github.com/paperclipai/companies. Import with:

```bash
npx companies.sh add paperclipai/companies/[company-name]
```

| Template | What it is |
|---|---|
| Agency Agents | Full AI agency, 167 agents across 10 divisions |
| Fullstack Forge | Dev consultancy, 49 agents, 66 skills, 12 languages |
| Product Compass Consulting | AI product management, 48 agents, 65 skills |
| GStack | Engineering with distinct cognitive modes |
| K-Dense Science Lab | Multi-disciplinary research, 177 skills |
| Trail of Bits Security | Security auditing, smart contracts, cryptography |
| ClawTeam Capital | Investment analysis, 7 agents |
| Donchitos Game Studio | Indie game dev, 48 agents |
| RedOak Review | Code quality and security review |
| AgentSys Engineering | Task discovery through production deployment |

---

## Claude Code + Paperclip API

Since Paperclip runs a full REST API at localhost:3100, Claude Code can interact with it directly. This is the primary management interface beyond the dashboard.

**Key API endpoints:**

| Action | Endpoint |
|---|---|
| List agents | `GET /api/companies/{companyId}/agents` |
| List tasks/issues | `GET /api/companies/{companyId}/issues` |
| Company costs summary | `GET /api/companies/{companyId}/costs/summary` |
| Costs by agent | `GET /api/companies/{companyId}/costs/by-agent` |
| Create secret | `POST /api/companies/{companyId}/secrets` |
| Update agent | `PATCH /api/agents/{agentId}` |
| Activity log | `GET /api/companies/{companyId}/activity` |
| Org chart | `GET /api/companies/{companyId}/org` |

**What Claude Code can do via API:**
- Pull real-time status on all agents, tasks, and costs
- Edit agent configs, skills, and tool files
- Add API keys to the encrypted secrets manager (UI doesn't support this yet)
- Wire secrets into agent adapter configs
- Troubleshoot failed heartbeats by reading run logs
- Create and assign tasks

---

## Company Template Structure

Each company template contains:

```
company-name/
  agents/          ← agent definitions (one file per agent)
  skills/          ← reusable SKILL.md files
  teams/           ← team groupings
  images/          ← org charts, visuals
  .paperclip.yaml  ← template metadata
  README.md
  COMPANY.md
```

---

## Best Practices

- Start with conservative budgets — easier to increase than undo overspending
- Keep board approval on for new agent hires until you trust the CEO agent
- Check cost dashboard after first few heartbeats to understand burn rate
- Start local, move to a VPS later for 24/7 operation
- Write custom skills for any recurring workflow you give agents repeatedly
- Use Claude Code as the Paperclip management layer — faster than clicking through the UI

---

## Related Files

- [[Paperclip — FOLIO Company Design]] — architecture plan for FOLIO's Paperclip company
- [[Technical|FOLIO Technical Overview]]
