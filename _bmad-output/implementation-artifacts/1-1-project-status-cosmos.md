# Story 1.1: Project Status in Cosmos

Status: ready-for-dev

<!-- Note: Validation is optional. Run validate-create-story for quality check before dev-story. -->

## Story

As a project owner,
I want project development status stored in Cosmos and updated via service bus messages,
so that the UI always shows reliable, current progress from a single source of truth.

## Acceptance Criteria

1. Project status is persisted on the `Project` entity in Cosmos with fields for `Status` and `StatusUpdatedUtc`, and is exposed by API responses and UI models.
2. `POST /api/development/start` validates the project and ownership, updates status to `queued`, and publishes a Service Bus message that includes `ProjectId`, `ProjectName`, `ProjectFolder`, `UserId`, `SessionId`, and `SessionApiBaseUrl`.
3. Codex publishes status updates (`in_progress`, `completed`, `failed`) to a dedicated Service Bus queue/topic with `ProjectId`, `UserId`, `Status`, optional `Details`, and `TimestampUtc`.
4. API runs a background consumer that updates `Project.Status` from status messages using allowed transitions and idempotency (ignore invalid or out-of-order updates).
5. UI polls the API for project status and updates the “Start Development” button: queued/in_progress show a spinner and disabled state, completed enables download, failed shows an error and allows retry.
6. The UI never connects directly to Service Bus; status shown in the UI is always read from the API.

## Tasks / Subtasks

- [ ] Add `Status` and `StatusUpdatedUtc` to `Project` entity and project DTOs; default new projects to `idle` (AC: 1)
- [ ] Update create/update project flows to preserve and return status (AC: 1)
- [ ] Extend `DocumentReadyMessage` to include `ProjectId` and publish it from `POST /api/development/start` (AC: 2)
- [ ] Implement a Service Bus status consumer in API that updates project status in Cosmos with transition validation (AC: 3, 4)
- [ ] Add config for the status queue/topic and wire it in `Program.cs` (AC: 3, 4)
- [ ] Update Codex to publish status updates to the status queue/topic (AC: 3)
- [ ] Update UI project type and add polling to surface `Project.Status` in the Document Map modal (AC: 5, 6)
- [ ] Add UI behavior for queued/in_progress/completed/failed states (AC: 5)

## Dev Notes

### Developer Context

- API currently publishes only `document-ready` messages and has no project status fields.
- Codex consumes the `document-ready` message and does not publish status updates.
- UI only calls `/api/development/start` and logs the response; it does not show status or poll.

### Technical Requirements

- Status source of truth is Cosmos (`Project` entity). UI reads status from API only.
- Add a dedicated status message (do not reuse the document-ready queue).
- Messages must include `ProjectId` so API can update the correct project.

### Architecture Compliance

- Keep ownership validation in API (project must belong to user before changing status).
- Service Bus credentials remain server-side only; no direct browser access.

### File Structure Requirements

- Entity + DTOs: `AgentChain_API/AgentChainAbstractions/Entites/Project/Project.cs`, `AgentChain_API/againt_chain_api/Controllers/ProjectsController.cs`
- Development start: `AgentChain_API/againt_chain_api/Controllers/DevelopmentController.cs`
- Service Bus: `AgentChain_API/againt_chain_api/Services/ServiceBusPublisher.cs`
- Codex SB processing: `AgentChain_Codex/CodexRunner/Program.cs`
- UI types + modal: `AgentChain_UI/src/types.ts`, `AgentChain_UI/src/DocumentMapModal.tsx`

### Testing Requirements

- API tests for status transitions and ownership validation.
- API tests for status message consumption idempotency and invalid transition rejection.
- UI tests for button state changes based on status values.

### References

- [Source: AgentChain_API/AgentChainAbstractions/Entites/Project/Project.cs]
- [Source: AgentChain_API/againt_chain_api/Controllers/ProjectsController.cs]
- [Source: AgentChain_API/againt_chain_api/Controllers/DevelopmentController.cs]
- [Source: AgentChain_API/againt_chain_api/Services/ServiceBusPublisher.cs]
- [Source: AgentChain_Codex/CodexRunner/Program.cs]
- [Source: AgentChain_UI/src/DocumentMapModal.tsx]
- [Source: AgentChain_UI/src/types.ts]

## Dev Agent Record

### Agent Model Used

TBD (filled by dev agent during implementation)

### Debug Log References

- Story context created from API/UI/Codex code review and user clarification.

### Completion Notes List

- Story prepared for cross-app project status lifecycle with Cosmos as source of truth.

### File List

- _bmad-output/implementation-artifacts/1-1-project-status-cosmos.md
