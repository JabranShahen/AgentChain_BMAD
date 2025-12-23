---
storyId: "1.2"
storyKey: "1-2-view-agent-details-metadata-menu-items-only"
epic: "1"
title: "View Agent Details (Metadata + Menu Items Only)"
status: "ready-for-dev"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 1.2: View Agent Details (Metadata + Menu Items Only)

Status: ready-for-dev

## Story

**FRs covered:** FR2, FR25, FR32

As a user,
I want to view an agent's details (including its menu options),
So that I can confidently decide whether to start a session with that agent.

## Acceptance Criteria

AC1
**Given** I select an agent from the catalog
**When** the agent detail view loads
**Then** the UI requests agent details from `GET {API_BASE_URL}/api/agents/{id}`
**And** the UI does not call `GET {API_BASE_URL}/agents/{id}` in MVP.

AC2
**Given** the API responds `200 OK`
**When** the UI receives the agent details
**Then** the response includes only: `id`, `title`, `description`, `icon`, `hasMenu`, `declaredCommands`, `version`, `menuItems[]`
**And** each `menuItems[]` entry includes: `label` and `cmd` (nullable)
**And** the response explicitly excludes persona/system prompt sections and any full raw config blob.

AC3
**Given** the agent does not exist
**When** `GET /api/agents/{id}` is called
**Then** the API returns `404 Not Found`
**And** the UI shows a clear "Agent not found" state.

AC4
**Given** the API request fails (non-2xx or network error)
**When** the agent detail view attempts to load
**Then** the UI shows a clear, user-friendly error state
**And** the UI does not display internal file paths, raw configs, or stack traces.

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
