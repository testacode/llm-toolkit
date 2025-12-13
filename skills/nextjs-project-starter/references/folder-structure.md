# Folder Structure Reference

## Recommended Project Structure

```
project-name/
├── .nvmrc                      # Node version
├── .env.example                # Environment template
├── .env.local                  # Local environment (gitignored)
├── .gitignore
├── CLAUDE.md                   # Claude Code instructions
├── README.md
├── next.config.ts
├── package.json
├── postcss.config.mjs          # If using Mantine
├── tsconfig.json
├── vitest.config.ts            # If using Vitest
│
├── public/
│   ├── favicon.ico
│   └── images/
│
└── src/
    ├── app/                    # Next.js App Router
    │   ├── layout.tsx          # Root layout
    │   ├── page.tsx            # Home page
    │   ├── globals.css
    │   │
    │   ├── api/                # API routes
    │   │   └── health/
    │   │       └── route.ts
    │   │
    │   ├── (auth)/             # Auth route group (no layout)
    │   │   ├── login/
    │   │   │   └── page.tsx
    │   │   ├── register/
    │   │   │   └── page.tsx
    │   │   └── callback/
    │   │       └── route.ts
    │   │
    │   └── (main)/             # Main app route group
    │       ├── layout.tsx      # Main layout with nav
    │       ├── dashboard/
    │       │   └── page.tsx
    │       └── settings/
    │           └── page.tsx
    │
    ├── components/             # React components
    │   ├── ui/                 # Base UI components
    │   │   ├── button.tsx
    │   │   ├── input.tsx
    │   │   └── index.ts
    │   │
    │   ├── layout/             # Layout components
    │   │   ├── header.tsx
    │   │   ├── footer.tsx
    │   │   ├── sidebar.tsx
    │   │   └── index.ts
    │   │
    │   └── features/           # Feature-specific components
    │       ├── auth/
    │       │   ├── login-form.tsx
    │       │   └── index.ts
    │       └── dashboard/
    │           ├── stats-card.tsx
    │           └── index.ts
    │
    ├── hooks/                  # Custom React hooks
    │   ├── use-user.ts
    │   ├── use-media-query.ts
    │   └── index.ts
    │
    ├── lib/                    # Core utilities
    │   ├── constants.ts
    │   ├── env.ts              # Type-safe env variables
    │   └── index.ts
    │
    ├── providers/              # React context providers
    │   ├── mantine-provider.tsx
    │   ├── query-provider.tsx
    │   └── index.ts
    │
    ├── stores/                 # Zustand stores
    │   ├── user-store.ts
    │   ├── ui-store.ts
    │   └── index.ts
    │
    ├── types/                  # TypeScript types
    │   ├── api.ts
    │   ├── database.ts         # Supabase generated types
    │   └── index.ts
    │
    ├── utils/                  # Utility functions
    │   ├── cn.ts               # className utility
    │   ├── format.ts
    │   ├── supabase/           # Supabase clients
    │   │   ├── client.ts
    │   │   ├── server.ts
    │   │   └── middleware.ts
    │   └── index.ts
    │
    ├── test/                   # Test setup & mocks
    │   ├── mocks/
    │   │   ├── handlers.ts     # MSW handlers
    │   │   └── server.ts
    │   └── setup.ts            # Vitest setup
    │
    └── middleware.ts           # Next.js middleware
```

## File Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Components | kebab-case | `login-form.tsx` |
| Hooks | use-kebab-case | `use-user.ts` |
| Stores | kebab-case-store | `user-store.ts` |
| Types | kebab-case | `api.ts` |
| Utils | kebab-case | `format.ts` |
| Pages | page.tsx | `page.tsx` |
| Layouts | layout.tsx | `layout.tsx` |
| API Routes | route.ts | `route.ts` |
| Tests | *.test.ts(x) | `login-form.test.tsx` |

## Index Files Pattern

Each folder should have an `index.ts` for clean imports:

```typescript
// src/components/ui/index.ts
export { Button } from './button';
export { Input } from './input';
export { Card } from './card';
```

Usage:
```typescript
import { Button, Input, Card } from '@/components/ui';
```

## Test File Location

Tests should be colocated with the code they test:

```
src/
├── components/
│   └── ui/
│       ├── button.tsx
│       ├── button.test.tsx     # Test next to component
│       └── __tests__/          # Or in __tests__ folder
│           └── button.test.tsx
│
└── utils/
    ├── format.ts
    └── format.test.ts
```

## Route Groups

Use route groups `(name)` for:
- Shared layouts without affecting URL
- Organizing related routes

```
app/
├── (auth)/           # /login, /register (no shared layout)
│   ├── login/
│   └── register/
│
├── (main)/           # /dashboard, /settings (shared layout)
│   ├── layout.tsx    # Header, sidebar, etc.
│   ├── dashboard/
│   └── settings/
│
└── (marketing)/      # /, /about, /pricing (landing layout)
    ├── layout.tsx
    ├── page.tsx      # Home page
    └── about/
```
