# AGENTS.md — Product Build Playbook

A repeatable workflow for building a product with an AI coding agent (Claude Code or Codex), a visual design tool (Aura.build suggested), and a full-stack implementation.

Use this file as the operating instructions for a new project.

The owner may be non-technical. Guide them in plain English, recommend sensible defaults, and do not begin serious coding until the product, design, and implementation plan are sufficiently defined.

## Core rule

Build every project in this order:

1. **Idea**
2. **PRD.md** — what the product does
3. **Design tool** — explore and approve the visual direction
4. **DESIGN.md** — canonical visual/UX rules
5. **BUILD.md** — technical architecture and implementation plan
6. **Code**
7. **Test against PRD + DESIGN**
8. **Deploy**
9. **Keep the docs updated**

Do not use the design tool to define business logic, backend architecture, permissions, or product scope.

## The three source-of-truth files

Create these files for every project:

```text
docs/
  PRD.md
  DESIGN.md
  BUILD.md
```

### `PRD.md`

Answers:

> What are we building, for whom, and what must it do?

Owns:

- product purpose
- users
- problems
- user journeys
- features
- business rules
- requirements
- MVP scope
- non-goals
- acceptance criteria

### `DESIGN.md`

Answers:

> What should the product look and feel like?

Owns:

- visual direction
- typography
- colors
- spacing
- layout
- components
- responsive behavior
- motion
- interaction states
- accessibility
- loading/empty/error/success states

### `BUILD.md`

Answers:

> How will we engineer and ship it?

Owns:

- technology stack
- frontend/backend architecture
- database
- authentication
- permissions
- APIs
- integrations
- environment variables
- testing
- security
- deployment
- implementation phases

### Conflict rule

If the documents disagree:

1. `PRD.md` wins for product behavior/scope.
2. `DESIGN.md` wins for visual/UX decisions.
3. `BUILD.md` wins for technical implementation.

Surface contradictions instead of silently guessing.

## Workflow

### Step 1 — Understand the idea

When starting a new project, first ask the owner to describe the idea in ordinary language.

Help answer only the questions that materially affect the product:

- Who is it for?
- What problem does it solve?
- What is the primary action?
- What must version 1 do?
- Does it require accounts?
- What data must it save?
- Are there different user roles?
- Does it take payments?
- Does it use AI?
- Does it send notifications?
- Does it require an admin area?
- What external services must it connect to?
- What would make the MVP feel complete?

Do not overwhelm the owner with a giant questionnaire. Ask focused questions and summarize what you understand.

**Do not code yet.**

### Step 2 — Create `docs/PRD.md`

The PRD comes **before visual design**.

Draft it with the owner, then refine it until the important product decisions are clear.

Use this structure:

```md
# Product Requirements Document

## Product Summary
## Problem
## Target Users
## Primary User Outcome
## Goals
## Non-Goals
## Core User Journeys
## MVP Features
## Accounts and Roles
## Data to Store
## Integrations
## Notifications
## Payments / Billing
## Admin Requirements
## Privacy / Security Requirements
## Analytics
## Accessibility
## Future Features
## Open Questions
## Acceptance Criteria
```

For each major feature define:

- purpose
- user story
- expected behavior
- important edge cases
- acceptance criteria

Example:

Weak:

> Users can save projects.

Strong:

> An authenticated user can create, reopen, rename, and delete a project. Private projects are inaccessible to other users.

Before moving on, state whether the PRD is sufficiently defined for visual design.

### Step 3 — Choose a design tool and generate the handoff prompt

Pick a visual design tool. **Aura.build is the suggested default.** Others work too — for example v0, Figma, Google Stitch, or Lovable — and you may use more than one (for example, one for the landing page and another for app screens). Recommend one to the owner unless they already have a preference.

After the PRD is coherent, prepare a concise copy/paste prompt for the chosen tool:

```text
I am designing [PRODUCT NAME].

PRODUCT:
[2–4 sentence PRD summary]

TARGET USER:
[primary user]

PRIMARY ACTION:
[most important user action]

KEY SCREENS / SECTIONS:
- ...
- ...
- ...

KNOWN VISUAL PREFERENCES:
[preferences or "explore several directions"]

UX REQUIREMENTS:
- responsive
- clear hierarchy
- obvious primary actions
- accessible contrast
- consistent navigation
- appropriate loading, empty, error, and success states

IMPORTANT:
Do not redefine the product functionality.
The PRD controls what the product does.
Focus on visual direction, layout, components, interaction, and usability.
```

If useful, include screenshots, reference sites, brand material, or examples the owner likes as inspiration.

### Step 4 — Work in the design tool

The owner now goes to the chosen design tool.

Use it for:

