# Project Overview

**Name:** AgentChain_BMAD documentation hub

**Purpose:** Document the multi-stack AgentChain platform so that future contributors and AI agents can understand how the React frontend, ASP.NET backend, and Codex runner collaborate.

**Executive Summary:**
- Monolithic yet modular repo housing UI (`AgentChain_UI`), API (`AgentChain_API`), and automation runner (`AgentChain_Codex`).
- Authentication uses Firebase/JWT, Azure Service Bus for messaging, Azure Blob Storage for artifacts.
- Generated documentation will now live under `_bmad-output/project-documentation/` with a master index (`index.md`).

**Tech Stack Snapshot:**
- Frontend: React 19 + TypeScript + Vite (rolldown) with Firebase integration.
- Backend: ASP.NET Core 8 Web APIs with Swashbuckle, JWT Bearer, Azure Storage/Service Bus packages.
- Automation: Codex runner (C# console) running builds and uploading zipped workspaces.

**Architecture Type:** Monolithic orchestrator (UI + API + automation runner).

**Repository Structure:** See `source-tree-analysis.md` for annotated tree.

