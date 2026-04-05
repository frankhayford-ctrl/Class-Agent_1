---
name: checkpoints
description: Index of all saved checkpoints. Appended by checkpoint skill. Used by rollback skill to list available restore points.
type: project
---

# Checkpoint Index

> Appended by the `checkpoint` skill. Read by the `rollback` skill.
> Never delete entries — mark as `[archived]` if no longer needed.

| Label | Timestamp | Git SHA | Entire ID | Notes |
|-------|-----------|---------|-----------|-------|

<!-- Rows appended here by checkpoint skill. Format:
| label | ISO datetime | short SHA | entire-id | user note or auto-label |
-->
