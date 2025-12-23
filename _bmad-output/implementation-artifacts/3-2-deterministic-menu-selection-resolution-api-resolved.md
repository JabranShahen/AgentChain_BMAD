---
storyId: "3.2"
storyKey: "3-2-deterministic-menu-selection-resolution-api-resolved"
epic: "3"
title: "Deterministic Menu Selection Resolution (API-Resolved)"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 3.2: Deterministic Menu Selection Resolution (API-Resolved)

Status: ready-for-dev

## Story

**FRs covered:** FR12, FR13

As a user,
I want to select an agent menu option by number, command, or label text,
So that the system resolves my intent deterministically and executes the correct next action.

## Acceptance Criteria

AC1
**Given** I have an active `sessionId` for an `agentId`
**When** I submit a menu selection input (raw text)
**Then** the UI sends the raw input to the API (not pre-resolved by the UI)
**And** the API evaluates the input against the agent's menu items in deterministic order.

AC2
**Given** the input matches a menu item number exactly
**When** the API resolves the selection
**Then** the API selects that menu item by position.

AC3
**Given** the input matches a menu item `cmd` (case-insensitive)
**When** the API resolves the selection
**Then** the API selects that menu item.

AC4
**Given** the input matches a unique substring of a menu item label (case-insensitive)
**When** the API resolves the selection
**Then** the API selects that menu item.

AC5
**Given** the input matches multiple menu item labels (ambiguous)
**When** the API resolves the selection
**Then** the API returns a "Please clarify" response
**And** includes the list of matching menu items for the user to choose from.

AC6
**Given** the input matches no menu items
**When** the API resolves the selection
**Then** the API returns "Not recognized"
**And** includes the full menu again.

AC7
**Given** the resolution succeeds
**When** the API responds
**Then** the API returns a structured outcome indicating the selected menu item (`label`, `cmd|null`)
**And** the UI renders the result and continues the flow.

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

- [ ] Task 4: Implement AC4 (AC: AC4)
  - [ ] Code changes
  - [ ] Tests (unit/integration where applicable; otherwise document manual verification)
  - [ ] Manual verification steps documented

- [ ] Task 5: Implement AC5 (AC: AC5)
  - [ ] Code changes
  - [ ] Tests (unit/integration where applicable; otherwise document manual verification)
  - [ ] Manual verification steps documented

- [ ] Task 6: Implement AC6 (AC: AC6)
  - [ ] Code changes
  - [ ] Tests (unit/integration where applicable; otherwise document manual verification)
  - [ ] Manual verification steps documented

- [ ] Task 7: Implement AC7 (AC: AC7)
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
