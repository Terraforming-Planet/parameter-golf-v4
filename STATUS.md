# V4 Status

## State

V4 is a **clean restart** of this workspace for OpenAI Parameter Golf development.

## Carried-over best verified baseline (from V3)

- `run_id`: `arch_v1_refined`
- `final_val_bpb`: `1.86808647`
- `final_val_loss`: `3.15418576`
- `final_artifact_size_bytes`: `4971557`
- `total_submission_size_int8_zlib`: `5019795`
- `code_size_bytes`: `48238`

This baseline is tracked in `records/best_run/` as V4's starting reference point.

## Current goal

Move from the current ~`1.868` baseline region toward competitive **top-10 / top-tier** territory through disciplined, high-signal iteration.

Project target framing for internal planning (not official leaderboard claims):

- top 10 target zone: `<= 1.115`
- strong contender zone: `<= 1.086`
- active #1 fight zone: `<= 1.080`
- long-shot championship zone: `~1.07x` or lower

## Current constraints

- Keep compatibility with official Parameter Golf workflow.
- FineWeb `val_bpb` remains the official benchmark metric.
- Submission artifact must remain under `16,000,000` bytes.
- Target environment is the official RunPod Parameter Golf template.
- **Custom datasets are frozen for now.**
