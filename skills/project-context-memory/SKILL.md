---
name: project-context-memory
description: Maintain a portable, evidence-based project context file so work can continue across Codex conversations, projects, and model providers.
metadata:
  short-description: Keep project understanding portable across conversations and models
---

# Project Context Memory

Use this skill when work changes the project's architecture, behavior, decisions, constraints, verification state, or next steps; when the user asks to update project understanding; or when preparing a handoff to another conversation or model.

## Canonical context file

Find the existing context file before creating one. Check these paths in order:

1. `.codex/project-context.md`
2. `PROJECT_CONTEXT.md`
3. `docs/project-context.md`

Use the first existing file and do not create a second competing copy. If none exists, create `PROJECT_CONTEXT.md` at the project root. Keep it ordinary Markdown so it can be read by Codex CLI, the desktop app, VS Code, and other models.

## What to maintain

Keep the context concise and factual. Preserve these sections, adding only what the project needs:

- **Mission and scope** — what the project is for and what is out of scope.
- **Current state** — what works now, what is in progress, and the last verified date.
- **System map** — important modules, data flows, entry points, and external dependencies.
- **Decisions** — dated decisions with the reason and the affected files or interfaces.
- **Constraints** — runtime, compatibility, privacy, licensing, performance, or user requirements.
- **Open questions** — unresolved items, assumptions, and who or what can resolve them.
- **Next handoff** — the smallest useful starting point for the next conversation, including the exact files or commands to inspect.
- **Verification** — checks that passed, checks that were not run, and known limitations.

When a change is made, update the affected section and add a short dated decision or verification note when it changes future work. Remove stale statements instead of accumulating contradictory summaries. Mark inferences as `Assumption` and unknowns as `Unverified`.

## Operating rules

- Read the context file before making a substantial project change, then inspect the source, configuration, and history needed to validate it.
- Update the context after meaningful changes, at the end of a task, and whenever the user asks for a handoff or project-level memory update.
- Record facts that another model can verify from the repository. Do not record hidden chain-of-thought, credentials, access tokens, private keys, or large copied logs.
- Prefer stable file paths, public interface names, and reproducible commands over conversation-specific references.
- Keep user decisions and unresolved choices visible; do not silently turn guesses into requirements.
- If the context conflicts with the code or current user instruction, treat the code and current instruction as authoritative, then correct the context.
- When handing off, update **Next handoff** first and include current status, the next concrete action, blockers, and the relevant paths.

## Handoff response

After updating the file, report its path and state what was added or corrected in one or two sentences. For a new conversation, begin by reading the canonical context file and checking the paths named in **Next handoff** before proposing work.
