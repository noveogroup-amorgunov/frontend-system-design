# Deep-dive topic catalog

This document helps you select a topic for a deep dive during a frontend system design interview and prepare a thoughtful answer. Each topic includes questions worth discussing with the interviewer, strengths of a good solution, and pitfalls that are easy to overlook.

## 1. Problem framing and architectural boundaries

### 1. Scope and assumptions

- Questions: what is definitely in scope; what can be left out; which scenarios are core flows; which constraints have already been set by the business.
- Strengths: reduces uncertainty; helps avoid designing unnecessary parts; gives the interviewer a clear frame for the discussion.
- Weaknesses and risks: a scope that is too narrow can hide important requirements; a scope that is too broad consumes time; assumptions should be stated rather than left implicit.

### 2. Interview format and ownership boundaries

- Questions: are we designing only the frontend, the frontend plus API, or the entire system; how deeply should we go into the backend; which parts can be treated as black boxes.
- Strengths: demonstrates maturity in steering the interview; helps select the right diagram level; reduces the risk of answering the wrong question.
- Weaknesses and risks: without clarifying the format, you may go into irrelevant depth; the interviewer may expect more detail about the API or infrastructure; boundaries should be reconfirmed periodically.

### 3. Users, devices, and network

- Questions: who the main users are; desktop or mobile-first; which regions and network conditions matter; whether older devices are supported; whether low-end Android devices and slow connections matter.
- Strengths: directly affects performance, offline support, bundle size, and UX; helps justify the technology stack; makes the solution more realistic.
- Weaknesses and risks: mobile constraints are easy to forget; average metrics can hide tail latency; different regions may require a CDN, edge computing, or data localization.

### 4. Prioritizing non-functional requirements

- Questions: which matters most: speed, accessibility, SEO, offline support, security, cost, or development velocity; which SLOs/SLAs are expected; which trade-offs are acceptable.
- Strengths: moves the conversation from a list of technologies to engineering trade-offs; helps select a deep-dive topic; demonstrates product maturity.
- Weaknesses and risks: everything cannot be maximized at once; without priorities, the NFR solution becomes generic; some NFRs conflict with one another.

### 5. Technology choices and trade-offs

- Questions: why this framework, protocol, state manager, or rendering method was selected; which alternatives were considered; what changes as traffic or the team grows.
- Strengths: demonstrates the ability to choose rather than familiarity with fashionable tools; connects the solution to requirements; makes the answer defensible.
- Weaknesses and risks: choosing something "because I know it" is a weak argument; overengineering complicates maintenance; the cost of a decision should be stated.

## 2. Rendering, delivery, and application loading

### 6. Client-Side Rendering (CSR)

- Questions: whether SEO is needed; how much data is required before the first meaningful render; whether a skeleton can be displayed; how deep links and loading errors are handled.
- Strengths: simple deployment model; works well for user dashboards and interactive applications; reduces the server-rendering load.
- Weaknesses and risks: worse first load on low-end devices; SEO requires additional solutions; users may see a blank screen if JavaScript fails.

### 7. Server-Side Rendering (SSR)

- Questions: which pages are rendered on the server; how data fetching works; what is cached; how authentication, redirects, and errors are handled.
- Strengths: improves initial load and SEO; delivers ready-to-display HTML; useful for public pages and marketplaces.
- Weaknesses and risks: complicates infrastructure; increases request cost; can cause hydration mismatches, personalized-data issues, and server load.

### 8. Static Site Generation and Incremental Static Regeneration

- Questions: which pages can be built ahead of time; how often content changes; whether invalidation is needed; how personalized blocks are handled.
- Strengths: fast TTFB; scales cheaply through a CDN; a good solution for content pages, documentation, and catalogs.
- Weaknesses and risks: complex invalidation; risk of stale content; poor fit for highly personalized or real-time pages.

### 9. Streaming SSR

- Questions: which parts of the page can be streamed independently; what to display before data is ready; how errors in individual sections are handled.
- Strengths: improves perceived performance; displays the shell sooner; works well for pages whose sections load at different speeds.
- Weaknesses and risks: harder to test and debug; can degrade UX without thoughtful fallbacks; requires careful handling of caches and Suspense boundaries.

