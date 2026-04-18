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




## Runs

| Day | Run Name | Change | Final val_bpb | Result | Notes |
|---|---|---|---:|---|---|
| Day 1 | `baseline_sp1024` | Baseline run | `1.34532795` | Baseline | First successful run |
| Day 1 | `lr_low_01` | Lower learning rates | `1.34016755` | Better | Best run so far |
| Day 1 | `warmdown_3600` | Added `WARMDOWN_ITERS=3600` | `1.41415815` | Worse | Did not fit well on 1xH100 |
| Day 1 | `lr_low_embed_025` | Lowered `TIED_EMBED_LR` to `0.025` | `1.34289739` | Worse | Slightly worse than best run |
|---|---|---|---:|---|---|
| Day 2 | `lr_low_wd400` | Added `WARMDOWN_ITERS=400` to the lower-LR setup | `1.32916827` | Better | Big improvement over earlier runs |
| Day 2 | `lr_low_wd500` | Increased warmdown from `400` to `500` | `1.32903575` | Best so far | Current best run |
| Day 2 | `lr_low_wd600` | Increased warmdown further | `1.32972707` | Worse | Suggests the sweet spot is around `400-500` |



##### What I Learned

### Day 1
- Lower `val_bpb` is better.
- The final compressed score matters most.
- Small learning-rate changes can improve results.
- A trick that helps on one setup may fail on another.
- It is better to change one thing at a time.

### Day 2
- Read key parts of `train_gpt.py` to understand how my command-line variables map into the code.
- Confirmed that my experiments so far were changing training behavior, not the model architecture itself.
- Learned that `MATRIX_LR`, `SCALAR_LR`, and `TIED_EMBED_LR` control different parameter groups in the optimizer setup.
- Learned that `WARMDOWN_ITERS` changes how the learning rate cools down near the end of training.
- Found that very large warmdown values like `3600` do not fit my `1xH100` setup well because my run only reaches around `~1180` steps in 10 minutes.
- Tested moderate warmdown values that better match my real run length.
- Best run of the day: `lr_low_wd500`
- Best score so far: `final_int8_zlib_roundtrip_exact val_bpb = 1.32903575`


}
