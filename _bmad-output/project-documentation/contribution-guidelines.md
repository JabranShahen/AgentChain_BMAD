# Contribution Guidelines

1. **Follow the `ai_agent.sln` structure.** Keep API projects (`againt_chain_api`, `agent_service`, `AiAgent.*`) passing `dotnet build` before proposing changes.
2. **Respect the React + TypeScript conventions.** Use `npm run lint` and `npm run test` from the UI folder and ensure changes satisfy ESLint + Vitest.
3. **Document new endpoints/features.** Mirror the style in `AgentChain_UI/project-context.txt` and `AgentChain_API/project-architecture.txt` by providing brief context, usages, and links.
4. **Keep `_bmad` stable.** Automation workflows rely on these YAML/Markdown files; only amend them when you understand the workflow dependencies.
5. **Stateful data safety.** When updating `sessionStorage.ts` or session management, ensure helpers gracefully handle missing or corrupted local storage data.
6. **Use PR descriptions.** Summarize key behaviors, mention integration points (UI ↔ API ↔ Codex runner), and cite affected directories.
7. **Run `git status` across all roots** (`AgentChain_UI`, `AgentChain_API`, `_bmad-output`) because the CI workflow builds artifacts under `_bmad-output/project-documentation`.

