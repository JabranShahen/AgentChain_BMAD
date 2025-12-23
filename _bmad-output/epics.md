---
stepsCompleted: [1, 2, 3, 4]
inputDocuments:
  - "{project-root}/_bmad-output/api-contracts-api.md"
  - "{project-root}/_bmad-output/architecture-api.md"
  - "{project-root}/_bmad-output/architecture-ui.md"
  - "{project-root}/_bmad-output/component-inventory-ui.md"
  - "{project-root}/_bmad-output/comprehensive-analysis-api.md"
  - "{project-root}/_bmad-output/comprehensive-analysis-ui.md"
  - "{project-root}/_bmad-output/contribution-guidelines.md"
  - "{project-root}/_bmad-output/data-models-api.md"
  - "{project-root}/_bmad-output/deployment-configuration.md"
  - "{project-root}/_bmad-output/development-guide-api.md"
  - "{project-root}/_bmad-output/development-guide-ui.md"
  - "{project-root}/_bmad-output/development-instructions.md"
  - "{project-root}/_bmad-output/index.md"
  - "{project-root}/_bmad-output/integration-architecture.md"
  - "{project-root}/_bmad-output/prd.md"
  - "{project-root}/_bmad-output/project-overview.md"
  - "{project-root}/_bmad-output/source-tree-analysis.md"
  - "{project-root}/_bmad-output/ux-design-specification.md"
---

# AgentChain - Epic Breakdown

## Overview

This document provides the complete epic and story breakdown for AgentChain, decomposing the requirements from the PRD, UX Design if it exists, and Architecture requirements into implementable stories.

## Requirements Inventory

### Functional Requirements

FR1: Users can list available agents from the catalog.
FR2: Users can view agent details including role, description, menus, and declared commands.
FR3: Users can distinguish agents by purpose and intended workflow outcomes.
FR4: Users can see which workflows/actions are available per agent.
FR5: Users can create a new session for a selected agent.
FR6: Users can send messages within an existing session.
FR7: Users can retrieve a session transcript at any time.
FR8: Users can reset a session and clear its state.
FR9: The system can associate messages with a specific session ID.
FR10: The system can maintain isolated state per session.
FR11: Agents can present menu-based greetings in menu mode.
FR12: Users can select menu options by number, command, or label.
FR13: The system can resolve ambiguous menu selections deterministically.
FR14: The system can provide clear feedback on invalid menu selections.
FR15: Users can follow guided prompts driven by menu choices.
FR16: Users can trigger workflows from agent menus.
FR17: The system can execute a workflow end-to-end for a session.
FR18: Workflows can produce structured artifacts as outputs.
FR19: The system can surface workflow progress or completion states.
FR20: The system can restrict workflow execution to allowlisted handlers.
FR21: The system can load agent configuration from AgentData at runtime.
FR22: The system can compose agent prompts deterministically from config.
FR23: The system can ensure identical inputs yield consistent behavior.
FR24: The system can apply configuration changes only to new sessions.
FR25: The system can expose agent menu definitions exactly as configured.
FR26: The system can log each request with sessionId, agentId, and outcome.
FR27: The system can return clear error responses for invalid actions.
FR28: The system can surface workflow/tool failures to users.
FR29: The system can trace an interaction to agent, menu selection, and tool/workflow execution.
FR30: The system can prevent unknown tools or workflows from executing.
FR31: API consumers can list agents via REST.
FR32: API consumers can fetch agent details via REST.
FR33: API consumers can create sessions via REST.
FR34: API consumers can send chat messages via REST.
FR35: API consumers can retrieve transcripts via REST.
FR36: API consumers can reset sessions via REST.
FR37: Operators can inspect logs for session-level failures.
FR38: Operators can trace failures to configuration, workflow, or tool execution.
FR39: Support users can explain outcomes using transcripts and menu selections.
FR40: Operators can verify that execution stayed within allowlisted tools/workflows.

### NonFunctional Requirements

