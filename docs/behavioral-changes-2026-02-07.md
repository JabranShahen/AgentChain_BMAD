# Behavioral Changes Log (2026-02-07)

This document captures the behavioral changes implemented across API, UI, and Codex runner so future agents can continue safely.

## 1) Development Cancel Flow

### API behavior
- Added/updated cancel endpoint behavior so cancel is allowed when project status is:
  - `queued`
  - `in_progress`
- Cancel action now:
  - Resets project status to `idle`
  - Updates status timestamps
  - Publishes a development-control cancel message to Service Bus

Relevant files:
- `AgentChain_API/againt_chain_api/Controllers/DevelopmentController.cs`
- `AgentChain_API/againt_chain_api/Services/ServiceBusPublisher.cs`

### UI behavior
- `Cancel Development` button now appears when project is:
  - `queued`
  - `in_progress`
- Cancel request posts to `/api/development/cancel`.

Relevant files:
- `AgentChain_UI/src/DocumentMapModal.tsx`
- `AgentChain_UI/src/DocumentMapModal.test.tsx`

## 2) Codex Runner Cancel Reliability

- Runner already consumed control cancel messages; behavior was strengthened to stop active work more reliably.
- Cancel now:
  - Cancels project token
  - Tracks active child processes by project
  - Force-kills active process tree for canceled project
- Queued messages with prior cancel are skipped.
- Canceled runs write manifest status as `Canceled`.

Relevant file:
- `AgentChain_Codex/CodexRunner/Program.cs`

## 3) Service Bus Status Consumer Improvements (API)

- API status consumer now attempts to ensure/create status queue on startup.
- If queue is missing (`MessagingEntityNotFound`), consumer stops instead of noisy repeated retries.

Relevant file:
- `AgentChain_API/againt_chain_api/Services/ProjectStatusConsumer.cs`

## 4) Document Workflow Model Selection

- Document infer/generate path now explicitly configured to use:
  - `OpenAI:Model = "gpt-4o-mini"`
- This avoids relying on implicit fallback behavior.

Relevant files:
- `AgentChain_API/againt_chain_api/appsettings.json`
- `AgentChain_API/againt_chain_api/appsettings.Development.json`
- `AgentChain_API/againt_chain_api/Configuration/AgentRuntimeServiceCollectionExtensions.cs`

## 5) Stack Selection Behavior in Codex Runner Prompt

- Removed previous prompt bias to prefer React Native.
- Added explicit instruction: if project metadata/docs call for Flutter, use Flutter (Dart).
- Added project metadata block to prompt:
  - Project name
  - Project description

Relevant file:
- `AgentChain_Codex/CodexRunner/Program.cs`

## 6) Project Description Propagation to Runner

- Service Bus document-ready payload now includes `ProjectDescription`.
- API sends project description from project entity.
- Runner reads and injects project description into implementation prompt.

Relevant files:
- `AgentChain_API/againt_chain_api/Services/ServiceBusPublisher.cs`
- `AgentChain_API/againt_chain_api/Controllers/DevelopmentController.cs`
- `AgentChain_Codex/CodexRunner/Program.cs`
- `AgentChain_API/agent_service.Tests/DevelopmentControllerTests.cs`

## 7) Runner Prompt Policy: No Unit Tests

- Runner-generated prompt and AGENTS template now instruct Codex to:
  - Not create unit/integration tests
  - Not run test commands

Relevant file:
- `AgentChain_Codex/CodexRunner/Program.cs`

## 8) Runner Process Startup Fix

- Fixed `StandardInputEncoding` runtime error by setting it only when stdin is redirected.
- Prevents false failed runs caused by process start exception.

Relevant file:
- `AgentChain_Codex/CodexRunner/Program.cs`

## 9) Build Command Behavior Change

- `BuildCommand` is now optional in runner config.
- If `BuildCommand` is empty/missing:
  - Runner skips build/fix loop
  - Run is marked `Succeeded` after implementation step
- Removed explicit npm test command from sample runner config to reduce stack confusion.

Relevant files:
- `AgentChain_Codex/CodexRunner/Program.cs`
- `AgentChain_Codex/job.json`

## 10) Operational Notes

- Restart API after configuration/code changes.
- Restart Codex runner after runner code/prompt changes.
- If runner binary is locked, build to alternate output path was used during verification.

## 11) Known Tradeoff

- With empty/missing `BuildCommand`, there is no automatic compile/build validation step in runner.
- This reduces false npm/test coupling but also reduces automatic build verification.
