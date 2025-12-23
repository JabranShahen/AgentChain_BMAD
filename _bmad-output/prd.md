---
stepsCompleted: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
inputDocuments:
  - "{project-root}/_bmad-output/index.md"
documentCounts:
  briefs: 0
  research: 0
  brainstorming: 0
  projectDocs: 1
workflowType: 'prd'
lastStep: 11
project_name: 'AgentChain'
user_name: 'Jabra'
date: '2025-12-22'
---
# Product Requirements Document - AgentChain

**Author:** Jabra
**Date:** 2025-12-22

## Executive Summary

AgentChain will deliver a web-native BMAD agent platform that exposes BMAD agents and workflows through a .NET 8 REST API and a React UI, replacing CLI/Codex-style interaction. It builds on the existing AgentChain architecture, keeping `.bmad/` as the source of truth and `agent_service` as the runtime library for persona loading, prompt composition, session management, and workflow/tool dispatch. The platform focuses on discoverability, stateful sessions, and BMAD-faithful behavior (menu-mode greetings, deterministic prompt composition, and governed action resolution), enabling users to work with agents through clear, structured workflows rather than ad-hoc prompting.

### What Makes This Special

This is not just "BMAD with a UI." It is a delivery layer that matches BMAD's structured, role-aware, menu-driven design. The platform makes agents and workflows inspectable, sessions stateful and resettable, and behavior deterministic and explainable. Users can see what each agent can do before engaging, follow guided menus instead of guessing commands, and run workflows intentionally with clear outcomes. In short: BMAD feels like a system, not a prompt collection.

## Project Classification

**Technical Type:** web_app + api_backend  
**Domain:** general  
**Complexity:** low  
**Project Context:** Brownfield - extending existing system

This PRD will define new functionality on top of the current React + Vite UI and ASP.NET Core API, aligned with existing architecture patterns and the agent_service runtime library.

## Success Criteria

### User Success

- Users can quickly discover the right agent without guessing commands.
- Users complete meaningful tasks (e.g., epics/stories, architecture review) via a single guided flow.
- Sessions preserve context; users don't need to re-explain or recover state.
- Users feel "this didn't fight me - it helped me."

### Business Success

**3 months (adoption + proof of value):**
- Intended users use AgentChain regularly.
- At least one core workflow runs end-to-end via the UI.
- Users prefer AgentChain over CLI/Codex for BMAD interactions.
- New agents/workflows can be added without core code changes.

**12 months (leverage + extensibility):**
- Multiple agents and workflows are used across use cases.
- Workflows produce durable artifacts (plans, decisions, reviews).
- The system is trusted in real delivery workflows.
- Adding agents/workflows is mostly configuration.

**Primary metrics:**
- Workflow completions.
- Repeat usage (returning users).
- Session depth (multi-turn, stateful chats).

**Secondary metrics:**
- Agent discovery -> chat conversion rate.
- Menu usage vs free-form prompting.
- Session resets vs abandoned sessions.

**Definitive signal:** users consistently complete structured workflows via AgentChain instead of ad-hoc prompting.

### Technical Success

**Reliability & Consistency (non-negotiable):**
- Deterministic prompt composition for identical agent configs.
- Menus render exactly as defined; selection resolution is deterministic.
- Session integrity with no cross-session leakage.
- Clear, user-visible failures on invalid menu/workflow/tool actions.

**Performance & Latency:**
- Responses within a few seconds under normal load.
- Catalog/transcript endpoints are near-instant.
- No UI-blocking filesystem/network calls per request.
- Workflow latency spikes are acceptable with clear progress.

**Operational Qualities (MVP must-have):**
- Structured logging (sessionId, agentId, request type, outcome).
- Traceability from user action -> agent response -> tool/workflow execution.
- Explicit error handling surfaced in API + UI.
- Safe defaults for unknown tools/workflows/configs.

**Technical failure conditions:**
- Inconsistent agent behavior without config changes.
- Session state loss or mixing.
- Silent partial workflow execution.
- Silent prompt changes.
- Errors swallowed or only visible in logs.

### Measurable Outcomes

- >=1 workflow (e.g., create-epics-and-stories) completed end-to-end via UI.
- Repeat usage from the same users across sessions.
- Multi-turn sessions with preserved state and transcripts.
- Deterministic prompt checks pass for identical agent configs.
- Menu interactions follow strict precedence with no ambiguity.

## Product Scope

### MVP - Minimum Viable Product

