# CampusOS --- System Architecture Document

**Version:** 1.0\
**Status:** Authoritative architecture\
**Architecture style:** Modular monolith / layered application for MVP\
**Future direction:** Multi-tenant SaaS

------------------------------------------------------------------------

# 1. Architecture Decision

CampusOS will NOT use microservices for the hackathon MVP.

Reason:

-   four-hour implementation window
-   four-person team
-   one primary Flutter developer
-   microservices add deployment and integration overhead
-   modular boundaries can provide scalability without
    distributed-system complexity

The MVP should be a **modular monolith with explicit boundaries**.

------------------------------------------------------------------------

# 2. High-Level Architecture

``` text
                    ┌───────────────────────┐
                    │       USERS           │
                    │ Student / Staff/Admin │
                    └───────────┬───────────┘
                                │
                                ▼
                    ┌───────────────────────┐
                    │     Flutter PWA       │
                    │   Android + Web       │
                    └───────────┬───────────┘
                                │
                                ▼
                    ┌───────────────────────┐
                    │ Presentation / UI     │
                    └───────────┬───────────┘
                                │
                                ▼
                    ┌───────────────────────┐
                    │ Application Layer     │
                    │ Use Cases / Services  │
                    └───────┬─────────┬─────┘
                            │         │
                ┌───────────┘         └────────────┐
                ▼                                  ▼
       ┌────────────────┐                ┌─────────────────┐
       │ Domain Modules │                │ Intelligence    │
       │                │                │ Engine          │
       │ Issues         │                │                 │
       │ Lost & Found   │                │ Matching        │
       │ Queue          │                │ Classification  │
       │ Notices        │                │ Priority        │
       └───────┬────────┘                │ Clustering      │
               │                         └────────┬────────┘
               └────────────────┬────────────────┘
                                ▼
                    ┌───────────────────────┐
                    │ Repository Interfaces│
                    └───────────┬───────────┘
                                ▼
                    ┌───────────────────────┐
                    │ Supabase              │
                    │ PostgreSQL            │
                    │ Auth / Storage        │
                    │ Realtime              │
                    └───────────────────────┘
```

------------------------------------------------------------------------

# 3. Flutter Application Architecture

Recommended conceptual structure:

``` text
lib/
├── core/
│   ├── config/
│   ├── routing/
│   ├── theme/
│   ├── errors/
│   ├── widgets/
│   └── utilities/
│
├── features/
│   ├── auth/
│   ├── dashboard/
│   ├── lost_found/
│   ├── campus_fix/
│   ├── queue/
│   ├── notices/
│   ├── activity/
│   └── admin/
│
├── domain/
│   ├── entities/
│   ├── repositories/
│   └── usecases/
│
├── data/
│   ├── models/
│   ├── repositories/
│   └── datasources/
│
└── main.dart
```

The exact folder structure can be adapted if Jitin's existing Flutter
architecture is demonstrably cleaner, but the dependency direction must
remain intact.

------------------------------------------------------------------------

# 4. Dependency Direction

Required:

``` text
Presentation
     ↓
Application
     ↓
Domain
     ↓
Repository Interfaces
     ↓
Data Implementations
     ↓
External Services
```

Do not allow:

``` text
Widget → Supabase client
Widget → intelligence algorithm
Widget → raw SQL
```

------------------------------------------------------------------------

# 5. Core Domain Modules

## 5.1 Authentication

Responsibilities:

-   login
-   session
-   role
-   authorization context

## 5.2 Campus

Responsibilities:

-   campus
-   department
-   location

## 5.3 CampusFix

Responsibilities:

-   issue creation
-   status
-   assignment
-   resolution
-   verification

## 5.4 Lost & Found

Responsibilities:

-   lost items
-   found items
-   matches
-   claims
-   recovery

## 5.5 Queue

Responsibilities:

-   queue
-   token
-   position
-   service state

## 5.6 Notices

Responsibilities:

-   creation
-   publication
-   deadline
-   visibility

------------------------------------------------------------------------

# 6. Campus Action Engine

This is the central conceptual engine.

``` text
Event
  ↓
Classify
  ↓
Prioritize
  ↓
Route
  ↓
Assign
  ↓
Track
  ↓
Resolve
  ↓
Verify
  ↓
Analyze
```

Different modules should reuse the same workflow concepts.

Example:

``` text
CampusFix:
Issue → Classify → Prioritize → Assign → Resolve → Verify

Lost & Found:
Item → Match → Claim → Verify → Recover

Queue:
Request → Token → Track → Serve → Complete
```

------------------------------------------------------------------------

# 7. Intelligence Engine

The intelligence engine should be isolated behind interfaces.

