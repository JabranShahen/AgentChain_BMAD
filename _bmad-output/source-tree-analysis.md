# Source Tree Analysis

## Overview
- Repository type: multi-part (UI + API)
- UI root: `AgentChain_UI/AgentChainUI`
- API root: `Agent_Chain_API`

## UI Tree (AgentChain_UI/AgentChainUI)
```
AgentChainUI/
|-- public/
|   |-- vite.svg
|-- src/
|   |-- assets/
|   |-- App.css
|   |-- App.tsx
|   |-- index.css
|   |-- main.tsx
|   |-- types.ts
|   |-- vite-env.d.ts
|-- .gitignore
|-- .node-version
|-- eslint.config.js
|-- index.html
|-- package-lock.json
|-- package.json
|-- README.md
|-- staticwebapp.config.json
|-- tsconfig.json
|-- tsconfig.node.json
|-- vite.config.js
```

## API Tree (Agent_Chain_API)
```
Agent_Chain_API/
|-- againt_chain_api/
|   |-- AgentData/
|   |-- Configuration/
|   |-- Controllers/
|   |-- Features/
|   |-- Properties/
|   |-- Program.cs
|   |-- WeatherForecast.cs
|   |-- appsettings.json
|   |-- appsettings.Development.json
|   |-- againt_chain_api.csproj
|-- agent_service/
|   |-- Abstractions/
|   |-- Agent/
|   |-- Chat/
|   |-- Factories/
|   |-- Personas/
|   |-- Tools/
|   |-- agent_service.csproj
|-- agent_service.Tests/
|   |-- agent_service.Tests.csproj
|-- ai_agent/
|   |-- Abstractions/
|   |-- Configuration/
|   |-- docs/
|   |-- Program.cs
|   |-- ai_agent.csproj
|-- project-root/
|-- ai_agent.sln
```

## Integration Points
- UI calls API endpoints from `src/App.tsx` using `VITE_API_BASE_URL`.
- API exposes controller routes and minimal endpoints (see `againt_chain_api/Program.cs`).

## Critical Folders Summary
- UI: `src/` (entry point `main.tsx`, root component `App.tsx`), `public/` (static assets)
- API: `againt_chain_api/` (web API host), `agent_service/` (shared services), `ai_agent/` (console/host), `agent_service.Tests/` (tests)