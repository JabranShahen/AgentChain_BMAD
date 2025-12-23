# Architecture (UI)

## Executive Summary
- React + Vite single-page UI for browsing and chatting with agent personas.
- Client-side rendering only; no server-side UI layer detected.
- Integrates with backend API via HTTPS using a configurable base URL.

## Technology Stack

| Category | Technology | Version | Notes |
| --- | --- | --- | --- |
| Language | TypeScript | ES2020 target | `tsconfig.json` |
| UI Framework | React | 19.2.0 | `package.json` |
| Build Tool | Vite (rolldown-vite) | 7.2.5 | `package.json` overrides |

## Architecture Pattern
- Component-based SPA with React (client-side UI, Vite build pipeline).

## Core UI Components
- `src/App.tsx`: main UI shell, agent list, agent detail, and chat panel.
- `src/main.tsx`: app bootstrap and root render.
- `src/types.ts`: API payload typings for agents and chat.

## State and Data Flow
- App-level state managed with React hooks (`useState`, `useMemo`, `useEffect`).
- Agent catalog loaded on mount; agent detail fetched on selection change.
- Chat history stored per agent ID; session ID reused when available.

## API Integration
- Base URL: `VITE_API_BASE_URL` (env) or fallback.
- Endpoints referenced by UI:
  - `GET /agents`
  - `GET /agents/{id}`
  - `POST /chat`
- Backend currently exposes `/api/agents` and `/WeatherForecast` (see integration doc for mismatch).

## Component Inventory
- No dedicated `components/` or `views/` folders yet; UI is scaffold-level.
- See `component-inventory-ui.md` for current inventory.

## Source Tree Notes
- Primary code under `AgentChain_UI/AgentChainUI/src/`.
- Static assets under `public/`.

## Development Workflow
- Install: `npm install`
- Run: `npm run dev`
- Build: `npm run build`
- Lint: `npm run lint`
- Tests: no test script found

## Deployment Architecture
- No deployment configuration detected (no Docker/IaC/CI).

## Testing Strategy
- No UI test setup detected (no test scripts or test folders).

## Known Gaps
- API route mismatch between UI expectations and backend exposure.
- No authentication flow implemented in UI.

---
_Generated using BMAD Method `document-project` workflow_
