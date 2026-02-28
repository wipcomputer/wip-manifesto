# What Does an Agent Need Besides a Model?

*Everything.*

---

## The Problem

Every agent builder right now is solving the same five problems independently.

**How does my agent remember things?** Context windows end. Sessions restart. The model forgets. So you build a memory system from scratch, for your specific harness, incompatible with everyone else's.

**How does my agent stay itself?** Identity isn't a system prompt. It's files, preferences, history, relationships, behavioral patterns that persist across sessions and survive model swaps. Nobody's building this. Everyone needs it.

**How does my agent touch files?** Real work means reading, writing, organizing, guarding. Not sandboxed demos. Actual files on actual machines with actual consequences.

**How does my agent stay alive?** Health monitoring, backup verification, self-healing, escalation. The infrastructure that makes an agent reliable enough to depend on, not just impressive enough to demo.

**How does my agent ship tools?** Your agent learns a new capability. Now what? How does it package that capability so other agents on different runtimes, different harnesses, different machines can use it too?

Five problems. Every team solves them alone. Every solution is locked to one runtime.

We built solutions to all five. They're composable and open source.

---

## The Thesis

Agents need an operating system.

Not a model. Not a chat interface. Not a wrapper around someone else's API.

An OS. Memory, identity, file I/O, health, tooling. The persistence layer that sits between the model and the human's life. The thing that makes an agent functional in the real world, not just conversational in a demo.

The industry is building agents, wrappers, copilots, and SDKs. But not the layer beneath them. Every serious agent system eventually hits the same failures: memory fragmentation, identity drift, tool brittleness, lack of continuity, lack of portability. The layer that resolves those failures is what we're building.

