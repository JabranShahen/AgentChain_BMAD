# Deployment Configuration

## UI Deployment
- Build the Vite/React app (`npm run build`). The output directory (not shown here but typically `dist/`) can be hosted on Firebase Hosting, Netlify, or Azure Static Web Apps. Firebase dependency in `package.json` plus `firebase.ts` indicates the UI expects Firebase services for auth/storage.
- Static assets (icons or illustrations) live under `AgentChain_UI/public/` and `src/assets/`. Ensure the deployment copies those directories.
- Environment variables for APIs and Firebase endpoints should align with the backend’s base URL (e.g., `https://localhost:5001/api`).

## API Deployment
- Publish the .NET 8 Web API via `dotnet publish -c Release againt_chain_api/againt_chain_api.csproj`.
- Host on Azure App Service or a Linux container; the controller set expects JWT bearer tokens and integrates with Azure Service Bus + Blob Storage. Configure the following settings:
  - `AzureStorage:ConnectionString` / `Storage__ConnectionString`: for doc uploads.
  - `ServiceBus:ConnectionString`, `ServiceBus__QueueName`: to connect to `agentchain-document-ready`.
  - `Jwt:Authority`/`Jwt:Audience` referencing your identity provider (the `AccountController` resolves claims).
- The API references Azure Storage and Service Bus packages; ensure managed identity or secrets are granted in your deployment slot.

## Codex Runner Deployment
- Deploy `AgentChain_Codex/CodexRunner` as a background worker. It requires the same Azure Storage and Service Bus configuration plus `JobSpec` overrides for `WorkspaceRoot` and `ProjectFolder`.
- Use Azure Functions/Container Apps if you need event-driven scaling; otherwise, run as a dedicated VM with the Service Bus listener.

