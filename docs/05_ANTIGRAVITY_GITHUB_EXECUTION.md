# CampusOS --- Antigravity + GitHub Execution Contract

**Version:** 1.0\
**Purpose:** This is the operational instruction document for AI coding
agents, especially Antigravity.\
**Status:** Authoritative execution workflow.

------------------------------------------------------------------------

# 1. Agent Mission

Antigravity must use the Phase 0 documents as the source of truth before
modifying code.

Required documents:

``` text
01_PRD.md
02_SRD.md
03_ARCHITECTURE.md
04_UX_DESIGN.md
05_ANTIGRAVITY_GITHUB_EXECUTION.md
```

The agent must not invent product requirements that conflict with these
documents.

------------------------------------------------------------------------

# 2. Source-of-Truth Priority

If documents conflict, use this priority:

``` text
1. PRD — what the product must do
2. SRD — technical requirements
3. Architecture — how it should be structured
4. UX Design — how users should experience it
5. Execution Contract — how the agent should implement it
```

If a conflict cannot be resolved safely, STOP and ask the human owner.

Do not silently choose a new architecture.

------------------------------------------------------------------------

# 3. Human Team Ownership

## TASK-1 --- Jitin

**CampusOS Full-Stack Application**

Owns:

-   Flutter
-   Android
-   Flutter Web/PWA
-   backend
-   database
-   API
-   integration

## TASK-2 --- Kartike

**Campus Intelligence Engine**

Owns:

-   matching
-   classification
-   priority
-   clustering
-   analytics

## TASK-3 --- Arko

**CampusOS Product Experience**

Owns:

-   UX
-   user flows
-   design system
-   product direction
-   presentation assets

## TASK-4 --- Ansh

**CampusOS Quality & Deployment**

Owns:

-   QA
-   testing
-   deployment
-   security checks
-   demo data
-   documentation

------------------------------------------------------------------------

# 4. GitHub Repository Structure

``` text
CampusOS/
├── README.md
├── docs/
│   ├── 01_PRD.md
│   ├── 02_SRD.md
│   ├── 03_ARCHITECTURE.md
│   ├── 04_UX_DESIGN.md
│   └── 05_ANTIGRAVITY_GITHUB_EXECUTION.md
│
├── task-1-campusos-fullstack/
├── task-2-campus-intelligence/
├── task-3-campusos-product-experience/
├── task-4-campusos-quality-deployment/
│
└── shared/
    ├── api-contracts/
    ├── database-schema/
    └── project-docs/
```

------------------------------------------------------------------------

# 5. Git Ownership

Task owners should normally modify only their own folder.

### Jitin

``` text
/task-1-campusos-fullstack/**
```

### Kartike

``` text
/task-2-campus-intelligence/**
```

### Arko

``` text
/task-3-campusos-product-experience/**
```

### Ansh

``` text
/task-4-campusos-quality-deployment/**
```

Shared files require coordination.

------------------------------------------------------------------------

# 6. Branch Rules

Never work directly on `main`.

Branch naming:

``` text
task-1/phase-1-foundation
task-1/phase-2-student-app
task-1/phase-3-backend
task-1/phase-4-integration

task-2/phase-1-intelligence-foundation
task-2/phase-2-smart-matching
task-2/phase-3-issue-intelligence
task-2/phase-4-campus-intelligence

task-3/phase-1-product-research
task-3/phase-2-user-flows
task-3/phase-3-design-system
task-3/phase-4-final-experience

task-4/phase-1-development-infrastructure
task-4/phase-2-quality-assurance
task-4/phase-3-security-deployment
task-4/phase-4-demo-documentation
```

------------------------------------------------------------------------

# 7. Antigravity Operating Rule

Before changing code:

1.  Read the relevant Phase 0 documents.
2.  Inspect the repository.
3.  Inspect existing code.
4.  Identify the task folder.
5.  Identify the current phase.
6.  Check dependencies.
7.  Create a short implementation plan.
8.  Implement only the requested scope.
9.  Run validation.
10. Report changed files and tests.
11. Do not merge your own PR.

------------------------------------------------------------------------

# 8. Antigravity Prompt Template

Each team member should use a command/prompt in this format:

``` text
You are working on CampusOS.

Read these files before coding:
- docs/01_PRD.md
- docs/02_SRD.md
- docs/03_ARCHITECTURE.md
- docs/04_UX_DESIGN.md
- docs/05_ANTIGRAVITY_GITHUB_EXECUTION.md

Your assigned task:
[TASK-X]

Your current phase:
[PHASE-X]

Your exact objective:
[OBJECTIVE]

Your allowed directory:
[DIRECTORY]

Do not modify another task's folder unless explicitly required.

Follow:
- SOLID principles
- architecture boundaries
- existing project conventions
- responsive Flutter requirements
- PWA requirements
- security requirements

Before coding:
1. inspect the repository
2. identify dependencies
3. explain the implementation plan briefly

Then implement the phase.

After implementation:
1. run formatter
2. run static analysis
3. run relevant tests
4. fix failures
5. summarize changed files
6. summarize validation
7. prepare the changes for a GitHub Pull Request

Do not merge the PR.
```

