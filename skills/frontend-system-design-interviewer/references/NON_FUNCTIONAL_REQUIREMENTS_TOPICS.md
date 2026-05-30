# Frontend non-functional requirements catalog

This catalog helps identify frontend-specific non-functional requirements (NFRs) during a system design interview. Do not try to apply every item to every product. Select the requirements that materially affect the user experience or architecture, make them measurable where possible, and explain the resulting trade-offs.

A useful frontend NFR is more specific than "the system should be fast" or "the system should scale." For example:

- Users on slow mobile networks should be able to reach the main content quickly. This affects the bundle budget, code splitting, caching, compression, and media loading strategy.
- Users from multiple regions should receive static assets with low latency. This affects CDN usage, cache headers, edge delivery, and possibly data residency decisions.
- Users should be able to read cached content while offline and synchronize safe mutations after reconnecting. This affects local persistence, service workers, mutation queues, conflict handling, and retry rules.

## 1. Performance and resource efficiency

### 1. Initial load performance

- Requirement: users should see useful content quickly after opening the application or a deep link.
- Consider when: the product has public landing pages, a large JavaScript bundle, mobile users, low-end devices, slow networks, or strict conversion targets.
- May affect: performance budgets; CSR vs SSR/SSG/streaming SSR; app-shell design; route-level code splitting; tree shaking; compression; preload and preconnect hints; critical CSS; font loading; skeletons; CDN caching; Web Vitals targets such as LCP and TTFB.

### 2. Interaction responsiveness

- Requirement: important user actions should produce immediate feedback and complete within an acceptable latency budget.
- Consider when: the product includes search, forms, editors, drag-and-drop, filters, likes, checkout, or other frequent interactions.
- May affect: INP targets; optimistic UI; debouncing and throttling; local state placement; background work; API latency budgets; loading indicators; Web Workers; memoization; render profiling.

### 3. Rendering smoothness and visual stability

- Requirement: scrolling, transitions, and layout updates should remain smooth and should not unexpectedly shift visible content.
- Consider when: the UI contains feeds, dashboards, complex tables, animations, ads, asynchronously loaded media, or frequently updated widgets.
- May affect: CLS targets; image dimensions; placeholder strategy; animation choices; virtualization; DOM size; layout and paint profiling; CSS containment; reduced-motion support.

### 4. Bundle size and network efficiency

- Requirement: the application should minimize transferred bytes and avoid unnecessary requests, especially on constrained networks.
- Consider when: users may rely on slow or expensive mobile data, the app has many routes or dependencies, or the product targets emerging markets.
- May affect: bundle budgets in CI; code splitting; lazy loading; dependency audits; compression; request batching; caching; prefetch rules; adaptive loading; removal of expensive third-party scripts.

### 5. CPU, memory, and battery efficiency

- Requirement: the application should avoid excessive CPU work, memory growth, and battery drain during long sessions.
- Consider when: the product targets mobile devices, low-end hardware, background tabs, long-lived dashboards, maps, editors, media playback, polling, or persistent realtime connections.
- May affect: polling frequency; WebSocket usage; tab-visibility handling; listener cleanup; bounded caches; Web Workers; animation complexity; memory-leak monitoring; background-task policies.

### 6. Media delivery efficiency

- Requirement: images, video, audio, and documents should load at an appropriate quality without dominating bandwidth or blocking the main experience.
- Consider when: the product is media-heavy, includes user uploads, targets mobile screens, or serves users across multiple regions.
- May affect: responsive images and `srcset`; modern image formats such as WebP or AVIF; compression; progressive placeholders; lazy loading; CDN usage; signed URLs; streaming protocols; upload limits; transcoding; direct-to-storage uploads.

### 7. Large dataset rendering

- Requirement: large lists, feeds, tables, and search results should remain usable as the number of items grows.
- Consider when: a screen may display hundreds or thousands of entities, use infinite scroll, or receive frequent inserts and updates.
- May affect: cursor pagination; virtualization; incremental rendering; list windowing; normalized state; sorting and filtering strategy; accessibility behavior; scroll-position restoration; API page size.

## 2. Platform and audience constraints

### 8. Slow and unreliable network support

- Requirement: core flows should remain understandable and recoverable when requests are slow, intermittent, or temporarily unavailable.
- Consider when: users are mobile, travel frequently, use public networks, or operate in regions with inconsistent connectivity.
- May affect: loading and stale states; retries with exponential backoff; request cancellation; timeouts; cache-first reads; offline indicators; mutation queues; idempotency; adaptive media; graceful degradation.

### 9. Low-end device support

