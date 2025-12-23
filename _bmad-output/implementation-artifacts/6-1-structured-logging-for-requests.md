---
storyId: "6.1"
storyKey: "6-1-structured-logging-for-requests"
epic: "6"
title: "Structured Logging for Requests"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 6.1: Structured Logging for Requests

Status: ready-for-dev

## Story

**FRs covered:** FR26, FR37

As an operator,
I want structured logs for each request,
So that I can trace failures by `sessionId`, `agentId`, action type, and outcome.

## Acceptance Criteria

AC1
**Given** any API request is processed
**When** the request completes
**Then** the system logs a structured event including `sessionId` (if available), `agentId` (if available), request type, and outcome.

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
