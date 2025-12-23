# AgentChain - Project Overview

**Date:** 2025-12-22
**Type:** multi-part (web + backend)
**Architecture:** SPA (React) + API-centric backend

## Executive Summary
AgentChain is a multi-part system composed of a React + Vite UI and an ASP.NET Core API. The UI presents a console for browsing agent personas and running chats, while the backend exposes an agent catalog endpoint and supporting services. Documentation highlights an integration gap: the UI references `/agents` and `/chat`, but the API currently exposes `/api/agents` and a sample `/WeatherForecast` endpoint.

## Project Classification

- **Repository Type:** multi-part
- **Project Type(s):** web (ui), backend (api)
- **Primary Language(s):** TypeScript, C#
- **Architecture Pattern:** Component-based SPA + service/API backend

## Multi-Part Structure

This project consists of 2 distinct parts:

### Web UI (ui)

- **Type:** web
- **Location:** `AgentChain_UI/AgentChainUI`
- **Purpose:** Browser UI for browsing agents and chatting
- **Tech Stack:** React 19, Vite (rolldown-vite), TypeScript

### Backend API (api)

- **Type:** backend
- **Location:** `Agent_Chain_API`
- **Purpose:** Agent catalog API + supporting services
- **Tech Stack:** ASP.NET Core (.NET 8), Swashbuckle, OpenAI SDK

### How Parts Integrate

The UI communicates with the backend over HTTPS using a configurable base URL (`VITE_API_BASE_URL`). It attempts to call `GET /agents`, `GET /agents/{id}`, and `POST /chat`. The backend currently exposes `GET /api/agents` and `GET /WeatherForecast`, so routing alignment is needed.

## Technology Stack Summary

### Web UI Stack

| Category | Technology | Version | Notes |
| --- | --- | --- | --- |
| Language | TypeScript | ES2020 target | `tsconfig.json` |
| UI Framework | React | 19.2.0 | `package.json` |
| Build Tool | Vite (rolldown-vite) | 7.2.5 | `package.json` overrides |

### Backend API Stack

| Category | Technology | Version | Notes |
| --- | --- | --- | --- |
| Runtime | .NET | 8.0 | `net8.0` target |
| Web Framework | ASP.NET Core | 8.0 | `Microsoft.NET.Sdk.Web` |
| API Docs | Swashbuckle.AspNetCore | 6.6.2 | Swagger UI in dev |
| AI SDK | OpenAI | 2.7.0 | `ai_agent` + `agent_service` |
| Testing | xUnit + Microsoft.NET.Test.Sdk + coverlet.collector | 2.9.2 / 17.11.1 / 6.0.2 | `agent_service.Tests` |

## Key Features

- Agent catalog browsing (UI + API)
- Agent detail inspection
- Chat UI workflow (pending backend endpoint alignment)
- Shared agent_service library

## Architecture Highlights

- UI: Single-page application with React, minimal component structure.
- API: Minimal endpoint + controller; service library provides core agent logic.
- Integration: UI uses environment-configurable base URL.

## Development Overview

### Prerequisites

- Node.js + npm (UI)
- .NET SDK 8.0 (API)

### Getting Started

- UI: `cd AgentChain_UI/AgentChainUI` then `npm install`
- API: `cd Agent_Chain_API` then `dotnet build`

### Key Commands

#### Web UI (ui)

- **Install:** `npm install`
- **Dev:** `npm run dev`

#### Backend API (api)

- **Install:** `dotnet restore`
- **Dev:** `dotnet run --project againt_chain_api/againt_chain_api.csproj`

## Repository Structure

- Root contains two primary parts: `AgentChain_UI/AgentChainUI` and `Agent_Chain_API`.
- UI code under `src/` with Vite tooling and configs.
- API code under `againt_chain_api/` with shared libraries under `agent_service/` and console host `ai_agent/`.

## Documentation Map

For detailed information, see:

- [index.md](./index.md) - Master documentation index
- [architecture-ui.md](./architecture-ui.md) - UI architecture
- [architecture-api.md](./architecture-api.md) - API architecture
- [source-tree-analysis.md](./source-tree-analysis.md) - Directory structure
- [development-guide-ui.md](./development-guide-ui.md) - UI development workflow
- [development-guide-api.md](./development-guide-api.md) - API development workflow
- [integration-architecture.md](./integration-architecture.md) - Cross-part integration

---
_Generated using BMAD Method `document-project` workflow_
