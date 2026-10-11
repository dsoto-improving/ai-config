---
name: task-frontend-review
description: Lightweight frontend review focused on React/Next.js patterns, Tailwind usage, and user-facing correctness.
---

# Task: Frontend code review

Review a frontend change quickly. Focus on correctness, consistency, and user-facing issues, not perfection.

## Checklist

1. **React / Next.js**
   - Server Component by default; `'use client'` only when justified.
   - No `useEffect` for derived state.
   - Keys are stable and correct in lists.
   - No hydration mismatches from rendering server/client differences.

2. **Styling**
   - Tailwind classes only. No inline styles except for dynamic values.
   - Responsive breakpoints used consistently.
   - Focus and accessible states present.
   - No hardcoded colors outside design tokens.

3. **State**
   - Zustand used for global state; local state for UI-only concerns.
   - No prop drilling beyond two levels without a good reason.

4. **API / data**
   - Loading and error states handled.
   - API URLs come from env, not hardcoded.
   - No secrets in client code.

5. **TypeScript**
   - Props typed. Avoid `any`. Use `unknown` when necessary and narrow.
   - No unchecked optional chaining that could hide bugs.

6. **UX / clarity**
   - Copy is clear and consistent.
   - Buttons and links are obviously clickable.
   - Empty/error states inform the user.

## Output

- Issues by severity: blocking / should-fix / nit.
- One sentence per issue with file/line reference when possible.
- Do not block on nits.