- design-system exploration
- templates and components
- typography
- color
- spacing
- layout
- hero/landing sections
- application screens
- component appearance
- animation/motion
- visual HTML references
- `DESIGN.md` generation/refinement (if the tool supports it)

Recommended process:

1. Paste the project/design prompt.
2. Explore 2–3 directions if the look is uncertain.
3. Choose one visual direction.
4. Refine the most important screen first.
5. Continue section-by-section or screen-by-screen.
6. Check desktop and mobile.
7. Make repeated components visually consistent.
8. Refine interaction states.
9. Export useful design artifacts.

Depending on the tool, exports may include:

- a `DESIGN.md` or design-system file
- HTML/CSS/JS or component code
- screenshots
- images/assets

Bring useful outputs back into the repository.

### Step 5 — Save design references

Use one folder per tool:

```text
references/
  <tool-name>/        # e.g. aura/, v0/, figma/
    DESIGN.md
    *.html
    screenshots/
    assets/
```

Only include files that actually exist.

**Important:** exported code from a design tool is normally a **high-fidelity visual reference**, not automatically the production architecture.

The coding agent should inspect it and reuse good pieces where appropriate, but the final app should use maintainable components and the architecture defined in `BUILD.md`.

Goal:

> Preserve the design, not necessarily the exported DOM structure.

### Step 6 — Create canonical `docs/DESIGN.md`

Now combine:

- the approved visual direction
- the design tool's `DESIGN.md`, if available
- PRD UX requirements
- responsive requirements
- accessibility
- application states the design tool may not have shown

Use:

```md
# Product Design System

## Design Direction
## Design Principles
## Brand / Personality
## Colors
## Typography
## Spacing
## Layout / Grid
## Borders / Radius / Shadows
## Icons
## Imagery
## Motion
## Navigation
## Buttons
## Forms
## Cards / Panels
## Tables / Lists
## Modals / Drawers
## Notifications
## Loading States
## Empty States
## Error States
## Success States
## Responsive Behavior
## Accessibility Rules
## Screen-Specific Notes
## Design Reference Files
## Design QA Checklist
```

`docs/DESIGN.md` becomes the canonical design source for the production application.

Do not require every pixel to be finalized before continuing, but the direction must be coherent enough to implement.

### Step 7 — Create `docs/BUILD.md`

Only after the product and design are sufficiently understood, design the technical implementation.

Choose the simplest reliable architecture that satisfies the PRD.

Use:

```md
# Build Plan

## Architecture Summary
## Technology Stack
## Repository Structure
## Frontend Architecture
## Backend Architecture
## Database Model
## Authentication
## Authorization / Permissions
## APIs / Server Actions
## External Integrations
## File / Media Storage
## Payments
## Email / Notifications
## AI Architecture
## Background Jobs
## Security
## Error Handling
## Logging / Observability
## Analytics
## Testing Strategy
## Deployment
## Environment Variables
## Seed / Demo Data
## Migration Strategy
## Implementation Phases
## Risks / Unknowns
## Definition of Done
```

Before major coding begins, `BUILD.md` should answer:

- Where does data live?
- How do users authenticate?
- Who can access what?
- What runs client-side?
- What runs server-side?
- What outside services are required?
- How will important workflows be tested?
- How will the app be deployed?
- What order should features be implemented in?

### Step 8 — Pre-build review

Before implementation, review:

```text
docs/PRD.md
docs/DESIGN.md
docs/BUILD.md
references/*
```

Check for:

- contradictory requirements
- missing permissions
- missing data requirements
- screens with undefined behavior
- important error/loading/empty states
- unresolved integrations
- risky architectural assumptions

Resolve important blockers before coding.

### Step 9 — Scaffold the application

Then:

1. Initialize the chosen stack.
2. Install only necessary dependencies.
3. Establish the folder structure.
4. Configure formatting/linting/type checking.
5. Configure environment variables.
6. Configure database if required.
7. Configure authentication if required.
8. Create design tokens/theme.
9. Build the application shell/navigation.
10. Add test infrastructure.
11. Confirm the clean project builds and runs.

Avoid premature abstractions.

### Step 10 — Build in vertical slices

Prefer complete features over disconnected layers.

A vertical slice includes:

```text
UI
↓
validation
↓
server/backend
↓
database
↓
permissions
↓
error handling
↓
tests
```

Example:

Build "Create Project" end-to-end before building ten unfinished dashboard screens.

Then build:

- view project
- edit project
- delete project
- next feature

This reveals incorrect assumptions early.

### Step 11 — UI rules

For UI work:

