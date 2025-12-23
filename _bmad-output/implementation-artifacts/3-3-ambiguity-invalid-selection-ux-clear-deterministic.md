---
storyId: "3.3"
storyKey: "3-3-ambiguity-invalid-selection-ux-clear-deterministic"
epic: "3"
title: "Ambiguity + Invalid Selection UX (Clear + Deterministic)"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 3.3: Ambiguity + Invalid Selection UX (Clear + Deterministic)

Status: ready-for-dev

## Story

**FRs covered:** FR13, FR14

As a user,
I want clear feedback when my menu selection is invalid or ambiguous,
So that I can correct it quickly without guesswork.

## Acceptance Criteria

AC1
**Given** I submit a selection that matches multiple menu items
**When** the API evaluates the input
**Then** the API returns a "Please clarify" response
**And** includes the matching menu items in their original menu order
**And** the UI renders the clarification prompt and the matching options.

AC2
**Given** I submit a selection that matches no menu items
**When** the API evaluates the input
**Then** the API returns "Not recognized"
**And** includes the full menu for the active agent
**And** the UI re-renders the menu and keeps the session active.

AC3
**Given** the API returns any error (non-2xx) during selection resolution
**When** the UI receives the error
**Then** the UI shows a clear, user-friendly error message
**And** does not display internal file paths, raw configs, stack traces, or persona/system prompt text.

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
