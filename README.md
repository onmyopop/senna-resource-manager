# Senna — Resource Manager

Timeline and resource management for the Senna team.

## Stack
- **Next.js 14** (App Router)
- **TypeScript**
- **JSON files** in `/data` as the database (committed to GitHub)

## Features
- 📊 **Gantt Chart** — timeline per project, grouped by project, color-coded by project with status indicators
- 👥 **Resource View** — daily grid showing who works on what
- ✏️ **Task CRUD** — add/edit/delete tasks with modal form
- 🎨 **Project & Resource CRUD** — manage projects and team members
- 🔍 **Filters** — filter by project, resource, status, and date range

## Setup

```bash
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

## Data

All data lives in `/data/*.json` files:
- `projects.json` — project list
- `resources.json` — team members
- `tasks.json` — all tasks with assignments

To reset to seed data, just discard changes to these files via git.

## File structure

```
/data
  projects.json
  resources.json
  tasks.json
/src
  /app
    /api
      /projects     GET POST PUT DELETE
      /resources    GET POST PUT DELETE
      /tasks        GET POST PUT DELETE (with filters)
      /timeline     GET (gantt or resource view, aggregated)
    /timeline       Main Gantt + Resource view page
    /projects       Project CRUD page
    /resources      Resource CRUD page
    layout.tsx      Root layout with sidebar
    globals.css     All styles
  /components
    GanttChart.tsx  Gantt bar chart
    ResourceGrid.tsx Daily resource assignment grid
    TaskModal.tsx   Add/edit task modal
    FilterBar.tsx   Filters: project, resource, status, date
    Sidebar.tsx     Navigation sidebar
  /lib
    db.ts           JSON file read/write helpers
  /types
    index.ts        TypeScript types
```

## Adding data

1. Click **+ Add Task** from the Timeline page
2. Or directly edit `/data/tasks.json` and restart the dev server

## Deploying

This app uses `fs` (file system) for storage, so it requires a Node.js server. Deploy to:
- **Vercel** (with persistent storage, note: Vercel's filesystem is ephemeral — for production, migrate to a DB)
- **Railway / Render / VPS** — works fine as-is with JSON files

For persistent production storage, swap `src/lib/db.ts` to use SQLite (via `better-sqlite3`) or PostgreSQL (via `pg`).
