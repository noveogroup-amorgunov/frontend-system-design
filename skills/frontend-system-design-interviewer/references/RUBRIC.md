# Evaluation Rubric

Use this rubric at the end of the mock interview.

Score each applicable category from 1 to 5. Compute the overall readiness score by averaging the category scores, multiplying the average by two, and rounding to the nearest whole number.

In **Frontend-only mode**, score API design based on whether the candidate identifies the client-facing capabilities and contracts the frontend depends on. Do not require endpoint-level detail.

Do not penalize requirements or design areas that were explicitly declared out of scope.

## Contents

- [1. Requirements clarification](#1-requirements-clarification)
- [2. Frontend-specific non-functional requirements](#2-frontend-specific-non-functional-requirements)
- [3. Numbers and constraints](#3-numbers-and-constraints)
- [4. Architecture](#4-architecture)
- [5. Data model](#5-data-model)
- [6. API design](#6-api-design)
- [7. Frontend deep dive](#7-frontend-deep-dive)
- [8. Failure modes](#8-failure-modes)
- [9. Communication](#9-communication)
- [Final feedback format](#final-feedback-format)

## 1. Requirements clarification

Strong candidate:

- Clarifies scope before designing
- Separates must-have from nice-to-have
- Converges on 3-5 critical functional requirements
- Explicitly marks secondary features as out of scope
- Asks about user types
- Asks about platform constraints
- Handles ambiguous product behavior

Weak candidate:

- Starts drawing components immediately
- Assumes requirements
- Accepts or lists every possible feature without prioritization
- Ignores logged-out, error, or edge flows

## 2. Frontend-specific non-functional requirements

Strong candidate:

- Discusses perceived performance
- Mentions accessibility
- Considers rendering strategy
- Discusses network constraints
- Thinks about caching and freshness
- Understands SEO when relevant
- Mentions observability and error tracking

Weak candidate:

- Only says “scalable” or “low latency”
- Uses backend-style NFRs without frontend interpretation
- Ignores user experience under failure

## 3. Numbers and constraints

Strong candidate:

- Estimates useful numbers
- Connects numbers to decisions
- Uses numbers to justify pagination, virtualization, caching, or rendering strategy

Weak candidate:

- Avoids numbers entirely
- Gives numbers but does not use them
- Over-indexes on fake precision

## 4. Architecture

Strong candidate:

- Separates app shell, routing, features, entities, shared UI, data layer, and services
- Defines API client boundaries
- Separates server state, client state, form state, and URL state
- Considers dependency injection or service boundaries
- Explains module ownership

Weak candidate:

- Creates a vague component tree only
- Puts all state in one global store
- Couples UI directly to API details
- Ignores growth of the codebase and team

## 5. Data model

Strong candidate:

- Identifies core entities and relationships
- Discusses normalization vs denormalization
- Models optimistic state
- Handles pagination and local-only fields
- Discusses cache invalidation

Weak candidate:

- Only describes backend tables
- Does not model loading/error states
- Ignores client-generated IDs
- Ignores stale or conflicting data

## 6. API design

Evaluate this section in detail only for **Frontend + API mode**.

For **Frontend-only mode**, evaluate whether the candidate understands what kind of backend/API capabilities the frontend depends on, without requiring full endpoint design.

Strong candidate:

- Defines query and mutation operations
- Handles pagination, filtering, sorting
- Discusses error format
- Mentions idempotency for risky mutations
- Considers upload flows
- Considers realtime contracts
- Discusses session refresh
- Connects API shape to frontend state, caching, rendering, and UX
- Distinguishes API DTOs from frontend domain models
- Designs responses around actual screen needs without overfitting every API to one page

Weak candidate:

- Only names generic CRUD endpoints
- Does not think about frontend consumption
- Ignores partial failures
- Ignores duplicate submissions
- Cannot explain how API choices affect cache invalidation or optimistic UI
- Pushes all complexity to “the backend” without defining the client contract

## 7. Frontend deep dive

Strong candidate:

- Can go deep on at least two critical areas
- Discusses trade-offs
- Explains why a rendering/state/realtime strategy fits the product
- Handles edge cases

Weak candidate:

- Stays at buzzword level
- Cannot explain trade-offs
- Does not connect solution to requirements

## 8. Failure modes

Strong candidate:

- Handles slow network, offline, retries, stale data, expired auth, duplicate events, and partial failures
- Designs graceful degradation
- Thinks about user trust and recovery

Weak candidate:

- Assumes happy path
- Treats failures as alerts only
- Does not explain recovery

## 9. Communication

Strong candidate:

- Structures the answer
- Summarizes decisions
- Makes trade-offs explicit
- Asks good clarifying questions
- Does not over-engineer too early

Weak candidate:

- Jumps between topics
- Gives disconnected details
- Cannot prioritize
- Needs constant interviewer steering

## Final feedback format

Use this structure:

```md
## Feedback

### Interview mode

Frontend-only / Frontend + API

### Strengths

- ...

### Gaps

- ...

### Missed trade-offs

- ...

### Frontend-specific depth

- ...

### Suggested improvements

- ...

### Scorecard

- Requirements clarification: X/5
- Frontend-specific NFRs: X/5
- Numbers and constraints: X/5
- Architecture: X/5
- Data model: X/5
- API design: X/5
- Frontend deep dive: X/5
- Failure modes: X/5
- Communication: X/5

### Readiness score

X/10

### Next practice recommendation

For the next round, practice: ...

### Scoring guide

9–10: Senior/staff-level frontend system design performance
7–8: Strong middle+/senior candidate with minor gaps
5–6: Understands basics but lacks depth or structure
3–4: Fragmented answer, many missed frontend concerns
1–2: Not interview-ready yet
```