NFR1: Agent catalog, session creation, and transcript endpoints respond in under 1 second under normal load.
NFR2: Chat responses return within a few seconds under normal load.
NFR3: Workflow execution may take longer but must show clear progress and end with explicit success/failure.
NFR4: UI remains responsive during long-running workflows.
NFR5: Deterministic behavior: same agent + same config produces identical prompt composition.
NFR6: No cross-session state leakage.
NFR7: Menu rendering and selection resolution is deterministic.
NFR8: Errors are explicit and never silently swallowed.
NFR9: Only allowlisted tools and workflows can execute.
NFR10: Unknown or malformed tool/workflow requests are rejected.
NFR11: User-facing errors must not expose internal file paths, raw configs, or stack traces.
NFR12: MVP treats data as non-sensitive; authentication is deferred.
NFR13: MVP assumes low concurrency and single-node deployment; API design stays stateless where possible for future scaling.
NFR14: Session boundaries are explicit to avoid coupling that blocks scaling.
NFR15: UI meets WCAG 2.1 AA intent with keyboard navigation, visible focus, and accessible errors; avoid animation-heavy interactions.
NFR16: Public APIs are clean and documented to support future integrations (issue trackers, repos, CI/CD).

### Additional Requirements

- UI/API route alignment required: UI expects `GET /agents`, `GET /agents/{id}`, `POST /chat`, while API exposes `GET /api/agents` and `GET /WeatherForecast` (sample); missing endpoints must be added or the UI must be updated to match.
- Backend is .NET 8 ASP.NET Core with Swagger in dev; shared runtime library `agent_service` is the source of truth for agent catalog, persona loading, prompt composition, session management, and workflow/tool dispatch.
- Deterministic prompt composition and strict menu fidelity are non-negotiable operational qualities; behavior must be explainable and traceable (request -> selection -> tool/workflow execution).
- No persistence layer detected (no DB/ORM/migrations); session state approach must be defined explicitly (in-memory vs filesystem vs future DB) while preserving isolation and transcript retrieval.
- No deployment/IaC/CI config detected; MVP may run dev-grade but should not assume production infrastructure exists.
- UI is currently scaffold-level with minimal component structure; UX prioritizes dense, tool-like UI with clear agent identity, workflow state, and outcome artifacts.

### FR Coverage Map

### FR Coverage Map

FR1: Epic 1 - List agents from catalog.
FR2: Epic 1 - View agent detail (role/description/menu/commands).
FR3: Epic 1 - Distinguish agents by purpose/outcomes.
FR4: Epic 1 - See workflows/actions per agent.
FR5: Epic 2 - Create new session for selected agent.
FR6: Epic 2 - Send messages within a session.
FR7: Epic 2 - Retrieve session transcript.
FR8: Epic 2 - Reset session and clear state.
FR9: Epic 2 - Associate messages to session ID.
FR10: Epic 2 - Maintain isolated state per session.
FR11: Epic 3 - Present menu-based greetings.
FR12: Epic 3 - Select menu options by number/command/label.
FR13: Epic 3 - Resolve ambiguous selections deterministically.
FR14: Epic 3 - Provide clear feedback on invalid selections.
FR15: Epic 3 - Follow guided prompts driven by menu choices.
FR16: Epic 4 - Trigger workflows from menus.
FR17: Epic 4 - Execute workflows end-to-end per session.
FR18: Epic 4 - Produce structured artifacts as outputs.
FR19: Epic 4 - Surface workflow progress/completion states.
FR20: Epic 4 - Restrict workflows to allowlisted handlers.
FR21: Epic 5 - Load agent configuration from AgentData at runtime.
FR22: Epic 5 - Compose agent prompts deterministically from config.
FR23: Epic 5 - Ensure consistent behavior for identical inputs/config.
FR24: Epic 5 - Apply config changes only to new sessions.
FR25: Epic 1 - Expose agent menu definitions exactly as configured.
FR26: Epic 6 - Log each request with sessionId/agentId/outcome.
FR27: Epic 6 - Return clear error responses for invalid actions.
FR28: Epic 6 - Surface workflow/tool failures to users.
FR29: Epic 6 - Trace interaction to agent/menu/tool/workflow execution.
FR30: Epic 6 - Prevent unknown tools/workflows from executing.
FR31: Epic 1 - REST: list agents.
FR32: Epic 1 - REST: fetch agent details.
FR33: Epic 2 - REST: create sessions.
FR34: Epic 2 - REST: send chat messages.
FR35: Epic 2 - REST: retrieve transcripts.
FR36: Epic 2 - REST: reset sessions.
FR37: Epic 6 - Operators inspect logs for session failures.
FR38: Epic 6 - Operators trace failures to config/workflow/tool.
FR39: Epic 6 - Support explain outcomes via transcripts/selections.
FR40: Epic 6 - Operators verify execution stayed allowlisted.

