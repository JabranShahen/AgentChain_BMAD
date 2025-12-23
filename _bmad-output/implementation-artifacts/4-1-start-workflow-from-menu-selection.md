---
storyId: "4.1"
storyKey: "4-1-start-workflow-from-menu-selection"
epic: "4"
title: "Start Workflow from Menu Selection"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 4.1: Start Workflow from Menu Selection

Status: ready-for-dev

## Story

**FRs covered:** FR16, FR17, FR20

As a user,
I want to start a workflow by selecting it from the agent menu,
So that I can complete structured tasks without ad-hoc prompting.

## Acceptance Criteria

AC1
**Given** I have an active `sessionId` with an agent that exposes workflow menu items
**When** I select a workflow menu item (resolved by the API)
**Then** the API starts that workflow for the session
**And** returns a workflow run identifier (e.g., `runId`) and an initial progress state.

AC2
**Given** the selected menu item references an unknown or non-allowlisted workflow
**When** the workflow start is attempted
**Then** the API rejects the request with a clear error response
**And** does not execute any workflow actions.

## Tasks / Subtasks

- [ ] Task 1: Implement AC1 (AC: AC1)
  - [ ] Code changes
  - [ ] Tests (unit/integration where applicable; otherwise document manual verification)
  - [ ] Manual verification steps documented

- [ ] Task 2: Implement AC2 (AC: AC2)
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
