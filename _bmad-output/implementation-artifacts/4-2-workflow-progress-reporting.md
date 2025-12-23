---
storyId: "4.2"
storyKey: "4-2-workflow-progress-reporting"
epic: "4"
title: "Workflow Progress Reporting"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 4.2: Workflow Progress Reporting

Status: ready-for-dev

## Story

**FRs covered:** FR19, FR28

As a user,
I want to see workflow progress as it runs,
So that I know what step the workflow is on and whether it succeeded or failed.

## Acceptance Criteria

AC1
**Given** a workflow is running for my session
**When** I view the workflow progress
**Then** I see a step-by-step progress log suitable for UI rendering
**And** the workflow ends with an explicit success or failure outcome.

AC2
**Given** a workflow fails mid-run
**When** the API returns failure
**Then** the user-visible failure message is explicit and non-leaky
**And** the session remains usable after the failure.

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
