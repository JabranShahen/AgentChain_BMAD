---
storyId: "6.2"
storyKey: "6-2-safe-explicit-error-responses"
epic: "6"
title: "Safe, Explicit Error Responses"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 6.2: Safe, Explicit Error Responses

Status: ready-for-dev

## Story

**FRs covered:** FR27, FR39

As a user,
I want errors that are clear and actionable,
So that I understand what failed without leaking internal details.

## Acceptance Criteria

AC1
**Given** an invalid action is requested (unknown agent, unknown session, unknown menu selection)
**When** the API rejects the request
**Then** the API returns an explicit error response (e.g., 404/400 as appropriate)
**And** does not expose internal file paths, raw configs, stack traces, or persona/system prompt text.

## Tasks / Subtasks

- [ ] Task 1: Implement AC1 (AC: AC1)
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
