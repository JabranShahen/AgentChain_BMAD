---
storyId: "2.3"
storyKey: "2-3-retrieve-transcript-messages-only"
epic: "2"
title: "Retrieve Transcript (Messages Only)"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 2.3: Retrieve Transcript (Messages Only)

Status: ready-for-dev

## Story

**FRs covered:** FR7, FR35

As a user,
I want to retrieve the transcript for my session,
So that I can review the conversation history at any time.

## Acceptance Criteria

AC1
**Given** I have an existing `sessionId`
**When** I open or refresh the session transcript view
**Then** the UI requests the transcript from `GET {API_BASE_URL}/api/sessions/{sessionId}/transcript`
**And** the transcript contains only user and assistant messages (messages-only).

AC2
**Given** the transcript is returned successfully
**When** the UI receives the transcript
**Then** the UI renders the messages in chronological order
**And** the UI associates the transcript to the correct `sessionId`.

AC3
**Given** the provided `sessionId` does not exist (or is invalid)
**When** `GET /api/sessions/{sessionId}/transcript` is called
**Then** the API returns `404 Not Found`
**And** the UI shows a clear "Session not found" state.

AC4
**Given** the transcript request fails (non-2xx or network error)
**When** the UI attempts to load the transcript
**Then** the UI shows a clear, user-friendly error state
**And** the UI does not display internal file paths, raw configs, stack traces, workflow/tool events, or persona/system prompt text.

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
