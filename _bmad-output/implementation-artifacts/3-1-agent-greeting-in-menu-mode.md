---
storyId: "3.1"
storyKey: "3-1-agent-greeting-in-menu-mode"
epic: "3"
title: "Agent Greeting in Menu Mode"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 3.1: Agent Greeting in Menu Mode

Status: ready-for-dev

## Story

**FRs covered:** FR11

As a user,
I want the agent to greet me in menu mode at session start,
So that I immediately see the available actions and can choose deterministically.

## Acceptance Criteria

AC1
**Given** I create a new session for an `agentId`
**When** the session is created successfully
**Then** the API response includes the agent greeting text in menu mode
**And** the response includes the agent's menu items in the exact configured order.

AC2
**Given** the agent has menu items
**When** the greeting is returned
**Then** the menu items are numbered and displayed as configured (label + cmd when present)
**And** the menu rendering is deterministic for identical agent config.

AC3
**Given** the agent has no menu
**When** the greeting is returned
**Then** the response indicates no menu is available
**And** the UI does not invent menu items.

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
