# Core premises - Folder Structure #2

## 1. Technology stack

* Expo React Native (managed workflow, no ejecting)
* TypeScript throughout
* Expo Router for file-based routing
* React Query for data fetching and caching
* Zustand for state management
* Reuse existing Next.js API endpoints (no new backend)

## 2. Feature independence

* Features are autonomous and self-contained.
* No direct imports between features.
* Shared code goes in `/shared/`.
* Clear boundaries and well-defined APIs.

## 3. Layered architecture within features

Each feature follows: Screen → Component → Hook → Service → Endpoint → Data

* Frontend: `/app/` (screens) → `/features/[name]/components/` → `/features/[name]/hooks/` → `/features/[name]/services/`
* Backend: `/server/api/v1/[name]/` → `/server/features/[name]/services/` → `/server/features/[name]/repositories/` → Database

## 4. Consistent structure across features

Each feature contains:

* `components/` - Feature-specific UI components
* `hooks/` - Feature-specific React hooks
* `services/` - Feature-specific business logic
* `types/` - Feature-specific TypeScript types
* `utils/` - Feature-specific utilities
* `constants/` - Feature-specific constants
* `index.ts` - Barrel exports for clean imports

## 5. Shared code centralization

* Common code lives in `/shared/` (components, hooks, services, types, utils, constants, providers).
* Avoid duplication across features.
* Reuse shared components and utilities.

## 6. Benefits focus

* Scalability: Independent features enable parallel work and independent deployment.
* Maintainability: Related code is co-located; easier to find and refactor.
* Reusability: Shared components and utilities reduce duplication.
* Testing: Tests are organized by feature for clear coverage.

## 7. Implementation principles

* Gradual migration: Move existing code into features incrementally.
* Clear boundaries: Well-defined interfaces between features.
* Consistent naming: Standardized conventions across features.
* Barrel exports: Use `index.ts` for clean import paths.

## 8. Data flow pattern

Screen → Component → Hook → Service → API 

Each layer has a specific responsibility and communicates only with adjacent layers.

---

These premises prioritize business-domain organization, feature autonomy, and shared code reuse to improve scalability and maintainability.

