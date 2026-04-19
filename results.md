# Results

## Current Best

| Run Name | Final val_bpb | Total submission size int8+zlib | Notes |
|---|---:|---:|---|
| `seq2048_wd500` | `1.31473195` | `12464038 bytes` | Best result so far |

## Best Results By Day

| Day | Best Run | Final val_bpb | Notes |
|---|---|---:|---|
| Day 1 | `lr_low_01` | `1.34016755` | 
| Day 2 | `lr_low_wd500` | `1.32903575` | 
| Day 3 | `seq2048_wd500` | `1.31473195` | 

## Full Experiment Table

| Day | Run Name | Final val_bpb | Status | 
|---|---|---:|---|---|
| Day 1 | `baseline_sp1024` | `1.34532795` | Baseline | 
| Day 1 | `lr_low_01` | `1.34016755` | Better | 
| Day 1 | `warmdown_3600` | `1.41415815` | Worse | 
| Day 1 | `lr_low_embed_025` | `1.34289739` | Worse | 
| Day 2 | `lr_low_wd400` | `1.32916827` | Better | 
| Day 2 | `lr_low_wd500` | `1.32903575` | Better | 
| Day 2 | `lr_low_wd600` | `1.32972707` | Worse | 
| Day 3 | `lr_low_wd450` | `1.32993010` | Worse | 
| Day 3 | `lr_low_wd500_scalar015` | `1.33120240` | Worse | 
| Day 3 | `lr_low_wd525` | `1.33273870` | Worse | 
| Day 3 | `lr_low_wd500_qk3_clip1` | `1.33071093` | Worse | 
| Day 3 | `lr_low_wd500_clip1` | `1.33456222` | Worse | 
| Day 3 | `lr_low_wd500_mat018` | `1.33240370` | Worse | 
| Day 3 | `seq2048_wd500` | `1.31473195` | Best so far | 
| Day 4 | `seq2048_wd400` | `1.31598763` | Little worse than last one | 