### 10. Hydration, partial hydration, and islands architecture

- Questions: which parts of the page are interactive; whether some HTML can remain JavaScript-free; where islands are needed; how JavaScript cost is measured.
- Strengths: reduces JavaScript size and CPU cost; improves performance on content-heavy sites; adds interactivity selectively.
- Weaknesses and risks: complicates the architecture; not every team or framework is ready for this model; island boundaries can be inconvenient for shared state.

### 11. Routing and navigation

- Questions: whether nested routing is needed; how protected routes work; what happens on refresh; how redirects, 404 pages, and route-level data loading work.
- Strengths: good routing makes the application predictable; helps manage permissions and layouts; improves navigation UX.
- Weaknesses and risks: complex route guards can easily break UX; deep links may not work; lazy routes can introduce unpleasant delays.

### 12. Code splitting and lazy loading

- Questions: where to split the code; what to load immediately; which chunks are critical; how prefetching affects network and memory use.
- Strengths: reduces the initial bundle; loads rarely used features on demand; improves startup time.
- Weaknesses and risks: too many chunks add overhead; lazy loading can delay important flows; fallbacks and error boundaries are needed.

### 13. Bundle optimization

- Questions: which dependencies are the heaviest; whether tree shaking works; how bundle size is measured; which budget limits should be enforced in CI.
- Strengths: directly affects LCP, TTI, and download cost; helps identify expensive dependencies; provides measurable control.
- Weaknesses and risks: optimization without profiling may be pointless; micro-optimizations can complicate the code; CPU parsing and execution matter in addition to file size.

### 14. Images, fonts, and static assets

- Questions: which image formats to use; whether responsive images are needed; how fonts are loaded; whether blur placeholders or lazy loading are used.
- Strengths: often substantially improves LCP; works well with a CDN; improves UX without changing business logic.
- Weaknesses and risks: incorrect dimensions break layouts and cause CLS; fonts can block text; aggressive compression reduces quality.

### 15. CDN and static asset caching

- Questions: which assets are immutable; how cache busting works; where HTML, JavaScript, and images live; whether geographic proximity to the user matters.
- Strengths: reduces latency and origin load; scales cheaply; works well for static assets.
- Weaknesses and risks: invalidation mistakes are difficult to roll back; HTML and JavaScript versions can drift apart; headers require careful handling.

### 16. Edge rendering and edge functions

- Questions: what can run closer to the user; whether geo-personalization, redirects, A/B testing, or authentication checks are needed at the edge; which runtime constraints apply.
- Strengths: reduces latency; useful for lightweight personalization and routing; offloads the core backend.
- Weaknesses and risks: constrained runtime; harder observability; stateful logic and heavy operations are a poor fit for the edge.

## 3. Data model, API, and state

### 17. REST API design

- Questions: which resources and endpoints are needed; how query parameters work; which error codes are used; how the API is versioned.
- Strengths: clear model; cache-friendly; easy to debug and document.
- Weaknesses and risks: overfetching and underfetching are possible; data from many sources is difficult to aggregate; real-time updates and batching require additional solutions.

### 18. GraphQL

- Questions: whether flexible field selection is needed; who owns the schema; how N+1 problems are solved; how queries and mutations are cached.
- Strengths: reduces overfetching; convenient for complex UIs; provides a typed contract between client and server.
- Weaknesses and risks: more complex infrastructure; caching is not as straightforward as in REST; the schema can become a large shared bottleneck.

### 19. RPC, tRPC, and gRPC-web

- Questions: whether a procedural API is needed; whether end-to-end type safety matters; which clients must be supported; how contracts are versioned.
- Strengths: fast developer experience; works well for tightly coupled frontend and backend applications; less boilerplate.
- Weaknesses and risks: strong coupling between client and server; weaker compatibility with external clients; harder migrations when the API changes.

### 20. Backend for Frontend (BFF)

- Questions: whether a separate backend for frontend is needed; which aggregations it performs; who owns it; how it scales and caches data.
- Strengths: simplifies the client; hides the complexity of internal services; optimizes the API for a specific UI.
- Weaknesses and risks: additional maintenance layer; risk of duplicating business logic; the BFF can become a bottleneck.

