# Next.js Standards

## Routing
- Use App Router (default for all new projects)
- Use route groups `(groupName)` to organize without affecting URL
- Implement `error.tsx` and `not-found.tsx` at appropriate route levels
- Use `loading.tsx` for streaming/suspense boundaries

## Server vs Client Components
- Server Components are the default — don't add "use client" unless needed
- Use "use client" only for: event handlers, useState/useEffect, browser APIs, third-party client libs
- Keep client components small and push them to the leaves of the component tree

## Data & Mutations
- Use Server Actions for form submissions and mutations
- Use `fetch` in Server Components for data loading (benefits from caching)
- Implement proper revalidation: `revalidatePath` / `revalidateTag`
- Use ISR (Incremental Static Regeneration) for content pages where appropriate

## Assets & Performance
- Use `next/image` for all images — never use raw `<img>` tags
- Use `next/font` for font loading (automatic optimization)
- Use `next/link` for client-side navigation

## Environment Variables
- Client-accessible vars must use `NEXT_PUBLIC_` prefix
- Server-only vars: no prefix, accessed only in Server Components / API routes / Server Actions
- Validate env vars at build time with `@t3-oss/env-nextjs` or zod

## Metadata & SEO
- Use the Metadata API (`generateMetadata`) for dynamic SEO
- Define `metadata` export in layout/page files
- Include Open Graph and Twitter card metadata for public pages

## Patterns
- Colocate components, hooks, and utils within route segments
- Use `lib/` for shared server utilities, `components/` for shared UI
- Prefer `server-only` package to prevent server code from leaking to client bundle
