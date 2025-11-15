# Core premises #1

## 1. Maintainability and reusability

* DRY: no duplication across modules; extract shared utilities.
* Module decoupling: components are generic and reusable; no hardcoded module-specific logic.
* Shared components: common functionality lives in `components/common/` with configuration objects.

## 2. Mobile-first performance

* Optimize for mobile: performance, memory, and UX are prioritized.
* Responsive design: use hooks for orientation/screen changes, not static dimensions.
* Native patterns: prefer bottom sheets, gestures, and mobile-optimized interactions.

## 3. SOLID architecture

* Dependency injection: all services accessed via `serviceContainer`; no direct instantiation.
* Interface-based design: depend on abstractions (interfaces), not concrete implementations.
* Single responsibility: each service/component has one clear purpose.

## 4. Type safety and reliability

* TypeScript: use union types for constrained values; avoid literal strings.
* Explicit checks: always check loading, error, and data existence before rendering.
* Error boundaries: wrap critical components to prevent crashes.

## 5. State management separation

* Server state → React Query (API data, caching, background refetching).
* Persistent client state → Zustand (preferences, selected project, theme).
* UI-only state → `useState` (form inputs, modal visibility).

## 6. Performance optimization

* Memoization: shared/reusable components must use `React.memo()`.
* Virtualization: use optimized lists for large datasets.
* Lazy loading: render charts only when screens are focused.
* Memory management: cleanup event listeners, intervals, and timeouts.

## 7. User experience

* Always provide feedback: show success/error toasts after async operations.
* Accessibility: support font scaling, screen readers, proper labels.
* Loading states: use informative skeleton screens matching final layouts.

## 8. Consistency across modules

* Shared patterns: all modules use the same architectural patterns.
* Generic components: charts and UI components are reusable across modules.
* Configuration-driven: module-specific behavior comes from props/config, not hardcoded logic.

## 9. Expo ecosystem

* Stay within Expo: prefer `expo-*` packages over native modules.
* File-based routing: use Expo Router conventions.

## 10. Code quality

* Testing: write tests for critical functionality, especially data transformations.
* File naming: follow consistent conventions (PascalCase for components, kebab-case for hooks).
* Documentation: document overrides of default configurations.