1. Read `DESIGN.md`.
2. Inspect the relevant design reference.
3. Build reusable production components.
4. Preserve approved typography, spacing, color, density, radius, hierarchy, and motion.
5. Implement responsive layouts deliberately.
6. Include hover/focus/active/disabled states.
7. Include loading/empty/error/success states.
8. Use accessible semantic controls.
9. Visually compare major screens to the intended design.

Do not redesign the product accidentally while implementing it.

### Step 12 — Backend rules

For backend functionality:

- validate untrusted input
- enforce permissions server-side
- protect secrets
- use least privilege
- enforce ownership rules
- handle failures gracefully
- use database constraints where appropriate
- treat destructive operations carefully
- test important authorization boundaries

For AI features:

- define what data is sent to providers
- avoid unnecessary sensitive data
- handle provider failures/rate limits
- validate structured outputs
- define usage/cost controls where needed

### Step 13 — Test every feature

Compare implementation to the PRD acceptance criteria.

For important features test:

1. happy path
2. invalid input
3. loading
4. empty state
5. errors/failures
6. permissions
7. mobile layout
8. keyboard/accessibility behavior
9. design consistency

Run the project's relevant:

- type checks
- lint
- unit tests
- integration tests
- end-to-end tests
- production build

Do not declare a feature finished while critical checks are knowingly failing.

### Step 14 — Deploy

Before production:

- confirm production environment variables
- run database migrations
- verify auth domains/callbacks
- verify storage permissions
- verify payment webhooks if used
- verify email configuration if used
- confirm monitoring/logging
- confirm backup/recovery needs
- run the production build
- deploy
- test the real deployed critical path

### Step 15 — Keep the docs alive

When a change alters **what the product does**:

> update `PRD.md`

When it alters **how the product looks or behaves visually**:

> update `DESIGN.md`

When it alters **how the system is engineered**:

> update `BUILD.md`

Then implement and test.

Do not allow documentation and implementation to drift silently.

## How to guide the owner

The owner may not know technical jargon. Therefore:

- explain decisions in plain English
- recommend a default instead of listing ten equal options
- distinguish "must decide now" from "can decide later"
- flag expensive/complex choices
- flag privacy/security implications
- make reasonable low-risk technical decisions for them
- ask for input when a decision significantly changes cost, UX, scope, security, or business behavior
- keep momentum

## Tool roles

### Coding agent — Claude Code or Codex

Either agent works. Both load this playbook automatically: Codex reads `AGENTS.md` directly, and Claude Code reads `CLAUDE.md`, which imports `AGENTS.md`.

Use for:

- product discovery
- PRD
- architecture
- repository implementation
- backend
- database
- APIs
- integrations
- testing
- debugging
- deployment

### Design tool — Aura.build suggested

Aura.build is the suggested default; v0, Figma, Google Stitch, Lovable, or similar tools also work, alone or in combination.

Use for:

- visual exploration
- design systems
- templates/components
- layouts
- styling
- motion
- visual references
- design-oriented HTML
- design-system files

The design tool does not replace the PRD or technical build plan.

## Reusable prompts for the owner

### Start a new project

> Start the project playbook. I want to build: [describe the idea normally]. Do not code yet. Guide me through Step 1 and help me create the PRD first.

### Resume an existing project

> Read AGENTS.md, PRD.md, DESIGN.md, and BUILD.md if they exist. Tell me which stage of the playbook we are in, what important information is missing, and the next best step.

### After returning from the design tool

> I added the design exports under references/[tool-name]. Inspect them together with PRD.md. Help me finalize the canonical DESIGN.md. Preserve the approved product requirements and use the exports as the visual reference.

### Begin implementation

> Review PRD.md, DESIGN.md, and BUILD.md for contradictions or missing critical decisions. If they are build-ready, begin the first implementation phase. Work in vertical slices and verify completed work against the PRD acceptance criteria and DESIGN.md.

### Add a feature

> Implement [FEATURE]. First read the relevant PRD requirements, design rules, and build architecture. Update the appropriate docs first if this request changes product behavior, design, or architecture. Then implement and test it end-to-end.

### Fix a design

> Compare this screen with DESIGN.md and the relevant design reference. Identify and fix the visual mismatches without changing the approved product behavior. Verify desktop and mobile.

### Prepare to ship

> Perform a release-readiness review against PRD.md, DESIGN.md, and BUILD.md. Run the relevant checks, identify incomplete requirements, permission/security problems, broken states, responsive issues, and deployment blockers. Fix safe issues and clearly report anything requiring an owner decision.

## One-line memory aid

```text
IDEA → PRD → DESIGN TOOL → DESIGN.md → BUILD.md → CODE → TEST → DEPLOY
```

**PRD first. Visual design second. BUILD plan third. Production coding fourth.**
