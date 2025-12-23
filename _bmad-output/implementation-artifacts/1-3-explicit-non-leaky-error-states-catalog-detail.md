---
storyId: "1.3"
storyKey: "1-3-explicit-non-leaky-error-states-catalog-detail"
epic: "1"
title: "Explicit, Non-Leaky Error States (Catalog + Detail)"
status: "done"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/prd.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-api.md"
  - "_bmad-output/architecture-ui.md"
---
# Story 1.3: Explicit, Non-Leaky Error States (Catalog + Detail)

Status: done

## Story

**FRs covered:** FR27

As a user,
I want clear error states when agent loading fails,
So that I understand what happened and what to do next without seeing internal details.

## Acceptance Criteria

AC1
**Given** the UI requests `GET {API_BASE_URL}/api/agents`
**When** the request returns a non-2xx response or a network error occurs
**Then** the UI displays a clear error state with a retry action
**And** the UI does not display stack traces, internal file paths, raw configs, or prompt/persona text.

AC2
**Given** the UI requests `GET {API_BASE_URL}/api/agents/{id}`
**When** the request returns `404 Not Found`
**Then** the UI displays an "Agent not found" state
**And** the UI does not attempt to start a session for that missing agent.

AC3
**Given** the UI requests `GET {API_BASE_URL}/api/agents/{id}`
**When** the request returns a non-2xx response (other than 404) or a network error occurs
**Then** the UI displays a clear error state with a retry action
**And** the UI preserves the selected agent context (so retry targets the same `id`).

## Tasks / Subtasks

- [x] Task 1: Implement AC1 (AC: AC1)
  - [x] Code changes
  - [x] Tests (unit/integration where applicable; otherwise document manual verification)
  - [x] Manual verification steps documented

- [x] Task 2: Implement AC2 (AC: AC2)
  - [x] Code changes
  - [x] Tests (unit/integration where applicable; otherwise document manual verification)
  - [x] Manual verification steps documented

- [x] Task 3: Implement AC3 (AC: AC3)
  - [x] Code changes
  - [x] Tests (unit/integration where applicable; otherwise document manual verification)
  - [x] Manual verification steps documented

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

GPT-5

### Debug Log References

- npm install (AgentChain_UI)
- npm test (vitest run)
- npm run lint
- npm test (vitest run) after review fixes
- npm run lint after review fixes

### Completion Notes List

- AC1: added catalog error copy in list panel and retry; added UI test coverage for catalog failure state; manual verification: simulate failed `GET /api/agents` (e.g., stop API) and confirm error + retry shown with no internal details.
- AC1 follow-up: clear stale catalog selection on error; retry test now exercises refresh behavior.
- AC2: added UI test coverage for 404 detail error and ensured no chat request fires; manual verification: request an invalid agent id and confirm "Agent not found" with retry.
- AC3: added UI test coverage for detail non-404/network errors, retry action, and selection preservation; manual verification: force detail endpoint to 500 and confirm retry targets same agent.

### File List

- _bmad-output/implementation-artifacts/1-3-explicit-non-leaky-error-states-catalog-detail.md
- _bmad-output/implementation-artifacts/1-2-view-agent-details-metadata-menu-items-only.md
- AgentChain_UI/.gitignore
- AgentChain_UI/package.json
- AgentChain_UI/package-lock.json
- AgentChain_UI/vite.config.js
- AgentChain_UI/src/setupTests.ts
- AgentChain_UI/src/App.test.tsx
- AgentChain_UI/src/App.tsx
