# Data Models (core)

## Storage entities defined under `AgentChain_API/AgentChainAbstractions/Entites`

### Project and related metadata
- `Project` (AgentChainAbstractions.Entites.Project.Project)
  - Fields: `Id`, `AccountId`, `Name`, optional `Description`, timestamps (`CreatedUtc`, `UpdatedUtc`). Projects group sessions, agents, and documents per user account.

### Agent assemblies
- `ProjectAgentTeam` & `ProjectAgentDefinition` (Entites.Agent)
  - Contains teams of agents seeded from catalog JSON files. `ProjectAgentDefinition` describes each agent’s persona, version, and behavior definition.
- `AgentChatRequest` / `AgentWorkflowRequest` / `AgentResponse` (Entites.Agent.AgentModels)
  - Capture agent conversations, chosen workflows, and actions executed via the agent layer.
- `AgentContextSnapshot`, `CapabilitiesSnapshot`, `SessionState` provide payload-safe snapshots for conversation context and tooling constraints.

### Sessions and transcripts
- `SessionDocument` (Entites.Sessions.SessionDocument)
  - Stores session metadata plus `AgentId`, `ProjectId`, timestamps, and references to transcripts stored in blob storage.
- `SessionTranscriptDocument` – shapes transcript slices that the UI can download or display with traceability.

### Persistence abstractions
- `IPresistance` (note misspelling) and `ISessionTranscriptStore`/`IAgentCatalog` define the repository contracts seen in controllers – they orchestrate reads/writes for the above entities.

### Additional helpers
- `Manifest` (Codex runner) stores job execution data: `ProjectId`, `RunId`, `Status`, `WorkspacePath`, `Logs`, `Errors`, `FinishedAtUtc`.
- `JobSpec` (Codex runner) defines the background job run configuration, including storage/service bus connection strings, maximum retries, and workspace layout.

