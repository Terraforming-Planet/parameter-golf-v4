# V4 Reference Snapshot for V5

This folder stores the minimal carried-over V4 reference needed to initialize V5 planning.

## Current best carried-over exact result

- `run_id`: `v4_top10_safe`
- `final_val_bpb`: **1.22064591**
- `final_val_loss`: 2.06100949
- `train_seq_len`: 4096
- `iterations`: 5000
- `warmup_steps`: 20
- `max_wallclock_seconds`: 0

## Stable backup reference

- `run_id`: `v4_restore_seq4096_exact`
- `final_val_bpb`: **1.22854984**

V5 starts from this reference context, without copying over broad legacy experiment clutter.
