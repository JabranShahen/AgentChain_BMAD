# API Contracts (API)

## Overview
- Framework: ASP.NET Core (.NET 8)
- Routing: Controllers + minimal endpoints in `Program.cs`
- Base middleware: HTTPS redirection, Authorization
- Auth: No explicit auth policies detected (only `UseAuthorization`)
- Documentation basis: Controllers + endpoint mapping in `againt_chain_api`

## Endpoints

### GET /WeatherForecast
- **Handler:** `WeatherForecastController.Get`
- **Route:** `[Route("[controller]")]` ? `/WeatherForecast`
- **Response:** `WeatherForecast[]` (inferred from controller return type)
- **Notes:** Sample/template controller from ASP.NET defaults

### GET /api/agents
- **Handler:** `AgentsEndpoints.GetAgents`
- **Route:** `/api/agents`
- **Response:** `List<AgentSummaryResponse>`
- **Notes:** Returns catalog entries mapped to response DTO

### GET /agents
- **Handler:** Not found in API project (UI uses `/agents`, verify base path or proxy)
- **Notes:** UI `App.tsx` calls `${API_BASE_URL}/agents` and `${API_BASE_URL}/chat` — endpoints not found in scanned backend files

### POST /chat
- **Handler:** Not found in API project (UI uses `/chat`, verify base path or proxy)

## Models

### AgentSummaryResponse
- **Fields:**
  - `Id` (string)
  - `Title` (string)
  - `Description` (string?)
  - `Icon` (string?)
  - `HasMenu` (bool)
  - `DeclaredCommands` (IReadOnlyList<string>)
  - `Version` (string)

## Gaps / To Verify
- Confirm base path / routing conventions in `Program.cs`
- Confirm if authentication/authorization is applied globally
- Validate WeatherForecast endpoint is still used in production
- Locate `/agents` and `/chat` handlers or proxy configuration