# Architecture (API)

## Executive Summary
- ASP.NET Core (.NET 8) backend providing agent catalog endpoints.
- Web API project `againt_chain_api` hosts minimal endpoints and controllers.
- Shared service library `agent_service` supplies agent catalog + tooling.

## Technology Stack

| Category | Technology | Version | Notes |
| --- | --- | --- | --- |
| Runtime | .NET | 8.0 | `net8.0` target |
| Web Framework | ASP.NET Core | 8.0 | `Microsoft.NET.Sdk.Web` |
| API Docs | Swashbuckle.AspNetCore | 6.6.2 | Swagger UI in dev |
| AI SDK | OpenAI | 2.7.0 | `ai_agent` + `agent_service` |
| Testing | xUnit + Microsoft.NET.Test.Sdk + coverlet.collector | 2.9.2 / 17.11.1 / 6.0.2 | `agent_service.Tests` |

## Architecture Pattern
- Service/API-centric ASP.NET Core backend; likely layered services with shared service library (`agent_service`).

## Core Components
- `againt_chain_api/Program.cs`: host configuration, middleware, endpoint mapping.
- `againt_chain_api/Features/Agents/Endpoints/AgentsEndpoints.cs`: minimal endpoint for agent catalog.
- `againt_chain_api/Controllers/WeatherForecastController.cs`: template controller.
- `agent_service/`: shared library for agent catalog, tools, personas, factories.
- `ai_agent/`: console host for running agents directly.

## API Design
- `GET /api/agents` via `AgentsEndpoints.GetAgents` returns `List<AgentSummaryResponse>`.
- `GET /WeatherForecast` sample controller endpoint.
- UI expects `/agents` and `/chat` (not found in API project).

## Data Architecture
- No database or ORM detected.
- DTOs only: `AgentSummaryResponse`.

## Source Tree Notes
- API host: `Agent_Chain_API/againt_chain_api`.
- Shared library: `Agent_Chain_API/agent_service`.
- Console host: `Agent_Chain_API/ai_agent`.
- Tests: `Agent_Chain_API/agent_service.Tests`.

## Development Workflow
- Build: `dotnet build`
- Run: `dotnet run --project againt_chain_api/againt_chain_api.csproj`
- Tests: `dotnet test`
- Launch profiles: `Properties/launchSettings.json` (http/https + Swagger)

## Deployment Architecture
- No deployment configuration detected (no Docker/IaC/CI).

## Testing Strategy
- Unit tests in `agent_service.Tests`.
- No API integration tests detected.

## Known Gaps
- Missing `/agents/{id}` and `/chat` endpoints expected by UI.
- No auth configuration detected beyond `UseAuthorization`.

---
_Generated using BMAD Method `document-project` workflow_
