# State Management Patterns (core)

- **Browser storage as source-of-truth** – `sessionStorage.ts` wraps `window.localStorage` under `agentchain-ui:sessions` and `agentchain-ui:selected-agent`. Reads/writes are sanitized so React components can quickly recall the active session tokens without extra API calls.
- **Session-first flows** – Controllers like `SessionsController` and `ChatController` expect a `sessionId` + JWT. The UI loads/stores that session metadata via the helpers above before calling `/api/chat` or `/api/projects`.
- **Modal-driven state** – `DocumentMapModal.tsx`, `MarkdownViewerModal.tsx`, and `App.tsx` maintain local state flags (open/closed, selected row) while `App.css`/`DocumentMapModal.css` keep styles aligned with the state. This indicates a pattern where React state determines UI focus rather than global stores.
- **Typed utilities** – `types.ts` and the `sessionStorage` helpers keep TypeScript safety around the `SessionInfo` shape, minimizing runtime surprises in the quick scan.
- **Global configuration entry point** – `main.tsx` bootstraps the React tree and registers service workers (if any), so state initialization likely happens there before screens render.

