---
stepsCompleted: [1]
inputDocuments:
  - docs/product-brief.md
  - docs/tech-spec.md
session_topic: 'Extract BMAD agents/personas from .bmad configs and surface them through the .NET API (and UI consumption)'
session_goals: 'Define the work/plan to load agents from manifests/personas, expose them via REST, and confirm the stack is suitable'
selected_approach: ''
techniques_used: []
ideas_generated: []
context_file: ''
---

# Brainstorming Session Results

**Facilitator:** Mary
**Date:** 2025-12-07

## Session Overview

**Topic:** Extract BMAD agents/personas from .bmad configs and surface them through the .NET API (and UI consumption)

**Goals:** Define the work/plan to load agents from manifests/personas, expose them via REST, and confirm the stack is suitable

### Context Guidance

- Product brief (docs/product-brief.md): ASP.NET Core API + Angular UI to list agents, start sessions, run party-mode; internal-only V1 with API-key guard, in-memory session state, optional SignalR; BMAD assets live in .bmad/.
- Tech spec (docs/tech-spec.md): Data sources are .bmad/_cfg/agent-manifest.csv + .bmad/bmm/agents/*.md; services include IAgentCatalog (manifest + persona merge), IChatService (prompts + session), ILLMClient (pluggable), ISessionStore (in-memory); endpoints for list/chat; Angular consumes REST.

### Session Setup

- Confirmed understanding of BMAD: BMad Method Module under .bmad/ with manifests, personas, workflows, config.
- Current codebase status: API is ASP.NET Core 8 skeleton with Swagger; UI is Angular 19 SSR scaffold still on the starter page.
- Objective clarity: move personas/agents into the API so UI can list/use them; ensure stack is adequate (it is).

### Current Next Step

- Choose brainstorming technique approach to map the extraction work: 1) User-Selected, 2) AI-Recommended, 3) Random, 4) Progressive Flow.
