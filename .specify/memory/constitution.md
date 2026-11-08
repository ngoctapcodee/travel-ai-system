# TravelAI 2.0 Constitution

## Core Principles

### I. Test-First and Quality

Every new feature MUST have appropriate automated tests. Measurable acceptance criteria and the
corresponding test cases MUST be defined before implementation; executable tests MUST be written
before the behavior they verify. Relevant tests MUST run after every implementation task. A task
MUST NOT be marked complete while required tests fail, are skipped, or lack execution evidence.
Existing functionality MUST NOT regress. This makes completion an evidence-based decision.

Changes MUST remain scoped, readable, and organized around explicit client, domain, persistence,
and AI boundaries. New dependencies or architectural layers MUST have a documented need. Changed
business rules MUST have automated unit tests; changed service boundaries MUST have integration
or contract tests; affected critical user journeys MUST have automated regression coverage.
Security-sensitive changes MUST test unauthorized access and ownership failures. Recognition changes
MUST test invalid inputs, unknown results, provider failures, and model quality against versioned
fixtures or datasets. Routine automated tests MUST use controlled doubles for paid providers;
external integration checks MUST be separately identified. Builds and configured static checks
MUST pass for affected modules. A successful build or manual demonstration alone is insufficient
proof of correct behavior.

### II. Data Privacy and Security

User personal data MUST NOT be transmitted to external services without explicit user authorization.
Every external data transfer MUST have explicit user approval covering the destination, purpose,
and data scope before transmission; a previously approved scope MAY be reused only while it remains
applicable. Production databases, credentials, tokens, and private user information MUST NOT be sent
to AI services. Tests MUST use synthetic or anonymized data with re-identification risk addressed.
Access MUST follow least privilege, and sensitive information MUST use secure storage.

Using Codex or another coding assistant MUST NOT be assumed private by default. Before selecting
content for a prompt, tool output, attachment, log, or other service upload, inspect what content
may be shared and minimize or redact it. Unverified privacy or retention settings MUST be recorded
as unknown; authorization MUST NOT be inferred from tool availability. Review MUST avoid exposing
sensitive content in the process of inspecting it. Cloud Vision, Kaggle, AI enrichment, and external
integration tests are subject to the same approval and data restrictions.

Protected HTTP and WebSocket operations MUST enforce server-side authentication, resource ownership,
and role-based authorization, including administrator actions. Client-supplied user identifiers MUST
NOT establish authority. Passwords MUST use an adaptive password hash; secrets MUST be supplied
through protected runtime configuration and MUST NOT appear in source, client bundles, model
artifacts, notebooks, or logs. Production transport MUST use TLS with restricted origins and
least-privilege service credentials. Image and camera flows MUST validate content type, size, and
decoding limits, enforce appropriate request limits, and request platform permissions explicitly.
Images, location, and account data MUST have documented collection, retention, and deletion rules;
logs MUST exclude secrets and sensitive payloads. Legacy security gaps MUST be recorded and
remediated through scoped changes; preservation MUST NOT justify shipping a known exploitable
path in an affected release.

### III. Specification Quality

Every feature specification MUST define WHAT is built, WHO it serves, and WHY it is needed.
Requirements MUST have stable identifiers, clear scope, and testable statements. Each mandatory
requirement MUST map to measurable acceptance criteria, including applicable failure cases and
platform differences. Critical ambiguities MUST be resolved before planning. Unclear, contradictory,
or untestable requirements MUST be corrected in the specification before work advances.

### IV. Mandatory Clarification

Every stage MUST identify ambiguous requirements, assumptions, and missing decisions. When a
necessary decision is absent, ask focused questions and record the answers in the governing
artifact. Business requirements MUST NOT be invented. An unresolved critical question MUST block
all dependent planning or execution until answered; independent work MAY proceed only if it does
not assume an answer. Critical questions include decisions affecting scope, acceptance, security,
data transfers, destructive operations, or API and platform compatibility.

### V. Plan Quality Gate

