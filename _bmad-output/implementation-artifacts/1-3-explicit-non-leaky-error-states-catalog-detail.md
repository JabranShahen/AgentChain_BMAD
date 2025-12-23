---
storyId: "1.3"
storyKey: "1-3-explicit-non-leaky-error-states-catalog-detail"
epic: "1"
title: "Explicit, Non-Leaky Error States (Catalog + Detail)"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 1.3: Explicit, Non-Leaky Error States (Catalog + Detail)

Status: ready-for-dev

## Story

**FRs covered:** FR27

As a user,
I want clear error states when agent loading fails,
So that I understand what happened and what to do next without seeing internal details.

## Acceptance Criteria

AC1
**Given** the UI requests `GET {API_BASE_URL}/api/agents`
**When** the request returns a non-2xx response or a network error occurs
**Then** the UI displays a clear error state with a retry action
**And** the UI does not display stack traces, internal file paths, raw configs, or prompt/persona text.

AC2
**Given** the UI requests `GET {API_BASE_URL}/api/agents/{id}`
**When** the request returns `404 Not Found`
**Then** the UI displays an "Agent not found" state
**And** the UI does not attempt to start a session for that missing agent.

AC3
**Given** the UI requests `GET {API_BASE_URL}/api/agents/{id}`
**When** the request returns a non-2xx response (other than 404) or a network error occurs
**Then** the UI displays a clear error state with a retry action
**And** the UI preserves the selected agent context (so retry targets the same `id`).

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
