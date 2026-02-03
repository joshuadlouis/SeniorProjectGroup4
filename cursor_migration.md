# AgentB — Lovable to Local Development Migration

This document gives an overview of the AgentB codebase and step-by-step instructions to remove Lovable.dev dependencies and run the app in a local development environment.

**Already done in this repo:** The Lovable plugin has been removed from `vite.config.ts`, `lovable-tagger` has been removed from `package.json`, `index.html` meta tags no longer point to Lovable, `README.md` has been rewritten for local dev, and `ARCHITECTURE.md` Lovable labels have been updated. You still need to run `npm install`, add a `.env` with Supabase (and any other) variables, and ensure the `src/` directory exists (see Steps 5 and 7 below).

---

## Codebase Overview

### What This Project Is

**AgentB** is an AI-powered adaptive learning platform. It provides:

- **Frontend**: React 18 + TypeScript + Vite
- **UI**: shadcn/ui (Radix primitives) + Tailwind CSS
- **Data**: Supabase (PostgreSQL, Auth, Storage, Edge Functions)
- **State/API**: React Query (@tanstack/react-query), React Router, React Hook Form + Zod

### Tech Stack Summary

| Layer | Technologies |
|-------|--------------|
| Build | Vite 5, TypeScript 5 |
| UI Framework | React 18 |
| Styling | Tailwind CSS, tailwindcss-animate, PostCSS |
| Components | shadcn/ui (Radix UI), Lucide icons, Recharts, Sonner toasts |
| Routing | React Router DOM v6 |
| Forms | react-hook-form, @hookform/resolvers, Zod |
| Data & Auth | @supabase/supabase-js, TanStack React Query |
| Other | date-fns, next-themes, cmdk, vaul, etc. |

### Expected Project Structure

The app entry is `index.html` → `/src/main.tsx`. Configuration expects a `src/` directory with (typically):

- **`src/main.tsx`** — App bootstrap and root render
- **`src/App.tsx`** — Root component and router
- **`src/index.css`** — Global and Tailwind styles
- **`src/components/`** — UI components (including `ui/` for shadcn)
- **`src/lib/`** — Utilities (e.g. `utils.ts` for cn), Supabase client
- **`src/hooks/`** — Custom hooks
- **Pages/features** — e.g. Index (Dashboard), Auth, Profile, Calendar (see `ARCHITECTURE.md`)

Paths use the `@/` alias pointing to `./src` (see `tsconfig.app.json`, `vite.config.ts`).

### Where Lovable Was Used

Lovable-related pieces in this repo:

1. **`lovable-tagger`** (devDependency) — Used in Vite dev mode to tag components for the Lovable editor.
2. **`vite.config.ts`** — Imports and conditionally applies `componentTagger()` when `mode === "development"`.
3. **`index.html`** — Open Graph and Twitter meta tags point to `lovable.dev` (og:image, twitter:site, twitter:image).
4. **`README.md`** — Written for Lovable (project URL, “Use Lovable”, “Publish” via Lovable, etc.).
5. **`ARCHITECTURE.md`** — Diagram labels mention “Lovable Platform” for AI/ML and CI/CD; these are conceptual and can be renamed.

There are **no runtime Lovable APIs** in the app; Supabase and your own backend/Edge Functions are the backend. Removing the tagger and updating docs is enough to “disconnect” Lovable.

---

## Step-by-Step: Disconnect Lovable and Run Locally

### Step 1: Remove the Lovable Vite plugin

**File:** `vite.config.ts`

- Remove the `lovable-tagger` import.
- Remove `componentTagger()` from the `plugins` array (so the array only uses the React plugin and any other non-Lovable plugins).

After this, the config should use only `react()` (and optionally other non-Lovable plugins). No references to `lovable-tagger` should remain.

### Step 2: Remove the Lovable dependency

**File:** `package.json`

- In `devDependencies`, remove the line for `"lovable-tagger": "^1.1.11"` (or whatever version is there).

Then reinstall dependencies so the lockfile no longer pulls in Lovable:

```bash
npm install
```

(or `bun install` if you use Bun).

### Step 3: Update Open Graph and Twitter meta tags (optional but recommended)

**File:** `index.html`

- Replace `og:image` and `twitter:image` with your own image URL or a placeholder (e.g. `/og-image.png` or your production URL).
- Replace `twitter:site` with your app’s Twitter handle or remove it if you don’t use Twitter.

This only affects link previews and branding, not app behavior.

### Step 4: Rewrite README for local development

**File:** `README.md`

- Remove Lovable-specific instructions (Lovable project URL, “Use Lovable”, “Publish” via Lovable, custom domain via Lovable).
- Add:
  - Short project description (e.g. “AgentB – local development”).
  - Prerequisites: Node.js (and npm or Bun).
  - How to run locally, for example:
    - Clone repo → `cd` into project → `npm install` → `npm run dev`.
  - How to build: `npm run build`; how to preview: `npm run preview`.
  - Point to `.env` (or `.env.example`) for Supabase and any other required env vars.

This keeps the repo self-contained and clear for anyone cloning it.

### Step 5: Environment variables

- Ensure a **`.env`** file exists in the project root (it’s in `.gitignore`; do not commit secrets).
- Add at least your Supabase keys, for example:
  - `VITE_SUPABASE_URL`
  - `VITE_SUPABASE_ANON_KEY`
- If you use Edge Functions or other backends, add any `VITE_*` or other variables the app expects.
- Optionally add a **`.env.example`** (with placeholder names and no real keys) and document required variables in the README.

Without the correct env vars, the app may run but auth and Supabase features will fail.

### Step 6: (Optional) Update ARCHITECTURE.md

**File:** `ARCHITECTURE.md`

- Replace “Lovable Platform” (or “AI/ML Services (Lovable Platform)”) with a generic label, e.g. “AI/ML Services” or “External AI / Backend”.
- Replace “Lovable Platform CI/CD” with “CI/CD” or your actual pipeline (e.g. “GitHub Actions”).

This keeps architecture docs platform-agnostic.

### Step 7: Restore or verify `src/` (if missing)

The app entry is `src/main.tsx`. **Note:** This repo may not include a `src/` directory (e.g. if it was generated by Lovable and the frontend lives elsewhere). If `src/` is missing:

- Restore it from your Lovable project export or from the commit that last contained it.
- Or re-create the minimal structure: `src/main.tsx`, `src/App.tsx`, `src/index.css`, and the Supabase client under `src/lib/` so the app can start.

After `src/` is present and Step 1–2 and 5 are done, you can run the app locally.

### Step 8: Run the app locally

From the project root:

```bash
npm install
npm run dev
```

Vite usually serves the app at `http://localhost:8080` (see `server.port` in `vite.config.ts`). Open that URL in a browser.

- **Build for production:** `npm run build`
- **Preview production build:** `npm run preview`

---

## Checklist Summary

- [ ] Remove `lovable-tagger` import and plugin from `vite.config.ts`
- [ ] Remove `lovable-tagger` from `devDependencies` in `package.json`
- [ ] Run `npm install` (or `bun install`)
- [ ] Update `index.html` og/twitter meta tags (optional)
- [ ] Rewrite `README.md` for local dev and env vars
- [ ] Add/update `.env` with Supabase (and any other) variables
- [ ] Optionally add `.env.example` and document in README
- [ ] Optionally update `ARCHITECTURE.md` to remove “Lovable” labels
- [ ] Ensure `src/` exists with `main.tsx` and app code
- [ ] Run `npm run dev` and confirm the app loads

After these steps, the project no longer depends on Lovable and can be developed and run entirely in your local environment (and deployed via your own CI/CD and hosting).