### 21. Pagination

- Questions: offset, cursor, or keyset; whether infinite scroll and reverse pagination are needed; how new items are handled; what happens when items are deleted.
- Strengths: cursor/keyset pagination preserves ordering more reliably when items are inserted; helps scale large lists; improves perceived performance.
- Weaknesses and risks: offset pagination breaks on frequently changing data; cursors are harder to debug; infinite scroll requires careful UX and accessibility design.

### 22. Server state caching

- Questions: what should be cached on the client; which TTL and invalidation rules apply; how mutations are synchronized; whether stale-while-revalidate is needed.
- Strengths: reduces network cost; improves responsiveness; works well for read-heavy scenarios.
- Weaknesses and risks: stale data; complex invalidation after mutations; different tabs may display different versions.

### 23. Client state management

- Questions: which state is local, server-side, global, or derived; whether Redux/Zustand/Reatom is needed; where the boundary lies between UI state and domain state.
- Strengths: makes complex UIs manageable; helps separate responsibilities; simplifies scenario testing.
- Weaknesses and risks: a global store can easily become a dumping ground; unnecessary abstraction slows development; server state should not be treated like ordinary client state.

### 24. Normalized entity store

- Questions: whether entities are repeated; whether updates by ID are needed; how relations are stored; how optimistic updates work.
- Strengths: reduces duplication; simplifies targeted updates; works well for complex domain models.
- Weaknesses and risks: increases complexity; selectors become critical; often unnecessary for simple pages.

### 25. Forms and validation

- Questions: where validation happens: client, server, or both; how errors are displayed; whether drafts, autosave, dirty state, and undo are needed.
- Strengths: good form design dramatically improves UX; local validation reduces round trips; server validation remains the source of truth.
- Weaknesses and risks: client and server rules can drift apart; complex forms quickly become separate state machines; autosave requires conflict handling.

### 26. Optimistic UI

- Questions: which operations can be applied optimistically; how errors are rolled back; whether a temporary ID is needed; how conflicts are resolved.
- Strengths: makes the interface feel fast; especially useful for likes, reactions, and comments; demonstrates product thinking.
- Weaknesses and risks: rollbacks can be painful; idempotency is needed; complex operations should not be optimized blindly.

### 27. Retries, idempotency, and deduplication

- Questions: which requests can be retried; whether an idempotency key exists; how duplicate creation is avoided; which retry and backoff rules apply.
- Strengths: improves reliability on poor networks; prevents duplicates; makes the system more resilient.
- Weaknesses and risks: incorrect retries add load; retrying non-idempotent operations is dangerous; users should understand the operation status.

### 28. Consistency and conflict resolution

- Questions: whether strong consistency is needed; where eventual consistency is acceptable; how conflicts across tabs, devices, or users are resolved.
- Strengths: supports an honest discussion of constraints; especially important for collaborative, offline, and real-time scenarios.
- Weaknesses and risks: strong consistency can be expensive; eventual consistency requires understandable UX; automatic conflict resolution can lose data.

### 29. Error handling and error UX

- Questions: which types of errors exist; what users should see; where retries, fallbacks, toast notifications, inline errors, or error pages are needed.
- Strengths: makes the system production-ready; demonstrates maturity; improves user trust.
- Weaknesses and risks: a generic "something went wrong" message is useless; too many toast notifications are irritating; errors should be logged and correlated with requests.

### 30. Data model for the UI

- Questions: which entities are central; which relationships the UI needs; what is stored on the server and what is computed on the client; which fields are needed for list and detail views.
- Strengths: connects requirements, API design, and state management; helps avoid missing important relationships; simplifies further decomposition.
- Weaknesses and risks: there is no need to design the entire database in a frontend-focused interview; the UI model can differ from the storage model; avoid going too deeply into the backend.

## 4. Real-time, offline, and collaboration

### 31. Short polling and long polling

- Questions: how fresh the data must be; how often to poll; how tab visibility is considered; what happens on errors and rate limits.
- Strengths: simple to implement; works almost everywhere; suitable for infrequent updates.
- Weaknesses and risks: unnecessary load; delay between events; scales poorly for frequent updates.