- Agent discovery (catalog + detail).
- Stateful chat sessions.
- Deterministic BMAD prompt composition.
- Menu-mode greeting and selection handling.
- At least one end-to-end workflow (create epics and stories).
- Clear logging and error reporting.

### Growth Features (Post-MVP)

- Session persistence across restarts.
- Multiple workflows per agent.
- Richer UI (history, saved artifacts).
- Improved observability (metrics/dashboards).
- More flexible tool integrations.

### Vision (Future)

- Governance/policy enforcement.
- Durable decision logs and audit trails.
- Multi-agent orchestration.
- Cross-agent workflow composition.
- Organization-level trust and inspection tooling.

## User Journeys

**Journey 1: PM Agent - Structured Planning Without Guesswork**  
A product lead opens AgentChain to plan a new initiative. Instead of searching docs or experimenting with prompts, they discover the PM agent in the catalog, read its purpose, and see the available menu options. They choose "Create epics and stories" and are guided through a structured workflow. The system preserves context, asks clarifying questions, and produces a complete epic/story breakdown. The user leaves with a sharable artifact, not just a chat transcript, and can return to the same session later without losing state.

**Journey 2: Architect Agent - Design Review With Clarity**  
A systems architect needs to evaluate a proposed change. They select the Architect agent, review its menu, and choose a design review workflow. The agent prompts for system constraints and integration points, then produces a structured review and architecture recommendations. The workflow is transparent, deterministic, and leaves a repeatable artifact for review and iteration.

**Journey 3: Analyst Agent - Problem Framing With Evidence**  
An analyst wants to clarify requirements before planning. They choose the Analyst agent, follow a guided "requirements analysis" menu path, and answer targeted prompts. The agent synthesizes inputs into a structured analysis, highlighting risks and unknowns. The outcome is a clear requirements artifact that can feed directly into later workflows.

**Journey 4: Developer Agent - Implementation Guidance With Guardrails**  
A developer opens AgentChain for implementation guidance. They select the Dev agent, choose a guided workflow, and receive deterministic, role-appropriate responses tied to the project context. The developer gets actionable steps (not vague suggestions) and can reference prior outputs without re-prompting.

**Journey 5: BMad Master - Orchestrated Workflow Execution**  
A user needs a multi-step flow involving multiple agents. They select the BMad Master orchestrator, which presents menu-driven paths and guides them through a coordinated sequence (e.g., discovery -> PRD -> epics). The orchestrator ensures the right agent handles each step and that outputs are consistent and traceable.

**Journey 6: System Operator - Traceable Operations**  
Jordan, the platform operator, investigates a workflow failure. They pull logs and trace a failed session to a specific agent, menu selection, and tool invocation. The system provides clear failure messages and structured logs so Jordan can identify whether the issue is configuration, tool execution, or runtime.

**Journey 7: Support Engineer - Explainable Outcomes**  
Sam receives a user report: "the agent behaved oddly." They retrieve the session transcript, including menu selections and prompt composition. Sam can explain exactly why the agent produced its output or why it failed, and guide the user to retry or reset.

**Journey 8: API Consumer - Programmatic Integration**  
Riley integrates AgentChain into another system. They call the REST API to list agents, create a session, trigger a workflow, and retrieve structured results. The API behavior is deterministic and session-based, enabling automation without relying on UI interaction.

### Journey Requirements Summary

These journeys imply required capabilities:

- Agent catalog + agent detail inspection from `AgentData` configs.
- Menu fidelity and deterministic prompt composition per agent persona.
- Stateful sessions with transcript access, reset, and no cross-session leakage.
- Workflow execution via menu-driven paths with clear artifacts produced.
- Orchestration support for multi-agent workflows (BMad Master).
- Observability: structured logging and traceability across sessions and tools.
- Explainability: access to prompt composition and menu selections.
- API-first access for listing agents, sessions, workflows, and transcripts.

## Innovation & Novel Patterns

### Detected Innovation Areas

- **BMAD as executable configuration:** agent identity, authority, menus, and workflows are treated as runtime contracts, not informal prompts.
- **Menu-driven constrained interaction:** structured menus replace open-ended prompting to improve reliability, repeatability, and confidence.
- **Web-native, sessionful agents:** persistent sessions, deterministic prompt composition, and inspectable transcripts make behavior explainable and operable.
- **Governed agent services:** tool/workflow execution is explicit, validated, and observable, laying the groundwork for trust and governance.

### Market Context & Competitive Landscape

This approach differentiates AgentChain from typical chat-first AI tools by emphasizing determinism, operational safety, and workflow fidelity. It positions AgentChain as an agent platform with governance-ready execution rather than a general-purpose conversational UI.