## Epic List

## Epic List

### Epic 1: Agent Catalog & Inspection (Discoverability)
Users can browse the agent catalog and inspect an agent's details (role, menu, commands) to choose intentionally.
**FRs covered:** FR1, FR2, FR3, FR4, FR25, FR31, FR32

### Epic 2: Stateful Sessions & Transcripts (Core Interaction)
Users can start a session with a chosen agent, chat within that session, view transcript, and reset state safely.
**FRs covered:** FR5, FR6, FR7, FR8, FR9, FR10, FR33, FR34, FR35, FR36

### Epic 3: Menu-Driven BMAD Interaction (Deterministic UX)
Users interact via deterministic menu greetings and robust selection handling (number/command/label, ambiguity resolution, invalid feedback).
**FRs covered:** FR11, FR12, FR13, FR14, FR15

### Epic 4: Workflow Execution & Artifact Outputs (Guided Outcomes)
Users trigger workflows from menus; workflows execute end-to-end with progress visibility and durable artifacts.
**FRs covered:** FR16, FR17, FR18, FR19, FR20

### Epic 5: Config-Driven Agent Runtime Fidelity (BMAD Source-of-Truth)
System loads agent config/personas and composes prompts deterministically; config changes apply to new sessions only.
**FRs covered:** FR21, FR22, FR23, FR24

### Epic 6: Observability, Governance, and Failure Transparency
Operators/support can trace actions end-to-end; system enforces allowlists, blocks unknown actions, and surfaces failures clearly.
**FRs covered:** FR26, FR27, FR28, FR29, FR30, FR37, FR38, FR39, FR40

## Epic 1: Agent Catalog & Inspection (Discoverability)

Users can browse the agent catalog and inspect an agent's details (role, menu, commands) to choose intentionally.

### Story 1.1: Load Agent Catalog via Canonical API Route

**FRs covered:** FR1, FR3, FR4, FR31

As a user,
I want to see a list of available agents in the UI,
So that I can choose the right agent intentionally before starting work.

**Acceptance Criteria:**

**Given** the AgentChain UI is opened
**When** the catalog view loads
**Then** the UI requests the agent list from `GET {API_BASE_URL}/api/agents`
**And** the UI does not call `GET {API_BASE_URL}/agents` in MVP.

**Given** the API responds successfully
**When** the UI receives the agent list
**Then** the UI renders each agent with `id`, `title`, `description`, `icon`, `hasMenu`, `declaredCommands`, `version`
**And** the list is usable for selecting an agent to view details.

**Given** the API request fails (non-2xx or network error)
**When** the catalog view attempts to load
**Then** the UI shows a clear, user-friendly error state
**And** the UI does not display internal file paths, raw configs, or stack traces.

### Story 1.2: View Agent Details (Metadata + Menu Items Only)

**FRs covered:** FR2, FR25, FR32

As a user,
I want to view an agent's details (including its menu options),
So that I can confidently decide whether to start a session with that agent.

**Acceptance Criteria:**

**Given** I select an agent from the catalog
**When** the agent detail view loads
**Then** the UI requests agent details from `GET {API_BASE_URL}/api/agents/{id}`
**And** the UI does not call `GET {API_BASE_URL}/agents/{id}` in MVP.

**Given** the API responds `200 OK`
**When** the UI receives the agent details
**Then** the response includes only: `id`, `title`, `description`, `icon`, `hasMenu`, `declaredCommands`, `version`, `menuItems[]`
**And** each `menuItems[]` entry includes: `label` and `cmd` (nullable)
**And** the response explicitly excludes persona/system prompt sections and any full raw config blob.