### 32. Server-Sent Events (SSE)

- Questions: whether only server-to-client events are needed; how recovery after reconnection works; whether last-event-id is needed; how connections are closed.
- Strengths: simpler than WebSocket; works well for feed updates, notifications, and live status; uses HTTP.
- Weaknesses and risks: unidirectional channel; browser connection limits; requires a reconnection and backpressure plan.

### 33. WebSocket

- Questions: whether bidirectional real-time communication is needed; which message types exist; how authentication, reconnection, heartbeat, and ordering work.
- Strengths: suitable for chats, games, and collaborative UIs; low latency; flexible communication protocol.
- Weaknesses and risks: harder to scale; requires sticky sessions or pub/sub; observability and backpressure are more complex.

### 34. WebRTC

- Questions: whether peer-to-peer communication is needed; audio/video or a data channel; how signaling and STUN/TURN work; how NAT and fallbacks are handled.
- Strengths: useful for calls, streaming, and peer-to-peer data; reduces server load for some scenarios.
- Weaknesses and risks: difficult to debug; TURN can be expensive; quality depends on the network and devices.

### 35. Web Push and notifications

- Questions: whether push notifications are needed; how permission is requested; which events warrant a push; how opt-in and quiet hours are managed.
- Strengths: brings users back to the product; useful for urgent events; works even without an open tab.
- Weaknesses and risks: permission fatigue; different browser and platform constraints; easy to turn into spam.

### 36. Reconnection, heartbeat, and offline detection

- Questions: how connection loss is detected; which backoff rules apply; how offline state is displayed; what is synchronized after reconnection.
- Strengths: makes real-time UX reliable; handles poor networks more gracefully; reduces load during mass reconnections.
- Weaknesses and risks: aggressive reconnection creates a thundering herd; `navigator.onLine` is not reliable enough; pending operations must be designed explicitly.

### 37. Ordering and delivery guarantees

- Questions: whether event ordering matters; whether sequence numbers are needed; how duplicates are handled; how missed events are processed.
- Strengths: critical for chats, notifications, likes, and collaborative UIs; makes state predictable.
- Weaknesses and risks: exactly-once delivery is almost always an illusion; ordering across different sources is difficult; reconciliation is needed.

### 38. Offline-first and PWA

- Questions: which scenarios should work offline; what the service worker caches; which operations can be queued; how synchronization status is displayed.
- Strengths: strong UX on poor networks; improves reliability; useful for mobile and field-use scenarios.
- Weaknesses and risks: complex cache invalidation; data conflicts; a service worker may leave users on an old version.

### 39. IndexedDB and local persistence

- Questions: which data should be stored locally; how much space can be used; whether schema migrations are needed; how old data is cleaned up.
- Strengths: enables offline support, drafts, and fast startup; better suited than localStorage for large local datasets.
- Weaknesses and risks: more complex API; quotas and eviction depend on the browser; sensitive data should not be stored without assessing the risk.

### 40. Collaborative editing, CRDT, and OT

- Questions: whether concurrent editing is needed; which types of conflicts exist; whether CRDT, OT, or server-side merging is needed; how history and undo are displayed.
- Strengths: powerful UX for documents, whiteboards, and editors; CRDT handles offline use and concurrency well; demonstrates deep design skills.
- Weaknesses and risks: high complexity; difficult to debug; operation size and history storage can become problems.

### 41. Presence, cursors, and live indicators

- Questions: whether users need to see one another; how often presence updates are sent; what to display for idle/offline users; how privacy is protected.
- Strengths: improves collaborative UX; cheaper than a full CRDT implementation; helps users understand context.
- Weaknesses and risks: noisy events load the real-time channel; stale presence undermines trust; update frequency should be carefully limited.

## 5. Frontend performance and scaling

### 42. Web Vitals

- Questions: which metrics are critical: LCP, CLS, INP, TTFB; how real user metrics are collected; which budget targets apply.
- Strengths: provides a measurable performance frame; connects UX and business outcomes; helps prioritize optimizations.
- Weaknesses and risks: lab metrics are not the same as field metrics; optimizing one metric may degrade another; segmentation by device and region is needed.

