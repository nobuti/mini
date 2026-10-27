---
name: peer-spec
description: Turn the current conversation into a spec document stored as Markdown under .idea. Use when the user invokes /peer-spec.
disable-model-invocation: true
---

Synthesize the current conversation and existing codebase understanding into a spec. Do NOT interview the user or start a new research phase.

Use the problem, scope, constraints, and decisions agreed with the user. Do not invent requirements or silently resolve open questions. Record unresolved questions in Further Notes, and distinguish proposed decisions from confirmed ones.

Write the document using the template below and save it to `.idea/<feature-slug>/spec.md`. Use a short, descriptive, lowercase hyphen-separated slug. Reuse the feature slug already agreed in the conversation or used by its existing `.idea/<feature-slug>/` directory so the spec and tickets live under the same feature.

If the spec already exists, update it to reflect the agreement without discarding unrelated content. Do not replace another feature's spec. Write in the language used in the conversation.

Keep the spec concise and concrete. Describe observable behavior and contracts precisely enough to guide tickets and tests. Do not create tickets, publish issues, or implement the solution.

<spec-template>

## Problem Statement

The problem being solved and who faces it, from the user's perspective.

## Solution

The agreed solution, from the user's perspective. Describe the expected behavior and what success looks like.

## User Stories

A numbered list covering the agreed scope. Use this format:

1. As an <actor>, I want a <feature>, so that <benefit>.

Include relevant edge cases and failure behavior discussed in the conversation. Do not expand the scope to make the list longer.

## Implementation Decisions

The decisions made during the conversation, including relevant constraints:

- Modules and responsibilities being added or changed.
- Interfaces, API contracts, and schema changes.
- Architectural decisions and compatibility or security requirements.

Include only relevant items. Do not include specific file paths or code snippets.

## Testing Decisions

How the agreed behavior will be verified:

- Observable outcomes to test, including agreed edge cases and failures.
- Modules or interfaces to test, favoring existing test boundaries.
- Relevant test patterns already identified in the codebase.

Test external behavior, not implementation details. Do not present unconfirmed testing choices as settled decisions.

## Out of Scope

What has explicitly been left out.

## Further Notes

Unresolved questions, assumptions that still need validation, and any other relevant context. State explicitly if there are none.

</spec-template>

After writing, report the document path and highlight any unresolved questions for the user's review.
