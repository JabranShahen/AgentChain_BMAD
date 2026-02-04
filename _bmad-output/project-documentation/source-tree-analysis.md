# Source Tree Analysis

```
AgentChain_BMAD/
├── AgentChain_UI/             # Vite/React single-page app with docs-focused modals and session helpers
├── AgentChain_API/            # ASP.NET Core backend, agent catalog, persistence, and shared abstractions
├── AgentChain_Codex/          # CodexRunner console app that listens to Azure Service Bus and uploads artifacts
├── _bmad/                     # BMAD infrastructure (workflows, templates, configs)
└── _bmad-output/              # Workflow artifacts and documentation outputs (project-documentation/ ...)
```

- **AgentChain_UI/** hosts `package.json` (scripts: dev/build/test) and `src/` (App, modals, session storage, Firebase wiring).
- **AgentChain_API/** contains `againt_chain_api/` (controllers, JWT-protected endpoints) plus helper projects (`agent_service`, `AiAgent.*`, `Dependencies`). The `.sln` ties them together.
- **AgentChain_Codex/** contains `CodexRunner/Program.cs` and `job.json`, showing a message-driven runner tightly coupled to Azure Storage and Service Bus.
- **_bmad/** houses automation workflows and output templates used by this documentation workflow (not part of runtime, but necessary for graceful scanning).
- **_bmad-output/project-documentation/** collects the files you are currently generating.

