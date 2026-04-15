# OpenAI Parameter Golf V4 Workspace

## What this repository is

This repository is a focused workspace for OpenAI Parameter Golf V4 development, evaluation, and submission packaging.

It is organized for reproducibility and technical review, with the official baseline stack and evaluation path treated as the source of truth.

## Current best official V4 baseline result

Official V4 baseline run:

- `run_id`: `v4_official_baseline`
- `final_val_bpb`: `1.34569660`
- `final_val_loss`: `2.7215235`
- `final_artifact_size_bytes`: `12715304`
- `total_submission_size_int8_zlib`: `12762990`

This is the current official baseline reference for this repository.

## Historical V3 reference result

Carried-over V3 reference run:

- `run_id`: `arch_v1_refined`
- `final_val_bpb`: `1.86808647`

This value is maintained for historical continuity only and should not be interpreted as the current V4 baseline.

## Repository layout

- `train_gpt.py` — primary V4 training/evaluation entrypoint.
- `data/` — dataset utilities and data preparation scripts for the official path.
- `records/` — run records and artifacts for tracked evaluations.
- `records/v4_official_baseline/` — canonical record for the current official V4 baseline run.
- `docs/v4/` — V4 technical notes, plans, and workflow documentation.
- `archive/` (if present) — historical or non-active experiment material kept for traceability.

## Official workflow

- V4 uses the official OpenAI Parameter Golf baseline stack as the source of truth.
- Evaluation is run on the official FineWeb path.
- Submission artifact size must stay under 16 MB.
- The main goal is to move from `1.3457` toward competitive territory through disciplined iteration.

## Current objective

- First stabilize and reproduce the official baseline environment.
- Then improve BPB through clean, controlled experiments.
- Custom datasets are not in the main competition path yet.

## Near-term upgrade plan

1. Learning-rate/schedule refinement.
2. Capacity/architecture refinement.
3. Compression/export refinement.