- Requirement: core flows should work acceptably on the minimum supported hardware, not only on developer machines.
- Consider when: the product has a broad consumer audience, targets emerging markets, or supports older phones and laptops.
- May affect: JavaScript budget; hydration cost; polyfills; animation complexity; DOM size; image quality; Web Worker usage; progressive enhancement; real-device testing; performance segmentation by device class.

### 10. Browser and device compatibility

- Requirement: the application should behave correctly across the supported browser, OS, screen, input, and device matrix.
- Consider when: the audience includes older browsers, embedded webviews, tablets, touch devices, keyboards, or enterprise-managed environments.
- May affect: browser support policy; polyfills; feature detection; progressive enhancement; CSS strategy; compatibility layers; cross-browser tests; fallback behavior for unsupported APIs.

### 11. Responsive and adaptive UX

- Requirement: the experience should remain usable across relevant screen sizes and input methods.
- Consider when: the product supports mobile web, desktop, tablets, landscape mode, touch, mouse, keyboard, or device-specific flows.
- May affect: mobile-first vs desktop-first design; breakpoints; adaptive layouts; navigation patterns; table and editor behavior; touch targets; hover fallbacks; safe areas; responsive images.

### 12. Accessibility

- Requirement: users with disabilities should be able to navigate, understand, and operate the product.
- Consider when: always; prioritize explicitly for public-sector, education, healthcare, financial, and enterprise products, or when WCAG conformance is required.
- May affect: semantic HTML; keyboard navigation; focus management; screen-reader support; ARIA usage; color contrast; reduced-motion support; captions; alt text; accessible component APIs; automated and manual accessibility testing.

### 13. Internationalization and localization

- Requirement: the application should support the required languages, locales, writing directions, and regional formats.
- Consider when: the audience spans countries or languages, or future expansion is likely.
- May affect: translation loading; locale-aware routing; pluralization; date, time, number, and currency formatting; RTL layouts; text expansion; sorting; icons and imagery; legal copy; localized metadata.

### 14. Multi-region delivery

- Requirement: users in supported regions should receive the application and static assets with acceptable latency and availability.
- Consider when: the product has a global audience, large media assets, region-specific content, or data residency constraints.
- May affect: CDN and edge delivery; cache headers; regional monitoring; origin placement; geo-routing; localization; edge redirects; asset replication; privacy and data residency decisions.

### 15. SEO and social discoverability

- Requirement: public pages should be crawlable, indexable, shareable, and stable enough to meet acquisition goals.
- Consider when: the product includes marketing pages, content, product catalogs, marketplaces, public profiles, or shareable pages.
- May affect: SSR/SSG/ISR; metadata; semantic HTML; headings; canonical URLs; sitemap; robots rules; structured data; Open Graph tags; redirect strategy; page performance; image alt text.

## 3. Reliability, data, and realtime behavior

### 16. Availability and graceful degradation

- Requirement: critical flows should remain useful, or fail clearly, when optional dependencies or backend capabilities are unavailable.
- Consider when: the product integrates third-party scripts, recommendations, ads, payments, maps, analytics, or multiple APIs.
- May affect: error boundaries; fallback UI; dependency isolation; timeout policies; feature degradation; cached reads; retry controls; circuit-breaker-like client behavior; third-party loading strategy.

### 17. Offline support and local persistence

- Requirement: selected flows should work without an active connection and synchronize appropriately after reconnection.
- Consider when: users travel, work in the field, edit drafts, consume saved content, or frequently experience poor connectivity.
- May affect: service workers; IndexedDB; cache invalidation; local schema migrations; draft storage; mutation queues; sync status; conflict resolution; storage limits; stale-content UX.

### 18. Data freshness

- Requirement: users should see data that is no older than the product's acceptable freshness window.
- Consider when: the product includes feeds, notifications, inventory, prices, sports scores, dashboards, collaborative data, or operational status.
- May affect: cache TTL; stale-while-revalidate; refetch triggers; polling intervals; SSE; WebSocket; push notifications; tab visibility behavior; background refresh; backend load.

### 19. Realtime latency and event volume

- Requirement: realtime events should arrive within an acceptable delay without overwhelming the browser, network, or backend.
- Consider when: the product includes chat, collaborative editing, live tracking, notifications, auctions, trading, or frequently updated feeds.
- May affect: polling vs long polling vs SSE vs WebSocket; reconnect strategy; heartbeat; backpressure; batching; rate limiting; event coalescing; ordering; deduplication; battery usage.

### 20. Consistency and conflict resolution

- Requirement: the product should define which data must be strongly consistent and where eventual consistency is acceptable.
- Consider when: the application uses optimistic UI, offline edits, collaborative editing, multiple tabs, multiple devices, inventory, payments, or permissions.
- May affect: optimistic-update rules; rollback UX; reconciliation; CRDT or OT evaluation; server version fields; merge policies; cache invalidation; user-visible conflict handling.

