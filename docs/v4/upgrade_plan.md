# V4 Upgrade Plan (Disciplined, High-Signal)

## 1) Baseline revalidation first (official RunPod template)

Goal: verify that the carried-over V3 baseline configuration is reproducible in the official environment before any broad changes.

**Command (baseline revalidation):**

```bash
RUN_ID=v4_baseline_revalidate_arch_v1_refined \
DATA_PATH=./data/datasets/fineweb10B_sp1024 \
TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
VOCAB_SIZE=1024 \
NUM_LAYERS=8 \
MODEL_DIM=384 \
NUM_HEADS=8 \
NUM_KV_HEADS=2 \
MLP_MULT=2 \
WARMUP_STEPS=60 \
ITERATIONS=300 \
VAL_LOSS_EVERY=50 \
TRAIN_LOG_EVERY=25 \
torchrun --standalone --nproc_per_node=1 train_gpt.py
```

Acceptance check:
- `val_bpb` should be in the same neighborhood as the carried-over baseline (~1.868 region).
- final artifact size remains safely below 16,000,000 bytes.

---

## 2) Exactly three high-signal experiment tracks

Each variant changes one main idea only.

### Experiment A — Learning-rate split refinement

Main idea: tune learning-rate split only (keep architecture + schedule shape unchanged).

**Command:**

```bash
RUN_ID=v4_expA_lr_split_refine \
DATA_PATH=./data/datasets/fineweb10B_sp1024 \
TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
VOCAB_SIZE=1024 \
NUM_LAYERS=8 \
MODEL_DIM=384 \
NUM_HEADS=8 \
NUM_KV_HEADS=2 \
MLP_MULT=2 \
WARMUP_STEPS=60 \
ITERATIONS=300 \
VAL_LOSS_EVERY=50 \
TRAIN_LOG_EVERY=25 \
LR=0.017 \
EMBED_LR_SCALE=0.30 \
OUTPUT_LR_SCALE=0.20 \
torchrun --standalone --nproc_per_node=1 train_gpt.py
```

Stop criteria:
- Stop after 3 seeds if median improvement is <0.005 `val_bpb` vs baseline.
- Stop early if any run trends unstable (loss spikes/divergence).

### Experiment B — Schedule / warmdown refinement

Main idea: change schedule timing only (warmup/warmdown shape), keep model capacity and optimizer family fixed.

**Command:**

```bash
RUN_ID=v4_expB_schedule_warmdown_refine \
DATA_PATH=./data/datasets/fineweb10B_sp1024 \
TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
VOCAB_SIZE=1024 \
NUM_LAYERS=8 \
MODEL_DIM=384 \
NUM_HEADS=8 \
NUM_KV_HEADS=2 \
MLP_MULT=2 \
WARMUP_STEPS=45 \
WARMUP2_RATIO=0.10 \
WARMDOWN_START=230 \
ITERATIONS=300 \
VAL_LOSS_EVERY=50 \
TRAIN_LOG_EVERY=25 \
torchrun --standalone --nproc_per_node=1 train_gpt.py
```

Stop criteria:
- Stop after 3 seeds if no consistent gain in final `val_bpb`.
- Stop if artifact size or runtime drifts outside submission-safe limits.

### Experiment C — Small capacity bump

Main idea: small model-capacity increase only, while keeping submission size comfortably below cap.

**Command:**

```bash
RUN_ID=v4_expC_small_capacity_bump \
DATA_PATH=./data/datasets/fineweb10B_sp1024 \
TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
VOCAB_SIZE=1024 \
NUM_LAYERS=9 \
MODEL_DIM=416 \
NUM_HEADS=8 \
NUM_KV_HEADS=2 \
MLP_MULT=2 \
WARMUP_STEPS=60 \
ITERATIONS=300 \
VAL_LOSS_EVERY=50 \
TRAIN_LOG_EVERY=25 \
torchrun --standalone --nproc_per_node=1 train_gpt.py
```

Stop criteria:
- Stop immediately if artifact size safety margin becomes tight.
- Stop after 3 seeds if gain is inconsistent or <0.005 median improvement.

---

## 3) Discipline rules for this phase

- No broad speculative architecture changes yet.
- No custom dataset changes in this phase.
- Keep one clear active training path: root `train_gpt.py`.
- Archive historical clutter; avoid re-importing stale experiment complexity into the active path.
