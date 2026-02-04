# Architecture Patterns

- **Monolithic Coordination Layer** – The repo is treated as a single combined application where the Vite/React UI, ASP.NET Core API, and Codex runner coexist. The UI lives under `AgentChain_UI`, the API under `AgentChain_API/againt_chain_api`, and the automation runner under `AgentChain_Codex/CodexRunner`.
- **Layered Web + Automation Stack** – The frontend communicates with the .NET backend (JWT-protected APIs with Swagger) while the Codex runner listens on the same Azure Service Bus queue and uploads artifacts to Azure Blob Storage. All three layers share common assets in the root workspace (`project-context.txt`, `project-architecture.txt`).
- **Messaging-driven Automation** – The Codex runner establishes a Service Bus processor against `agentchain-document-ready`, consumes messages, executes `dotnet build`, and streams logs/manifests before uploading zipped results to `documents/{projectFolder}/code/`. This implies an event-driven blend of UI user actions triggering backend services, which in turn may schedule Codex-based implementation jobs.
- **Shared Persistence/Infrastructure** – Backend project references include Cosmos persistence and agent orchestration services, revealing a centralized data layer behind the API.
- **Quick Scan Simplification** – Because we’re running a pattern-based quick scan, the architecture summary leans on manifest files (`package.json`, `.csproj`, `Program.cs`) rather than deep source analysis.

