# ADR-001 — Mrngflow Technology Stack

**Status:** Accepted
**Date:** 2026-09-24

## Context

Mrngflow is a cross-platform personal productivity ecosystem consisting of web, desktop, and mobile applications.

The system must support:

* Tasks and to-do lists
* Habit tracking
* Calendar events
* Journaling
* Notes
* Whiteboards
* Projects
* Cross-device synchronization
* Notifications
* Offline capabilities in later phases
* Shared user data across all clients

The architecture therefore needs strong type safety, maintainable boundaries, shared packages, and a backend capable of supporting multiple clients.

## Decision

Mrngflow will use the following technology stack.

### Repository

* Monorepo: Turborepo
* Package manager: pnpm
* Language: TypeScript

### Applications

* Web: Next.js
* Desktop: Tauri
* Mobile: React Native with Expo

### Backend

* Framework: NestJS
* API style: REST
* Validation: Zod
* Authentication: server-managed sessions

### Data

* Database: PostgreSQL
* ORM: Prisma
* Cache/infrastructure: Redis

### Testing

* Unit/integration: Vitest
* End-to-end: Playwright

### Development tooling

* ESLint
* Prettier
* Docker Compose
* GitHub Actions

## Architecture

The high-level architecture is:

Client applications communicate with the NestJS API through explicit REST contracts.

```text
Web
 │
Desktop ────────→ NestJS API ─────→ PostgreSQL
 │                    │
Mobile                 └───────────→ Redis
```

Shared domain types, validation schemas, UI components, and utilities are maintained as workspace packages.

## Principles

1. Business logic must not live inside UI components.
2. Controllers remain thin and delegate to application services.
3. Database access remains behind defined backend boundaries.
4. Shared types are maintained in dedicated packages.
5. Runtime validation is required at external input boundaries.
6. Infrastructure dependencies must be reproducible locally.
7. Architecture should support offline synchronization without requiring offline-first implementation in the initial MVP.
8. New technologies should only be introduced when a concrete product or engineering requirement justifies them.

## Consequences

### Positive

* Shared TypeScript ecosystem
* Strong type safety
* Clear application boundaries
* Lightweight desktop distribution
* Reusable packages
* Good foundation for cross-device synchronization
* Reproducible local development

### Negative

* Monorepo introduces additional tooling complexity
* Three client platforms increase testing requirements
* Tauri requires learning Rust/native integration where necessary
* React Native introduces platform-specific considerations
* Synchronization will require additional architecture in later phases

## Rejected Alternatives

### GraphQL

Not required for the initial product scope. REST provides simpler contracts and lower initial complexity.

### Electron

Rejected for the initial desktop direction because Mrngflow does not require a Chromium-based runtime and a lighter desktop application is desirable.

### Microservices

Rejected at the current stage. Mrngflow will begin with a modular monolithic backend. Service extraction will only be considered when scale or ownership boundaries justify it.

### MongoDB

Rejected as the primary database because Mrngflow contains strongly relational concepts such as users, workspaces, tasks, habits, schedules, calendar events, projects, and references between entities.

## Review Conditions

This decision should be revisited if:

* API requirements materially change
* Offline synchronization becomes a primary architectural concern
* Desktop requirements exceed Tauri's capabilities
* Mobile requirements require native functionality that Expo cannot reasonably provide
* Product scale requires service decomposition
