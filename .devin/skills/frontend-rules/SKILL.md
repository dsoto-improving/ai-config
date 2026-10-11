---
name: frontend-rules
description: Frontend development rules for the measurable Next.js app. Keep velocity high while matching the existing Tailwind + Zustand stack.
---

# Frontend development rules

Stack: Next.js 16 (App Router), React 19, TypeScript, Tailwind 4, Zustand.

## Code style

- Follow existing patterns in `src/app/` and `src/components/`.
- Do not introduce CSS Modules, Sass, or Styled Components unless the user explicitly asks. Use Tailwind.
- Use clear, pronounceable names in English. Avoid generic names like `data`, `info`, `temp`.
- Keep components focused. If a component exceeds one screen, split by logical section.
- Prefer composition over props drilling, but do not over-engineer context providers.

## Next.js App Router

- Use Server Components by default.
- Add `'use client'` only when you need: browser APIs, React state/effects, Zustand, or event handlers.
- Keep data fetching close to where it is rendered. Server Components can call the backend directly via `NEXT_PUBLIC_API_URL` or an internal fetch.
- Use `loading.tsx` and `error.tsx` for route-level boundaries only when they add value.

## Components

- Place components in `src/components/<domain>/` (e.g. `src/components/report-lab/`).
- Co-locate subcomponents when they are not reused elsewhere.
- Export the main component as default from its file.
- Use TypeScript interfaces for props. Name the interface `[ComponentName]Props`.

## State

- Use Zustand for global state. Stores live in `src/stores/` or co-located if small.
- Use `useState` for local UI state.
- Avoid `useEffect` for derived state; compute it directly or use memoization if needed.
- Do not add React Query/RTK unless the user asks.

## Styling

- Tailwind 4 classes only. Avoid arbitrary values (`w-[123px]`) unless necessary.
- Use existing design tokens (colors, spacing, font sizes) from `globals.css`.
- Responsive breakpoints: `sm`, `md`, `lg` in that order.
- Ensure interactive elements have a visible focus state.

## Tests

- Tests live in `tests/`.
- Use the existing Node/Playwright test patterns when adding coverage for flows (auth, report generation, integrations).
- Add a test when the change fixes a bug or introduces a critical user flow.
- Do not test pure markup unless it drives behavior.

## API calls

- Use the existing fetch helpers or axios patterns in the codebase.
- Handle loading and error states in the UI.
- Do not hardcode API URLs; read from `NEXT_PUBLIC_API_URL`.

## When to ask the user

- Changes that affect routing or authentication.
- Changes that require new environment variables.
- Changes that break existing report rendering or integration flows.
