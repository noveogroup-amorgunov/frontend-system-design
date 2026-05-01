# Project Bank

Use this file to select a system when the user does not provide one.

Each project contains:
- Product prompt
- Core requirements
- Frontend-specific discussion topics
- Common candidate misses
- Strong-signal follow-up questions

---

## 1. Twitter-like Feed

### Prompt

Design the frontend architecture for a Twitter-like social feed.

Backend is a black box that exposes APIs. Focus on the frontend application, data layer, rendering, realtime behavior, state management, and user experience.

### Core requirements

- User can view home feed
- User can create a post
- User can like/unlike a post
- User can comment on a post
- User can upload images
- User can open post details
- User can view user profiles
- User can follow/unfollow users
- User can receive feed updates
- User can log in and stay authenticated

### Frontend topics

- Infinite scroll
- Cursor pagination
- Feed cache
- Optimistic likes
- Optimistic post creation
- Image upload flow
- Post composer state
- Comment thread loading
- Realtime updates via SSE or WebSocket
- Notification badges
- Normalized entities
- URL-driven modal or detail route
- Virtualized lists
- Skeleton UI
- Error boundaries
- Session refresh
- Multi-tab synchronization

### Common misses

- Treating likes as purely backend-driven with no optimistic UI
- Ignoring duplicate realtime events
- Forgetting image upload lifecycle
- Not separating server state from client UI state
- Not discussing cache invalidation after mutations
- Not handling deleted or moderated posts
- Forgetting accessibility for composer and timeline updates

### Follow-up questions

- How would you avoid the feed jumping when new posts arrive?
- What happens if optimistic like succeeds locally but fails on the server?
- How do comments update without refetching the whole post?
- Would you use SSE or WebSocket for likes and new posts?
- How do you model uploaded media before the post is published?

---

## 2. News Feed / Media Homepage

### Prompt

Design the frontend architecture for a personalized news feed or media homepage.

### Core requirements

- User can view personalized feed
- User can open article pages
- User can save/bookmark articles
- User can filter by topic
- User can see breaking news
- User can search articles
- User can view logged-out homepage
- Editors can pin top stories, if admin surface is in scope

### Frontend topics

- SSR/SSG/ISR
- SEO
- Core Web Vitals
- Image optimization
- Personalization vs cacheability
- Ad slots and layout stability
- Breaking-news updates
- Content preview cards
- Accessibility for articles
- Analytics events
- Experimentation
- CDN caching
- BFF for page composition
- Partial hydration / islands

### Common misses

- Not discussing SEO
- Forgetting ad layout shift
- Over-personalizing and losing cacheability
- Ignoring editorial overrides
- Not separating anonymous and logged-in experiences

### Follow-up questions

- Which parts of the page should be cacheable?
- How do you keep the page fast with ads and images?
- How would breaking news appear without destroying reading experience?
- What rendering strategy would you choose for article pages?

---

## 3. Chat / Messenger

### Prompt

Design the frontend architecture for a real-time chat application.

### Core requirements

- User can see conversation list
- User can open a conversation
- User can send messages
- User can receive messages in realtime
- User can see message delivery/read states
- User can upload attachments
- User can search messages
- User can receive notifications

### Frontend topics

- WebSocket lifecycle
- Message ordering
- Optimistic sending
- Temporary client IDs
- Retry and deduplication
- Offline queue
- Reconnect strategy
- Presence
- Typing indicators
- Virtualized message list
- Scroll anchoring
- Media attachments
- End-to-end encryption, if in scope
- IndexedDB cache
- Push notifications
- Multi-device sync

### Common misses

- Not handling reconnects
- Not deduplicating optimistic and server-confirmed messages
- Forgetting scroll behavior
- Ignoring offline send queue
- Overusing global state for every message
- Not modeling message statuses

### Follow-up questions

- How do you merge a locally-created message with the server-confirmed one?
- How do you preserve scroll position when older messages load?
- What happens if messages arrive out of order?
- What data should be stored locally?

---

## 4. Collaborative Document Editor

### Prompt

Design the frontend architecture for a collaborative document editor like Google Docs or Notion.

### Core requirements

- User can edit a document
- Multiple users can collaborate in realtime
- User can see cursors or presence
- User can comment
- User can access version history
- User can work with flaky network
- User can share document with permissions

### Frontend topics

