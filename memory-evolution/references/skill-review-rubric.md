# Skill Review Rubric

## When To Review Another Skill

If another skill was used in the task, run a lightweight review check at task end.

Enter deep review when any of these are true:

- a critical step is missing
- the skill recommends a stale or wrong command
- a required prerequisite is missing
- failure handling is weak or absent
- validation or acceptance steps are missing
- trigger wording is too narrow or too broad

## Review Questions

1. Is the skill goal still clear?
2. Does the trigger description cover the real usage pattern?
3. Is the workflow missing any branch?
4. Does the skill need a new reference or template?
5. Should the skill be fixed instead of relying on ordinary memory?

## Outcomes

### No Action

Choose this when the mismatch is rare or task-specific.

### Ask Whether To Patch The Skill

Choose this when the skill content is incomplete, stale, or clearly wrong, and the defect is actionable.

When this outcome applies:

- ask the user directly whether they want the skill modified
- if the user agrees, output a concise modification outline
- the outline should name the target skill, the defect, the planned logic change, and the validation steps
- do not silently edit the skill during passive review unless the user explicitly asks for implementation in the current turn

### Record A Temporary Correction

Choose this when it is too early to rewrite the skill, or when the user declines to modify the skill. Record a short-term note in `corrections.md` and re-evaluate after another occurrence.