### 43. Render performance and unnecessary rerenders

- Questions: where the bottlenecks are: reconciler, layout, paint, or JavaScript; how to profile; which components are heavy; whether memoization is needed.
- Strengths: improves responsiveness; especially important for complex dashboards and editors; demonstrates frontend depth.
- Weaknesses and risks: premature memoization complicates the code; without a profiler it is easy to optimize the wrong thing; some problems originate in the data flow.

### 44. Virtualized lists and large tables

- Questions: how many items are displayed; whether variable row height is needed; how keyboard navigation and screen readers work; what happens with search, sorting, and filtering.
- Strengths: renders large lists efficiently; reduces DOM size; improves scrolling performance.
- Weaknesses and risks: complex accessibility; problems with find-in-page and printing; dynamic height can break scroll position.

### 45. Web Workers

- Questions: which computations are expensive; whether parsing, search, compression, or image processing can be moved off the main thread; how data is transferred.
- Strengths: offloads the main thread; improves INP; useful for editors, tables, and large files.
- Weaknesses and risks: serialization overhead; harder debugging; shared state and cancellation should be designed separately.

### 46. Memory leaks

- Questions: where listeners, timers, subscriptions, and caches are created; how object URLs are cleaned up; how heap growth is measured.
- Strengths: important for long-lived tabs; improves stability; distinguishes production thinking from demo thinking.
- Weaknesses and risks: leaks are difficult to reproduce; problems may appear only after hours; caches must be bounded.

### 47. Network loading, preload, and prefetch

- Questions: which resources are critical; what should use preload, preconnect, or prefetch; how mobile networks are considered; when prefetch should be avoided.
- Strengths: improves perceived speed; reduces waterfalls; helps prepare the next route.
- Weaknesses and risks: unnecessary requests can saturate the network; prefetching is expensive on mobile; incorrect priorities degrade LCP.

### 48. Client-side backpressure and rate limiting

- Questions: what happens during a flood of events; how request frequency is limited; whether a queue is needed; how degraded behavior is communicated to users.
- Strengths: protects the backend and client; useful for real-time updates, search, autosave, and analytics; makes UX resilient.
- Weaknesses and risks: important events can be lost; delays should be understandable; drop, merge, and retry rules are needed.

### 49. Large upload/download scenarios

- Questions: whether chunked uploads, resume, progress, and retries are needed; how file type and size are checked; where virus scanning and transcoding happen.
- Strengths: mature UX for media and documents; can scale through direct-to-storage uploads; demonstrates systems thinking.
- Weaknesses and risks: network errors are common; security and limits are needed; large files affect memory and mobile devices.

### 50. Search, autocomplete, and typeahead

- Questions: local or server-side search; debounce or throttle; how results are ranked; how results are cached; what to display when there are no results.
- Strengths: improves core UX; naturally connects frontend, API, and performance; good practice for latency trade-offs.
- Weaknesses and risks: overly frequent requests; stale results; accessibility for keyboard navigation is often forgotten.

### 51. Canvas, SVG, and complex editors

- Questions: Canvas, SVG, or DOM; whether a scene graph is needed; how zoom and pan work; how undo/redo is stored; how collaborative editing is handled.
- Strengths: demonstrates deep frontend skills; suitable for Figma-like tools, draw.io, maps, and editors; offers many interesting trade-offs.
- Weaknesses and risks: accessibility is harder; performance quickly becomes an issue; hit testing, selection, and history should be designed separately.

### 52. Mobile performance and battery usage

- Questions: which devices are targeted; what the CPU, memory, and battery constraints are; how JavaScript, animations, polling, and background work are reduced.
- Strengths: makes the product accessible to a broader audience; supports a performance deep dive; closely tied to business metrics.
- Weaknesses and risks: desktop profiling does not reveal mobile pain points; animations and real-time updates can drain the battery; testing on real devices is needed.

## 6. Product platform, UI architecture, and team scaling

### 53. Design system

