# Epic: AgentChain V1 Enablement

Purpose: deliver the first usable slice of the AgentChain API + UI so internal users can list BMAD agents, view personas, and start basic chat sessions with API-key protection.

## Scope
- Backend: ASP.NET Core 8, REST-first; API-key guard; in-memory session store; stub LLM client; Swagger in dev only.
- Data source: BMAD assets under `BMAD_ROOT` (default `.bmad/`): `_cfg/agent-manifest.csv` + `bmm/agents/*.md`.
- Frontend: React SSR; agents list, detail, and chat placeholder wired to REST.

## Stories

1) API foundation — **Done**
- Build API-key middleware using `x-api-key`; configurable via appsettings/env.
- Enable Swagger only in dev; set config defaults (`BMAD_ROOT`, `API_KEY`, `LLM` placeholders).
- Acceptance: Requests without/invalid key return 401/403; Swagger reachable only in Development; config loads defaults and allows env override.

2) Agent catalog + endpoints — **Done**
- Implement `IAgentCatalog`: parse manifest CSV; load persona markdown; merge fields; sanitize icons/text; handle missing personas gracefully.
- Add `GET /agents` (summaries) and `GET /agents/{id}` (detail + principles/description).
- Acceptance: `/agents` returns list with manifest data; unknown id yields 404; icons/text are safe for UI; catalog tolerates missing persona file without crash.

3) Chat skeleton — **Done**
- Add in-memory `ISessionStore`; stub `ILLMClient`.
- Implement `POST /chat` and `GET /chat/{sessionId}` using agent detail for prompt assembly; enforce API key; 404 on unknown agent/session.
- Acceptance: `/chat` rejects missing key (401), unknown agent (404), returns sessionId + messages with stub reply; `/chat/{sessionId}` returns stored turns or 404.

4) Logging and tests
- Log `requestId, sessionId, agentId, duration, outcome`; central exception handling to 500 with minimal leakage.
- Tests: unit (catalog parsing happy/edge; session store CRUD); integration (`/agents` 200/404; `/chat` 401/200 with stub).
- Acceptance: Logs emitted per request with the listed fields; tests cover stated cases and pass locally.

- 5) React UI MVP
- Replace starter page with agents list (cards); agent detail view (description, principles); chat placeholder posting to `/chat`.
- Handle missing icons/descriptions gracefully; basic loading/error states; maintain “3 clicks to first session” path (list → select → chat).
- Acceptance: UI renders agent list from `/agents`; detail fetches `/agents/{id}`; chat form posts to `/chat` and shows response; empty/missing icon does not break layout.

## Out of scope (V1)
- Durable persistence, RBAC, billing/quotas, advanced analytics.
- SignalR streaming (may be enabled later, not required for this epic).
