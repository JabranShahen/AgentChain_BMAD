# Story: Inject Generated Project Documents Into Every Agent Prompt

Status: review

## Summary
As a project user, I want each agent to preload all generated markdown docs for my project so that every chat starts with the full, shared context.

## Why
Generated docs live in blob storage but are only used for document generation dependencies, not for agent prompts, which makes cross-agent responses inconsistent.

## Scope
- Session/chat flows where `projectId` is known.
- Include generated docs from blob storage under `documents/{projectFolder}/generated/`.

## Out of Scope
- Changing document generation content or UI.
- Simple chat without a project id.

## Acceptance Criteria
1. Agents created/restored for a project append a "Generated Documents" section to the system prompt containing every `.md` blob in the project’s generated folder (plus legacy generated paths if needed), ordered by last modified desc.
2. Documents are filtered by project metadata (projectId/projectFolder) so no cross-project leakage; non-markdown blobs are ignored.
3. Prompt augmentation is idempotent (re-creating or restoring sessions must not duplicate the section).
4. If no generated docs exist, the prompt remains unchanged.
5. Safety limits are enforced: per-doc and total size caps with a clear `[TRUNCATED]` marker when content is shortened.

## Tasks/Subtasks
- [x] Extend blob store to list generated markdown docs for a project.
- [x] Add list method to `IUserDocumentBlobStore` for generated docs (prefix + metadata filter) returning path/last-modified/content.
- [x] Implement list method in `UserDocumentBlobStore` with ordering by last modified desc and `.md` filtering only.
- [x] Build prompt augmentation helper to append a single "Generated Documents" section with per-file headings, enforcing per-doc and total caps, and `[TRUNCATED]` markers.
- [x] Ensure prompt augmentation is idempotent (do not duplicate section on restore/recreate).
- [x] Wire helper into session create and restore flows (`SessionsController`, `ChatController`) and persist enriched prompt to `SessionDocument`.
- [x] Add tests for SessionsController prompt augmentation, empty-doc no-op, and idempotency.
- [x] Add tests for ChatController restore path and project isolation.
- [x] Add stub blob store in tests to validate ordering and truncation behavior.

## Dev Notes (code anchors)
- Generated docs are saved to `documents/{projectFolder}/generated/{fileName}` in the session document flow. `AgentChain_API/againt_chain_api/Controllers/SessionsController.cs:608`
- Existing dependency bundle logic (with truncation pattern) can be reused as a model. `AgentChain_API/againt_chain_api/Controllers/SessionsController.cs:1257`
- Metadata used to isolate project docs is set and validated in the blob store. `AgentChain_API/againt_chain_api/Services/UserDocumentBlobStore.cs:57` and `AgentChain_API/againt_chain_api/Services/UserDocumentBlobStore.cs:221`
- Prompt overrides are honored by the agent factory; you’ll need to build the enriched prompt before CreateAgent. `AgentChain_API/agent_service/Factories/AgentFactory.cs:28`
- `IUserDocumentBlobStore` currently only supports read + latest; you’ll likely add a list method. `AgentChain_API/againt_chain_api/Services/IUserDocumentBlobStore.cs:6`

## Implementation Tasks
- Add a list/read-many method to `IUserDocumentBlobStore` (or a helper in SessionsController) that enumerates generated docs by prefix and metadata, then reads their content.
- Build a prompt augmentation helper that appends a single “Generated Documents” section (with per-file headings + content) and enforces size caps.
- Wire the helper into session creation and session restore flows (SessionsController + ChatController) and persist the enriched prompt in SessionDocument to keep restores consistent.
- Add/update tests for sessions/chat to assert prompt augmentation, project isolation, truncation, and idempotency.

## Testing Strategy
- Unit tests in `agent_service.Tests` for SessionsController and ChatController: verify prompt override contains generated docs, does nothing when empty, and doesn’t duplicate on restore.
- Add a stub document blob store returning multiple docs with metadata to validate ordering + truncation.

## Open Questions
- Why do you want all generated docs (vs. a dependency subset) in the prompt: precision or completeness?
- What’s your acceptable max prompt size cap before you’d rather summarize or truncate?
- Should legacy paths like `documents/generated/product_brief/` be included, or only the project folder?
## Dev Agent Record
### Debug Log
- dotnet test AgentChain_API/ai_agent.sln
- dotnet test AgentChain_API/ai_agent.sln

### Completion Notes
- Added generated-doc listing to IUserDocumentBlobStore and UserDocumentBlobStore with metadata filtering, markdown-only selection, and last-modified ordering (including legacy-prefix handling).
- Implemented GeneratedDocumentsPromptHelper to build a single "Generated Documents" section with per-doc and total truncation + [TRUNCATED] markers and idempotency checks.
- Wired prompt augmentation into session create/restore in SessionsController and ChatController, using persona prompts when needed and persisting enriched prompts in SessionDocument.
- Added sessions/chat tests covering augmentation, no-op behavior, idempotency, restore path, project isolation, ordering, and truncation with a stub document blob store.

## File List
- againt_chain_api/Services/IUserDocumentBlobStore.cs
- againt_chain_api/Services/UserDocumentBlobStore.cs
- againt_chain_api/Services/GeneratedDocumentsPromptHelper.cs
- againt_chain_api/Controllers/SessionsController.cs
- againt_chain_api/Controllers/ChatController.cs
- agent_service.Tests/SessionsEndpointsTests.cs
- agent_service.Tests/ChatEndpointsTests.cs

## Change Log
- 2026-02-04: Implemented generated-doc prompt augmentation, blob listing, and associated tests.
