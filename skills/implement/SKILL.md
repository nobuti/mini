---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets.

The user should provide the path to a local Markdown ticket, typically `.idea/<feature-slug>/tickets/<NN>-<ticket-slug>.md`. Read the full file and state its title before starting. If no ticket is clearly identified, the reference is ambiguous, or the file cannot be read, ask the user which ticket to implement before proceeding. Do not select a ticket on the user's behalf or use an issue tracker.

Call the Skill tool with "tdd" where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Once done, call the Skill tool with "code-review" to review the work.

Commit your work to the current branch.
