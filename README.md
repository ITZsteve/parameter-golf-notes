{
# Parameter Golf Notes

I am learning the OpenAI Parameter Golf challenge by running experiments on RunPod and trying to understand how small language models are trained, evaluated, and compressed.

## Challenge Goal

Train a language model that:
- fits under 16MB after compression
- trains within 10 minutes
- gets the lowest possible `val_bpb`

## My Setup

- Platform: RunPod
- GPU: 1x H100
- Codebase: `openai/parameter-golf`

## Current Best Run

- Run name: `lr_low_01`
- Final `val_bpb`: `1.34016755`
- Notes: best result so far after lowering learning rates

## Runs

| Day | Run Name | Change | Final val_bpb | Result | Notes |
|---|---|---|---:|---|---|
| Day 1 | `baseline_sp1024` | Baseline run | `1.34532795` | Baseline | First successful run |
| Day 1 | `lr_low_01` | Lower learning rates | `1.34016755` | Better | Best run so far |
| Day 1 | `warmdown_3600` | Added `WARMDOWN_ITERS=3600` | `1.41415815` | Worse | Did not fit well on 1xH100 |
| Day 1 | `lr_low_embed_025` | Lowered `TIED_EMBED_LR` to `0.025` | `1.34289739` | Worse | Slightly worse than best run |

## What I Learned

### Day 1
- Lower `val_bpb` is better.
- The final compressed score matters most.
- Small learning-rate changes can improve results.
- A trick that helps on one setup may fail on another.
- It is better to change one thing at a time.

}
