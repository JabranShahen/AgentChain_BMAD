---
storyId: "6.4"
storyKey: "6-4-end-to-end-traceability-for-sessions-and-actions"
epic: "6"
title: "End-to-End Traceability for Sessions and Actions"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 6.4: End-to-End Traceability for Sessions and Actions

Status: ready-for-dev

## Story

**FRs covered:** FR29, FR38

As an operator,
I want to trace a user interaction end-to-end (agent, menu selection, workflow/tool execution),
So that I can debug failures and explain outcomes confidently.

## Acceptance Criteria

AC1
**Given** a user performs actions in a `sessionId`
**When** the system processes requests and produces responses
**Then** each interaction is traceable via structured logs that link `sessionId`, `agentId`, selection/action type, and outcome.

AC2
**Given** a workflow or tool execution fails for a session
**When** an operator inspects logs for that `sessionId`
**Then** the logs provide enough detail to identify whether the failure came from configuration, workflow execution, or tool execution
**And** user-facing error messages remain non-leaky.

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
