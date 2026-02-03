# AgentB — Your Personalized Learning Platform

AgentB is an AI-powered campus assistant providing personalized learning, campus resources, and adaptive study tools tailored to your learning style.

## Tech stack

- **Vite** — Build tool and dev server
- **TypeScript** — Type-safe JavaScript
- **React** — UI framework
- **shadcn/ui** — Component library (Radix UI + Tailwind)
- **Tailwind CSS** — Styling
- **Supabase** — Backend (Auth, Database, Storage, Edge Functions)

## Prerequisites

- **Node.js** (v18 or newer recommended) — [Install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating) or from [nodejs.org](https://nodejs.org/)
- **npm** (or Bun / yarn)

## Local development

### 1. Clone and install

```bash
git clone <YOUR_GIT_URL>
cd <PROJECT_DIRECTORY>
npm install
```

### 2. Environment variables

Create a `.env` file in the project root with your Supabase credentials (and any other env vars the app expects). For example:

```env
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key
```

Do not commit `.env` or real keys. You can add a `.env.example` with placeholder variable names for other developers.

### 3. Run the dev server

```bash
npm run dev
```

The app is served at **http://localhost:8080** (or the port shown in the terminal). Edits will hot-reload.

### 4. Build and preview

```bash
# Production build
npm run build

# Preview the production build locally
npm run preview
```

## Scripts

| Command        | Description                    |
|----------------|--------------------------------|
| `npm run dev`  | Start dev server with HMR      |
| `npm run build`| Production build (output: `dist`) |
| `npm run build:dev` | Build in development mode |
| `npm run preview`   | Serve production build locally |
| `npm run lint`      | Run ESLint                     |

## Project structure

- `src/` — Application source (entry: `src/main.tsx`)
- `src/components/` — React components (including `ui/` for shadcn)
- `src/lib/` — Utilities and shared code (e.g. Supabase client)
- `src/hooks/` — Custom React hooks

Path alias `@/` points to `src/` (e.g. `@/components/ui/button`).

For a high-level architecture and migration notes from Lovable, see **ARCHITECTURE.md** and **cursor_migration.md**.
