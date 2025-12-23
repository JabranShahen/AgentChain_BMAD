---
storyId: "5.2"
storyKey: "5-2-deterministic-agent-versioning"
epic: "5"
title: "Deterministic Agent Versioning"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 5.2: Deterministic Agent Versioning

Status: ready-for-dev

## Story

**FRs covered:** FR22, FR23

As an operator,
I want each agent to have a deterministic version identifier derived from its definition,
So that clients can detect changes and sessions can be audited against a known agent version.

## Acceptance Criteria

AC1
**Given** an agent definition file is unchanged
**When** the API loads the agent catalog or agent detail
**Then** the returned `version` value is identical across runs.

AC2
**Given** an agent definition file changes
**When** the API reloads the agent
**Then** the returned `version` changes deterministically based on content.

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
