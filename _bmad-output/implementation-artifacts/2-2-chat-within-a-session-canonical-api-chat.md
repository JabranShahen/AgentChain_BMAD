---
storyId: "2.2"
storyKey: "2-2-chat-within-a-session-canonical-api-chat"
epic: "2"
title: "Chat Within a Session (Canonical `/api/chat`)"
status: "done"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 2.2: Chat Within a Session (Canonical `/api/chat`)

Status: done

## Story

**FRs covered:** FR6, FR9, FR10, FR34

As a user,
I want to send a message to the selected agent within my session,
So that I can have a stateful conversation with that agent.

## Acceptance Criteria

AC1
**Given** I have an existing `sessionId` created for an `agentId`
**When** I send a chat message
**Then** the UI sends the payload `{ agentId, sessionId, message }` to `POST {API_BASE_URL}/api/chat`
**And** the UI does not call `POST {API_BASE_URL}/chat` in MVP.

AC2
**Given** the chat request succeeds
**When** the API responds
**Then** the response includes the agent's reply text
**And** the UI appends both the user message and agent reply to the visible conversation for that session.

AC3
**Given** the provided `sessionId` does not exist (or is invalid)
**When** `POST /api/chat` is called
**Then** the API returns `404 Not Found`
**And** the UI shows a clear "Session not found" state.

AC4
**Given** the provided `agentId` does not exist
**When** `POST /api/chat` is called
**Then** the API returns `404 Not Found`
**And** the UI shows a clear "Agent not found" state.

AC5
**Given** the API request fails (non-2xx or network error)
**When** the UI attempts to send a chat message
**Then** the UI shows a clear, user-friendly error state
**And** the UI does not display internal file paths, raw configs, or stack traces.

## Tasks / Subtasks

- [x] Task 1: Implement AC1 (AC: AC1)
  - [x] Add canonical `/api/chat` endpoint that validates the catalog and stored session, and returns `{ sessionId, messages[] }` with user + assistant entries (no raw config leaks).
  - [x] Covered the endpoint with `agent_service.Tests/ChatEndpointsTests.cs` to exercise bad payloads, missing agents, invalid sessions, and the happy path.
  - [x] Manual verification: POSTing `/api/chat` against a valid session returns both user/assistant messages and the expected session id.

- [x] Task 2: Implement AC2 (AC: AC2)
  - [x] Updated `AgentChain_UI/src/App.tsx` to include `sessionId`/`agentId`/`message` in the `/api/chat` payload, append the returned messages, and keep chat disabled until a session exists.
  - [x] Added Vitest coverage (`App.test.tsx`) confirming the chat payload, the UI appending assistant replies, and that chat never runs before the session is ready.
  - [x] Manual verification: send text after a session is created and confirm the network trace shows `/api/chat` with the proper JSON and the UI renders both messages.

- [x] Task 3: Implement AC3 (AC: AC3)
  - [x] `ChatEndpoints` returns `ErrorResponse("Session not found.")` for missing/mismatched sessions so clients get non-leaky 404s.
  - [x] UI displays "Session not found." in the header/chat panel, clears the stale session, and blocks chat until the user retries.
  - [x] Manual verification: hitting `/api/chat` with an invalid session shows the friendly session error without exposing internal details.

- [x] Task 4: Implement AC4 (AC: AC4)
  - [x] Invalid `agentId` in the chat payload now produces a 404 + `ErrorResponse("Agent not found.")`, and the UI surfaces the message via the chat error scope.
  - [x] Vitest ensures the chat UI shows the agent-level error without firing a chat retry or leaking stack traces.
  - [x] Manual verification: send a payload for a nonexistent agent and confirm the UI error reads "Agent not found."

- [x] Task 5: Implement AC5 (AC: AC5)
  - [x] Chat failure handling now distinguishes 404 vs. other failures, showing user-friendly text and keeping logs clean.
  - [x] Added UI tests for the general failure path and the session-not-found retry flow so `POST /api/chat` is never retried blindly.
  - [x] Manual verification: simulate a 500 response and observe the header error + disabled send button without leaking internals.

## Dev Notes

- `/api/chat` now enforces the agent/session contract via `AiAgent.Abstractions.IAgentSessionStore` and returns deterministic `ChatMessageResponse` entries that the UI can append directly.
- The UI sends `{ agentId, sessionId, message }`, waits for the session to exist before enabling the send button, and surfaces clear text for session/agent errors without leaking stack traces.
- Vitest covers successful replies plus both session/missing agent scenarios, while the backend tests guard every chat error path and response shape.
- Primary references: `_bmad-output/epics.md` (Story 2.2), `_bmad-output/architecture-api.md`, `_bmad-output/architecture-ui.md`

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

- Added canonical `POST /api/chat` that validates agent/session and returns user + assistant messages along with a structured error response.
- Updated the UI to include `{ agentId, sessionId, message }`, disable chat until a session exists, and surface session/agent errors with retryable UI affordances.
- Extended Vitest with chat success/failure coverage so the send button never fires before a session is ready and session-level errors stay visible.
- Documented results, reran backend/unit tests, and linted the UI (`dotnet test`, `npm test`, `npm run lint`).

### File List

- `AgentChain_API/againt_chain_api/Features/Chat/Endpoints/ChatEndpoints.cs`
- `AgentChain_API/agent_service.Tests/ChatEndpointsTests.cs`
- `AgentChain_UI/src/App.tsx`
- `AgentChain_UI/src/App.test.tsx`
