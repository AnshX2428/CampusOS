# CampusOS --- Software Requirements Document (SRD)

**Version:** 1.0\
**Phase:** Phase 0 --- Engineering Requirements\
**Status:** Authoritative engineering specification

------------------------------------------------------------------------

# 1. Engineering Objective

Build CampusOS as a single Flutter codebase targeting:

1.  Android
2.  Flutter Web
3.  Installable Progressive Web App

The system must use a backend/database capable of authentication,
persistent data, file storage and realtime updates.

The initial implementation should favor **Supabase** because it provides
PostgreSQL, authentication, storage and realtime capabilities without
requiring the team to build a custom server during a four-hour
hackathon.

The backend choice can be substituted only if the team already has a
faster, proven alternative.

------------------------------------------------------------------------

# 2. Required Technology

## Frontend

-   Flutter
-   Dart
-   Flutter Web
-   Android target

## Backend

Preferred:

-   Supabase
-   PostgreSQL
-   Supabase Auth
-   Supabase Storage
-   Supabase Realtime

## Source Control

-   GitHub
-   Pull Requests
-   protected `main`

## Deployment

Any stable Flutter-compatible hosting platform.

Flutter release web builds use:

``` bash
flutter build web --release
```

Flutter's official documentation confirms Flutter can target Android and
web from the same codebase and documents web release/deployment
workflows. [Flutter
Web](https://docs.flutter.dev/platform-integration/web) [Flutter
deployment](https://docs.flutter.dev/deployment/web)

------------------------------------------------------------------------

# 3. Functional Requirements

## FR-001 Authentication

The system shall support authenticated users.

Minimum roles:

-   student
-   faculty
-   staff
-   admin

Role-based access must prevent students from accessing admin functions.

------------------------------------------------------------------------

## FR-002 Campus Context

Every operational record should be associated with a campus.

Required conceptual field:

``` text
campus_id
```

This enables future multi-campus SaaS.

------------------------------------------------------------------------

## FR-003 Lost & Found

System shall allow creation of:

``` text
LostItem
FoundItem
Match
Claim
Recovery
```

### LostItem

Required:

-   id
-   campus_id
-   user_id
-   category
-   item_name
-   brand
-   color
-   location
-   occurred_at
-   description
-   image_url
-   status
-   created_at

### FoundItem

Equivalent fields.

### Match

Required:

-   lost_item_id
-   found_item_id
-   score
-   matched_attributes
-   created_at

------------------------------------------------------------------------

# 4. Lost & Found Verification

The claimant must provide at least one ownership-verification answer.

The system must not expose sensitive hidden item details publicly.

Claim workflow:

``` text
Potential Match
      ↓
Claim Submitted
      ↓
Ownership Verification
      ↓
Approved / Rejected
      ↓
Recovered
```

------------------------------------------------------------------------

# 5. CampusFix

Issue fields:

-   id
-   campus_id
-   reporter_id
-   category
-   type
-   description
-   location_id
-   severity
-   priority
-   department_id
-   assigned_to
-   status
-   before_image_url
-   after_image_url
-   created_at
-   resolved_at
-   verified_at

Status enum:

``` text
reported
verified
assigned
in_progress
resolved
student_verified
closed
```

------------------------------------------------------------------------

# 6. Queue System

Entities:

``` text
Queue
QueueToken
```

Queue must support:

-   service name
-   location
-   active/inactive state
-   current token
-   waiting count

Token must contain:

-   queue_id
-   user_id
-   token_number
-   status
-   joined_at
-   served_at

Statuses:

``` text
waiting
called
served
cancelled
```

------------------------------------------------------------------------

# 7. Notice System

Notice fields:

-   id
-   campus_id
-   author_id
-   title
-   category
-   body
-   priority
-   deadline
-   published_at
-   active

Categories:

-   academic
-   examination
-   fees
-   event
-   placement
-   hostel
-   emergency
-   general

------------------------------------------------------------------------

# 8. My Activity

The client should provide a unified activity view.

Activity items may reference:

-   issue
-   lost item
-   found item
-   match
-   queue token
-   notice

The activity UI must not require each feature to implement a completely
different timeline architecture.

------------------------------------------------------------------------

# 9. Intelligence Interfaces

The intelligence layer must expose simple interfaces.

Conceptual API:

``` text
calculateMatch(lostItem, foundItem)
classifyIssue(issueText, locationContext)
calculatePriority(issueContext)
clusterIssues(issues)
calculateCampusScore(metrics)
```

The UI must not contain intelligence algorithms.

------------------------------------------------------------------------

# 10. API / Service Layer

Flutter should not scatter raw database queries throughout widgets.

Preferred dependency flow:

``` text
UI
 ↓
Controller / ViewModel
 ↓
Use Case / Application Service
 ↓
Repository Interface
 ↓
Repository Implementation
 ↓
Supabase
```

Intelligence should be called through services/use cases rather than
directly from presentation widgets.

------------------------------------------------------------------------

# 11. Database Requirements

Minimum tables:

``` text
users
campuses
departments
locations
issues
issue_updates
lost_items
found_items
matches
claims
queues
queue_tokens
notices
notifications
```

Optional:

``` text
events
activity_log
issue_clusters
```

------------------------------------------------------------------------

# 12. Security Requirements

Minimum:

-   authenticated access
-   role-based authorization
-   campus-level data isolation
-   server-side authorization rules
-   no secret keys committed to GitHub
-   environment variables for credentials
-   controlled file uploads
-   validation of user-generated input

Never place service-role credentials or private API keys in Flutter
source code.

------------------------------------------------------------------------

# 13. PWA Requirements

The web build should:

-   load over HTTPS
-   be responsive
-   expose application metadata/icons
-   be installable where browser/platform support allows
-   support direct navigation to application routes
-   preserve the app shell appropriately

Important current Flutter consideration:

Flutter no longer generates/manages an offline caching service worker by
default in newer versions. If offline caching is required, the team must
explicitly configure it. Therefore **offline-first behavior is not an
MVP dependency**. [Flutter Web
FAQ](https://docs.flutter.dev/platform-integration/web/faq)

------------------------------------------------------------------------

# 14. Responsive Requirements

### Mobile

Primary layout.

Target:

-   approximately 360--430 px width

### Tablet

Adaptive layout.

### Desktop

Admin dashboard optimized for approximately 1280 px and above.

The student app should remain usable on desktop.

------------------------------------------------------------------------

# 15. Error Handling

Every network-dependent workflow needs:

-   loading state
-   success state
-   empty state
-   error state
-   retry action

Never leave the user on an infinite loading spinner.

------------------------------------------------------------------------

# 16. Logging

Use structured logs during development.

At minimum log:

-   authentication failures
-   API failures
-   intelligence failures
-   unexpected state transitions

Do not log passwords, tokens or sensitive personal data.

------------------------------------------------------------------------

# 17. Testing Requirements

Minimum:

### Unit

-   match scoring
-   classification
-   priority
-   analytics

### Widget

-   dashboard
-   issue form
-   lost/found form
-   queue state

### Integration

At least:

1.  Lost → Found → Match
2.  Issue → Classification → Admin
3.  Queue → Token → Status
4.  Notice → Student view

------------------------------------------------------------------------

# 18. SOLID Design Requirement

All maintainable production code should follow SOLID principles.

The five principles are:

-   Single Responsibility
-   Open/Closed
-   Liskov Substitution
-   Interface Segregation
-   Dependency Inversion

These principles are intended to make software easier to understand,
test and extend. [Martin Fowler discussion of
SOLID](https://martinfowler.com/articles/testing-culture.html)

### CampusOS application

**Single Responsibility**

Do not create giant widgets or services.

Bad:

``` text
CampusService
- auth
- database
- notifications
- matching
- queue
- analytics
```

Better:

``` text
AuthRepository
IssueRepository
LostFoundRepository
QueueRepository
NoticeRepository
NotificationService
```

**Open/Closed**

Adding a new workflow should not require rewriting existing workflows.

**Liskov Substitution**

Repository/service implementations must honor the contracts expected by
their interfaces.

**Interface Segregation**

Prefer focused interfaces:

``` text
IssueReader
IssueWriter
IssueAssigner
```

rather than one enormous interface.

**Dependency Inversion**

Business logic should depend on abstractions, not directly on Supabase
SDK calls.

Example:

``` text
IssueUseCase
    ↓
IssueRepository
    ↓
SupabaseIssueRepository
```

------------------------------------------------------------------------

# 19. Architecture Constraints

Do not:

-   put database calls directly inside reusable UI widgets
-   put matching algorithms inside screens
-   hardcode admin credentials
-   duplicate models across features
-   create circular dependencies
-   create unnecessary microservices
-   introduce an ML pipeline solely for presentation value

The hackathon architecture should be modular without being
over-engineered.

------------------------------------------------------------------------

# 20. Definition of Done

A feature is done only if:

-   code compiles
-   UI works
-   backend operation works
-   error state exists
-   basic test exists where applicable
-   no credentials are exposed
-   documentation is updated
-   PR is reviewed
-   PR is merged into `main`

------------------------------------------------------------------------

# 21. MVP Technical Definition

The MVP is technically complete when:

``` text
Flutter Web/PWA
        ↓
Authentication
        ↓
Database
        ↓
Student workflow
        ↓
Intelligence
        ↓
Admin workflow
        ↓
Resolution
        ↓
Analytics
```

can be demonstrated end-to-end.
