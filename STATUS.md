# V5 Status

## Current state

- V5 is a **clean restart** focused on disciplined, competition-ready execution.
- Scope in this step is repository structure and baseline reference preservation only.

## Carried-over V4 reference

- Best recent exact V4 run:
  - `run_id`: `v4_top10_safe`
  - `final_val_bpb`: **1.22064591**
  - `final_val_loss`: 2.06100949
  - `train_seq_len`: 4096
  - `iterations`: 5000
  - `warmup_steps`: 20
  - `max_wallclock_seconds`: 0
- Stable backup:
  - `run_id`: `v4_restore_seq4096_exact`
  - `final_val_bpb`: **1.22854984**

## Next objective

- Beat **1.22064591** cleanly under official-compatible assumptions.

## Deferred items

- Step 2: auxiliary dataset integration and ZIP export (deferred).
- Step 3: exact RunPod training/evaluation instructions (deferred).
