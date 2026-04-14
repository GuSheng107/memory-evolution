# Compression Policy

## Thresholds

- soft threshold: `memory.md + corrections.md` in one scope is over 8,000 characters
- hard threshold: `memory.md + corrections.md` in one scope is over 12,000 characters

## Soft Threshold Behavior

When the soft threshold is exceeded:

- the current task may finish
- task end must evaluate compression
- if there are repeated rules, stale cases, or obvious duplication, compress immediately

## Hard Threshold Behavior

When the hard threshold is exceeded:

- do not keep appending blindly
- compress first, then append
- if it is still too large, remove case detail before removing durable rules

## Compression Order

Always:

1. deduplicate
2. remove one-off commands, one-off cases, and noise
3. merge similar rules
4. promote repeated corrections into `memory.md`
5. shrink `corrections.md` to recent unstable entries

## Compression Target

`memory.md` should stay:

- compact
- durable
- rule-oriented

`corrections.md` should stay:

- recent
- unstable
- limited to a small number of necessary cases

## Scope Safety

Even during compression:

- current user instruction still wins
- project memory still wins over global memory
- do not rewrite global memory just because a project conflicts with it