- CRDT vs OT
- Local-first editing
- Conflict resolution
- Presence channel
- Document model
- Editor state vs persisted state
- Undo/redo
- Autosave
- Offline persistence
- Permission-aware UI
- Large document performance
- Lazy loading blocks
- Comment anchors
- Version snapshots
- WebSocket sync
- IndexedDB

### Common misses

- Treating document state like a normal REST resource
- Not separating presence from persisted document data
- Forgetting undo/redo semantics
- Ignoring offline edits
- Not discussing permission changes during editing

### Follow-up questions

- What is the source of truth while the user is offline?
- How do you handle two users editing the same paragraph?
- How do comments stay anchored when the document changes?
- What should be synced over WebSocket?

---

## 5. Kanban Board / Project Management Tool

### Prompt

Design the frontend architecture for a Trello-like kanban board.

### Core requirements

- User can view boards
- User can create columns
- User can create cards
- User can drag cards between columns
- User can assign users
- User can comment on cards
- User can attach files
- Multiple users can collaborate
- User can filter/search cards

### Frontend topics

- Drag-and-drop state
- Optimistic reorder
- Positioning algorithms
- Realtime board updates
- Conflict handling
- Normalized board data
- Permissions
- Activity feed
- Card detail modal
- File upload
- Offline mutations
- Virtualized columns/cards
- URL state for filters
- Undo

### Common misses

- Not modeling card order carefully
- Refetching the whole board after each drag
- Ignoring concurrent reorder conflicts
- Forgetting keyboard accessibility for drag-and-drop
- Not handling partial failure after optimistic move

### Follow-up questions

- How would you represent card order?
- What happens if two users move the same card?
- How do you make drag-and-drop accessible?
- Which data should update in realtime?

---

## 6. Video Streaming Platform

### Prompt

Design the frontend architecture for a YouTube-like video watch page.

### Core requirements

- User can watch a video
- User can see recommendations
- User can like/dislike
- User can comment
- User can subscribe
- User can search videos
- User can continue watching
- User can change quality and captions

### Frontend topics

- Media player architecture
- Adaptive bitrate streaming
- Lazy loading recommendations
- Comment pagination
- Watch progress persistence
- Analytics beacons
- SSR for metadata/SEO
- Hydration strategy
- Ads
- Captions and accessibility
- Error states for playback
- Preloading
- Service worker caching, if relevant
- Device constraints

### Common misses

- Ignoring player lifecycle
- Treating video as a normal file download
- Forgetting watch progress sync
- Not discussing SEO for public video pages
- Not considering caption accessibility

### Follow-up questions

- What owns video player state?
- How do you persist watch progress without sending too many events?
- What should render server-side?
- How do you handle playback errors?

---

## 7. E-commerce Product Page and Cart

### Prompt

Design the frontend architecture for an e-commerce product page and shopping cart.

### Core requirements

- User can browse product details
- User can choose product variants
- User can add to cart
- User can update cart quantity
- User can apply promo code
- User can check out
- User can view recommendations
- User can see inventory state

### Frontend topics

- SSR/SEO
- Product data cache
- Variant selection state
- Cart state
- Guest cart vs logged-in cart
- Optimistic cart updates
- Inventory freshness
- Payment flow boundaries
- Error handling
- Analytics
- A/B testing
- Image optimization
- Accessibility
- Performance budgets
- Security around checkout

### Common misses

- Not distinguishing guest and authenticated cart
- Assuming inventory never changes
- Forgetting SEO
- Not handling payment redirects or failures
- Putting sensitive payment logic in frontend

### Follow-up questions

- Where should cart state live?
- How do you reconcile guest cart after login?
- How fresh does inventory need to be?
- What must not be handled directly in the frontend?

---

## 8. Booking / Calendar Scheduling App

### Prompt

Design the frontend architecture for a booking system like Calendly.

### Core requirements

- User can view available slots
- User can select date and time
- User can book a meeting
- User can reschedule or cancel
- Host can configure availability
- User receives confirmation
- Time zones are supported

### Frontend topics

- Time zone handling
- Calendar UI state
- Slot freshness
- Optimistic vs pessimistic booking
- Race conditions
- Form validation
- URL-based booking pages
- SSR for public pages
- Calendar integration boundaries
- Error handling
- Accessibility for date/time picker
- Internationalization
- Confirmation flow

### Common misses