------------------------------------------------------------------------

# 9. TASK-1 Antigravity Commands

## Phase 1

``` text
Read all Phase 0 documents.

You are TASK-1 / Jitin.

Implement Phase 1:
CampusOS Full-Stack Foundation.

Create the Flutter project architecture, Flutter Web support,
Android support, PWA configuration, routing, theme, dependency
boundaries, and backend connection.

Do not implement secondary product features yet.

Follow the architecture and SOLID requirements.

After implementation, validate that the application launches
on Flutter Web and Android.
```

## Phase 2

``` text
Read all Phase 0 documents.

You are TASK-1 / Jitin.

Implement TASK-1 Phase 2:
CampusOS Student Application.

Implement:
- login
- dashboard
- Lost & Found
- CampusFix
- Queue
- Notices
- My Activity

Use the UX document as the authoritative interaction specification.

Do not implement intelligence algorithms inside UI code.
Use service/use-case boundaries for intelligence calls.

Run analysis and tests before preparing the PR.
```

## Phase 3

``` text
Implement TASK-1 Phase 3:
Backend and database.

Create the required database schema, authentication,
storage, repositories and application services.

Follow the SRD and Architecture documents.

Ensure campus_id exists wherever required for future
multi-campus support.

Do not expose secrets in source code.

Validate database operations before preparing the PR.
```

## Phase 4

``` text
Implement TASK-1 Phase 4:
System integration.

Connect:
Flutter → application services → repositories → backend
and integrate TASK-2 intelligence interfaces.

Do not rewrite TASK-2 intelligence internally.

Validate:
- Lost & Found
- CampusFix
- Queue
- Notices
- My Activity

Prepare the application for final MVP integration.
```

------------------------------------------------------------------------

# 10. TASK-2 Antigravity Commands

## Phase 1

``` text
Read the Phase 0 documents.

You are TASK-2 / Kartike.

Implement the Campus Intelligence Engine interfaces.

Create clean, independently testable services for:
- matching
- classification
- priority
- clustering
- analytics

Do not create Flutter UI.

Keep intelligence independent from Supabase and Flutter.

Follow SOLID and dependency inversion.
```

## Phase 2

``` text
Implement TASK-2 Phase 2:
Smart Lost & Found Matching.

Build deterministic weighted matching using:
- category
- brand
- color
- location
- time
- description

Return:
- score
- matched attributes
- match strength

Write unit tests for edge cases.

Do not build UI.
```

## Phase 3

``` text
Implement TASK-2 Phase 3:
Issue classification and priority.

Input:
issue text + location/context.

Return:
category
type
department
priority

Use an explainable MVP approach.
Do not introduce a complex ML pipeline.

Write tests for representative campus issues.
```

## Phase 4

``` text
Implement TASK-2 Phase 4:
Campus Intelligence.

Implement:
- issue clustering
- issue density
- resolution rate
- recovery rate
- average resolution time
- campus reliability score
- department performance

All calculations must be deterministic and testable.
```

------------------------------------------------------------------------

# 11. TASK-3 Antigravity Commands

TASK-3 is primarily documentation/design work.

## Phase 1

``` text
You are TASK-3 / Arko.

Define CampusOS product requirements from the PRD.

Create:
- user personas
- problem statements
- product flows

Do not add features not approved by the PRD.
```

## Phase 2

``` text
Create exact UX flows for:
- Lost & Found
- CampusFix
- Queue
- Notices
- My Activity
- Admin dashboard

The output must be implementation-ready for TASK-1.
```

## Phase 3

``` text
Create the CampusOS design system.

Define:
- typography
- spacing
- semantic colors
- components
- status system
- responsive behavior
- accessibility requirements

Keep the design implementable within the hackathon MVP.
```

## Phase 4

``` text
Finalize the CampusOS product experience.

Review implemented screens against the UX specification.

Identify:
- confusing flows
- unnecessary screens
- inconsistent components
- missing states
- accessibility issues

Prepare final presentation/product assets.
```

------------------------------------------------------------------------

# 12. TASK-4 Antigravity Commands

## Phase 1

``` text
You are TASK-4 / Ansh.

Configure GitHub and development infrastructure.

Create:
- PR template
- issue template
- branch protection documentation
- environment configuration documentation
- deployment configuration

Do not modify product behavior.
```

## Phase 2

``` text
Create the CampusOS QA suite.

Test complete workflows, not only isolated buttons.

Required:
Lost & Found
CampusFix
Queue
Notices
Authentication
Admin authorization

Document failures clearly.
```

## Phase 3

``` text
Validate CampusOS security and deployment.

Check:
- role access
- authentication
- database permissions
- secret exposure
- file uploads
- PWA behavior
- HTTPS
- production build

Do not introduce product features.
```

## Phase 4

``` text
Prepare the final CampusOS demonstration.

Create realistic demo data.

Validate the complete end-to-end workflow.

Prepare:
- demo account
- admin account
- demo data
- README
- setup instructions
- deployment instructions
- final demo script

Do not merge the PR.
```

