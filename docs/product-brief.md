# Product Brief: AgentChain (Agentic API + Angular Console)

## Problem
Teams want to expose BMAD agents/workflows through simple APIs and UI, but current usage is CLI/manual. There is no easy way to list agents, start sessions, or orchestrate multi-agent discussions from applications.

## Users
- Primary: Internal developers/builders integrating AI agents into products.
- Secondary: Product/ops teams using the UI to trigger workflows.

## Solution (V1)
ASP.NET Core API that lists BMAD agents from the manifest and lets clients chat with agents or run workflows; Angular UI to browse agents, start sessions, and view streaming responses.

## Top Use Cases (V1)
1) List agents and their capabilities.  
2) Start a chat/session with a chosen agent.  
3) Run party-mode (multi-agent) and stream responses.  
4) View session history.

## Scope
- In: REST endpoints for list/chat/run, in-memory session state, optional SignalR streaming, simple API-key auth stub, Angular screens for agent list, chat console, session list.
- Out (V1): Durable persistence, role-based auth, billing, advanced analytics.

## Success Metrics
- Time-to-first-response < 2s p95.
- First session started in < 3 clicks.
- ≥3 workflows run per week by a pilot team.
- 0 unhandled errors on happy-path runs in QA.

## Constraints/Assumptions
- BMAD assets live in `.bmad/`.
- LLM backend TBD (pluggable).
- Internal use only for V1.
- Deploy on current stack (ASP.NET Core + Angular SSR).

## First Sprint Goal
Deliver list + chat endpoints and Angular UI to select an agent and exchange messages (REST or SignalR), with API key guard and basic logging.

## Risks
- LLM latency impacting UX.
- Session state across instances (needs later persistence).
- Streaming UX may lag without SignalR.
