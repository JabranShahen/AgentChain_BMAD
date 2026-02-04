# Technology Stack Summary

| Layer | Technology | Justification |
| --- | --- | --- |
| Frontend | Vite 7.2.5 (rolldown fork), React 19.2, TypeScript 5.9 | `AgentChain_UI/package.json` defines a modern Vite+React SPA with Firebase+ESLint+Vitest developer tooling.
| Frontend Hosting | Vite preview/dev server + `firebase` runtime | Scripts include `vite`, and Firebase dependency suggests the UI is meant to be hosted via Firebase or static hosting.
| Backend API | ASP.NET Core (.NET 8 Web SDK with JWT auth, Azure Storage Blobs, Service Bus, Swashbuckle) | `againt_chain_api.csproj` shows references to `Microsoft.AspNetCore.Authentication.JwtBearer`, `Azure.Messaging.ServiceBus`, `Swashbuckle.AspNetCore`, plus project references to `agent_service`, `AiAgent.McpServer`, persistence/cosmos layers.
| Agent Service & Persistence | Internal project references (`agent_service`, `AiAgent.McpServer`, `AgentChain.Persistence.Cosmos`) | Indicates layered services handling agent orchestration, MCPS server hosting, and Cosmos persistence.
| Automation Runner | CodexRunner (C# Console) listening to Service Bus messages, uploading zipped artifacts to Azure Blob) | `AgentChain_Codex/CodexRunner/Program.cs` reveals a Service Bus processor, storage/upload helpers, Codex invocation, and manifest logging, so it is responsible for running Codex-based automation jobs.
| Messaging & Storage | Azure Service Bus queues (`agentchain-document-ready`), Azure Storage Blobs (container prefix `user-`, document/code artifacts) | Documented directly in runner code and csproj packages.
| Tooling & CI | Vite scripts (dev/build/lint/test), dotnet build (Release), local `project-context` and `project-architecture` notes | Scripts and docs signal developer workflow and gating for automation.

