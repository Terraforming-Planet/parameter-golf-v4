# OpenAI Parameter Golf — V5 Workspace

This repository is a **clean V5 workspace** for OpenAI Parameter Golf.

It is organized for professional, competition-focused iteration from a known V4 reference region toward improved validation bits-per-byte (val_bpb), while keeping official-baseline compatibility and reproducibility standards.

## Carried-over V4 reference (historical baseline)

The current strongest carried-over exact reference from V4 is:

- `run_id`: `v4_top10_safe`
- `final_val_bpb`: **1.22064591**
- `final_val_loss`: 2.06100949
- `train_seq_len`: 4096
- `iterations`: 5000
- `warmup_steps`: 20
- `max_wallclock_seconds`: 0

Stable backup reference:

- `run_id`: `v4_restore_seq4096_exact`
- `final_val_bpb`: **1.22854984**

See `records/v4_reference/README.md` for the preserved reference snapshot.

## Current V5 objective

- Beat the carried-over exact reference **1.22064591** cleanly.
- Maintain official-compatible assumptions for training and evaluation.
- Keep iteration loops short, traceable, and audit-ready.

## Future work (deferred in this step)

- **Step 2 (deferred):** auxiliary error/training dataset integration and ZIP export.
- **Step 3 (deferred):** exact RunPod training and evaluation command set.

## Repository layout

- `STATUS.md` — current project state and immediate objectives.
- `docs/v5/` — V5 roadmap, target path, and design principles.
- `records/` — compact, structured experiment record storage.
- `records/v4_reference/` — carried-over V4 baseline reference only.
- `tools/` — utility scripts and operational helpers for V5 workflows.
- `data/` — data notes/placeholders and data-related utilities (no auxiliary dataset added yet in V5 step 1).
- `archive/` — optional historical storage; not the canonical source of truth for active V5 progress.

## Compatibility stance

V5 starts from **official-compatible training/evaluation assumptions** and avoids unverified shortcuts. Any future optimization work should preserve exact run traceability (run IDs, configs, logs, and eval outputs) and prioritize measurable val_bpb improvement.