### Validation Approach

- Validate determinism by running identical sessions and comparing prompt composition outputs.
- Validate menu fidelity by asserting menu ordering and selection resolution from config.
- Validate session integrity by replaying sessions and verifying transcript consistency.
- Validate governance boundaries by rejecting unknown tools/workflows and logging failures.

### Risk Mitigation

- If constrained interaction feels too rigid, offer progressive disclosure (menu-first, free-form second).
- If determinism reveals config drift issues, enforce versioned config snapshots per session.
- If workflow execution fails mid-stream, surface clear error states and preserve partial artifacts for recovery.

## Project-Type Specific Requirements

### Project-Type Overview

AgentChain is a **web_app + api_backend** product. The API exposes agent/session/workflow capabilities, while the SPA provides the primary interaction layer for discovery, guided menus, and stateful chat.

### Technical Architecture Considerations

- API must provide deterministic, structured responses with clear error handling.
- UI must be fast, stateful, and fully client-side (SPA) with responsive support.
- System should be designed for future auth, rate limiting, and versioning without breaking contracts.

### API Backend Requirements

**Endpoint Specifications:**
- `GET /api/agents` - list available agents.
- `GET /api/agents/{id}` - agent details (menus, commands).
- `POST /api/agents/{agentId}/sessions` - create session.
- `POST /api/agents/{agentId}/chat` - send message (sessionId optional).
- `GET /api/sessions/{sessionId}/transcript` - fetch transcript.
- `POST /api/sessions/{sessionId}/reset` - reset session.
- Future: internal tool/workflow execution endpoints (not public in MVP).

**Authentication Model:**
- MVP: no auth (local/dev/internal use).
- Future-ready for JWT/Bearer.
- Authorization boundaries: agent visibility + tool/workflow allowlists.
- Agent authority is config-driven, not token-driven.

**Data Schemas & Formats:**
- JSON only, UTF-8.
- Consistent response envelope for success/error.
- Message schema includes role, content, timestamp, optional name, metadata.

**Rate Limits & Quotas:**
- None for MVP.
- Design so rate limiting can be added via middleware/gateway.

**Versioning:**
- Unversioned `/api/*` routes initially.
- Introduce `/api/v1` once contract stabilizes.

**SDKs:**
- None for MVP; REST API is the contract.
- SDKs optional later if demand grows.

### Web App Requirements

**Platform & Browser Support:**
- SPA (React + Vite), client-side routing only.
- Evergreen browsers (latest 2 versions of Chrome, Edge, Firefox, Safari).
- Responsive support for iOS Safari and Android Chrome.

**SEO:**
- Not required.

**Real-Time Features:**
- Not required for MVP.
- Optional later: streaming/progress indicators for long workflows.

**Accessibility:**
- WCAG 2.1 AA intent.
- Keyboard navigation, focus states, accessible controls.
- Avoid animation-heavy interactions.

## Project Scoping & Phased Development

### MVP Strategy & Philosophy

**MVP Approach:** Platform MVP  
**Resource Requirements:** Medium scope, focused engineering team with .NET + React + workflow orchestration experience.

This MVP validates AgentChain as a stable platform for web-native BMAD agents, focusing on correctness, determinism, and workflow execution rather than scale or monetization.

### MVP Feature Set (Phase 1)

**Core User Journeys Supported:**
- PM agent journey (create epics and stories end-to-end)
- Agent discovery + menu-driven interaction
- Stateful sessions with transcripts and reset

**Must-Have Capabilities:**
- Agent discovery (list agents + detailed menus/commands)
- Stateful chat sessions with session reset
- Deterministic prompt composition from BMAD configs
- Menu greeting + deterministic selection resolution
- At least one complete workflow (create epics and stories)
- Structured logging + clear user-visible errors

### Post-MVP Features

**Phase 2 (Post-MVP):**
- Session persistence across restarts
- Observability (metrics, dashboards)
- Multiple workflows per agent
- Richer UI (history, saved artifacts)
- Authentication & authorization (role-based access)

**Phase 3 (Expansion):**
- Governance & policy enforcement
- Durable system of record (audit trails, decisions, artifacts)
- Multi-agent orchestration
- External integrations (issue trackers, repos, CI/CD)
- Enterprise controls (fine-grained permissions, compliance tooling)

### Risk Mitigation Strategy

**Technical Risks:**  
- Non-deterministic behavior -> deterministic prompt composition + strict menu resolution.  
- Workflow/tool failures -> allowlisted tools, validated inputs, explicit error handling.  
- Session leakage -> per-session isolation, serialized turns, clear reset semantics.

