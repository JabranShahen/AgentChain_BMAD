# Development Instructions

## Frontend (AgentChain_UI)
1. `cd AgentChain_UI`
2. `npm install` or `npm ci` to install dependencies (Vite, React 19.2, Firebase, Vitest).
3. `npm run dev` to start the Vite development server (hot reload). `npm run build` creates optimized artifacts; `npm run test` runs Vitest suites.
4. Firebase is included (`firebase.ts`), so configure `.env` or Firebase CLI as needed before invoking additional authentication flows.

## Backend (AgentChain_API/againt_chain_api)
1. `dotnet build againt_chain_api/againt_chain_api.csproj` to compile the Web API.
2. `dotnet run --project againt_chain_api/againt_chain_api.csproj` launches the server with Swagger available (Swashbuckle referenced).
3. Controllers expect JWT tokens; you can point `AccountController` or `DevelopmentController` to stub tokens stored in `_bmad-output` or environment variables.
4. `AgentChain_API/agent_service`, `AiAgent.McpServer`, and `Dependencies/AgentChain.Persistence.Cosmos` provide shared services; build the solution (`ai_agent.sln`) to ensure dependencies are restored.

## Automation (AgentChain_Codex/CodexRunner)
1. `dotnet run --project AgentChain_Codex/CodexRunner/CodexRunner.csproj -- AgentChain_Codex/job.json` to execute the message listener.
2. The runner consumes Service Bus queue `agentchain-document-ready` and uploads zipped artifacts to Azure Storage. Set connection strings via environment variables (`ServiceBus:ConnectionString`, `Storage:ConnectionString`).
3. Job configuration also specifies a `WorkspaceRoot` and `ProjectId` — tune these in `job.json` before launching long-running Codex builds.

## Tips
- Use `git status` frequently; the workspace is multi-root, so watch for changed files under `_bmad-output` as you generate documentation.
- Keep `.env` files (e.g., `AgentChain_UI/.env`, `AgentChain_API/.env.example`) updated with keys for Firebase, Azure Storage, or Service Bus.

