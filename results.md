# Results

## Current Best

| Run Name | Final val_bpb | Total submission size int8+zlib | Notes |
|---|---:|---:|---|
| `seq2048_wd500` | `1.31473195` | `12464038 bytes` | Best result so far |

## Best Results By Day

| Day | Best Run | Final val_bpb | Notes |
|---|---|---:|---|
| Day 1 | `lr_low_01` | `1.34016755` | Lower learning rates improved over baseline |
| Day 2 | `lr_low_wd500` | `1.32903575` | Moderate warmdown beat local alternatives |
| Day 3 | `seq2048_wd500` | `1.31473195` | Increasing sequence length to `2048` gave the biggest jump |

## Full Experiment Table

| Day | Run Name | Final val_bpb | Status | Main Change |
|---|---|---:|---|---|
| Day 1 | `baseline_sp1024` | `1.34532795` | Baseline | Starter setup |
| Day 1 | `lr_low_01` | `1.34016755` | Better | Lower learning rates |
| Day 1 | `warmdown_3600` | `1.41415815` | Worse | Warmdown too large for `1xH100` |
| Day 1 | `lr_low_embed_025` | `1.34289739` | Worse | Lower tied embedding LR did not help |
| Day 2 | `lr_low_wd400` | `1.32916827` | Better | Moderate warmdown |
| Day 2 | `lr_low_wd500` | `1.32903575` | Better | Best warmdown found |
| Day 2 | `lr_low_wd600` | `1.32972707` | Worse | Slightly worse than `wd500` |
| Day 3 | `lr_low_wd450` | `1.32993010` | Worse | Local warmdown test |
| Day 3 | `lr_low_wd500_scalar015` | `1.33120240` | Worse | Lower scalar LR |
| Day 3 | `lr_low_wd525` | `1.33273870` | Worse | Local warmdown test |
| Day 3 | `lr_low_wd500_qk3_clip1` | `1.33071093` | Worse | QK gain + clipping |
| Day 3 | `lr_low_wd500_clip1` | `1.33456222` | Worse | Clipping only |
| Day 3 | `lr_low_wd500_mat018` | `1.33240370` | Worse | Lower matrix LR |
| Day 3 | `seq2048_wd500` | `1.31473195` | Best so far | Increased `TRAIN_SEQ_LEN` to `2048` |

