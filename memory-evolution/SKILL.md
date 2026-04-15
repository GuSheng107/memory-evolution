---
name: memory-evolution
description: Handle retrospective review, negative feedback, memory compression, and skill review for IDE coding work. Use after command failures, test failures, runtime or build errors, or when the user says "wrong", "not right", "that is not it", "not what I meant", or equivalent rejection. Also use at task end to inspect whether other skills were used and whether they need updates, and when the user explicitly asks for a retrospective, memory optimization, or skill review. When another skill looks defective, confirm with the user before changing that skill.
---

# Memory Evolution

## Overview

Use this skill after failures, explicit rejection, task completion, or explicit review requests. Decide whether to record a lesson, compress memory, promote a rule, or review a skill used during the task.

When a reviewed skill looks incomplete, stale, or wrong, do not silently patch it during passive review. Ask the user whether they want that skill modified. If the user agrees, output a concise modification outline. If the user declines, follow the normal memory path and record a temporary correction when warranted.

## Read Before Acting

Read in this order:

1. `SKILL.md`
2. `references/triggers-and-outcomes.md`
3. `references/compression-policy.md` when thresholds or compression may matter
4. `references/skill-review-rubric.md` when other skills were used or the user asks for skill review
5. `../memory-governance/memory.md`
6. `../memory-governance/corrections.md`
7. If the project root contains `.ai-memory/`, then read project memory and project corrections

Keep the same precedence:

1. current explicit user instruction
2. project memory
3. global memory

## Mandatory Passive Triggers

Use this skill for:

- command execution failure
- test failure
- runtime error
- build failure
- explicit user rejection such as "wrong", "not right", "that is not it", "not what I meant"
- self-detected mistakes
- explicit retrospective, failure summary, memory optimization, or skill review requests

## End-Of-Task Review

Run a lightweight check after every task:

1. Were any other skills used?
2. If yes, do they show missing steps, stale commands, missing prerequisites, weak failure handling, missing validation, or inaccurate trigger descriptions?
3. If a reviewed skill has a clear defect, should the user be asked whether to modify that skill?
4. Did this task produce a reusable correction, failure lesson, or repeated win?
5. Has memory crossed a compression threshold?

The lightweight check is mandatory. Deep review is conditional on value.

## Workflow

1. Identify the trigger source: failure, rejection, task end, or explicit user request.
2. Classify the issue: ordinary task lesson, memory conflict, memory bloat, or skill quality problem.
3. Choose the scope: global or project.
4. If other skills were used, apply the skill review rubric and decide whether they need changes.
5. If a reviewed skill clearly needs improvement, ask the user whether they want that skill modified.
6. If the user confirms, output a concise modification outline for that skill and wait for the next instruction instead of silently patching it.
7. If the user declines, or if the issue is too early to patch, write a short entry to the correct `corrections.md`.
8. Promote only stable, reusable, repeatedly validated rules to `memory.md`.
9. If memory is over threshold, compress before continuing to append.

## Passive Trigger Phrases

Treat these as explicit rejection:

- "wrong"
- "not right"
- "that is not it"
- "not what I meant"
- "you misunderstood"
- the equivalent Chinese negatives "cuo le", "bu dui", and "bu shi zhe yang"

Do not learn from silence. Do not turn vague dissatisfaction into stable rules.

## Compression Rules

Compression applies to the total characters of `memory.md + corrections.md` within one scope:

- over 8,000 characters: run compression evaluation at task end
- over 12,000 characters: compress before adding more entries

Compression order is fixed:

1. deduplicate
2. remove one-off entries
3. merge similar rules
4. promote repeated corrections into stable memory
5. keep only a small number of recent examples in `corrections.md`

Full details live in `references/compression-policy.md`.

## Skill Review Rules

If another skill was used in the task, do not assume it needs changes. Check whether it:

- missed a critical step
- recommended a stale or wrong command
- missed a prerequisite
- lacks a failure branch
- lacks validation steps
- has trigger wording that is too narrow or too broad

If the skill clearly needs improvement, ask the user whether they want that skill modified.

If the user says yes:

- output a concise modification outline
- include the target skill, the defect, the intended logic change, and the validation plan
- do not silently edit the skill as part of passive review unless the user explicitly asks for the patch in the current turn

If the user says no:

- fall back to the ordinary memory path
- record a temporary correction in `corrections.md` when the lesson is still worth keeping

Full details live in `references/skill-review-rubric.md`.

## Output Style

Report only the high-signal result, for example:

- this is a project-scoped failure lesson and should enter project `corrections.md`
- memory crossed the soft threshold and should be compressed
- another skill used in this task needs review because its failure handling is incomplete
- another skill appears incomplete; ask the user whether to modify it, and if yes provide a modification outline

Do not expand the full compression log unless the user asks for it.