**Given** the agent does not exist
**When** `GET /api/agents/{id}` is called
**Then** the API returns `404 Not Found`
**And** the UI shows a clear "Agent not found" state.

**Given** the API request fails (non-2xx or network error)
**When** the agent detail view attempts to load
**Then** the UI shows a clear, user-friendly error state
**And** the UI does not display internal file paths, raw configs, or stack traces.

### Story 1.3: Explicit, Non-Leaky Error States (Catalog + Detail)

**FRs covered:** FR27

As a user,
I want clear error states when agent loading fails,
So that I understand what happened and what to do next without seeing internal details.

**Acceptance Criteria:**

**Given** the UI requests `GET {API_BASE_URL}/api/agents`
**When** the request returns a non-2xx response or a network error occurs
**Then** the UI displays a clear error state with a retry action
**And** the UI does not display stack traces, internal file paths, raw configs, or prompt/persona text.

**Given** the UI requests `GET {API_BASE_URL}/api/agents/{id}`
**When** the request returns `404 Not Found`
**Then** the UI displays an "Agent not found" state
**And** the UI does not attempt to start a session for that missing agent.

**Given** the UI requests `GET {API_BASE_URL}/api/agents/{id}`
**When** the request returns a non-2xx response (other than 404) or a network error occurs
**Then** the UI displays a clear error state with a retry action
**And** the UI preserves the selected agent context (so retry targets the same `id`).

## Epic 2: Stateful Sessions & Transcripts (Core Interaction)

Users can start a session with a chosen agent, chat within that session, view transcript, and reset state safely.

### Story 2.1: Create Session for Selected Agent

**FRs covered:** FR5, FR9, FR10, FR33

As a user,
I want to create a new session for a selected agent,
So that my conversation state is isolated and can be continued reliably.

**Acceptance Criteria:**

**Given** I have selected a valid `agentId` from the catalog
**When** the UI requests a new session
**Then** the API creates a session via `POST {API_BASE_URL}/api/sessions`
**And** the request body includes `agentId`.

**Given** the session is created successfully
**When** the API responds
**Then** the response includes a new `sessionId`
**And** the `sessionId` is used by the UI for subsequent chat calls to `POST {API_BASE_URL}/api/chat`.

**Given** the provided `agentId` does not exist
**When** `POST /api/sessions` is called
**Then** the API returns `404 Not Found`
**And** the UI shows a clear "Agent not found" state.

**Given** the API request fails (non-2xx or network error)
**When** the UI attempts to create a session
**Then** the UI shows a clear, user-friendly error state
**And** the UI does not display internal file paths, raw configs, or stack traces.

### Story 2.2: Chat Within a Session (Canonical `/api/chat`)

**FRs covered:** FR6, FR9, FR10, FR34

As a user,
I want to send a message to the selected agent within my session,
So that I can have a stateful conversation with that agent.

**Acceptance Criteria:**

**Given** I have an existing `sessionId` created for an `agentId`
**When** I send a chat message
**Then** the UI sends the payload `{ agentId, sessionId, message }` to `POST {API_BASE_URL}/api/chat`
**And** the UI does not call `POST {API_BASE_URL}/chat` in MVP.

**Given** the chat request succeeds
**When** the API responds
**Then** the response includes the agent's reply text
**And** the UI appends both the user message and agent reply to the visible conversation for that session.

**Given** the provided `sessionId` does not exist (or is invalid)
**When** `POST /api/chat` is called
**Then** the API returns `404 Not Found`
**And** the UI shows a clear "Session not found" state.

**Given** the provided `agentId` does not exist
**When** `POST /api/chat` is called
**Then** the API returns `404 Not Found`
**And** the UI shows a clear "Agent not found" state.

**Given** the API request fails (non-2xx or network error)
**When** the UI attempts to send a chat message
**Then** the UI shows a clear, user-friendly error state
**And** the UI does not display internal file paths, raw configs, or stack traces.

### Story 2.3: Retrieve Transcript (Messages Only)

**FRs covered:** FR7, FR35

As a user,
I want to retrieve the transcript for my session,
So that I can review the conversation history at any time.

