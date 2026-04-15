# V4 under-1.10 track

## Why this is the next serious track

This track stays within motifs that are already visible on the official merged leaderboard while keeping the default V4 codepath intact:

- SP4096/SP8192 tokenizers.
- Parallel residual blocks.
- Small depth recurrence on selected layers.
- Muon-side weight decay increase and QK gain initialization at 5.0.

The intent is to create a minimal, legal path from the current V4 baseline toward lower validation BPB without adding custom data or disputed methods.

## Exact experiment commands

### Experiment A

```bash
RUN_ID=v4_sp4096_parallel \
DATA_PATH=./data/datasets/fineweb10B_sp4096 \
TOKENIZER_PATH=./data/tokenizers/fineweb_4096_bpe.model \
VOCAB_SIZE=4096 \
NUM_LAYERS=9 \
MODEL_DIM=512 \
NUM_HEADS=8 \
NUM_KV_HEADS=4 \
MLP_MULT=2 \
PARALLEL_RESIDUAL=1 \
VAL_LOSS_EVERY=0 \
TRAIN_LOG_EVERY=0 \
torchrun --standalone --nproc_per_node=1 train_gpt.py
```

### Experiment B

```bash
RUN_ID=v4_sp4096_parallel_recur \
DATA_PATH=./data/datasets/fineweb10B_sp4096 \
TOKENIZER_PATH=./data/tokenizers/fineweb_4096_bpe.model \
VOCAB_SIZE=4096 \
NUM_LAYERS=9 \
MODEL_DIM=512 \
NUM_HEADS=8 \
NUM_KV_HEADS=4 \
MLP_MULT=2 \
PARALLEL_RESIDUAL=1 \
RECURRENCE_LAYERS=4,5 \
RECURRENCE_STEPS=2 \
VAL_LOSS_EVERY=0 \
TRAIN_LOG_EVERY=0 \
torchrun --standalone --nproc_per_node=1 train_gpt.py
```

### Experiment C

```bash
RUN_ID=v4_sp4096_parallel_recur_wd_qk \
DATA_PATH=./data/datasets/fineweb10B_sp4096 \
TOKENIZER_PATH=./data/tokenizers/fineweb_4096_bpe.model \
VOCAB_SIZE=4096 \
NUM_LAYERS=9 \
MODEL_DIM=512 \
NUM_HEADS=8 \
NUM_KV_HEADS=4 \
MLP_MULT=2 \
PARALLEL_RESIDUAL=1 \
RECURRENCE_LAYERS=4,5 \
RECURRENCE_STEPS=2 \
MUON_WD=0.09 \
QK_GAIN_INIT=5.0 \
VAL_LOSS_EVERY=0 \
TRAIN_LOG_EVERY=0 \
torchrun --standalone --nproc_per_node=1 train_gpt.py
```

### Experiment D

```bash
RUN_ID=v4_sp8192_parallel_recur_wd_qk \
DATA_PATH=./data/datasets/fineweb10B_sp8192 \
TOKENIZER_PATH=./data/tokenizers/fineweb_8192_bpe.model \
VOCAB_SIZE=8192 \
NUM_LAYERS=9 \
MODEL_DIM=512 \
NUM_HEADS=8 \
NUM_KV_HEADS=4 \
MLP_MULT=2 \
PARALLEL_RESIDUAL=1 \
RECURRENCE_LAYERS=4,5 \
RECURRENCE_STEPS=2 \
MUON_WD=0.09 \
QK_GAIN_INIT=5.0 \
VAL_LOSS_EVERY=0 \
TRAIN_LOG_EVERY=0 \
torchrun --standalone --nproc_per_node=1 train_gpt.py
```

## Expected upside

- Parallel residuals can improve optimization efficiency at fixed parameter budget.
- Limited recurrence can increase effective depth with minimal code and memory overhead.
- Higher Muon weight decay and higher initial QK gain are aligned with published leaderboard-style settings.
- SP8192 can reduce tokenization inefficiency versus smaller vocabularies.

## Main risks

- Parallel residual and recurrence together can destabilize early training for some seeds.
- Recurrence increases per-step compute, so wallclock-limited training may lose iterations.
- Muon weight decay at 0.09 can over-regularize on some configurations.
- SP8192 may not dominate SP4096 under strict 10-minute runtime depending on hardware throughput.
