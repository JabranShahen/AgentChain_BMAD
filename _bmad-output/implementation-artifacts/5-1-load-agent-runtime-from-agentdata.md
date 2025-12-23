---
storyId: "5.1"
storyKey: "5-1-load-agent-runtime-from-agentdata"
epic: "5"
title: "Load Agent Runtime from AgentData"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 5.1: Load Agent Runtime from AgentData

Status: ready-for-dev

## Story

**FRs covered:** FR21

As an operator,
I want the system to load agent definitions from AgentData,
So that agents can be added or updated without code changes.

## Acceptance Criteria

AC1
**Given** the AgentData agents directory is configured
**When** the API loads the agent catalog
**Then** agents are discovered from AgentData
**And** catalog order is deterministic.

AC2
**Given** the AgentData directory is missing or unreadable
**When** the API attempts to load agents
**Then** the API returns a clear error response
**And** does not leak filesystem paths in user-facing messages.

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
