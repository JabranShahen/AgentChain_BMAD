---
storyId: "2.1"
storyKey: "2-1-create-session-for-selected-agent"
epic: "2"
title: "Create Session for Selected Agent"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 2.1: Create Session for Selected Agent

Status: ready-for-dev

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
