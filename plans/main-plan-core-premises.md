# Main Plan - Core premises

## 1. Technology stack

* Expo React Native (managed workflow, no ejecting)
* TypeScript throughout
* Expo Router for file-based routing
* React Query for data fetching and caching
* Zustand for state management
* Reuse existing Next.js API endpoints (no new backend)

## 2. Architecture

* Feature parity with the web app
* Minimalist UI/UX
* Simplified navigation: max 2 levels deep
* Hamburger menu (like web app) + 3 bottom tabs (Home, Alerts, Menu)
* modules: ?

## 3. Integration

* Mobile app is frontend-only; backend already exists
* Reuse all existing Next.js API endpoints
* No new backend development required

## 4. Development

* Stay within Expo ecosystem (use built-in solutions)
* Feature branching by phase (one branch per phase)
* Component reusability: adapt web app components for mobile
* Phase-by-phase execution with review/approval gates
* Critical phases: ?

## 5. Design

* Match web app color scheme (shadcn/Tailwind colors)
* Light and dark mode from day 1
* Translate functionality from day 1
* Mobile-optimized: 44x44pt minimum touch targets, generous whitespace
* Native feel: platform-specific patterns (iOS vs Android)
* Consistent spacing: 4px base unit

## 6. Performance

* App loads in < 2 seconds on 4G
* Smart caching with React Query (30s stale time, 24h cache)
* Offline support with graceful degradation
* Optimistic updates and skeleton screens
* Network resilience: retry logic, exponential backoff

## 7. Deployment

* EAS Build and EAS Submit for iOS/Android
* OTA updates via Expo Updates
* Repository: Optec GitHub organization ?
* TestFlight (iOS) and Google Play internal testing (Android)

## 8. Success criteria

* Feature parity: all 11 modules functional
* Reliability: >99% auth success, >99.5% crash-free
* User experience: >4.5 stars App Store rating
* Adoption: 80% of web users use mobile app within 3 months

## 9. Component reusability

* Reuse web app logic, adapt UI for mobile
* Share TypeScript types
* Keep endpoint calls and data transformations
* Adapt complex components: date range selector, datapoint analysis, charts and calendar

## 10. Development flow

* Sequential phase execution
* First 4 phases are foundational and in good order
* Review and approval before merging each phase
* Sub-branches per module in Phase 7 if needed

