---
storyId: "2.4"
storyKey: "2-4-reset-session-state"
epic: "2"
title: "Reset Session State"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 2.4: Reset Session State

Status: ready-for-dev

## Story

**FRs covered:** FR8, FR36

As a user,
I want to reset my session,
So that I can clear the conversation state and start fresh with the same agent.

## Acceptance Criteria

AC1
**Given** I have an existing `sessionId`
**When** I request a reset
**Then** the UI calls `POST {API_BASE_URL}/api/sessions/{sessionId}/reset`.

AC2
**Given** the reset succeeds
**When** the API responds
**Then** the session state and transcript for that `sessionId` are cleared
**And** the UI shows an empty conversation view for that session.

AC3
**Given** the provided `sessionId` does not exist (or is invalid)
**When** `POST /api/sessions/{sessionId}/reset` is called
**Then** the API returns `404 Not Found`
**And** the UI shows a clear "Session not found" state.

AC4
**Given** the reset request fails (non-2xx or network error)
**When** the UI attempts to reset the session
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
