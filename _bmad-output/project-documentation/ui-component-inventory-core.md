# UI Component Inventory (core)

1. **`App.tsx` + `App.css`** – Root layout, context providers, and routing (if any) for the Vite/React SPA. Looks like the gate that loads the document map, login, and workspace content.
2. **`DocumentMapModal.tsx` + `DocumentMapModal.css`** – Floating modal that renders the document map, likely referencing tree/summary info and letting users jump between docs.
3. **`MarkdownViewerModal.tsx`** – Standalone modal for previewing markdown files with customizable headers/footers.
4. **`LoginPage.tsx`** – Presents the authentication entry point; couples with `types.ts` for typed form fields.
5. **`sessionStorage.ts`** – Utility, but also an architectural component (manages session tokens and persisted agent selection).
6. **`firebase.ts`** – Firebase client setup, implying the UI may call Firebase services for authentication or hosting; tied into component state.
7. **`main.tsx` + `index.css`** – Application bootstrap that mounts `App` and wires up global styles.
8. **`assets/`** – Static assets folder for icons/images referenced by components (documented by the inventory even if not yet wired explicitly).

