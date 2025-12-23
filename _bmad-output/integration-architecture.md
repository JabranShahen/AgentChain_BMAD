# Integration Architecture

## Summary
- Multi-part system: React Vite UI (web) integrates with ASP.NET Core API (backend).
- UI makes browser fetch calls to API over HTTPS.

## Integration Points

### UI -> API (HTTP)
- Base URL: `VITE_API_BASE_URL` (env) or fallback
  - Dev fallback: `https://localhost:7193`
  - Prod fallback: `https://agentchainapi20251208182424.azurewebsites.net`
- Endpoints referenced by UI:
  - `GET /agents`
  - `GET /agents/{id}`
  - `POST /chat`

### API Endpoints Exposed
- `GET /api/agents` (minimal API endpoint)
- `GET /WeatherForecast` (controller route)

## Data Flow
1. UI loads agent catalog from `GET /agents`.
2. UI loads agent detail from `GET /agents/{id}`.
3. UI sends chat payload to `POST /chat` with `{ agentId, message, sessionId }`.

## Integration Gaps / Mismatches
- UI calls `/agents` and `/chat`, but API exposes `/api/agents` and `/WeatherForecast`.
- No `POST /chat` endpoint found in the API project.
- No `GET /agents/{id}` endpoint found in the API project.

## Auth / Security
- No authentication integration detected between UI and API.

## Notes
- UI depends on `import.meta.env.VITE_API_BASE_URL` for API routing.
- API uses HTTPS redirection and Swagger in development.
