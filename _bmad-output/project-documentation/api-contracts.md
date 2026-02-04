# API Contracts (core)

## Key controllers and endpoints discovered in `AgentChain_API/againt_chain_api/Controllers`

| Resource | Description |
| --- | --- |
| `POST /api/chat` | Accepts chat requests tied to an existing session (`ChatController`). Validates session/agent, appends transcript entries, and returns the OpenAI-style response pair. Also exposes `/simple` for unauthenticated quick questions.
| `GET /api/projects` & `POST /api/projects` | Project CRUD resides in `ProjectsController` and `ProjectDocumentsController`, managing metadata plus the related documents/teams. `/api/projects/{projectId}/agents` (`ProjectAgentsController`) handles agent bootstrap and summaries.
| `GET /api/agents` | Lists available agent definitions (see `AgentsController`).
| `POST /api/projects/{projectId}/agents/bootstrap` | Bootstraps agents per project using `agent catalog` JSON files stored beside the repo.
| `GET /api/sessions`, `POST /api/sessions`, `POST /api/sessions/{sessionId}/resume` | `SessionsController` tracks interactive sessions with transcripts stored via `ISessionTranscriptStore` and `ISessionTranscriptBlobStore`.
| `POST /api/blob-documents` | `BlobDocumentsController` handles document ingestion/export from Azure blob storage (used by integration with Codex runner artifacts).
| `POST /api/development/restart` (sample) | `DevelopmentController` exposes maintenance ops for templates, caching, and agent build/test helper tasks.
| `POST /api/storage/upload`, `GET /api/storage/info` | `StorageController` provides support endpoints for uploaded artifacts and diagnostic info.
| `AccountController` | Exposes account claims + user context (sign-in/out, identity) so every endpoint can resolve `AccountId` from JWT before persisting.

## Contracts and Payloads

- **Chat payloads** (`ChatController` + `AgentChainAbstractions.Entites):
  - `ChatRequest`: `AgentId`, `SessionId`, `Message`, optional `SessionState`.
  - `ChatResponse`: `SessionId`, consecutive `ChatMessageResponse` entries (`user` / `assistant`).
- **Agent bootstrap** (`ProjectAgentsController`): returns `BootstrapAgentsResponse` containing `ProjectAgentDefinition` entries populated from JSON catalog files under `agent_service/agents`.
- **Session documents** (`SessionsController` + `SessionDocument` entity) persist transcripts plus metadata for retrieval by the UI (the UI polls `api/sessions`).
- **Project metadata** (`Project` entity) includes `AccountId`, `Name`, `Description`, and timestamps. Every project-level controller validates ownership via JWT (`AccountController` helper) before calling persistence stores.

## Security

- JWT bearer authentication (`Microsoft.AspNetCore.Authentication.JwtBearer` in `againt_chain_api.csproj`).
- Controllers apply `[Authorize]` except the “simple chat” variant (depending on request validation) and rely on `ResolveAccountId` helpers before touching persistence.

