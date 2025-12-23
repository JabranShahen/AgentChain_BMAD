# Data Models (API)

## Overview
- No database migrations or ORM configs detected in scanned directories.
- Models appear focused on API response DTOs.

## Models

### AgentSummaryResponse
- **Location:** `againt_chain_api/Features/Agents/Models/AgentSummaryResponse.cs`
- **Type:** record
- **Fields:**
  - `Id` (string)
  - `Title` (string)
  - `Description` (string?)
  - `Icon` (string?)
  - `HasMenu` (bool)
  - `DeclaredCommands` (IReadOnlyList<string>)
  - `Version` (string)

## Gaps / To Verify
- If there is a persistence layer, document it once located (DbContext, migrations, connection strings).