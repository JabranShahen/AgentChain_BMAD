---
storyId: "6.3"
storyKey: "6-3-governance-block-unknown-tools-workflows"
epic: "6"
title: "Governance: Block Unknown Tools/Workflows"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 6.3: Governance: Block Unknown Tools/Workflows

Status: ready-for-dev

## Story

**FRs covered:** FR20, FR30, FR40

As an operator,
I want the system to prevent execution of unknown tools or workflows,
So that only allowlisted behaviors can run.

## Acceptance Criteria

AC1
**Given** a request attempts to execute a tool or workflow not on the allowlist
**When** the system evaluates the request
**Then** execution is blocked
**And** the response is explicit to the user
**And** an audit log entry records the block decision.

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