------------------------------------------------------------------------

# 13. Pull Request Requirements

Every PR must contain:

``` text
## Objective

## What Changed

## Files Changed

## Implementation Notes

## Tests Run

## Screenshots / Evidence

## Known Issues

## Dependencies

## Checklist
- [ ] Scope matches assigned phase
- [ ] No unrelated changes
- [ ] Formatting passed
- [ ] Static analysis passed
- [ ] Tests passed
- [ ] No secrets committed
- [ ] Documentation updated
```

------------------------------------------------------------------------

# 14. PR Merge Policy

A PR may be merged only when:

1.  It belongs to the correct task.
2.  It is within the current phase.
3.  It passes validation.
4.  Another teammate reviews it.
5.  No critical regression exists.

The task owner must **not self-approve and self-merge**.

------------------------------------------------------------------------

# 15. Phase Gates

## Gate 0 --- Documentation

Must exist:

``` text
PRD
SRD
Architecture
UX Design
Antigravity/GitHub Execution
```

No feature coding begins before Gate 0.

## Gate 1 --- Foundation

Flutter + backend foundation works.

## Gate 2 --- Feature Development

Core workflows exist.

## Gate 3 --- Intelligence

Matching/classification/priority are integrated.

## Gate 4 --- MVP Integration

Student + admin workflows work end-to-end.

## Gate 5 --- Release

QA passes and all accepted PRs are merged.

------------------------------------------------------------------------

# 16. Final Integration Rule

The final MVP is NOT considered complete because each PR is complete.

It is complete only after:

``` text
TASK-1 PRs
     +
TASK-2 PRs
     +
TASK-3 PRs
     +
TASK-4 PRs
     ↓
ALL REQUIRED PRs MERGED
     ↓
MAIN
     ↓
Flutter build web
     ↓
DEPLOY
     ↓
LIVE CAMPUSOS MVP
```

The GitHub `main` branch must always represent the closest working
version of the product.

------------------------------------------------------------------------

# 17. Final MVP Acceptance Test

The team must demonstrate:

### Scenario A --- Lost & Found

``` text
Student reports lost calculator
        ↓
Found calculator submitted
        ↓
94% potential match
        ↓
Ownership verification
        ↓
Recovered
```

### Scenario B --- CampusFix

``` text
Student reports broken projector
        ↓
Classification
        ↓
Priority = HIGH
        ↓
Admin receives request
        ↓
Admin assigns technician
        ↓
Technician resolves
        ↓
Student verifies
        ↓
Analytics update
```

### Scenario C --- Queue

``` text
Student joins queue
        ↓
Token generated
        ↓
Position updates
        ↓
Service completed
```

### Scenario D --- Notices

``` text
Admin publishes notice
        ↓
Student sees notice
        ↓
Deadline displayed
```

------------------------------------------------------------------------

# 18. Hard Scope Rules for Antigravity

Antigravity MUST NOT:

-   invent additional major features
-   rewrite architecture without approval
-   introduce microservices
-   introduce a complex ML system unnecessarily
-   modify another task's folder without permission
-   change the database schema without checking SRD
-   add dependencies without justification
-   expose credentials
-   commit generated build artifacts unnecessarily
-   replace working code with speculative abstractions
-   optimize prematurely
-   create duplicate models/services
-   bypass repository boundaries

If a requested change conflicts with these rules:

**STOP → explain conflict → request human decision.**

------------------------------------------------------------------------

# 19. Coding Quality Rules

All code should prioritize:

-   readability
-   small cohesive classes
-   explicit interfaces
-   dependency injection
-   testability
-   error handling
-   meaningful names
-   minimal duplication
-   documented non-obvious decisions

SOLID principles are mandatory architectural guidance.

Do not apply SOLID mechanically by creating excessive abstractions.

The goal is **appropriate separation of responsibilities**, not maximum
number of classes.

------------------------------------------------------------------------

# 20. Final Definition of Done

CampusOS Phase 0 + MVP is complete when:

``` text
[✓] Five authoritative MD documents exist
[✓] GitHub repository structure exists
[✓] Four task ownership boundaries exist
[✓] Phase branches are defined
[✓] PR workflow is defined
[✓] Flutter Android build works
[✓] Flutter Web build works
[✓] PWA works
[✓] Backend works
[✓] Database works
[✓] Lost & Found works
[✓] Smart matching works
[✓] CampusFix works
[✓] Classification works
[✓] Priority works
[✓] Queue works
[✓] Notices work
[✓] Admin workflow works
[✓] Analytics work
[✓] QA passes
[✓] All accepted PRs are merged
[✓] main contains the integrated MVP
[✓] Live deployment is available
```

------------------------------------------------------------------------

# 21. Final Agent Instruction

> **Build only what is specified.**
>
> **Prefer a working simple implementation over a sophisticated
> incomplete implementation.**
>
> **Respect task ownership.**
>
> **Follow SOLID principles and the documented architecture.**
>
> **Every change must be testable and reviewable.**
>
> **The final objective is one integrated, deployable CampusOS MVP on
> `main`, not four independent projects.**
