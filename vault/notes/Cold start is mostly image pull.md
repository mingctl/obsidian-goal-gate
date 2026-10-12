---
type: note
kind: mechanism
goal: [G1]
status: live
implication: Pre-pull common base images; scheduler tuning won't move cold start much.
supersedes:
superseded_by:
related: []
---
# Cold start is mostly image pull

## What we know
In the example measurements, most cold-start time is spent pulling the image, not waiting on the scheduler.
