# Component Inventory

- **App** – Entry point for the React SPA, wires `DocumentMapModal`, `LoginPage`, and session helpers.
- **DocumentMapModal** – Multi-tab modal for browsing documents and navigating within the repo’s knowledge graph.
- **MarkdownViewerModal** – Lightweight markdown preview engine (reads raw markdown files and renders them for the reviewer).
- **LoginPage** – Handles Firebase-backed sign-in and obtains JWT tokens for API requests.
- **SessionStorage utilities** – Provide persistent support for caching `SessionId` + `token` per agent or user.
- **CodexRunner** – Background component that orchestrates builds, uploads artifacts, and writes manifests.
- **Controllers** (`ProjectsController`, `ChatController`, `SessionsController`, `ProjectAgentsController`, etc.) – Represent server-side action points (CRUD + telecom) for the API layer.

