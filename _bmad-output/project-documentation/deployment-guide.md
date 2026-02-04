# Deployment Guide

- **UI**: Build with `npm run build`. Deploy the produced `dist/` to Firebase Hosting, Azure Static Web Apps, or any CDN. Align `firebase.ts` config with actual endpoints and ensure env files provide the backend base URL.
- **API**: `dotnet publish -c Release againt_chain_api/againt_chain_api.csproj`. Host behind Azure App Service/NGINX, configure JWT secrets, and whitelist the frontend origin for CORS.
- **Codex Runner**: Run as a worker (container or App Service) connected to Service Bus `agentchain-document-ready`. Provide blob connection strings for artifact uploads and `WorkspaceRoot` paths for job isolation.
- **Infrastructure**: Validate Service Bus access and container existence before running; the runner uploads to `documents/{projectFolder}/code/` — ensure those containers have correct access policies.

