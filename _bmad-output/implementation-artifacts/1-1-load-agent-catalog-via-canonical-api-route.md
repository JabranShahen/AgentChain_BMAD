---
storyId: "1.1"
storyKey: "1-1-load-agent-catalog-via-canonical-api-route"
epic: "1"
title: "Load Agent Catalog via Canonical API Route"
status: "done"
createdBy: "SM (*create-story #yolo)"
sourceArtifacts:
  - "_bmad-output/epics.md"
  - "_bmad-output/integration-architecture.md"
  - "_bmad-output/architecture-ui.md"
  - "_bmad-output/api-contracts-api.md"
---

# Story 1.1: Load Agent Catalog via Canonical API Route

Status: done

## Story

As a user,
I want to see a list of available agents in the UI,
so that I can choose the right agent intentionally before starting work.

## Acceptance Criteria

AC1
**Given** the AgentChain UI is opened
**When** the catalog view loads
**Then** the UI requests the agent list from `GET {API_BASE_URL}/api/agents`
**And** the UI does not call `GET {API_BASE_URL}/agents` in MVP.

AC2
**Given** the API responds successfully
**When** the UI receives the agent list
**Then** the UI renders each agent with `id`, `title`, `description`, `icon`, `hasMenu`, `declaredCommands`, `version`
**And** the list is usable for selecting an agent to view details.

AC3
**Given** the API request fails (non-2xx or network error)
**When** the catalog view attempts to load
**Then** the UI shows a clear, user-friendly error state
**And** the UI does not display internal file paths, raw configs, or stack traces.

## Tasks / Subtasks

- [x] Task 1: Update UI catalog endpoint to `/api/agents` (AC: AC1)
  - [x] Locate agent catalog fetch in `AgentChain_UI/AgentChainUI/src/App.tsx`
  - [x] Change fetch path from `/agents` to `/api/agents`
  - [x] Verify no remaining UI calls to `/agents` for catalog

- [x] Task 2: Ensure catalog rendering uses expected fields (AC: AC2)
  - [x] Confirm UI types align with API response fields (update `AgentChain_UI/src/types.ts` if needed)
  - [x] Verify agent list renders title/description/icon/menu indicator without regressions

- [x] Task 3: Error handling is explicit and non-leaky (AC: AC3)
  - [x] Ensure fetch failure renders a readable message + retry affordance (if one exists)
  - [x] Do not surface raw error objects/stack traces in the UI

## Dev Notes

### API Contract (catalog)
- Endpoint: `GET /api/agents`
- Response item fields: `id`, `title`, `description?`, `icon?`, `hasMenu`, `declaredCommands[]`, `version`
- Source: `_bmad-output/api-contracts-api.md`

### UI Integration Constraints
- Base URL is `VITE_API_BASE_URL` (or UI fallback); ensure the final URL is `{API_BASE_URL}/api/agents`.
- Avoid route duplication: MVP does **not** call `/agents` (canonical is `/api/agents`).
- Source: `_bmad-output/integration-architecture.md`, `_bmad-output/architecture-ui.md`

### Testing Requirements
- UI repo currently has no test harness configured (no `npm test`), so add tests only if project already supports them.
- Minimum verification (manual):
  1) Run UI + API locally; confirm agent list loads.
  2) Confirm DevTools network shows `GET /api/agents` (and no `/agents`).
  3) Simulate API down; confirm user-friendly error and no internal leak.

### References
- `_bmad-output/epics.md` (Epic 1 / Story 1.1 acceptance criteria)
- `_bmad-output/integration-architecture.md` (route mismatch context)
- `_bmad-output/architecture-ui.md` (UI structure + API usage)
- `_bmad-output/api-contracts-api.md` (catalog endpoint contract)

## Dev Agent Record

### Agent Model Used

GPT-5 (Codex CLI)

### Debug Log References

- `npm run lint` (AgentChain_UI)
- `npm run lint` (AgentChain_UI) after code review fixes

### Completion Notes List

- Updated catalog endpoint to `/api/agents` for list fetch; list renders id/title/description/icon/menu/version/commands.
- Catalog rendering now uses API summary fields (title, description, icon, hasMenu, declaredCommands, version).
- Added retry affordance for catalog load failures; error messaging remains non-leaky.
- Code review fix: detail endpoint now uses `/api/agents/{id}` and menu items render using `label`/`cmd` to match API detail shape.
- Lint passed; no automated tests configured in UI project.

### File List

- `AgentChain_UI/src/App.tsx`
- `AgentChain_UI/src/types.ts`
