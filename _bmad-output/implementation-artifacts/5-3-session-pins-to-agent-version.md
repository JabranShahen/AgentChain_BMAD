---
storyId: "5.3"
storyKey: "5-3-session-pins-to-agent-version"
epic: "5"
title: "Session Pins to Agent Version"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 5.3: Session Pins to Agent Version

Status: ready-for-dev

## Story

**FRs covered:** FR23, FR24

As a user,
I want my session to remain stable even if an agent definition changes,
So that ongoing work is not disrupted.

## Acceptance Criteria

AC1
**Given** a session is created for an `agentId`
**When** the session is created
**Then** the session records the agent `version` used for that session.

AC2
**Given** the agent definition changes after session creation
**When** I continue chatting in the existing session
**Then** behavior remains consistent with the pinned agent version
**And** new sessions use the latest agent version.

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