### 21. Mutation reliability and duplicate prevention

- Requirement: important user actions should not be lost, repeated accidentally, or left in an ambiguous state.
- Consider when: the product creates orders, payments, bookings, uploads, messages, comments, or any mutation users may retry.
- May affect: idempotency keys; disabled submit states; retry policy; exponential backoff; deduplication; pending-operation UI; outbox queues; request tracing; server contract design.

### 22. Cache correctness and version compatibility

- Requirement: cached HTML, JavaScript, assets, and API data should not produce stale or incompatible application states.
- Consider when: the product uses a CDN, service worker, long-lived tabs, aggressive browser caching, SSR, or independently deployed frontend artifacts.
- May affect: hashed asset names; cache-control headers; HTML caching policy; cache busting; service-worker update UX; API version compatibility; stale-data indicators; rollback strategy.

## 4. Security, privacy, and permissions

### 23. Client-side security

- Requirement: the frontend should reduce exposure to common web attacks and should not treat browser-side checks as a security boundary.
- Consider when: the application handles authentication, user-generated content, cookies, rich text, third-party scripts, sensitive actions, or embedded content.
- May affect: XSS prevention; HTML sanitization; CSP; CSRF protection; SameSite cookies; CORS configuration; clickjacking protection; security headers; dependency review; safe rendering defaults.

### 24. Privacy, PII, and consent

- Requirement: personal and sensitive data should be collected, stored, displayed, and transmitted only as allowed by product and legal policies.
- Consider when: the application handles user profiles, analytics, session replay, health data, financial data, location, children, or users from regulated regions.
- May affect: analytics schema; consent management; redaction; local-storage policy; logging; session replay masking; retention; data export and deletion flows; regional behavior.

### 25. Authentication and authorization-aware UX

- Requirement: session changes and permission changes should be reflected predictably in the UI without exposing unauthorized actions.
- Consider when: the product has login, multiple roles, expiring sessions, multiple tabs, organization membership, admin tools, or sensitive workflows.
- May affect: session storage; token refresh; cookie policy; multi-tab synchronization; protected routes; permission-aware components; cache clearing; reauthentication UX; backend authorization requirements.

## 5. Operability and product evolution

### 26. Observability and production diagnostics

- Requirement: the team should be able to detect, investigate, and measure frontend failures and regressions in production.
- Consider when: always; prioritize for high-traffic, revenue-critical, multi-region, or frequently released products.
- May affect: error tracking; structured logs; Web Vitals and real-user monitoring; release tags; source maps; request correlation IDs; analytics events; privacy redaction; alert thresholds; device and region segmentation.

### 27. Release safety and rollback

- Requirement: frontend changes should be releasable incrementally and recoverable when regressions occur.
- Consider when: the product releases frequently, uses cached assets, includes risky migrations, has multiple teams, or cannot tolerate long incidents.
- May affect: CI/CD; automated checks; canary releases; feature flags; kill switches; backward-compatible APIs; artifact versioning; cache strategy; monitoring; rollback procedures.

### 28. Maintainability and team scalability

- Requirement: the frontend codebase and delivery workflow should support the expected team size and rate of change.
- Consider when: multiple teams work in parallel, the product has several domains, shared UI patterns, white-label variants, or independent release needs.
- May affect: module boundaries; ownership; monorepo vs multi-repo; design system; component APIs; dependency constraints; microfrontend evaluation; documentation; test strategy; code review and governance.

## Interview usage

During an interview:

1. Select the 3-6 NFRs that most strongly shape the product.
2. Ask for a measurable target or an explicit assumption where useful.
3. Connect each selected NFR to architecture decisions.
4. State trade-offs: optimizing one requirement can make another harder.
5. Mark lower-priority requirements as out of scope instead of silently ignoring them.

Useful prompts:

- Which devices, browsers, regions, and network conditions should we support?
- What should the user experience be on a slow or interrupted connection?
- Which Web Vitals or interaction latency budgets matter?
- How fresh must the data be, and is realtime delivery required?
- Which actions must survive retries, reconnects, or duplicate submissions?
- Do public pages need SEO, social previews, or fast first render?
- Are accessibility, localization, privacy, or regulatory constraints explicit?
- How frequently do we release, and how quickly must we detect and roll back a regression?

## Source material

This catalog adapts and expands ideas from:

- [A Simple Framework For Mobile System Design Interviews](https://github.com/weeeBox/mobile-system-design/tree/master?tab=readme-ov-file)
- [Frontend System Design Guide](https://github.com/devkodeio/frontend-system-design)
