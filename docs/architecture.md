# AgentChain Architecture Addendum

Concrete implementation details to accompany the existing tech spec. Scope: V1 REST-first with optional SignalR later; in-memory state; API-key guard; BMAD assets under `.bmad/`.

## Configuration
- `BMAD_ROOT` (default `.bmad/`), override via appsettings/env.
- Required assets: `{BMAD_ROOT}/_cfg/agent-manifest.csv`, `{BMAD_ROOT}/bmm/agents/*.md`.
- `API_KEY` for `x-api-key` header validation.
- `LLM` config placeholder (provider, model, key); `ENABLE_SIGNALR` toggle (future).

## Data Contracts (DTOs)
- `AgentSummary`: `id, displayName, title, icon, role`.
- `AgentDetail`: `AgentSummary` + `description, principles`.
- `ChatRequest`: `{ agentId, message, sessionId? }`.
- `ChatResponse`: `{ sessionId, messages: [{ from, content, ts }] }`.

## Backend Components
- `IAgentCatalog`: parses manifest CSV; loads persona markdown (frontmatter/body) to merge fields; normalizes/sanitizes icons/text; returns summaries/details; handles missing persona gracefully.
- `IChatService`: assembles prompts from agent detail + transcript; calls `ILLMClient`; stores turns via `ISessionStore`; supports streaming when enabled.
- `ISessionStore`: in-memory `{ sessionId -> transcript }`; swappable later (Redis/DB).
- `ILLMClient`: abstraction for completion/stream; initial stub.
- `IAuthorizationService`/middleware: validates `x-api-key`.

## Controllers / Endpoints
- `GET /agents`: list `AgentSummary`; 200 on success; 401 if no/invalid key.
- `GET /agents/{id}`: `AgentDetail`; 404 on unknown id.
- `POST /chat`: `ChatRequest` → `ChatResponse`; 401 on auth failure; 404 on unknown agent; 400 on bad payload.
- `GET /chat/{sessionId}`: transcript; 404 if missing (in-memory).
- (Later) SignalR hub `/chatHub` mirrors chat flow.

## Data Flow
- List/detail: Controller → auth → `IAgentCatalog` (merge manifest+persona) → DTO serialization.
- Chat: Controller → auth → agent validation via catalog → `IChatService` → `ILLMClient` (stub) → `ISessionStore` update → response/stream.

## Error Handling & Logging
- 401 for missing/invalid API key; 404 for unknown agent/session; 500 with minimal leakage.
- Log `requestId, sessionId, agentId, duration, outcome`; optionally prompt/response in dev.
- Swagger enabled in dev only.

## Frontend Expectations (Angular 19)
- Pages: Agents list (cards with name/title/icon/role snippet), Agent detail (description, principles), Chat placeholder wired to POST `/chat`.
- Graceful fallback for missing icons/descriptions; preserve “3 clicks to first session” goal (list → select → chat).

## Testing Checklist
- Unit: manifest parse happy/edge, persona merge, session store CRUD, chat service assembly with stub LLM.
- Integration: `GET /agents` 200, `GET /agents/{id}` 404, `POST /chat` 401 without key, `POST /chat` 200 with stub LLM and valid agent.