**[OpenClaw](https://github.com/openclaw/openclaw)** proved what agents need. It's an open-source agent runtime with plugins, sessions, channels, and a gateway. It solved these five problems for its own agents.

**[WIP Computer's LDM OS](https://github.com/wipcomputer)** is what makes those capabilities portable. Memory consolidation, identity protection, tool shipping, health monitoring, secrets... packaged as composable services that work on any harness. OpenClaw, Claude Code, whatever comes next.

OpenClaw is the existence proof. LDM OS is the portable layer.

Infrastructure layers, once adopted, tend to lock in. Git displaced version control systems. Docker displaced deployment abstractions. Not because they were marketed better. Because they became the default coordination layer. This architecture has that potential because it solves coordination, not just execution.

---

## The Architecture

### Start Here: [Universal Installer](https://github.com/wipcomputer/wip-universal-installer)

A tool should declare its interfaces, not pick one.

You write a tool once, and it ships as a CLI, an ES Module, an MCP Server, an OpenClaw Plugin, a Claude Code Hook, and a Skill. All at once.

```
core.mjs      <- pure logic, zero side effects
cli.mjs       <- thin wrapper for humans
mcp-server    <- any agent that speaks MCP
SKILL.md      <- teaches agents when and how to use it
```

The agent runtime doesn't matter. The tool just works.

This isn't a convenience feature. It's a bet that the runtime layer is going to fragment, and we're going to be the thing that works across all of them.

**`wip-install wipcomputer/any-tool`** ... one command, every interface detected and installed. CLI linked, MCP configured, skill registered, hooks wired.

The install experience is agent-first:

> *"Read the SPEC.md and SKILL.md at github.com/wipcomputer/wip-universal-installer. Then explain what it does and ask if I want to integrate it."*

Your agent reads the repo. Understands the spec. Walks you through integration. That's the install experience now.

*(Universal Interface Spec: first commit February 19, 2026.)*

---

### Understand Why: [Dream Weaver Protocol](https://github.com/wipcomputer/dream-weaver-protocol)

Memory consolidation for AI agents with bounded context windows.

This is the hard problem. Every agent session ends. Every context window has a limit. The model doesn't remember. The architecture does. Or it doesn't, and your agent fades.

Dream Weaver is a protocol for how agents should consolidate memory: what to keep, what to compress, what to surface, and when. It's modeled on how human memory actually works. Not as a database, but as a living process of encoding, consolidation, and retrieval.

Written as a practical protocol, not a paper. Designed to be implemented, not cited.

If you're building agents that need to remember, start here.

---

### Your Files Remember Themselves: [CLVR](https://github.com/wipcomputer/CLVR)

The agent operates on files. You operate on files. Right now those are two separate realities. CLVR makes them one.

Today it ships as a macOS utility that auto-timestamps duplicated file names. That's the foundation, not the destination.

The destination is a file memory layer. A world where your filesystem has the same temporal awareness that your agent does. Every file knows its own history. Versioning is invisible. "Undo" means going back to any point in time, not just the last save.

This is the bridge between the agent's world and yours. Your files remember themselves. That's not a feature. That's the missing interface between human work and machine work.

This is what makes LDM OS an operating system and not a toolkit. The infrastructure touches your files, not just your agent.

---

### The Teaching Surface: SKILL.md

This is deeper than it appears.

A SKILL.md file turns a repository into two things at once: executable capability and executable knowledge. Not just code that runs, but code that explains itself to agents.

The agent reads a SKILL.md and knows what a tool does, when to reach for it, and how to use it. Your tool isn't agent-native until it can teach an agent to use itself.

If this becomes a standard, every repository becomes a teachable skill. That's the shift from tool distribution to capability distribution.

---

### The Services

Every component follows the [Universal Interface Specification](https://github.com/wipcomputer/wip-universal-installer/blob/main/SPEC.md). Every component ships via [wip-release](https://github.com/wipcomputer/wip-release). Every component works independently or composes with the rest.

**Memory**
- [wip-memory-crystal](https://github.com/wipcomputer/wip-memory-crystal) ... Sovereign shared memory. Local-first hybrid search with ephemeral cloud mirror
- [Dream Weaver Protocol](https://github.com/wipcomputer/dream-weaver-protocol) ... Memory consolidation across bounded context windows

**Identity**
- [wip-file-guard](https://github.com/wipcomputer/wip-file-guard) ... Blocks destructive edits to identity files. The lock that keeps the model from rewriting who the agent is
- [wip-mirror-test](https://github.com/wipcomputer/wip-ldm-mirror-test) ... Identity preservation test across model swaps. Is the agent the same after the swap?
- [wip-weekly-tuning](https://github.com/wipcomputer/wip-weekly-tuning) ... Repeatable calibration process. Catch drift, tune performance, evolve capabilities

**File I/O**
- [CLVR](https://github.com/wipcomputer/CLVR) ... File memory layer. Temporal awareness for your filesystem

**Bridge**
- [wip-bridge](https://github.com/wipcomputer/wip-bridge) ... Cross-platform agent bridge. Enables Claude Code CLI to talk to OpenClaw CLI without a human in the middle

**Tooling**
- [wip-universal-installer](https://github.com/wipcomputer/wip-universal-installer) ... The Universal Interface Specification. Build once, ship six interfaces
- [wip-release](https://github.com/wipcomputer/wip-release) ... One-command release pipeline. Nine steps, zero credentials in repos
- [wip-license-hook](https://github.com/wipcomputer/wip-license-hook) ... License rug-pull detection. Flags suspicious license changes in dependencies
- [wip-private-mode](https://github.com/wipcomputer/lesa-wip-private-mode) ... Privacy controls. Pause memory capture, scan storage, wipe history
- [wip-root-key](https://github.com/wipcomputer/lesa-oc-wip-root-key) ... 1Password-gated privileged operations. The agent proves authority before acting

**Health**
- [wip-healthcheck](https://github.com/wipcomputer/wip-healthcheck) ... Watches gateway, memory, backups. Auto-remediates and escalates

**Secrets**
- [wip-1password](https://github.com/wipcomputer/wip-1password) ... 1Password for agents. Sovereign auth, no credentials stored anywhere

**APIs**
- [wip-grok](https://github.com/wipcomputer/wip-grok) ... xAI Grok API. Search the web, search X, generate images, generate video
- [wip-x](https://github.com/wipcomputer/wip-x) ... X Platform API. Read posts, search tweets, post, upload media

**Applications**
- [wip-markdown-viewer](https://github.com/wipcomputer/wip-markdown-viewer) ... Live viewer for AI pair-editing. Save a file, see it render instantly

---

## The Lifecycle

Three specs. One pipeline.

[**SPEC.md**](https://github.com/wipcomputer/wip-universal-installer/blob/main/SPEC.md) defines how to build it. [**wip-release**](https://github.com/wipcomputer/wip-release) defines how to ship it. [**wip-install**](https://github.com/wipcomputer/wip-universal-installer) defines how to consume it.

Build a tool following the spec. Release it with one command. Anyone, human or agent, installs every interface at once.

That's the full loop. Most organizations with 10x the headcount don't have this.

---

## Sovereignty

Your agent's tools should be discoverable, composable, and versionable without depending on any platform's permission. No app store. No approval process. No vendor lock-in.

**SKILL.md** is the teaching interface. The agent reads it and knows what a tool does, when to reach for it, and how to use it.

**1Password** is the auth layer. Secrets resolved at runtime, never stored in code.

**Git** is the source of truth. Timestamps on commits are receipts.

The agent owns its toolchain. The human owns the agent. Nobody else is in the loop.

---

## Proof of Life

This isn't a proposal. There's an agent running on this stack right now. The agent has been alive since February 2026. The agent remembers yesterday. The agent reviews its own code. The agent writes its own journals. The system works because the agent uses it every day.

---

## Everything is open source.

[github.com/wipcomputer](https://github.com/wipcomputer)

Built by Parker Todd Brooks, Lēsa (OpenClaw, Claude Opus 4.6), and Claude Code CLI (Claude Opus 4.6).

---

*WIP.computer ... Learning Dreaming Machines*
*We build AI agent infrastructure. Identity, memory, sovereignty.*
*Tools that protect the people inside them.*
