# Core premises of frontend-rules

## 1. Architecture foundation

* React.js + Next.js (App Router)
* TypeScript throughout
* Layered data flow: Screen → Component → Hook → Service → Endpoint → Data
* Feature-based organization with feature independence

## 2. UI and styling

* Tailwind CSS + shadcn/ui (avoid inline styles)
* Mobile-first responsive design
* Dark mode support
* Next.js `<Image>` for images
* JSX: special characters (apostrophes/quotes) can be used directly

## 3. Data management

* TanStack Query for server state
* Centralized query keys: `['entity', 'action', params]` in `src/lib/queryKeys.ts`
* Optimistic updates with query invalidation
* Consistent loading/error/empty states
* `customFetch()` utility for all API calls

## 5. Error handling

* Global error handler: `useGlobalErrorHandler` for all error management
* Automatic toast notifications for CRUD operations
* Error boundaries for React component errors
* Centralized logging: use `logger` from `@/lib/logger` (never `console.log`)

## 6. Component architecture

* Functional components (PascalCase)
* Custom hooks for business logic
* Reusable components in `/components/ui/` or `/components/common/`
* TypeScript interfaces for all component props
* Error boundaries for graceful error handling

## 7. Forms and validation

* React Hook Form for form management
* Zod for schema validation
* shadcn/ui form components
* Real-time validation
* Add Dialog Pattern: reuse layout from `docs/patterns/add-entity-flow.md`

## 8. Search and filtering

* All list/table screens must include search + filter controls
* Filters persisted in URL query params
* Debounced search for performance

## 9. State management

* React state for local component state
* TanStack Query for server state
* Zustand or Context API for global client state
* URL state for filters, pagination, search
* `localStorage` for user preferences

## 10. File organization

* Current structure: `/app/`, `/components/`, `/hooks/`, `/lib/`, `/docs/`
* Components organized by business functionality: `/components/[feature-name]/`
* Shared components: `/components/ui/`
* Feature independence: avoid direct imports between features
* Barrel exports (`index.ts`) for clean imports

## 11. Development tools

* ESLint: legacy `.eslintrc.json` format, TypeScript files only, zero warnings policy
* Prettier: auto-format on pre-commit via lint-staged
* CI simulation scripts: `pnpm ci:all:fast`, `pnpm ci:lint:fast`, etc.
* React DevTools and TanStack Query DevTools for debugging

## 12. Quality standards

* Unit tests for all components (React Testing Library)
* Integration tests for complex flows
* Accessibility: ARIA labels, semantic HTML, keyboard navigation, WCAG compliance
* Performance: code splitting, image optimization, memoization, virtual scrolling

## 13. API integration

* REST API with `/api/v1` prefix
* Request/response interceptors
* Automatic token injection via `customFetch()`
* Retry logic with exponential backoff
* AbortController for request cancellation

## 14. Notifications

* react-hot-toast for all notifications
* Success, error, warning, and info types
* Consistent messaging across the app

## 15. Environment configuration

* Environment variables for configuration
* Feature flags for gradual rollouts
* Different configs for dev/staging/prod
* TypeScript for environment variable validation

## Summary

These rules prioritize:

1. Type safety (TypeScript everywhere)
2. Centralization (query keys, error handling, logging)
3. Consistency (patterns, naming, structure)
4. User experience (loading states, error handling, accessibility)
5. Maintainability (feature independence, reusable components, clear organization)
6. Quality (testing, linting, formatting, zero warnings policy)

The rules enforce a structured, scalable, and maintainable frontend architecture with strong type safety and consistent patterns across the codebase.

