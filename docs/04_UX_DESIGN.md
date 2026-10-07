# CampusOS --- UX and Design Specification

**Version:** 1.0\
**Owner:** Arko\
**Consumers:** Jitin, Kartike, Ansh\
**Status:** Authoritative UX direction

------------------------------------------------------------------------

# 1. UX Goal

CampusOS should feel like a **single campus command center**, not an ERP
dashboard.

The student should be able to answer:

1.  What do I need to know?
2.  What can I do?
3.  What is happening with my request?

within a few seconds.

------------------------------------------------------------------------

# 2. Design Principles

## 2.1 Action-first

The home screen should prioritize actions.

Primary actions:

-   Report Issue
-   Lost & Found
-   Join Queue
-   Notices

## 2.2 Status visibility

Users should always understand:

-   what happened
-   what happens next
-   who owns the request
-   whether action is required

## 2.3 Minimal input

Forms should ask only what is needed.

Use:

-   dropdowns
-   location selectors
-   predefined categories
-   photo upload
-   short description

## 2.4 Progressive disclosure

Do not show administrative complexity to students.

------------------------------------------------------------------------

# 3. Information Architecture

``` text
CampusOS
│
├── Home
├── Lost & Found
├── CampusFix
├── Queue
├── Notices
├── My Activity
└── Profile
```

Admin:

``` text
Admin
│
├── Overview
├── Issues
├── Lost & Found
├── Queues
├── Notices
└── Analytics
```

------------------------------------------------------------------------

# 4. Student Home

Top:

``` text
CampusOS
Good morning, [Name]
```

Primary action grid:

``` text
[ Report Issue ]
[ Lost & Found ]

[ Join Queue ]
[ Notices ]
```

Then:

``` text
My Active Requests
```

Then:

``` text
Campus Status
```

Then:

``` text
Important Notices
```

------------------------------------------------------------------------

# 5. CampusFix UX

## Step 1

Choose category:

-   classroom
-   electrical
-   Wi-Fi
-   equipment
-   cleanliness
-   water
-   hostel
-   other

## Step 2

Choose location.

## Step 3

Describe.

## Step 4

Upload optional image.

## Step 5

Submit.

After submission:

``` text
Issue #1042

Status:
Reported

Category:
Equipment

Location:
Room 204

Next:
Waiting for assignment
```

------------------------------------------------------------------------

# 6. CampusFix Status UX

Use a visible stepper:

``` text
● Reported
│
● Verified
│
● Assigned
│
○ In Progress
│
○ Resolved
│
○ Verified
```

The student should never have to guess the state.

------------------------------------------------------------------------

# 7. Lost & Found UX

Home:

``` text
Lost & Found

[ I Lost Something ]
[ I Found Something ]

Search items
```

Lost form:

-   item category
-   name
-   brand
-   color
-   location
-   approximate time
-   description
-   photo

After submission:

``` text
Potential Matches

Casio Calculator
Library
94% match
```

CTA:

`View Match`

------------------------------------------------------------------------

# 8. Match UX

Show why the system believes it is a match:

``` text
94% potential match

✓ Same category
✓ Same brand
✓ Same color
✓ Nearby location
✓ Similar time
```

This is important because the intelligence must be explainable.

CTA:

`Claim Item`

Then ownership verification.

------------------------------------------------------------------------

# 9. Queue UX

Show:

``` text
Accounts Office

Your Token
#27

Now Serving
#22

People Ahead
4

Estimated Position
~12 minutes
```

Use a clear status:

`You're approaching`

------------------------------------------------------------------------

# 10. Notices UX

Use categories:

-   Important
-   Exam
-   Academic
-   Fees
-   Placement
-   Event
-   Hostel

Important notices should visually stand out.

Each notice:

``` text
TITLE
Category
Deadline
Short description
[View]
```

------------------------------------------------------------------------

# 11. My Activity

Timeline style:

``` text
Today

10:42
Projector issue assigned

09:30
Calculator match found

Yesterday

Accounts queue completed
```

This creates the feeling of one unified platform.

------------------------------------------------------------------------

# 12. Admin Dashboard

The first screen should answer:

> **What needs attention right now?**

Top metrics:

``` text
Critical Issues
Active Issues
Resolved Today
Recovery Rate
```

Then:

``` text
Priority Queue
```

Then:

``` text
Problem Hotspots
```

Then:

``` text
Department Performance
```

------------------------------------------------------------------------

# 13. Visual Language

Use a modern campus-tech visual language.

Recommended:

-   neutral/light base
-   one primary brand color
-   high contrast
-   restrained gradients
-   rounded cards
-   clear typography
-   minimal decorative elements

Avoid:

-   excessive glassmorphism
-   excessive gradients
-   neon colors
-   crowded dashboards
-   tiny text

------------------------------------------------------------------------

# 14. Status Colors

Semantic only:

``` text
Critical  → Red
High      → Orange
Medium    → Yellow
Assigned  → Blue
Resolved  → Green
Pending   → Neutral
```

Color must never be the only status indicator; include text/icon as
well.

------------------------------------------------------------------------

# 15. Responsive Behavior

### Mobile

Bottom navigation.

### Tablet

Adaptive two-column layouts where useful.

### Desktop

Sidebar navigation and wider dashboard cards.

Admin desktop experience should use screen width effectively.

------------------------------------------------------------------------

# 16. Accessibility

Minimum:

-   readable contrast
-   touch targets large enough for mobile
-   semantic labels
-   icons accompanied by text where ambiguous
-   do not communicate state only through color
-   keyboard navigation where practical on web

------------------------------------------------------------------------

# 17. UX Constraints

Do not:

-   create more than necessary navigation levels
-   hide critical status information
-   force students to fill long forms
-   use jargon like "workflow orchestration" in student-facing screens
-   expose internal priority algorithms to users beyond useful
    explanations

------------------------------------------------------------------------

# 18. UX Definition of Done

A UX flow is accepted when:

-   a first-time student can complete it without instructions
-   the next action is obvious
-   status is visible
-   errors are understandable
-   mobile layout works
-   desktop layout does not look like a stretched phone UI