Before planning, review the specification for completeness, clarity, consistency, testability,
and resolved critical questions. Reject any specification that fails these checks and update it
before continuing. Every plan MUST record a constitution compliance assessment, requirement
coverage, existing-code reuse, service boundaries, dependencies, verification strategy, and
migration impact. Constitution violations MUST block plan acceptance pending correction or an
explicitly approved, recorded exception under Governance.

### VI. Task Dependencies

Implementation MUST be divided into small, independently verifiable tasks. Every task MUST reference
its requirement identifiers, declare dependencies, define completion criteria, and identify required
tests or other verification evidence. Prerequisite and foundational tasks MUST precede dependent
work. Parallel execution is permitted only where declared dependencies and shared changes allow it.
Missing traceability or completion criteria MUST be corrected before the task is implemented.

### VII. Cross-Document Analysis

Before implementation, cross-check the constitution, specification, plan, applicable checklists,
and tasks for missing requirements, contradictions, security risks, and incomplete coverage.
Mandatory requirements MUST trace through acceptance criteria, planned work, tasks, and verification.
Required artifacts that are missing MUST be reported as gaps. Critical findings MUST be resolved
before implementation; changed artifacts MUST be rechecked for affected inconsistencies. Findings,
resolutions, and supporting evidence MUST be recorded rather than silently discarded.

### VIII. Controlled Implementation

Tasks MUST be implemented in dependency order. After each implementation task, run relevant tests,
verify its completion and acceptance criteria, and record outcomes before updating task status.
If any required checklist item is unchecked, STOP the affected workflow and request user
clarification or approval. Incomplete required items MUST NOT be silently skipped or marked checked
without evidence. Destructive changes MUST NOT be performed without explicit user approval covering
the proposed operation and impact. Existing local changes and unrelated source MUST be preserved.
A failed required test MUST keep the task incomplete even if an exception allows investigation
or other independent work to continue.

### IX. Convergence Loop

Convergence MUST compare actual code and test evidence against the constitution, specification,
plan, applicable checklists, and tasks. Identify every missing or incomplete mandatory requirement,
create new tasks with requirement references, dependencies, completion criteria, and verification,
then repeat implementation and testing. Unresolved critical questions, checklist gates, security
issues, and constitution violations MUST remain visible blockers.

Report CONVERGED only when a requirement-to-evidence review confirms full mandatory coverage and
all required tests pass against the reviewed code state. Otherwise report NOT CONVERGED with the
specific blockers, missing evidence, and remaining work. Task checkmarks, successful builds, stale
test results, or a manual demonstration alone MUST NOT establish convergence. Repeat until all
mandatory requirements pass; if blocked, report the blocker without claiming completion.

### X. Cross-Platform Architecture

TravelAI 2.0 MUST evolve the existing application incrementally. Changes MUST preserve unrelated
source code, local work, existing user journeys, persisted data, and externally consumed API
behavior. Blanket rewrites, starter resets, and deletion of existing modules to simplify new work
are prohibited. An intentional retirement or incompatible migration MUST document its rationale,
consumer impact, replacement, regression evidence, and rollback plan and receive explicit user approval and maintainer review.
Repository behavior MUST be inspected before planning; README claims alone are not proof of a
working feature. This protects the value and continuity of the existing application.

The web application and administration interface MUST remain React applications. Android and iOS
clients MUST use React Native with Expo. All clients MUST reuse existing backend APIs and domain
rules. Shared portable API types, validation, and client utilities MUST be reused where compatible;
platform UI, navigation, permissions, and camera integration MAY remain separate. Business rules
MUST NOT be independently recreated in each client. Every feature specification MUST identify its
supported platforms and any intentional differences, including accessible interaction and error
states. Mobile delivery MUST extend the existing system without requiring a web rewrite.