**Acceptance Criteria:**

**Given** I have an existing `sessionId`
**When** I open or refresh the session transcript view
**Then** the UI requests the transcript from `GET {API_BASE_URL}/api/sessions/{sessionId}/transcript`
**And** the transcript contains only user and assistant messages (messages-only).

**Given** the transcript is returned successfully
**When** the UI receives the transcript
**Then** the UI renders the messages in chronological order
**And** the UI associates the transcript to the correct `sessionId`.

**Given** the provided `sessionId` does not exist (or is invalid)
**When** `GET /api/sessions/{sessionId}/transcript` is called
**Then** the API returns `404 Not Found`
**And** the UI shows a clear "Session not found" state.

**Given** the transcript request fails (non-2xx or network error)
**When** the UI attempts to load the transcript
**Then** the UI shows a clear, user-friendly error state
**And** the UI does not display internal file paths, raw configs, stack traces, workflow/tool events, or persona/system prompt text.

### Story 2.4: Reset Session State

**FRs covered:** FR8, FR36

As a user,
I want to reset my session,
So that I can clear the conversation state and start fresh with the same agent.

**Acceptance Criteria:**

**Given** I have an existing `sessionId`
**When** I request a reset
**Then** the UI calls `POST {API_BASE_URL}/api/sessions/{sessionId}/reset`.

**Given** the reset succeeds
**When** the API responds
**Then** the session state and transcript for that `sessionId` are cleared
**And** the UI shows an empty conversation view for that session.

**Given** the provided `sessionId` does not exist (or is invalid)
**When** `POST /api/sessions/{sessionId}/reset` is called
**Then** the API returns `404 Not Found`
**And** the UI shows a clear "Session not found" state.

**Given** the reset request fails (non-2xx or network error)
**When** the UI attempts to reset the session
**Then** the UI shows a clear, user-friendly error state
**And** the UI does not display internal file paths, raw configs, or stack traces.

## Epic 3: Menu-Driven BMAD Interaction (Deterministic UX)

Users interact via deterministic menu greetings and robust selection handling (number/command/label, ambiguity resolution, invalid feedback).

### Story 3.1: Agent Greeting in Menu Mode

**FRs covered:** FR11

As a user,
I want the agent to greet me in menu mode at session start,
So that I immediately see the available actions and can choose deterministically.

**Acceptance Criteria:**

**Given** I create a new session for an `agentId`
**When** the session is created successfully
**Then** the API response includes the agent greeting text in menu mode
**And** the response includes the agent's menu items in the exact configured order.

**Given** the agent has menu items
**When** the greeting is returned
**Then** the menu items are numbered and displayed as configured (label + cmd when present)
**And** the menu rendering is deterministic for identical agent config.

**Given** the agent has no menu
**When** the greeting is returned
**Then** the response indicates no menu is available
**And** the UI does not invent menu items.

### Story 3.2: Deterministic Menu Selection Resolution (API-Resolved)

**FRs covered:** FR12, FR13

As a user,
I want to select an agent menu option by number, command, or label text,
So that the system resolves my intent deterministically and executes the correct next action.

**Acceptance Criteria:**

**Given** I have an active `sessionId` for an `agentId`
**When** I submit a menu selection input (raw text)
**Then** the UI sends the raw input to the API (not pre-resolved by the UI)
**And** the API evaluates the input against the agent's menu items in deterministic order.

**Given** the input matches a menu item number exactly
**When** the API resolves the selection
**Then** the API selects that menu item by position.

**Given** the input matches a menu item `cmd` (case-insensitive)
**When** the API resolves the selection
**Then** the API selects that menu item.

**Given** the input matches a unique substring of a menu item label (case-insensitive)
**When** the API resolves the selection
**Then** the API selects that menu item.

**Given** the input matches multiple menu item labels (ambiguous)
**When** the API resolves the selection
**Then** the API returns a "Please clarify" response
**And** includes the list of matching menu items for the user to choose from.

**Given** the input matches no menu items
**When** the API resolves the selection
**Then** the API returns "Not recognized"
**And** includes the full menu again.

