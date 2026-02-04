# Integration Architecture

1. **UI ↔ API** – The React UI (`AgentChain_UI/src`) authenticates via Firebase tokens and calls the ASP.NET API under `/api`. JWT tokens are validated by `AccountController` and forwarded to controllers like `ChatController`, `ProjectsController`, and `SessionsController`.
2. **API ↔ Persistence** – The API uses shared persistence interfaces (`IPresistance`, `IAgentCatalog`, session stores) to read/write `Project`, `ProjectAgentTeam`, `SessionDocument`, `SessionTranscriptDocument`, and agent definitions located in `AgentChain_API/AgentChainAbstractions`.
3. **API ↔ Service Bus** – When sessions complete or new documents arrive, the API can trigger the Codex runner by pushing messages to the `agentchain-document-ready` Service Bus queue (mirroring the queue referenced by `CodexRunner.JobSpec`).
4. **Codex Runner ↔ Storage** – The runner listens for Service Bus messages and runs `dotnet build`. After each run it zips `workspace` and uploads artifacts to `documents/{projectFolder}/code/` in Azure Blob Storage, enabling the API or UI to download the outputs.
5. **Telemetry and Logging** – `CodexRunner` writes `manifest.json` with logs/errors, which can be surfaced through API endpoints or existing documentation artifacts, completing the loop for human/LLM consumption.

