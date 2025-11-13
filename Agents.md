# AGENTS.md - MPNext Development Guide

## Commands
- **Dev**: `npm run dev` (Next.js dev server)
- **Build**: `npm run build` (production build, runs type checking)
- **Lint**: `npm run lint` (ESLint)
- **Tests**: No test framework configured yet

### Type Generation Notes
- Generated types automatically quote field names with special characters (e.g., `"Allow_Check-in"`)

## Architecture
- **Framework**: Next.js 16 (App Router) with React 19, TypeScript strict mode
- **Auth**: No authentication configured yet, will use passport.js
- **UI**: Radix UI primitives + shadcn/ui components, Tailwind CSS v4
- **Path Alias**: `@/*` maps to `src/*`

## Code Style
- **Imports**: Use `@/` alias for all internal imports
- **Components**: React Server Components by default, "use client" only when needed for interactivity
- **Types**: TypeScript interfaces
- **Naming**: 
  - PascalCase for components/types
  - camelCase for functions/variables
  - kebab-case for all component files and folders
- **Exports**: Use named exports for all components (no default exports)
- **UI Components**: Keep in `src/components/ui/` following shadcn conventions
- **Feature Components**: Organize in kebab-case folders with index.ts barrel exports
- **Actions**: 
  - Feature-specific actions: co-locate in component folder as `actions.ts`
  - Shared actions: place in `src/components/actions/`

## Component Organization
```
src/components/
├── actions/              # Shared actions used across features
├── ui/                   # shadcn/ui components
├── feature-name/         # Feature components (kebab-case)
│   ├── feature-name.tsx
│   ├── actions.ts        # Feature-specific server actions
│   └── index.ts          # Barrel exports
└── shared-component.tsx  # Shared/layout components
```

## Import Patterns
```typescript
// Feature components (using barrel exports)
import { ContactLookup } from '@/components/contact-lookup';

// Application DTOs
import { ContactSearch, ContactLookupDetails } from '@/lib/dto';

// Feature-specific actions (relative path within same folder)
import { searchContacts } from './actions';

// Cross-feature actions
import { getCurrentUserProfile } from '@/components/user-menu/actions';

// Shared actions
import { sharedAction } from '@/components/actions/shared';

// Named exports (required)
export function MyComponent() { ... }  // ✅ Correct
export default MyComponent;            // ❌ Avoid
```