**Given** the resolution succeeds
**When** the API responds
**Then** the API returns a structured outcome indicating the selected menu item (`label`, `cmd|null`)
**And** the UI renders the result and continues the flow.

### Story 3.3: Ambiguity + Invalid Selection UX (Clear + Deterministic)

**FRs covered:** FR13, FR14

As a user,
I want clear feedback when my menu selection is invalid or ambiguous,
So that I can correct it quickly without guesswork.

**Acceptance Criteria:**

**Given** I submit a selection that matches multiple menu items
**When** the API evaluates the input
**Then** the API returns a "Please clarify" response
**And** includes the matching menu items in their original menu order
**And** the UI renders the clarification prompt and the matching options.

**Given** I submit a selection that matches no menu items
**When** the API evaluates the input
**Then** the API returns "Not recognized"
**And** includes the full menu for the active agent
**And** the UI re-renders the menu and keeps the session active.

**Given** the API returns any error (non-2xx) during selection resolution
**When** the UI receives the error
**Then** the UI shows a clear, user-friendly error message
**And** does not display internal file paths, raw configs, stack traces, or persona/system prompt text.

### Story 3.4: Menu Redisplay Command (`*menu`)

**FRs covered:** FR15

As a user,
I want to redisplay the active agent's menu on demand,
So that I can re-orient and choose an action without restarting the session.

**Acceptance Criteria:**

**Given** I have an active `sessionId`
**When** I submit the input `*menu`
**Then** the API returns the current agent menu in menu mode
**And** the menu items are returned in the exact configured order.

**Given** the active agent has no menu
**When** I submit `*menu`
**Then** the API responds that no menu is available
**And** the UI does not invent menu items.

**Given** the request fails (non-2xx or network error)
**When** the UI attempts to redisplay the menu
**Then** the UI shows a clear, user-friendly error state
**And** the UI does not display internal file paths, raw configs, stack traces, or persona/system prompt text.

## Epic 4: Workflow Execution & Artifact Outputs (Guided Outcomes)

Users trigger workflows from menus; workflows execute end-to-end with progress visibility and durable artifacts.

### Story 4.1: Start Workflow from Menu Selection

**FRs covered:** FR16, FR17, FR20

As a user,
I want to start a workflow by selecting it from the agent menu,
So that I can complete structured tasks without ad-hoc prompting.

**Acceptance Criteria:**

**Given** I have an active `sessionId` with an agent that exposes workflow menu items
**When** I select a workflow menu item (resolved by the API)
**Then** the API starts that workflow for the session
**And** returns a workflow run identifier (e.g., `runId`) and an initial progress state.

**Given** the selected menu item references an unknown or non-allowlisted workflow
**When** the workflow start is attempted
**Then** the API rejects the request with a clear error response
**And** does not execute any workflow actions.

### Story 4.2: Workflow Progress Reporting

**FRs covered:** FR19, FR28

As a user,
I want to see workflow progress as it runs,
So that I know what step the workflow is on and whether it succeeded or failed.

**Acceptance Criteria:**

**Given** a workflow is running for my session
**When** I view the workflow progress
**Then** I see a step-by-step progress log suitable for UI rendering
**And** the workflow ends with an explicit success or failure outcome.

**Given** a workflow fails mid-run
**When** the API returns failure
**Then** the user-visible failure message is explicit and non-leaky
**And** the session remains usable after the failure.

### Story 4.3: Persist Workflow Artifacts

**FRs covered:** FR18

As a user,
I want workflow outputs saved as durable artifacts,
So that I can review and reuse them after the workflow finishes.

**Acceptance Criteria:**

**Given** a workflow produces an output artifact
**When** the workflow completes
**Then** the artifact is saved to the configured artifacts location
**And** the API returns artifact metadata (e.g., `artifactId`, `name`, `type`, `createdAt`).

### Story 4.4: List and Retrieve Artifacts

**FRs covered:** FR18

As a user,
I want to list and retrieve artifacts created by workflows,
So that I can inspect results without rerunning workflows.

**Acceptance Criteria:**

