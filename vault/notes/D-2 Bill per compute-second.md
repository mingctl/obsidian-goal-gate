---
type: note
kind: decision
goal: [G0]
status: live
implication: Metering has to record runtime per job, so it moves into G1 scope.
supersedes: "[[D-1 Bill per job run]]"
superseded_by:
related: []
---
# D-2 Bill per compute-second

## Why
In the example, job lengths ranged from seconds to hours, so a flat per-run price was unfair at both ends.
