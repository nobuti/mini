---
name: tickets
description: Break a spec, plan, or conversation into small, verifiable tickets stored as Markdown files under .idea. Use when the user invokes /tickets.
disable-model-invocation: true
---

Break the agreed work into small vertical slices, each declaring the tickets that block it. Store one Markdown file per ticket under `.idea/<feature-slug>/tickets/`.

## Process

### 1. Gather context

Work from the spec and decisions already in the conversation. If the user provides a local spec path, read it in full. Otherwise, use `SPEC.md` if it exists, or the conversation itself.

Respect the agreed scope, constraints, and contracts. Do not invent requirements or silently resolve open questions. Flag any unresolved decision that prevents a useful breakdown before proceeding.

### 2. Explore the codebase if needed

Use the existing codebase understanding. Inspect the relevant code only if needed to identify dependencies, existing test boundaries, or refactoring that must happen before a slice can be implemented. Respect the project's conventions and architectural decisions.

### 3. Draft vertical slices

- Each ticket delivers a narrow but complete behavior across the layers it needs, including tests. Do not split the work into separate schema, API, and UI tickets by default.
- A completed ticket must be demoable or verifiable on its own.
- Keep each ticket small enough to implement and verify in a single fresh agent context.
- Include any necessary preparatory refactoring before the work that depends on it. Avoid unrelated cleanup.
- Define concrete acceptance criteria based on observable behavior, suitable for implementation with TDD.

For each ticket, identify its blockers: only tickets that genuinely must be completed before it can start. Do not add dependencies just to force a linear sequence. A ticket with no blockers can start immediately.

Wide mechanical refactors are an exception to vertical slicing. If a change cannot land safely in one slice, use expand-contract: add the new form alongside the old, migrate callers in small batches, then remove the old form. Each migration depends on the expansion; removal depends on every migration. Keep tests passing after each ticket. If that is not possible, surface the integration constraint for the user's approval rather than implying the tickets can land independently.

### 4. Review the breakdown with the user

Present a numbered list. For each ticket, show its title, what it delivers, and its blockers.

Ask the user whether the granularity and dependencies are right, and whether any tickets should be merged or split. Highlight any unresolved decisions affecting the breakdown.

Wait for approval before writing files. Revise the breakdown as needed.

### 5. Write the approved tickets

Use `.idea/<feature-slug>/tickets/<NN>-<ticket-slug>.md`, with short, descriptive slugs. Number tickets from `01` in dependency order, blockers first. Numbering is for reference, not an additional dependency.

Use one file per ticket, never a single combined file. If the feature already has tickets, preserve their identifiers and unrelated content. Do not overwrite an existing ticket with different work; continue numbering for new tickets and keep dependency references valid.

Use the template below. Link each blocker to its Markdown file using a relative link. A ticket with no blockers must explicitly say so.

<ticket-template>

# <NN>: <Ticket title>

## What to build

The end-to-end behavior this ticket delivers, from the user's perspective. Describe the relevant contracts and constraints without prescribing a layer-by-layer implementation checklist.

## Acceptance criteria

- [ ] Observable outcome that can be verified with a test.
- [ ] Relevant edge case or failure behavior agreed in the spec.

## Blocked by

- [<NN>: <Blocking ticket title>](<NN>-<blocking-ticket-slug>.md)

Or: None (can start immediately).

</ticket-template>

Avoid specific implementation file paths and code snippets in ticket bodies; they can become outdated. References to the source spec and links to blocking tickets are fine.

After writing, report the created file paths and identify which tickets have no blockers. For subsequent implementation, a ticket can start when all its blockers are complete.

Do not implement the tickets, modify the source spec, or use an external issue tracker.