- Mishandling time zones
- Optimistically confirming unavailable slots
- Not discussing race conditions
- Forgetting accessibility of calendar controls
- Ignoring reschedule/cancel flows

### Follow-up questions

- How do you prevent two users booking the same slot?
- What time zone is shown to the guest?
- Should booking be optimistic?
- What should happen if availability changes while the page is open?

---

## 9. Dashboard / Analytics Product

### Prompt

Design the frontend architecture for an analytics dashboard.

### Core requirements

- User can view metrics
- User can filter by date range
- User can compare segments
- User can drill into charts
- User can export data
- User can save dashboard views
- User can share reports

### Frontend topics

- Query state in URL
- Server state caching
- Expensive query loading states
- Chart rendering
- Large data sets
- Aggregation boundaries
- Polling vs manual refresh
- Permissions
- Export flow
- Empty states
- Error handling
- Data freshness
- Observability
- Design system

### Common misses

- Keeping filters only in local component state
- Not discussing loading and partial data states
- Rendering too much data in the browser
- Ignoring permissions for shared dashboards
- Not defining data freshness expectations

### Follow-up questions

- Which state belongs in the URL?
- How do you handle slow queries?
- Where should aggregation happen?
- How do you avoid re-rendering expensive charts?

---

## 10. AI Coding Agent Web App

### Prompt

Design the frontend architecture for a web-based AI coding agent similar to OpenCode, but as a browser application.

### Core requirements

- User can open a project/workspace
- User can chat with an agent
- User can approve or reject file changes
- User can inspect diffs
- User can run commands or tasks, if allowed
- User can see streaming agent output
- User can manage sessions
- User can recover from errors

### Frontend topics

- Streaming responses
- Agent session state
- Diff viewer
- File tree
- Editor integration
- Permission gates
- Tool execution UI
- Long-running task state
- Cancellation
- Optimistic UI vs confirmed changes
- WebSocket/SSE
- Security boundaries
- Audit log
- Error recovery
- Large text performance
- State machines

### Common misses

- Not modeling agent run lifecycle
- Forgetting cancellation and retry
- Treating streamed output like a normal response
- Not separating proposed changes from applied changes
- Ignoring dangerous tool permissions

### Follow-up questions

- How do you model an agent run?
- What is the UI state before, during, and after tool execution?
- How do users review and approve file edits?
- How do you prevent accidental destructive actions?

---

## 11. Local-first Multiplayer Game

### Prompt

Design the frontend architecture for a local-first multiplayer card game using WebRTC and conflict resolution.

### Core requirements

- User can create or join a game
- Players can make moves
- Game works with peer-to-peer sync
- State is persisted locally
- Conflicts are resolved
- Moves may be signed or verified
- User can reconnect

### Frontend topics

- Local-first architecture
- CRDT or deterministic event log
- WebRTC signaling boundary
- Peer discovery
- Game state machine
- Move validation
- Conflict resolution
- Local persistence
- Reconnect handling
- Anti-cheat limitations
- Blockchain/signature boundary, if relevant
- UI synchronization
- Latency compensation

### Common misses

- Not defining source of truth
- Ignoring invalid moves
- Treating P2P as always connected
- Not modeling reconnection
- Overpromising cheat prevention on the client

### Follow-up questions

- What is the canonical game state?
- How do peers agree on move order?
- What happens when a player disconnects?
- What can and cannot be trusted on the client?

---

## 12. Design System / Component Platform

### Prompt

Design the frontend architecture for an internal design system and component documentation platform.

### Core requirements

- Developers can browse components
- Developers can view examples
- Designers can reference usage guidelines
- Components are versioned
- Teams can install packages
- Users can search documentation
- Accessibility rules are documented and tested

### Frontend topics

- Package architecture
- Component API design
- Documentation site
- MDX or content pipeline
- Theming
- Versioning
- Visual regression testing
- Accessibility testing
- Bundle size
- Tree-shaking
- Token system
- Release process
- Migration guides
- Monorepo boundaries

### Common misses

- Treating design system as only UI components
- Ignoring versioning and migration
- Not discussing accessibility automation
- Forgetting package consumption constraints
- Not defining ownership and contribution model

### Follow-up questions

- How do teams consume the design system?
- How do you prevent breaking changes?
- How do you test components visually and accessibly?
- How are design tokens distributed?