**Market Risks:**  
- Users don't see value over ad-hoc prompting -> validate repeat usage on one high-value workflow.  
- Perceived as "just another chatbot" -> emphasize menus, workflows, inspectability, saved outcomes.

**Resource Risks:**  
- Limited engineering time -> strict MVP scope, defer persistence/auth/governance.  
- Over-engineering early -> validate Platform MVP before expansion.  
- Single maintainer bottleneck -> configuration-driven behavior to reduce code churn.

## Functional Requirements

### Agent Discovery & Catalog

- FR1: Users can list available agents from the catalog.
- FR2: Users can view agent details including role, description, menus, and declared commands.
- FR3: Users can distinguish agents by purpose and intended workflow outcomes.
- FR4: Users can see which workflows/actions are available per agent.

### Session & Transcript Management

- FR5: Users can create a new session for a selected agent.
- FR6: Users can send messages within an existing session.
- FR7: Users can retrieve a session transcript at any time.
- FR8: Users can reset a session and clear its state.
- FR9: The system can associate messages with a specific session ID.
- FR10: The system can maintain isolated state per session.

### Menu-Driven Interaction

- FR11: Agents can present menu-based greetings in menu mode.
- FR12: Users can select menu options by number, command, or label.
- FR13: The system can resolve ambiguous menu selections deterministically.
- FR14: The system can provide clear feedback on invalid menu selections.
- FR15: Users can follow guided prompts driven by menu choices.

### Workflow Execution

- FR16: Users can trigger workflows from agent menus.
- FR17: The system can execute a workflow end-to-end for a session.
- FR18: Workflows can produce structured artifacts as outputs.
- FR19: The system can surface workflow progress or completion states.
- FR20: The system can restrict workflow execution to allowlisted handlers.

### Agent Configuration & Behavior Fidelity

- FR21: The system can load agent configuration from AgentData at runtime.
- FR22: The system can compose agent prompts deterministically from config.
- FR23: The system can ensure identical inputs yield consistent behavior.
- FR24: The system can apply configuration changes only to new sessions.
- FR25: The system can expose agent menu definitions exactly as configured.

### Observability & Error Handling

- FR26: The system can log each request with sessionId, agentId, and outcome.
- FR27: The system can return clear error responses for invalid actions.
- FR28: The system can surface workflow/tool failures to users.
- FR29: The system can trace an interaction to agent, menu selection, and tool/workflow execution.
- FR30: The system can prevent unknown tools or workflows from executing.

### API Consumer Integration

- FR31: API consumers can list agents via REST.
- FR32: API consumers can fetch agent details via REST.
- FR33: API consumers can create sessions via REST.
- FR34: API consumers can send chat messages via REST.
- FR35: API consumers can retrieve transcripts via REST.
- FR36: API consumers can reset sessions via REST.

### Admin / Operator Support

- FR37: Operators can inspect logs for session-level failures.
- FR38: Operators can trace failures to configuration, workflow, or tool execution.
- FR39: Support users can explain outcomes using transcripts and menu selections.
- FR40: Operators can verify that execution stayed within allowlisted tools/workflows.

## Non-Functional Requirements

### Performance

- API endpoints for agent catalog, session creation, and transcript retrieval should respond in under 1 second under normal load.
- Chat responses should return within a few seconds under normal load.
- Workflow execution may take longer, but must provide clear progress and end with explicit success or failure.
- UI must remain responsive during long-running workflows.

### Reliability

- Deterministic behavior: same agent + same config produces identical prompt composition.
- No cross-session state leakage.
- Menu rendering and selection resolution is deterministic.
- Errors are explicit and never silently swallowed.
- MVP uptime is best-effort/dev-grade (no production SLA required).

### Security

- Only allowlisted tools and workflows can execute.
- Unknown or malformed tool/workflow requests must be rejected.
- User-facing errors must not expose internal file paths, raw configs, or stack traces.
- Data is treated as non-sensitive in MVP; auth is deferred.

### Scalability

- MVP assumes low concurrent usage and single-node deployment.
- API design should remain stateless where possible to allow future scaling.
- Session boundaries must be explicit to avoid coupling that blocks scaling.

### Accessibility

- UI must meet WCAG 2.1 AA intent.
- Keyboard navigation, focus states, and accessible form controls are required.
- Error messages must be readable and accessible.
- Avoid animation-heavy interactions that impair usability.

### Integration

- No external integrations required for MVP.
- Public APIs must be clean and documented to support future integrations (issue trackers, repos, CI/CD).

