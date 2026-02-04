# Development Guide

1. **Frontend**: `cd AgentChain_UI` → `npm install` → `npm run dev` to start the local Vite server. Use `npm run build` before committing to ensure the rollup output is healthy.
2. **Backend**: `cd AgentChain_API` → `dotnet build ai_agent.sln` → `dotnet run --project againt_chain_api/againt_chain_api.csproj`. Ensure JWT issuer and Azure settings are available via `.env` or user secrets.
3. **Automation**: `cd AgentChain_Codex` → `dotnet run --project CodexRunner/CodexRunner.csproj -- job.json`. The runner expects Azure Storage and Service Bus secrets (
   `Storage:ConnectionString`, `ServiceBus:ConnectionString`).
4. **Testing**: Run Vitest (`npm run test`) for the UI and any unit tests in `agent_service.Tests` for backend pieces.
5. **Linting**: Keep ESLint satisfied with `npm run lint` (React + TypeScript). For dotnet, rely on `dotnet build` warnings.
6. **Documentation**: Update `_bmad-output/project-documentation/index.md` after any structural tweaks so the documentation portal stays in sync.

