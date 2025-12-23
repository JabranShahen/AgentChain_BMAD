# Development Instructions

## UI (web)
- Location: AgentChain_UI/AgentChainUI
- Prereqs: Node.js (version not specified), npm
- Install: `npm install`
- Run: `npm run dev`
- Build: `npm run build`
- Lint: `npm run lint`
- Tests: no test script found
- Config: `vite.config.js`, `tsconfig.json`, `staticwebapp.config.json`
- Env: no `.env*` files found

## API (backend)
- Location: Agent_Chain_API
- Prereqs: .NET SDK 8.0
- Restore: `dotnet restore` (from solution or project)
- Build: `dotnet build`
- Run: `dotnet run --project againt_chain_api/againt_chain_api.csproj`
- Tests: `dotnet test` (agent_service.Tests)
- Config: `appsettings.json`, `appsettings.Development.json`
- Local profiles: `Properties/launchSettings.json` (ASPNETCORE_ENVIRONMENT=Development; http/https profiles)