Spring Boot MUST own application business rules, authorization, transactions, and persistence through
Spring Data JPA and PostgreSQL. FastAPI MUST own AI inference orchestration and model integration.
Changes MUST inspect existing controllers, services, repositories, and client adapters before adding
an endpoint or abstraction. Reuse or incremental extraction of existing logic is required unless a
reviewed technical reason prevents it. API changes MUST document request and response schemas,
errors, authentication, and compatibility impact. Incompatible changes MUST include a consumer
migration and rollback plan. Clients MUST NOT access the application database directly or acquire
cloud service credentials. This keeps behavior consistent across web, admin, Android, and iOS.

Database and infrastructure choices MUST be validated against the existing repository before
planning changes. PostgreSQL and the current service boundaries are the baseline; any replacement
MUST document compatibility, migration, operational impact, and explicit user approval for any
destructive step. Platform compatibility MUST be verified for every affected web, Android, and iOS
consumer; source reuse alone is not evidence of runtime compatibility.

### XI. Governance at Every Stage

ALL specification, clarification, planning, checklist generation, task generation, analysis,
implementation, testing, review, and convergence activities MUST check compliance with this
constitution. Violations are blocking issues. Exceptions MUST be recorded and explicitly approved
by the user before dependent work proceeds. No stage MAY silently waive a rule, invent an approval,
or treat elapsed time as consent. Constitution amendments MUST remain limited to governance;
feature implementation MUST occur only in a separately authorized implementation activity.

## Architecture and Technology Constraints

The repository inspection baseline at adoption is:

- `frontend/`: existing React, Vite, and Tailwind customer web application with detection,
  destination, hotel and tour booking, payment UI, feed, profile, messages, and notifications routes.
- `admin/`: separate React and Vite administration application for management and moderation.
- `apps/mobile/`: React Native and Expo Router starter; Android/iOS business feature parity is a
  target, not an established capability.
- `backend/`: Spring Boot with JPA, PostgreSQL, REST controllers, and WebSocket messaging;
  existing business behavior spans controllers, repositories, and services.
- `ai-service/ai/main.py`: FastAPI recognition service using Google Cloud Vision with supplementary
  enrichment. The web AI adapter calls FastAPI directly; Spring Boot's `/api/ai/detect` currently
  contains filename heuristics and is not an equivalent inference implementation.
- YOLO inference and a Kaggle training workflow were not found in the inspected application source.
  They are architectural targets governed by this constitution, not completed features.
- Web and admin package scripts expose builds without automated test commands; a Spring Boot
  context-loading test exists. These are baseline gaps, not evidence of regression coverage.

Future plans MUST account for these actual boundaries and MUST NOT assume the backend AI endpoint
already proxies FastAPI. Any change to AI routing MUST document client compatibility and service
security. Dependency upgrades MUST verify compatibility within each application; shared React code
MUST account for the distinct web and mobile dependency trees. Existing supplementary functionality
MUST remain intact unless an approved migration explicitly changes it. No particular YOLO release,
training dataset, hardware target, or numerical quality threshold is mandated without feature-level
evaluation and documented selection.


Google Cloud Vision MUST remain the primary landmark recognition provider. YOLO MUST be the model
family for real-time Vietnamese cultural object detection. These tasks MUST have distinct labels,
contracts, and evaluation sets; generic object labels MUST NOT be presented as verified landmarks
or authoritative cultural facts. Existing supplementary AI enrichment MAY be preserved behind
explicit service boundaries. Responses MUST communicate confidence, detection provenance, and
unknown or unsupported results. Provider outages, low confidence, and malformed images MUST have
explicit error or fallback behavior. Fabricated confidence or filename heuristics MUST NOT be
represented as production inference. Before delivery, each recognition feature MUST define and
measure accuracy and latency acceptance thresholds on representative data and target devices;
real-time claims MUST include measured frame rate and end-to-end latency.

Kaggle MUST be the training and experimentation environment for custom cultural object models.
Training runs MUST record dataset origin and permitted use, label definitions, dataset version,
train/validation/test splits, preprocessing, configuration, seeds, dependency versions, and resulting
model artifacts. Test data MUST remain independent of training and tuning. Evaluation MUST report
per-class precision and recall, mAP for object detection, and relevant failure cases for Vietnamese
cultural contexts. Model promotion MUST require the feature's predefined quality and runtime gates,
a versioned artifact, and a rollback path. Production inference MUST load an approved model artifact
without depending on a live Kaggle notebook. Personal images and credentials MUST NOT be uploaded
to Kaggle without explicit user approval and applicable data-use permission.

