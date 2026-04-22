# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
bun install       # Install dependencies
bun run dev       # Start dev server (http://localhost:3000)
bun run build     # Production build
bun run start     # Start production server
bun run typecheck # TypeScript type checking
```

## Architecture

**Stack:** Next.js 15 (App Router), React 19, TypeScript, @dnd-kit for drag-and-drop.

**Data flow:**
- In-memory store (`lib/store.ts`) persists across Next.js dev hot-reloads via `globalThis`
- API routes (`app/api/**/route.ts`) CRUD operations on the store
- Client components (`components/**`) fetch API and handle drag-and-drop interactions

**File structure:**
- `lib/store.ts` — Single `IssueStore` instance with methods: `list()`, `get()`, `create()`, `update()`, `delete()`, `reorder()`
- `lib/types.ts` — `Issue` interface and `Status` type (`backlog` | `todo` | `in_progress` | `done`)
- `app/api/issues/route.ts` — GET (list), POST (create)
- `app/api/issues/[id]/route.ts` — GET, PATCH, DELETE
- `app/api/columns/[status]/reorder/route.ts` — PUT for column reordering
- `components/Board.tsx` — Main kanban board with `DndContext`, drag-and-drop handlers
- `components/Column.tsx` — Droppable column wrapper with `SortableContext`
- `components/IssueCard.tsx` — Sortable draggable issue cards

**Drag-and-drop:** Uses `@dnd-kit/core` with `PointerSensor` (4px activation). `handleDragOver` provides visual feedback; `handleDragEnd` persists order via `/api/columns/:status/reorder`.
