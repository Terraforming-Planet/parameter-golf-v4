# Parameter Golf V4 Workspace

This repository is a **clean, competition-focused OpenAI Parameter Golf workspace**.

It is aligned to the official challenge workflow in [`openai/parameter-golf`](https://github.com/openai/parameter-golf), with FineWeb `val_bpb` as the primary benchmark metric and the official submission artifact budget of **< 16,000,000 bytes**.

## Objective

V4 starts from a clean baseline and is focused on disciplined progress from a proven carried-over baseline in the ~`1.868` `val_bpb` region toward competitive top-tier performance.

This repository is intended to be:
- reproducible on the official RunPod Parameter Golf template,
- easy to review by challenge/grant/research evaluators,
- explicit about what is official path vs archived history.

## Current carried-over reference baseline (from V3)

Best verified V3 run (carried over as reference baseline):

- `run_id`: `arch_v1_refined`
- `final_val_bpb`: `1.86808647`
- `final_val_loss`: `3.15418576`
- `final_artifact_size_bytes`: `4971557`
- `total_submission_size_int8_zlib`: `5019795`
- `code_size_bytes`: `48238`

> Note: this is a carried-over internal baseline reference, not a claim about current official leaderboard rank.

## Repository layout

- `train_gpt.py` — single primary training/evaluation script for the active V4 path.
- `STATUS.md` — current program status and goals.
- `records/best_run/` — canonical carried-over baseline record for V4 continuity.
- `docs/v4/` — planning docs for the current V4 phase.
- `archive/` — historical material moved out of the active submission path.

## Official benchmark path vs archive

### Active / official-facing path
Use the root-level workflow and `records/best_run/` when revalidating or reporting V4 progress.

### Archived historical material
Legacy experiments and prior record folders are kept under `archive/` for traceability only. They are **not** the active submission path for V4.

## Benchmark policy guardrails

- FineWeb + `val_bpb` remains the official benchmark path.
- Submission artifact must remain under `16,000,000` bytes total.
- No fabricated results.
- No custom dataset integration in this phase.
- Prefer minimal, high-signal, reproducible changes.