- Questions: which components belong in the core; how tokens work; how versioning works; who owns the quality bar.
- Strengths: speeds up development; improves consistency; simplifies accessibility and theming.
- Weaknesses and risks: can become a bottleneck; over-abstracted components are inconvenient; an adoption and migration strategy is needed.

### 54. Component API and composition model

- Questions: which props are public; controlled or uncontrolled; slots/render props/compound components; how backward compatibility is preserved.
- Strengths: good components are reusable and testable; reduces coupling; helps scale the UI.
- Weaknesses and risks: an overly flexible API is complex; breaking changes are painful; components can start absorbing business logic.

### 55. Microfrontends

- Questions: why independent deployments are needed; how domains are split; how dependencies, routing, and authentication are shared; how a consistent UX is maintained.
- Strengths: scales teams; enables independent releases; useful for large organizations.
- Weaknesses and risks: runtime overhead; duplicated dependencies; complex integration bugs and version skew.

### 56. Monorepo and build pipeline

- Questions: how many packages and teams exist; whether affected builds are needed; how CI is cached; how shared packages are versioned.
- Strengths: simplifies shared code; improves refactoring; works well with a design system and platform libraries.
- Weaknesses and risks: CI can become slow; package boundaries become blurred; ownership rules and dependency constraints are needed.

### 57. Feature flags

- Questions: which types of flags are needed: release, experiment, ops, permission; where flags are evaluated; how old flags are cleaned up.
- Strengths: reduces release risk; enables canaries and kill switches; useful for gradual rollouts.
- Weaknesses and risks: flag debt; complex test matrix; an incorrect default can break production.

### 58. A/B testing

- Questions: what the experimental unit is; how buckets are assigned; which metrics and guardrails apply; how SEO and performance regressions are avoided.
- Strengths: connects frontend decisions to product value; supports data-informed decisions; useful for growth products.
- Weaknesses and risks: flicker; sample ratio mismatch; many experiments complicate code and analytics.

### 59. Analytics and product metrics

- Questions: which events are needed; where the event schema lives; how duplicates are prevented; how consent is handled; which events are critical.
- Strengths: helps measure the success of decisions; connects UX and business outcomes; supports experiments.
- Weaknesses and risks: analytics code pollutes the UI; events can be lost during navigation; privacy and consent cannot be ignored.

### 60. Internationalization and localization

- Questions: which languages, regions, and formats are needed; whether RTL is needed; how translations are loaded; how dynamic content is translated.
- Strengths: expands the audience; affects layout, routing, and SEO; demonstrates attention to detail.
- Weaknesses and risks: strings can break layouts; pluralization is harder than it looks; dates, currencies, and sorting depend on locale.

### 61. Accessibility

- Questions: which WCAG targets apply; how keyboard navigation is supported; how screen readers are handled; how contrast, focus, and semantics are tested.
- Strengths: makes the product more accessible; improves UI quality; often required by enterprise and public-sector clients.
- Weaknesses and risks: accessibility cannot be added only at the end; custom components can easily break semantics; automated tests do not cover everything.

### 62. SEO

- Questions: which pages should be indexed; whether SSR/SSG is needed; how metadata, sitemap, canonical URLs, and structured data are generated.
- Strengths: critical for content and marketplace products; connected to performance and rendering; provides clear technical requirements.
- Weaknesses and risks: an SPA without SSR may underperform; duplicate pages harm indexing; personalized content can conflict with crawlers.

### 63. Responsive and adaptive design

- Questions: which breakpoints are needed; mobile-first or desktop-first; whether UX differs across devices; how touch, hover, and viewport are handled.
- Strengths: improves device coverage; affects layout architecture; important for the real user experience.
- Weaknesses and risks: simply "shrinking desktop" is not enough; tables and complex editors adapt poorly; orientation and safe areas should be considered.

### 64. Theming, white-label, and multi-brand

- Questions: whether themes, brands, or customer customization are needed; which tokens change; whether layout can change; how contrast is validated.
- Strengths: useful for B2B products and platforms; works well with design tokens; reduces customization cost.
- Weaknesses and risks: unlimited customization makes maintenance difficult; themes can break accessibility; visual states become harder to test.

