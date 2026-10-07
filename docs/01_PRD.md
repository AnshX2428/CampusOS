# CampusOS --- Product Requirements Document (PRD)

**Version:** 1.0\
**Phase:** Phase 0 --- Product Definition\
**Status:** Authoritative product specification\
**Owners:** Jitin (Full-Stack), Kartike (Intelligence), Arko
(Product/UX), Ansh (QA/DevOps)

------------------------------------------------------------------------

## 1. Product Definition

### 1.1 Product Name

**CampusOS**

### 1.2 Product Positioning

> **CampusOS is a Progressive Web App and cross-platform campus
> operating layer that converts fragmented student requests and campus
> problems into trackable, accountable workflows and converts
> operational activity into campus intelligence.**

CampusOS is **not** intended to be another college ERP, notice board, or
collection of unrelated utility screens.

Its central product mechanism is:

**Discover / Report / Request → Classify → Prioritize → Route → Assign →
Track → Resolve → Verify → Analyze**

The individual features are applications of this common workflow engine.

------------------------------------------------------------------------

## 2. Problem Statement

College students currently interact with campus services through
fragmented channels:

-   WhatsApp groups
-   verbal complaints
-   notice boards
-   PDFs
-   separate portals
-   physical queues
-   informal student groups
-   department-specific processes

This creates five major problems:

1.  **Requests disappear into conversations.**
2.  **Students cannot reliably track status.**
3.  **Staff receive poorly structured requests.**
4.  **Repeated problems are not aggregated into useful operational
    data.**
5.  **Students need multiple disconnected channels for basic campus
    tasks.**

CampusOS addresses this by providing a single app-centric PWA with a
common request/action model.

------------------------------------------------------------------------

## 3. Target Users

### 3.1 Student

Primary user.

Needs:

-   report a problem
-   report/find lost property
-   join a queue
-   read important notices
-   track personal requests
-   receive status updates

### 3.2 Faculty

Needs:

-   view relevant campus notices
-   report facility problems
-   access operational information

### 3.3 Staff / Maintenance

Needs:

-   receive assigned requests
-   update status
-   attach resolution proof
-   close completed tasks

### 3.4 Campus Administrator

Needs:

-   manage requests
-   assign departments
-   publish notices
-   manage queues
-   review analytics
-   identify recurring campus problems

------------------------------------------------------------------------

## 4. Product Principles

### Principle 1 --- Action over information

CampusOS should not merely tell users what is happening. It should allow
them to act.

### Principle 2 --- Closed-loop workflows

Every operational request should have:

-   creator
-   timestamp
-   category
-   status
-   owner/department
-   resolution
-   verification state

### Principle 3 --- One platform, multiple workflows

Lost & Found, CampusFix, Queue and Notices must use shared platform
primitives rather than independent mini-app architectures.

### Principle 4 --- Mobile-first, PWA-first

The same Flutter codebase should support:

-   Android
-   responsive web
-   installable PWA

