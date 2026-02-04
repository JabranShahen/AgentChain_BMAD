# Architecture Overview

- **Layer 1: Frontend Workspace** – `AgentChain_UI` is a Vite-powered React SPA. It stores session tokens locally (`sessionStorage.ts`), renders document maps/modals, and calls the API endpoints defined under `api/`.
- **Layer 2: ASP.NET Core API** – `AgentChain_API/againt_chain_api` exposes secured REST controllers (`ChatController`, `SessionsController`, `ProjectsController`, `ProjectAgentsController`, etc.). Authentication uses JWT bearer tokens; Swashbuckle provides Swagger docs for quick verification.
- **Layer 3: Agent Orchestration** – Shared projects (`agent_service`, `AgentChainAbstractions`) supply agent catalogs, session definitions, persistence interfaces, and Cosmos-friendly models used by the API and Codex runner.
- **Layer 4: Automation Runner** – `AgentChain_Codex/CodexRunner` listens on Azure Service Bus queue `agentchain-document-ready`, runs builds, writes manifests, and uploads zipped code to Azure Blob Storage. It mirrors the API’s document handling by persisting artifacts for retrieval.
- **Infrastructure Components** – Azure Service Bus, Blob Storage, and Firebase (per UI) are referenced in code and configuration; they form the glue for integration, identity, and artifact storage.

