---
storyId: "2.2"
storyKey: "2-2-chat-within-a-session-canonical-api-chat"
epic: "2"
title: "Chat Within a Session (Canonical `/api/chat`)"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 2.2: Chat Within a Session (Canonical `/api/chat`)

Status: ready-for-dev

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

- [ ] Task 1: Implement AC1 (AC: AC1)
  - [ ] Code changes
  - [ ] Tests (unit/integration where applicable; otherwise document manual verification)
  - [ ] Manual verification steps documented

- [ ] Task 2: Implement AC2 (AC: AC2)
  - [ ] Code changes
  - [ ] Tests (unit/integration where applicable; otherwise document manual verification)
  - [ ] Manual verification steps documented

- [ ] Task 3: Implement AC3 (AC: AC3)
  - [ ] Code changes
  - [ ] Tests (unit/integration where applicable; otherwise document manual verification)
  - [ ] Manual verification steps documented

- [ ] Task 4: Implement AC4 (AC: AC4)
  - [ ] Code changes
  - [ ] Tests (unit/integration where applicable; otherwise document manual verification)
  - [ ] Manual verification steps documented

- [ ] Task 5: Implement AC5 (AC: AC5)
  - [ ] Code changes
  - [ ] Tests (unit/integration where applicable; otherwise document manual verification)
  - [ ] Manual verification steps documented

## Dev Notes

- Primary source of truth: _bmad-output/epics.md (this story section)
- Keep outputs non-leaky: no internal file paths, raw configs, stack traces, or persona/system prompt text in user-visible errors.

### References
- _bmad-output/epics.md
- _bmad-output/prd.md
- _bmad-output/integration-architecture.md
- _bmad-output/architecture-api.md
- _bmad-output/architecture-ui.md

## Dev Agent Record

### Agent Model Used

TBD

### Debug Log References

TBD

### Completion Notes List

TBD

### File List

TBD
