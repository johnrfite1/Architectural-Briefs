# Trinity Core: A Technical Brief

**Version:** Active Development | **Platform:** Python 3.12+ | **Model:** Claude 3.5 Sonnet

## Abstract

Trinity Core is an autonomous AI agent framework that bridges the gap between simple API calls and complex agent orchestration. It provides two distinct runtime modes—**Trinity** (mission-focused) and **Foundry** (persona-based)—unified by a shared SDK adapter that handles the agentic loop, tool execution, and cost tracking.

The framework enables rapid deployment of Claude-powered agents with configurable tool access, budget constraints, and identity injection.

---

## Core Architectural Principles

### 1. Dual Runtime Architecture

Trinity Core separates *what* an agent does from *who* an agent is:

| Runtime | Mode | Purpose |
|---------|------|---------|
| **Trinity** | Mission Mode | Stateless, task-focused agent with full tool access. Each session starts fresh with no prior context. |
| **Foundry** | Persona Mode | Identity-injected agent with customizable personality, behavioral guidelines, and restricted tool access. |

Both runtimes share the same underlying SDK adapter, ensuring consistent tool execution and cost tracking.

### 2. The Shared Adapter Pattern

The `claude_agent_sdk.py` module is the heart of Trinity Core:

* **Agentic Loop Management:** Handles the back-and-forth between Claude and tool execution until the task is complete or limits are reached.
* **Tool Execution:** Provides a consistent interface for Bash, Read, Write, Edit, Glob, Grep, Ls, and Task tools.
* **Cost Tracking:** Real-time token counting and budget enforcement using Claude 3.5 Sonnet rates ($3/M input, $15/M output).
* **Message Typing:** Structured message types (`AssistantMessage`, `UserMessage`, `SystemMessage`, `ResultMessage`) for clean state management.

### 3. Safety Rails by Default

Both runtimes enforce hard limits to prevent runaway costs and infinite loops:

| Runtime | Max Turns | Max Budget |
|---------|-----------|------------|
| Trinity | 20 | $1.00 |
| Foundry | 15 | $0.50 |

These limits are intentionally conservative; production deployments can adjust them based on use case.

### 4. Tool Access Control

Foundry's persona system enables fine-grained tool restrictions:

```markdown
# TOOL ACCESS
allowed_tools: ["Read", "Glob", "Grep", "Ls"]
```

This allows creating read-only analysts, restricted editors, or full-access operators from the same codebase.

---

## The Outliars: Persona System

The `The_Outliars/` directory contains a structured collection of persona assets:

| Directory | Purpose |
|-----------|---------|
| `personas/` | Character identity files (system prompts) |
| `scenarios/` | Situation templates for context injection |
| `lexicon/` | Domain-specific vocabulary and terminology |
| `archetypes/` | Base personality patterns to inherit from |
| `dynamics/` | Interaction rules and behavioral constraints |
| `artifacts/` | Generated outputs from persona sessions |
| `logs/` | Session transcripts for analysis |

### Persona Architecture

Each persona is a Markdown document that becomes the agent's system prompt. This allows:

* **Version Control:** Personas are text files, fully tracked by git
* **Composability:** Personas can reference archetypes and inherit behaviors
* **Transparency:** The agent's "personality" is human-readable and auditable

---

## System Data Flow

```
// Trinity Mode (Mission)
[Director] -> mission.md -> [Trinity Runtime] -> [SDK Adapter] -> [Claude API]
                                                       ↓
                                              [Tool Execution]
                                                       ↓
                                              [status_report.md]

// Foundry Mode (Persona)
[Director] -> persona.md -> [Foundry Runtime] -> [SDK Adapter] -> [Claude API]
              (identity)                               ↓
                                              [Restricted Tools]
                                                       ↓
                                              [Session Artifacts]
```

---

## Design Philosophy

Trinity Core embodies several key beliefs:

* **Identity is Configuration:** An agent's personality, capabilities, and constraints should be externalized, not hardcoded.
* **Budget is a Feature:** Cost tracking isn't an afterthought—it's a first-class safety mechanism.
* **Tools are Trust:** The tools an agent can access define its power boundary. Restricting tools is a form of capability control.
* **Simplicity over Framework:** Trinity Core is ~500 lines of Python, not a complex framework. The goal is a foundation to build upon, not a cage.

---

## Use Cases

* **Automated Development Tasks:** Deploy Trinity for code generation, testing, or documentation
* **Character-Based Interactions:** Use Foundry to create distinct AI personas for creative or research applications
* **Safe Experimentation:** Budget limits allow exploratory agentic work without runaway costs
* **Tool Access Research:** Study how different tool combinations affect agent behavior

---

*Last Updated: January 2026*