Flutter officially supports web deployment and app-centric PWA
experiences; release builds are produced with `flutter build web`.
[Flutter Web
documentation](https://docs.flutter.dev/platform-integration/web)

### Principle 5 --- MVP before breadth

The hackathon MVP must prioritize working end-to-end workflows over
feature count.

------------------------------------------------------------------------

# 5. Core MVP

The MVP must contain the following:

## 5.1 Student Dashboard

Shows:

-   Lost & Found
-   Report Campus Issue
-   Queue
-   Notices
-   My Activity
-   basic campus status

## 5.2 Lost & Found

Student can:

-   report lost item
-   report found item
-   view relevant items
-   receive potential matches
-   submit a claim
-   complete ownership verification
-   mark recovery

### Smart matching

A matching service compares:

-   category
-   brand
-   color
-   location
-   time
-   description

The MVP may use deterministic weighted scoring. A complex ML model is
explicitly out of scope.

## 5.3 CampusFix

Student can:

-   select category
-   select location
-   describe issue
-   upload image
-   submit issue
-   view status

Workflow:

`Reported → Verified → Assigned → In Progress → Resolved → Student Verified → Closed`

## 5.4 Digital Queue

Student can:

-   select a service
-   join a queue
-   receive token
-   view people ahead
-   view estimated position/status

Admin can:

-   open/close queue
-   advance queue
-   view waiting users

## 5.5 Notices

Admin can publish:

-   title
-   category
-   description
-   deadline
-   priority

Student can:

-   browse notices
-   filter by category
-   view deadlines

## 5.6 My Activity

A unified timeline of the student's CampusOS activity.

Examples:

-   lost item matched
-   issue assigned
-   issue resolved
-   queue token active
-   notice acknowledged

------------------------------------------------------------------------

# 6. Intelligence MVP

CampusOS intelligence is deliberately lightweight and explainable.

## 6.1 Matching Engine

Output:

-   score from 0--100
-   match strength
-   matched attributes

Example:

`94% — Strong potential match`

## 6.2 Issue Classification

Input:

> "The projector in room 204 is not working."

Output:

``` text
category: equipment
type: projector
department: IT
location: room_204
```

MVP may use rules/keywords.

## 6.3 Priority Engine

Outputs:

-   LOW
-   MEDIUM
-   HIGH
-   CRITICAL

Factors:

-   severity
-   number affected
-   location importance
-   recurrence

## 6.4 Problem Clustering

Group semantically or textually similar reports in the same
location/time window.

Example:

`Wi-Fi down`, `no internet`, `network unavailable`

→ `Possible network outage`

------------------------------------------------------------------------

# 7. Admin Intelligence

The MVP dashboard should calculate:

-   active issues
-   resolved issues
-   average resolution time
-   Lost & Found recovery rate
-   issue category distribution
-   issue location distribution
-   recurring problem clusters
-   basic campus reliability score

------------------------------------------------------------------------

# 8. Secondary / Roadmap Features

These should **not block MVP completion**:

-   campus map
-   room/lab availability
-   events
-   BorrowBack
-   peer help
-   marketplace
-   hostel management
-   transport
-   emergency module
-   resource sharing
-   QR-triggered workflows
-   predictive maintenance
-   IoT integration
-   multi-campus tenant administration

They may appear in the UI as roadmap/coming-soon only if doing so does
not confuse the MVP.

------------------------------------------------------------------------

# 9. Product USP

## Primary USP

> **CampusOS turns campus activity into action, accountability and
> intelligence.**

### Action

Requests are classified, prioritized and routed.

### Accountability

Every request has a status, owner and resolution proof.

### Intelligence

Aggregated activity reveals recurring problems and operational hotspots.

------------------------------------------------------------------------

# 10. QR Interaction Layer

Future/optional MVP enhancement.

Physical QR codes can deep-link into specific actions:

-   classroom QR → report classroom issue
-   laboratory QR → report equipment problem
-   office QR → join queue
-   Lost & Found counter → report/claim item
-   library QR → view library information

Concept:

> **The physical campus becomes an interface for the digital campus.**

------------------------------------------------------------------------

# 11. Success Metrics

For the hackathon demo, success is measured by:

### Functional

-   user can create a request
-   request appears in backend
-   intelligence processes request
-   admin sees request
-   admin can update status
-   student sees updated status
-   complete workflow can be demonstrated

### Product

-   at least 2 complete workflows are functional
-   UI works on desktop and mobile
-   PWA can be installed
-   demo data exists
-   no critical demo blocker remains

### Intelligence

-   Lost & Found produces explainable match scores
-   issues receive categories
-   issues receive priorities
-   recurring issue cluster can be demonstrated

------------------------------------------------------------------------

# 12. Non-Goals for the Hackathon

Do not build:

-   payment gateway
-   production-grade government/identity verification
-   facial recognition
-   biometric authentication
-   complex ML training pipeline
-   real-time GPS fleet tracking
-   full ERP replacement
-   full attendance management
-   full academic LMS
-   complete marketplace
-   complicated microservice infrastructure

------------------------------------------------------------------------

# 13. Scalability Vision

CampusOS should eventually support multiple institutions.

Concept:

``` text
CampusOS Platform
    ├── Campus A
    │   ├── Users
    │   ├── Departments
    │   ├── Locations
    │   └── Workflows
    ├── Campus B
    └── Campus C
```

Every operational record should be designed with a `campus_id` boundary
even if only one campus is used in the MVP.

------------------------------------------------------------------------

# 14. Business Direction

Potential future model:

**B2B/B2B2C SaaS**

Institution pays for:

-   workflow management
-   analytics
-   admin tools
-   campus configuration
-   integrations

Students use the platform as the campus service interface.

------------------------------------------------------------------------

# 15. Definition of Product Success

The MVP is complete only when this sentence is demonstrably true:

> **A student can create a campus request, CampusOS can intelligently
> process it, the responsible administrator can act on it, the student
> can track it, and the final resolution is reflected in campus
> intelligence.**