Provider selection does not authorize a data transfer. Recognition MUST use authorized inputs;
training and evaluation MUST use synthetic, anonymized, or appropriately licensed nonpersonal data.
Production user information and secrets remain prohibited AI-service inputs under Principle II.

## Development Workflow and Quality Gates

1. Inspect affected source and consumers using privacy-preserving reads. Inventory current behavior,
   existing local changes, reusable APIs, infrastructure, and known security or test gaps.
2. Define WHAT, WHO, WHY, requirement identifiers, and measurable acceptance criteria. Resolve
   critical ambiguities through focused clarification before planning.
3. Review and correct the specification; accept a plan only after its constitution check passes.
   Define platform support, data handling, service contracts, test strategy, and AI quality budgets.
4. Generate dependency-ordered tasks with requirement references, completion criteria, and required
   tests. Cross-analyze all applicable governing artifacts and resolve critical findings.
5. Check required checklists before implementation. STOP on any unchecked required item and seek
   user clarification or approval. Confirm explicit approval before destructive changes or external
   transfers. Implement tests before behavior and preserve unrelated code and local work.
6. After each implementation task, run relevant tests and verify acceptance criteria. Record the
   command, reviewed code state, outcome, and limitations. Update completion status only after all
   required verification passes. Refactoring MUST preserve behavior unless explicitly changed by
   an approved requirement; persistence changes MUST include migration and recovery guidance.
7. Before merge, run affected builds, configured lint/type checks, and relevant automated unit,
   integration, contract, security, and regression checks. Model changes additionally require
   reproducible evaluation and target-runtime evidence. Address coverage gaps in touched behavior;
   record unrelated gaps as scoped follow-up work. Provide safe structured diagnostics.
8. Compare the delivered code and evidence with every mandatory requirement. Add missing tasks,
   re-run implementation and verification, and repeat the convergence loop. Report CONVERGED only
   with full verified coverage and passing required tests; otherwise report NOT CONVERGED and blockers.

## Governance

This constitution governs ALL TravelAI 2.0 specification, planning, task execution, testing, and
convergence activities, including their supporting clarification, analysis, and review stages.
Every stage MUST record its compliance assessment. Existing nonconforming code is a migration
baseline, not evidence of compliance or permission to introduce new violations. New and modified
behavior MUST comply; broader remediation MUST be tracked without forcing unrelated rewrites.

Amendments MUST propose exact changes, explain rationale and compatibility impact, identify any
migration, and receive explicit user approval and maintainer review before merge. The user's explicit
request to amend the constitution authorizes drafting that amendment; it does not authorize features,
destructive operations, or data transfers. A violation blocks dependent work until corrected or
covered by an explicitly user-approved exception. Exceptions MUST record the rule, scope,
justification, risk, owner, expiration, remediation plan, and approval evidence. An exception MUST NOT
misrepresent a failed test as passing, an unverified task as complete, or incomplete coverage as
CONVERGED. Permanent policy changes require an amendment. Reviewers MUST verify exception validity.

Constitution versions follow semantic versioning: MAJOR for incompatible principle removals or
redefinitions; MINOR for added principles or materially expanded guidance; PATCH for clarifications
without policy changes. The application name “2.0” does not determine the constitution version.
Initial adoption was 1.0.0 on 2026-11-04. Version 2.0.0 introduces incompatible mandatory stage gates
and replaces maintainer-only exceptions with explicit user approval. Later amendments MUST preserve
the ratification date and update the last-amended date. The temporary Sync Impact Report MUST be
removed before the amendment is committed.

**Version**: 2.0.0 | **Ratified**: 2026-11-04 | **Last Amended**: 2026-11-04
