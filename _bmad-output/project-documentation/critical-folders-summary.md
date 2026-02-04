# Critical Folders Summary

- `AgentChain_UI/` – Hosts the Vite/React SPA, modals, session utilities, and Firebase integration. Critical for user-facing flows and session management.
- `AgentChain_API/againt_chain_api/` – Core Web API (JWT + Swagger) exposing chat, project, session, storage, and development endpoints.
- `AgentChain_API/agent_service/` and `AgentChainAbstractions/` – Provide reusable agent definitions, persistence contracts, and helper factories used by the API controllers.
- `AgentChain_Codex/CodexRunner/` – Background job runner that listens on Azure Service Bus, runs Codex builds, and uploads zipped artifacts to Azure Blob Storage.
- `_bmad/` – Workflow automation repository that controls how this documentation is orchestrated.
- `_bmad-output/project-documentation/` – Target folder for all generated documentation. It mirrors the final documentation portal that will be referenced by AI agents or humans.
- `_bmad-output/planning-artifacts` (exists but not yet populated) – reserved for higher-level planning outputs; note that the documentation index may point toward this if future workflows populate it.

