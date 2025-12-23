---
storyId: "2.1"
storyKey: "2-1-create-session-for-selected-agent"
epic: "2"
title: "Create Session for Selected Agent"
status: "done"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 2.1: Create Session for Selected Agent

Status: done

## Story

**FRs covered:** FR5, FR9, FR10, FR33

As a user,
I want to create a new session for a selected agent,
So that my conversation state is isolated and can be continued reliably.

## Acceptance Criteria

AC1
**Given** I have selected a valid `agentId` from the catalog
**When** the UI requests a new session
**Then** the API creates a session via `POST {API_BASE_URL}/api/sessions`
**And** the request body includes `agentId`.

AC2
**Given** the session is created successfully
**When** the API responds
**Then** the response includes a new `sessionId`
**And** the `sessionId` is used by the UI for subsequent chat calls to `POST {API_BASE_URL}/api/chat`.

AC3
**Given** the provided `agentId` does not exist
**When** `POST /api/sessions` is called
**Then** the API returns `404 Not Found`
**And** the UI shows a clear "Agent not found" state.

AC4
**Given** the API request fails (non-2xx or network error)
**When** the UI attempts to create a session
**Then** the UI shows a clear, user-friendly error state
**And** the UI does not display internal file paths, raw configs, or stack traces.

## Tasks / Subtasks

- [x] Task 1: Implement AC1 (AC: AC1)
  - [x] Add `IAgentSessionStore` + `InMemoryAgentSessionStore`, register via `AddAgentCatalogServices`
  - [x] Create `POST /api/sessions` that validates `agentId` with `IAgentCatalog`, returns `sessionId`/`version`, and covers 404 via new endpoint tests
  - [x] Manual verification: call `/api/sessions` for an existing agent and confirm the created session id is returned (covered by tests)

- [x] Task 2: Implement AC2 (AC: AC2)
  - [x] Update `AgentChain_UI/src/App.tsx` to POST `/api/sessions` after agent detail loads, store the session, and block chat sends until a session exists
  - [x] Extend `AgentChain_UI/src/App.test.tsx` to assert the session request payload/sequence and keep chat disabled before session creation
  - [x] Manual verification: select an agent in the UI and confirm the network requests follow `GET /api/agents/{id}` → `POST /api/sessions` before `/api/chat`

- [x] Task 3: Implement AC3 (AC: AC3)
  - [x] Ensure the session endpoint returns 404 when `agentId` is unknown and surface the "Agent not found" copy without leaking internal details
  - [x] Add UI behavior/tests so a missing agent produces the same friendly message and prevents chat from running
  - [x] Manual verification: request a session for an invalid agent and confirm the user-facing "Agent not found." state with retry

- [x] Task 4: Implement AC4 (AC: AC4)
  - [x] Surface a user-friendly session error in the header/chat panel and provide a retry action, avoiding stack traces/raw configs
  - [x] Cover failure + retry flows in Vitest so the chat endpoint never fires while a session is unavailable
  - [x] Manual verification: force `POST /api/sessions` to fail (500) and ensure the retry button recreates the session without leaking details

## Dev Notes

- Session creation now flows through `AiAgent.Abstractions.IAgentSessionStore` backed by `InMemoryAgentSessionStore`, and the service is registered alongside the agent catalog so catalog metadata (from `AgentData`) is reused for deterministic versioning.
- `POST /api/sessions` validates the requested `agentId`, returns `{ sessionId, agentId, version }`, and surfaces 404 for missing agents without leaking stack traces.
- The UI waits for the agent detail response, posts to `/api/sessions`, stores the returned `sessionId`, blocks chat submissions until the session exists, and surfaces session errors with retry actions in both the header and chat panel.
- Vitest now covers session success, failure, and retry flows in addition to the existing non-leaky error assertions so the chat endpoint only runs after a session is ready.
- Primary references: `_bmad-output/epics.md` (Story 2.1), `_bmad-output/architecture-api.md`, `_bmad-output/architecture-ui.md`

### References
- _bmad-output/epics.md
- _bmad-output/prd.md
- _bmad-output/integration-architecture.md
- _bmad-output/architecture-api.md
- _bmad-output/architecture-ui.md

## Dev Agent Record

### Agent Model Used

GPT-5 (Codex CLI)

### Debug Log References

- `dotnet test agent_service.Tests/agent_service.Tests.csproj`
- `npm test`
- `npm run lint`

### Completion Notes List

- Added the session store interface/implementation, wired it through DI, and created unit tests for `POST /api/sessions`.
- Implemented UI session creation, blocking, and retry states plus Vitest coverage for success/failure flows.
- Documented deterministic version usage, friendly errors, and the chat lockout until a session is available.
- Verified backend tests, Vitest, and ESLint (`dotnet test`, `npm test`, `npm run lint`).

### File List

- `AgentChain_API/againt_chain_api/Configuration/AgentCatalogServiceCollectionExtensions.cs`
- `AgentChain_API/againt_chain_api/Features/Sessions/Endpoints/SessionsEndpoints.cs`
- `AgentChain_API/againt_chain_api/Program.cs`
- `AgentChain_API/agent_service/Abstractions/IAgentSessionStore.cs`
- `AgentChain_API/agent_service/Sessions/InMemoryAgentSessionStore.cs`
- `AgentChain_API/agent_service.Tests/SessionsEndpointsTests.cs`
- `AgentChain_UI/src/App.tsx`
- `AgentChain_UI/src/App.test.tsx`
- `AgentChain_UI/src/types.ts`