**Given** my session has produced artifacts
**When** I request the artifact list for that session
**Then** the API returns artifacts in deterministic order (e.g., by creation time)
**And** the UI can request a specific artifact by id to view its content.

## Epic 5: Config-Driven Agent Runtime Fidelity (BMAD Source-of-Truth)

System loads agent config/personas and composes prompts deterministically; config changes apply to new sessions only.

### Story 5.1: Load Agent Runtime from AgentData

**FRs covered:** FR21

As an operator,
I want the system to load agent definitions from AgentData,
So that agents can be added or updated without code changes.

**Acceptance Criteria:**

**Given** the AgentData agents directory is configured
**When** the API loads the agent catalog
**Then** agents are discovered from AgentData
**And** catalog order is deterministic.

**Given** the AgentData directory is missing or unreadable
**When** the API attempts to load agents
**Then** the API returns a clear error response
**And** does not leak filesystem paths in user-facing messages.

### Story 5.2: Deterministic Agent Versioning

**FRs covered:** FR22, FR23

As an operator,
I want each agent to have a deterministic version identifier derived from its definition,
So that clients can detect changes and sessions can be audited against a known agent version.

**Acceptance Criteria:**

**Given** an agent definition file is unchanged
**When** the API loads the agent catalog or agent detail
**Then** the returned `version` value is identical across runs.

**Given** an agent definition file changes
**When** the API reloads the agent
**Then** the returned `version` changes deterministically based on content.

### Story 5.3: Session Pins to Agent Version

**FRs covered:** FR23, FR24

As a user,
I want my session to remain stable even if an agent definition changes,
So that ongoing work is not disrupted.

**Acceptance Criteria:**

**Given** a session is created for an `agentId`
**When** the session is created
**Then** the session records the agent `version` used for that session.

**Given** the agent definition changes after session creation
**When** I continue chatting in the existing session
**Then** behavior remains consistent with the pinned agent version
**And** new sessions use the latest agent version.

## Epic 6: Observability, Governance, and Failure Transparency

Operators/support can trace actions end-to-end; system enforces allowlists, blocks unknown actions, and surfaces failures clearly.

### Story 6.1: Structured Logging for Requests

**FRs covered:** FR26, FR37

As an operator,
I want structured logs for each request,
So that I can trace failures by `sessionId`, `agentId`, action type, and outcome.

**Acceptance Criteria:**

**Given** any API request is processed
**When** the request completes
**Then** the system logs a structured event including `sessionId` (if available), `agentId` (if available), request type, and outcome.

### Story 6.2: Safe, Explicit Error Responses

**FRs covered:** FR27, FR39

As a user,
I want errors that are clear and actionable,
So that I understand what failed without leaking internal details.

**Acceptance Criteria:**

**Given** an invalid action is requested (unknown agent, unknown session, unknown menu selection)
**When** the API rejects the request
**Then** the API returns an explicit error response (e.g., 404/400 as appropriate)
**And** does not expose internal file paths, raw configs, stack traces, or persona/system prompt text.

### Story 6.3: Governance: Block Unknown Tools/Workflows

**FRs covered:** FR20, FR30, FR40

As an operator,
I want the system to prevent execution of unknown tools or workflows,
So that only allowlisted behaviors can run.

**Acceptance Criteria:**

**Given** a request attempts to execute a tool or workflow not on the allowlist
**When** the system evaluates the request
**Then** execution is blocked
**And** the response is explicit to the user
**And** an audit log entry records the block decision.

### Story 6.4: End-to-End Traceability for Sessions and Actions

**FRs covered:** FR29, FR38

As an operator,
I want to trace a user interaction end-to-end (agent, menu selection, workflow/tool execution),
So that I can debug failures and explain outcomes confidently.

**Acceptance Criteria:**

**Given** a user performs actions in a `sessionId`
**When** the system processes requests and produces responses
**Then** each interaction is traceable via structured logs that link `sessionId`, `agentId`, selection/action type, and outcome.

**Given** a workflow or tool execution fails for a session
**When** an operator inspects logs for that `sessionId`
**Then** the logs provide enough detail to identify whether the failure came from configuration, workflow execution, or tool execution
**And** user-facing error messages remain non-leaky.
