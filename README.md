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





### Day 1
- Lower `val_bpb` is better.
- The final compressed score matters most.
- Small learning-rate changes can improve results.
- A trick that helps on one setup may fail on another.

### Day 2
- Read key parts of `train_gpt.py` to understand how my command-line variables map into the code.
- Confirmed that my experiments so far were changing training behavior, not the model architecture itself.
- Learned that `MATRIX_LR`, `SCALAR_LR`, and `TIED_EMBED_LR` control different parameter groups in the optimizer setup.
- Learned that `WARMDOWN_ITERS` changes how the learning rate cools down near the end of training.
- Found that very large warmdown values like `3600` do not fit my `1xH100` setup well because my run only reaches around `~1180` steps in 10 minutes.
- Best run of the day: `lr_low_wd500`
- Best score so far: `final_int8_zlib_roundtrip_exact val_bpb = 1.32903575`

### Day 3
- Continued from the previous best run: `lr_low_wd500` with `final_int8_zlib_roundtrip_exact val_bpb = 1.32903575`.
- Tested a few small local changes around the warmdown and optimizer settings.
- Nearby warmdown values and extra optimizer tweaks did not beat the best run from Day 2.
- The biggest improvement came from increasing `TRAIN_SEQ_LEN` from `1024` to `2048` while keeping the proven lower-LR + `WARMDOWN_ITERS=500` setup.
- This became the new best run so far.


}
