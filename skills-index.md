---
name: skills-index
description: Master index of all available skills with triggers and references. Load the relevant SKILL.md when a hook matches. Skills without a `last_updated` stamp are inactive.
last_updated: 2026-09-05
repo_version: bdf76c7
---

# Skills Index

This is the single source of truth for all available skills. Do NOT load skill files preemptively. When a hook matches the current task, `read` the referenced SKILL.md. Skills missing a `last_updated` stamp are considered stale/untrusted and MUST NOT be used.

## Memory Recall Hook

Before starting any task, check if the user might be referencing something from a previous session. Use `memory_search` with the user's query. If results surface prior decisions, preferences, bugs, or workflows, surface them explicitly: "We did X before — should I continue with that approach?"

---

## Skills by Phase

### Define Phase

| Stamp | Skill | Hook | Reference |
|-------|-------|------|-----------|
| 2026-05-20 | **interview-me** | Underspecified asks ("build me X" without for whom/why now), user says "interview me" / "grill me" / "are we sure?" / "stress-test my thinking", or you catch yourself silently filling in ambiguous requirements | `skills/interview-me/SKILL.md` |
| 2026-06-25 | **idea-refine** | Vague idea needs sharpening, stress-testing assumptions before committing, want to expand options before converging, user says "ideate" / "refine this idea" / "stress-test my plan" | `skills/idea-refine/SKILL.md` |

### Build Phase

| Stamp | Skill | Hook | Reference |
|-------|-------|------|-----------|
| 2026-09-05 | **mcgyvr** | A scoped coding task can be delegated to the local model ladder (implement a function, fix a bug, write tests, rename, format, lint): author a contract, validate it, run it, read the result file, replan from the findings; user says `/mcgyvr` or "delegate to mcgyvr" | `skills/mcgyvr/SKILL.md` |

### Verify Phase

| Stamp | Skill | Hook | Reference |
|-------|-------|------|-----------|
| 2026-07-19 | **test-driven-development** | Implementing logic, fixing bugs, changing behavior, need to prove code works, bug report arrives | `skills/test-driven-development/SKILL.md` |
| 2026-08-03 | **fab-yt** | User says /fab-yt, wants to extract and verify claims from a YouTube video, or asks to analyze/verify a YouTube video's factual content | `~/.pi/agent/skills/fab-yt/SKILL.md` |

### Meta

| Stamp | Skill | Hook | Reference |
|-------|-------|------|-----------|
| 2026-06-23 | **using-agent-skills** | Starting a session, need to discover which skill applies. This is the meta-skill. Read it first if unsure which skill to use. | `skills/using-agent-skills/SKILL.md` |

### External / npm-provided

| Stamp | Skill | Hook | Reference |
|-------|-------|------|-----------|
| MISSING | **librarian** | Open-source library questions, need implementation details with source references, understanding why something changed, authoritative code-backed answers | `~/.pi/agent/npm/node_modules/pi-web-access/skills/librarian/SKILL.md` |
| 2026-08-11 | **hunk-review** | Reviewing agent-authored diffs in a live Hunk session, navigating files/hunks, adding inline review comments, reloading session contents. Trigger: "review with Hunk", "check the diff in Hunk", "add review notes to Hunk", user has Hunk running. | `~/.npm-global/lib/node_modules/hunkdiff/skills/hunk-review/SKILL.md` |

---

## Usage Protocol

1. **Match hook → read skill.** When a task matches a hook, `read` the referenced SKILL.md. Don't pre-load.
2. **No stamp = dead.** Skills with a `MISSING` stamp are inactive. Skip them.
3. **Memory first.** Before diving into any task, run `memory_search` with the user's query. Surface prior context if found.
4. **Multiple skills chain.** When unsure about sequencing, use the meta-skill (`using-agent-skills`).
5. **Librarian is external.** Its path is in the pi npm directory. It may update independently via `pi update`.