``` text
IntelligenceService
├── MatchingService
├── ClassificationService
├── PriorityService
├── ClusteringService
└── AnalyticsService
```

Each service has one clear responsibility.

This is directly aligned with Single Responsibility and Dependency
Inversion.

------------------------------------------------------------------------

# 8. Data Model

Conceptual relationships:

``` text
Campus
  ├── Departments
  ├── Locations
  ├── Users
  ├── Issues
  ├── LostItems
  ├── FoundItems
  ├── Queues
  └── Notices
```

User:

``` text
User
 ├── campus_id
 ├── role
 └── profile
```

Issue:

``` text
Issue
 ├── campus_id
 ├── reporter_id
 ├── location_id
 ├── department_id
 ├── assigned_to
 └── status
```

Lost/Found:

``` text
LostItem
 └── campus_id

FoundItem
 └── campus_id

Match
 ├── lost_item_id
 └── found_item_id
```

------------------------------------------------------------------------

# 9. Multi-Tenant Design

Even though MVP has one campus, all major data entities should carry:

``` text
campus_id
```

This prevents a future redesign when multiple institutions are
introduced.

Future:

``` text
Tenant
 ├── Campus
 │   ├── Users
 │   ├── Departments
 │   ├── Locations
 │   └── Data
```

------------------------------------------------------------------------

# 10. Admin Architecture

Admin application can be another route tree inside the same Flutter
Web/PWA application.

``` text
/
├── /login
├── /student
│   ├── /home
│   ├── /lost-found
│   ├── /issues
│   ├── /queue
│   └── /activity
│
└── /admin
    ├── /dashboard
    ├── /issues
    ├── /lost-found
    ├── /queues
    ├── /notices
    └── /analytics
```

Role guards must protect `/admin`.

------------------------------------------------------------------------

# 11. Realtime Architecture

Realtime is useful for:

-   queue position
-   issue status
-   notifications
-   admin updates

Do not make every screen permanently realtime.

Use realtime only where state changes need immediate visibility.

------------------------------------------------------------------------

# 12. File Storage

Storage is required for:

-   issue before photos
-   issue after photos
-   lost item images
-   found item images

Store URLs/references in the database, not binary files directly in
relational rows.

------------------------------------------------------------------------

# 13. Notification Architecture

Conceptual:

``` text
Event
 ↓
Notification Service
 ↓
User Notification
```

Examples:

``` text
Match found
Issue assigned
Issue resolved
Queue approaching
New critical notice
```

Push notification implementation may be simplified for MVP.

------------------------------------------------------------------------

# 14. Analytics Architecture

Analytics should derive from operational records rather than maintaining
duplicate manually edited numbers.

Examples:

``` text
Recovery Rate =
Recovered Items / Total Lost Items

Resolution Rate =
Resolved Issues / Total Issues

Average Resolution Time =
Average(resolved_at - created_at)
```

------------------------------------------------------------------------

# 15. QR Architecture

Optional MVP extension:

``` text
QR
 ↓
Deep Link
 ↓
CampusOS Route
 ↓
Pre-filled Context
```

Example:

``` text
QR classroom-204
      ↓
/report-issue?location=classroom-204
```

This reduces user input.

------------------------------------------------------------------------

# 16. Scalability Strategy

MVP:

**Modular monolith**

Future:

``` text
Flutter Client
       ↓
API Gateway
       ↓
Domain Services
       ↓
Database / Event Layer
```

Only extract services when scale actually requires it.

Potential future modules:

-   notification service
-   intelligence service
-   analytics service
-   campus configuration service

Do not prematurely create these as separate deployed services.

------------------------------------------------------------------------

# 17. SOLID Architecture Rules

### S --- Single Responsibility

One class/service/widget should have one reason to change.

### O --- Open/Closed

New campus workflows should be added through new modules/use cases
rather than rewriting core infrastructure.

### L --- Liskov Substitution

Implementations must be safely substitutable for their abstractions.

### I --- Interface Segregation

Use focused repository/service interfaces.

### D --- Dependency Inversion

High-level business rules depend on abstractions, not Supabase-specific
implementations.

------------------------------------------------------------------------

# 18. Failure Strategy

If intelligence fails:

The core workflow must still function.

Example:

``` text
Matching unavailable
       ↓
Show:
"Automatic matching unavailable.
You can browse potential matches manually."
```

CampusOS must degrade gracefully.

------------------------------------------------------------------------

# 19. Architecture Definition of Done

Architecture is accepted when:

-   Flutter and backend are separated by service/repository boundaries
-   intelligence is isolated
-   role-based access exists
-   campus_id exists in tenant-bound records
-   UI does not directly contain business logic
-   secrets are not in source control
-   core workflows can operate without intelligence failures