### 65. RBAC and permissions in the UI

- Questions: which roles and permissions exist; where the source of truth lives; how actions are hidden; what happens when permissions change during a session.
- Strengths: important enterprise topic; connects authentication, routing, and API design; reduces the risk of unauthorized actions.
- Weaknesses and risks: frontend checks do not replace backend authorization; complex roles break UX; cached permissions can become stale.

## 7. Security, reliability, and delivery

### 66. Authentication and session management

- Questions: cookie or token; where the session is stored; how refresh works; whether multi-tab logout, device management, and MFA are needed.
- Strengths: fundamental production topic; affects API design, routing, and security; demonstrates maturity.
- Weaknesses and risks: storing tokens in localStorage increases the XSS risk; refresh flows are easy to break; authentication state should be synchronized across tabs.

### 67. XSS

- Questions: where user-generated content exists; how HTML is sanitized; whether `dangerouslySetInnerHTML` is used; how Markdown and rich text are handled.
- Strengths: demonstrates frontend security awareness; important for comments, editors, and profiles; helps establish safe defaults.
- Weaknesses and risks: escaping is easy to implement incompletely; third-party widgets increase the attack surface; sanitizers should be kept up to date.

### 68. CSRF, CORS, and the browser security model

- Questions: whether cookies are used; which SameSite settings apply; which origins are allowed; whether CSRF tokens are needed.
- Strengths: connects frontend and backend security; supports correct authentication design; reduces a common class of attacks.
- Weaknesses and risks: CORS is not an authorization mechanism; an incorrect wildcard is dangerous; cookie-based authentication requires CSRF protection.

### 69. CSP and security headers

- Questions: which CSP is needed; whether `unsafe-inline` can be avoided; which third-party scripts are allowed; how violation reports are collected.
- Strengths: reduces the impact of XSS; useful for enterprise security; helps control external scripts.
- Weaknesses and risks: a strict CSP breaks legacy code; nonces and hashes complicate SSR; report-only mode is needed before enforcement.

### 70. Privacy, PII, and consent

- Questions: which personal data exists on the client; what is sent to analytics; whether consent is needed; how data is deleted or exported.
- Strengths: important for real products; informs analytics and storage design; reduces legal risks.
- Weaknesses and risks: PII must not be logged accidentally; session replay may capture sensitive fields; local storage is also a risk.

### 71. Observability: errors, logs, and metrics

- Questions: which errors are logged; how a frontend error is correlated with a backend request; which release/version/user/session dimensions are needed.
- Strengths: makes the system maintainable; speeds up incident response; supports data-informed decisions.
- Weaknesses and risks: too much noise; PII in logs; errors are difficult to fix without source maps and release tags.

### 72. Testing strategy

- Questions: what to cover with unit, integration, contract, and E2E tests; which flows are critical; how data fetching and errors are tested.
- Strengths: reduces regressions; helps maintain complex UIs; demonstrates engineering maturity.
- Weaknesses and risks: E2E tests can be slow and flaky; unit tests do not catch integration issues; behavior should be tested rather than implementation.

### 73. E2E and visual regression

- Questions: which scenarios are critical; where screenshots are needed; how flaky tests are handled; how responsive states and themes are tested.
- Strengths: catches real user-facing regressions; useful for design systems and visually complex products.
- Weaknesses and risks: expensive to maintain; false positives frustrate the team; data and environments should be stabilized.

### 74. CI/CD, canary, and rollback

- Questions: how often releases happen; whether canaries are used; how quickly a rollback can happen; how deployments, migrations, flags, and monitoring interact.
- Strengths: reduces delivery risk; demonstrates a production mindset; works well with feature flags.
- Weaknesses and risks: frontend rollback is difficult with cached HTML/JavaScript; canaries require metrics; migrations may not be backward compatible.

### 75. Dependencies and supply chain security

- Questions: how dependencies are checked; whether a lockfile policy exists; how major versions are updated; how vulnerabilities are handled.
- Strengths: reduces operational risk; important for large frontend applications; helps keep builds reproducible.
- Weaknesses and risks: transitive dependencies are opaque; automated updates can break production; abandoned packages become technical debt.
