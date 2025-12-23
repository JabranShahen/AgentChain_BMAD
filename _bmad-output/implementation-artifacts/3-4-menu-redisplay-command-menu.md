---
storyId: "3.4"
storyKey: "3-4-menu-redisplay-command-menu"
epic: "3"
title: "Menu Redisplay Command (`*menu`)"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 3.4: Menu Redisplay Command (`*menu`)

Status: ready-for-dev

## Story

**FRs covered:** FR15

As a user,
I want to redisplay the active agent's menu on demand,
So that I can re-orient and choose an action without restarting the session.

## Acceptance Criteria

AC1
**Given** I have an active `sessionId`
**When** I submit the input `*menu`
**Then** the API returns the current agent menu in menu mode
**And** the menu items are returned in the exact configured order.

AC2
**Given** the active agent has no menu
**When** I submit `*menu`
**Then** the API responds that no menu is available
**And** the UI does not invent menu items.

AC3
**Given** the request fails (non-2xx or network error)
**When** the UI attempts to redisplay the menu
**Then** the UI shows a clear, user-friendly error state
**And** the UI does not display internal file paths, raw configs, stack traces, or persona/system prompt text.

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
