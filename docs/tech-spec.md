# Tech Spec: AgentChain API + Angular Console (V1)

## Goals
- Expose BMAD agents/workflows via an HTTP API for internal consumers.
- Provide a UI to browse agents, start sessions, and view streaming or buffered replies.
- Keep V1 simple: in-memory session state, API-key guard, pluggable LLM client.

## Non-Goals (V1)
- Durable persistence, RBAC, billing/quotas, audit trails.
- Multi-tenant isolation beyond a shared API key.
- Advanced analytics/observability beyond basic logging.

## Architecture Overview
- **Backend:** ASP.NET Core API.
- **Agent data source:** BMAD assets at `.bmad/` (manifest at `.bmad/_cfg/agent-manifest.csv`, persona files under `.bmad/bmm/agents/`).
- **LLM client:** Pluggable interface (e.g., `ILLMClient`) with an initial concrete implementation deferred until a provider is chosen.
- **Session store:** In-memory per-process; replaceable via interface.
- **Streaming:** Optional SignalR hub for incremental tokens; fallback to REST responses.
- **Frontend:** Angular 19 (SSR scaffold present) consuming the API.

## Backend Components
- **Controllers**
  - `AgentsController`
    - `GET /agents` → list agents (id, displayName, title, role, icon) from manifest.
    - `GET /agents/{id}` → details (merged manifest + persona summary).
  - `ChatController`
    - `POST /chat` → start session with `{agentId, message, sessionId?}`; returns sessionId + reply (or stream via SignalR).
    - `GET /chat/{sessionId}` → fetch session transcript (in-memory for V1).
  - `PartyController` (optional V1.1)
    - `POST /party` → start multi-agent session (`agentIds?` optional to select subset).
    - Streams messages via SignalR; REST fallback returns aggregated turn.
- **Services**
  - `IAgentCatalog` → loads manifest CSV and resolves agent personas (minimal parse of markdown frontmatter/title/description).
  - `IChatService` → routes prompts to LLM with agent persona context; handles session state.
  - `ISessionStore` → in-memory dictionary `{sessionId → transcript}`.
  - `ILLMClient` → abstraction for model calls (provider TBD).
  - `IAuthorizationService` (simple) → validates API key from header (e.g., `x-api-key`).
- **Models**
  - `AgentSummary` { id, displayName, title, icon, role }
  - `AgentDetail` { summary fields + persona snippets (description, principles) }
  - `ChatRequest` { sessionId?, agentId, message }
  - `ChatResponse` { sessionId, messages: [{ from, content, ts }] }
  - `PartyRequest` { sessionId?, agentIds?, message }
- **Configuration**
  - `BMAD_ROOT` defaults to repo root `.bmad/`.
  - `LLM` provider/config placeholders (API key, model name).
  - `API_KEY` for simple auth.

## Data Flow (Chat, REST path)
1. Client calls `POST /chat` with `{agentId, message, sessionId?}`.
2. `ChatController` validates API key, binds request.
3. `IAgentCatalog` loads agent persona + manifest data.
4. `IChatService` builds prompt with agent persona and prior transcript (if sessionId present).
5. `ILLMClient` generates reply (sync for REST); `IChatService` stores turn in `ISessionStore`.
6. Response returns `{sessionId, messages:[latest turn]}`.

## Data Flow (Chat, SignalR path)
1–4 as above; 5 emits tokens/events over SignalR hub (`/chatHub`), updating store on completion; 6 acknowledges sessionId to caller.

## Frontend (Angular) Pages
- **Agents list:** Fetch `/agents`, show cards; click to open chat.
- **Chat console:** Select agent, send message, display transcript; if SignalR enabled, stream tokens.
- **Sessions list (simple):** Show recent in-memory sessions (optional V1); link to resume chat if store retained.

## Error Handling
- 401 on missing/invalid API key.
- 404 on unknown agentId.
- 429 optional guard if rate limits added later.
- 500 with minimal leakage; log exceptions server-side.

## Logging
- Request/response metadata: requestId, sessionId, agentId, duration, outcome (success/error).
- Optionally log prompts/responses to console in dev; redact in prod.

## Testing Plan
- Unit: `IAgentCatalog` manifest parsing; `IChatService` session assembly; `ISessionStore` CRUD.
- Integration: `GET /agents`, `POST /chat` happy-path with stub LLM client; auth failure returns 401; unknown agent returns 404.
- Frontend e2e (later): agents list renders; chat flow posts and renders reply (with mocked backend).

## Migration/Deployment
- Single-process in-memory sessions for V1; note that scaling out will lose history (call out in README).
- Config via appsettings + env overrides.
- Enable Swagger for internal use.

## Open Decisions
- Choose LLM provider SDK (OpenAI, Azure OpenAI, local).
- Decide whether to include SignalR in V1 or defer to V1.1.
- Persistence upgrade path (Redis/DB) for sessions.

## API Endpoint Contracts (REST, V1)
Headers (all endpoints)
- `x-api-key: <key>` (required, simple shared secret)

`GET /agents`
- Response 200:
```json
{
  "agents": [
    { "id": "analyst", "displayName": "Mary", "title": "Business Analyst", "icon": "🧭", "role": "Strategic Business Analyst + Requirements Expert" }
  ]
}
```

`GET /agents/{id}`
- Response 200:
```json
{
  "id": "analyst",
  "displayName": "Mary",
  "title": "Business Analyst",
  "icon": "🧭",
  "role": "Strategic Business Analyst + Requirements Expert",
  "description": "…",
  "principles": [
    "Every business challenge has root causes…",
    "Articulate requirements with precision…"
  ]
}
```
- 404 if unknown id.

`POST /chat`
- Request:
```json
{
  "agentId": "analyst",
  "message": "Summarize the project vision",
  "sessionId": "optional-existing-session-id"
}
```
- Response 200 (REST mode):
```json
{
  "sessionId": "generated-or-reused-id",
  "messages": [
    { "from": "user", "content": "Summarize the project vision", "ts": "2025-12-06T01:00:00Z" },
    { "from": "analyst", "content": "Project vision is…", "ts": "2025-12-06T01:00:01Z" }
  ]
}
```
- Errors: 401 (missing/invalid key), 404 (agent), 400 (invalid payload).

`GET /chat/{sessionId}`
- Response 200:
```json
{
  "sessionId": "abc123",
  "messages": [
    { "from": "user", "content": "Hi", "ts": "…" },
    { "from": "analyst", "content": "Hello!", "ts": "…" }
  ]
}
```
- 404 if session not found (note: in-memory only for V1).

## SignalR (optional V1.1)
- Hub: `/chatHub`
- Events:
  - Client → Server: `SendMessage(agentId, sessionId?, message)`
  - Server → Client stream: `message` event `{ sessionId, from, content, ts, isFinal }`
- REST and SignalR should share session store/LLM client to keep transcripts consistent.

## Example Angular Usage (REST)
- List agents: `GET /agents` → render cards.
- Start chat: `POST /chat` with agentId/message → display returned messages; keep `sessionId` for follow-ups.
- Resume chat: call `POST /chat` with same `sessionId`.

## Minimal Interfaces (sketch)
```csharp
public interface IAgentCatalog {
    Task<IReadOnlyList<AgentSummary>> ListAsync();
    Task<AgentDetail?> GetAsync(string id);
}

public interface ISessionStore {
    Task<ChatSession> GetAsync(string sessionId);
    Task UpsertAsync(ChatSession session);
}

public interface ILLMClient {
    Task<string> CompleteAsync(string prompt, CancellationToken ct = default);
    // Optionally: IAsyncEnumerable<string> StreamAsync(...)
}
```
