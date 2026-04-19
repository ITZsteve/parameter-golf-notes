# Commands

These are the main commands I used while learning the OpenAI Parameter Golf challenge on RunPod.

## Day 1

### Clone the repository

    cd /workspace
    git clone https://github.com/openai/parameter-golf.git
    cd parameter-golf

### Download a small dataset for warm-up

    python3 data/cached_challenge_fineweb.py --variant sp1024 --train-shards 1

### Baseline run

    RUN_ID=baseline_sp1024 \
    DATA_PATH=./data/datasets/fineweb10B_sp1024/ \
    TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
    VOCAB_SIZE=1024 \
    torchrun --standalone --nproc_per_node=1 train_gpt.py

### Download more training shards

    python3 data/cached_challenge_fineweb.py --variant sp1024 --train-shards 10

### Lower learning-rate experiment

    RUN_ID=lr_low_01 \
    DATA_PATH=./data/datasets/fineweb10B_sp1024/ \
    TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
    VOCAB_SIZE=1024 \
    MAX_WALLCLOCK_SECONDS=600 \
    VAL_LOSS_EVERY=200 \
    TRAIN_LOG_EVERY=50 \
    MATRIX_LR=0.02 \
    SCALAR_LR=0.02 \
    TIED_EMBED_LR=0.03 \
    torchrun --standalone --nproc_per_node=1 train_gpt.py

### Warmdown experiment that failed on 1xH100

    RUN_ID=lr_low_wd3600 \
    DATA_PATH=./data/datasets/fineweb10B_sp1024/ \
    TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
    VOCAB_SIZE=1024 \
    MAX_WALLCLOCK_SECONDS=600 \
    VAL_LOSS_EVERY=200 \
    TRAIN_LOG_EVERY=50 \
    MATRIX_LR=0.02 \
    SCALAR_LR=0.02 \
    TIED_EMBED_LR=0.03 \
    WARMDOWN_ITERS=3600 \
    torchrun --standalone --nproc_per_node=1 train_gpt.py

### Lower tied embedding LR experiment

    RUN_ID=lr_low_embed_025 \
    DATA_PATH=./data/datasets/fineweb10B_sp1024/ \
    TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
    VOCAB_SIZE=1024 \
    MAX_WALLCLOCK_SECONDS=600 \
    VAL_LOSS_EVERY=200 \
    TRAIN_LOG_EVERY=50 \
    MATRIX_LR=0.02 \
    SCALAR_LR=0.02 \
    TIED_EMBED_LR=0.025 \
    torchrun --standalone --nproc_per_node=1 train_gpt.py

--------------------------------------------------------------------------------------------------------------

## Day 2

### Moderate warmdown experiment

    RUN_ID=lr_low_wd400 \
    DATA_PATH=./data/datasets/fineweb10B_sp1024/ \
    TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
    VOCAB_SIZE=1024 \
    MAX_WALLCLOCK_SECONDS=600 \
    VAL_LOSS_EVERY=200 \
    TRAIN_LOG_EVERY=50 \
    MATRIX_LR=0.02 \
    SCALAR_LR=0.02 \
    TIED_EMBED_LR=0.03 \
    WARMDOWN_ITERS=400 \
    torchrun --standalone --nproc_per_node=1 train_gpt.py

### Best run so far

    RUN_ID=lr_low_wd500 \
    DATA_PATH=./data/datasets/fineweb10B_sp1024/ \
    TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
    VOCAB_SIZE=1024 \
    MAX_WALLCLOCK_SECONDS=600 \
    VAL_LOSS_EVERY=200 \
    TRAIN_LOG_EVERY=50 \
    MATRIX_LR=0.02 \
    SCALAR_LR=0.02 \
    TIED_EMBED_LR=0.03 \
    WARMDOWN_ITERS=500 \
    torchrun --standalone --nproc_per_node=1 train_gpt.py

### Warmdown 600 experiment

    RUN_ID=lr_low_wd600 \
    DATA_PATH=./data/datasets/fineweb10B_sp1024/ \
    TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
    VOCAB_SIZE=1024 \
    MAX_WALLCLOCK_SECONDS=600 \
    VAL_LOSS_EVERY=200 \
    TRAIN_LOG_EVERY=50 \
    MATRIX_LR=0.02 \
    SCALAR_LR=0.02 \
    TIED_EMBED_LR=0.03 \
    WARMDOWN_ITERS=600 \
    torchrun --standalone --nproc_per_node=1 train_gpt.py

----------------------------------------------------------------------------------------------------------------

## Day 3

### Warmdown 450 experiment

    RUN_ID=lr_low_wd450 \
    DATA_PATH=./data/datasets/fineweb10B_sp1024/ \
    TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
    VOCAB_SIZE=1024 \
    MAX_WALLCLOCK_SECONDS=600 \
    VAL_LOSS_EVERY=200 \
    TRAIN_LOG_EVERY=50 \
    MATRIX_LR=0.02 \
    SCALAR_LR=0.02 \
    TIED_EMBED_LR=0.03 \
    WARMDOWN_ITERS=450 \
    torchrun --standalone --nproc_per_node=1 ./train_gpt.py

### Lower scalar LR experiment

    RUN_ID=lr_low_wd500_scalar015 \
    DATA_PATH=./data/datasets/fineweb10B_sp1024/ \
    TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
    VOCAB_SIZE=1024 \
    MAX_WALLCLOCK_SECONDS=600 \
    VAL_LOSS_EVERY=200 \
    TRAIN_LOG_EVERY=50 \
    MATRIX_LR=0.02 \
    SCALAR_LR=0.015 \
    TIED_EMBED_LR=0.03 \
    WARMDOWN_ITERS=500 \
    torchrun --standalone --nproc_per_node=1 ./train_gpt.py

### Warmdown 525 experiment

    RUN_ID=lr_low_wd525 \
    DATA_PATH=./data/datasets/fineweb10B_sp1024/ \
    TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
    VOCAB_SIZE=1024 \
    MAX_WALLCLOCK_SECONDS=600 \
    VAL_LOSS_EVERY=200 \
    TRAIN_LOG_EVERY=50 \
    MATRIX_LR=0.02 \
    SCALAR_LR=0.02 \
    TIED_EMBED_LR=0.03 \
    WARMDOWN_ITERS=525 \
    torchrun --standalone --nproc_per_node=1 ./train_gpt.py

### QK gain + gradient clipping experiment

    RUN_ID=lr_low_wd500_qk3_clip1 \
    DATA_PATH=./data/datasets/fineweb10B_sp1024/ \
    TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
    VOCAB_SIZE=1024 \
    MAX_WALLCLOCK_SECONDS=600 \
    VAL_LOSS_EVERY=200 \
    TRAIN_LOG_EVERY=50 \
    MATRIX_LR=0.02 \
    SCALAR_LR=0.02 \
    TIED_EMBED_LR=0.03 \
    WARMDOWN_ITERS=500 \
    QK_GAIN_INIT=3.0 \
    GRAD_CLIP_NORM=1.0 \
    torchrun --standalone --nproc_per_node=1 ./train_gpt.py

### Gradient clipping only experiment

    RUN_ID=lr_low_wd500_clip1 \
    DATA_PATH=./data/datasets/fineweb10B_sp1024/ \
    TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
    VOCAB_SIZE=1024 \
    MAX_WALLCLOCK_SECONDS=600 \
    VAL_LOSS_EVERY=200 \
    TRAIN_LOG_EVERY=50 \
    MATRIX_LR=0.02 \
    SCALAR_LR=0.02 \
    TIED_EMBED_LR=0.03 \
    WARMDOWN_ITERS=500 \
    GRAD_CLIP_NORM=1.0 \
    torchrun --standalone --nproc_per_node=1 ./train_gpt.py

### Lower matrix LR experiment

    RUN_ID=lr_low_wd500_mat018 \
    DATA_PATH=./data/datasets/fineweb10B_sp1024/ \
    TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
    VOCAB_SIZE=1024 \
    MAX_WALLCLOCK_SECONDS=600 \
    VAL_LOSS_EVERY=200 \
    TRAIN_LOG_EVERY=50 \
    MATRIX_LR=0.018 \
    SCALAR_LR=0.02 \
    TIED_EMBED_LR=0.03 \
    WARMDOWN_ITERS=500 \
    torchrun --standalone --nproc_per_node=1 ./train_gpt.py

### Best run so far: sequence length 2048

    RUN_ID=seq2048_wd500 \
    DATA_PATH=./data/datasets/fineweb10B_sp1024/ \
    TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
    VOCAB_SIZE=1024 \
    MAX_WALLCLOCK_SECONDS=600 \
    VAL_LOSS_EVERY=200 \
    TRAIN_LOG_EVERY=50 \
    MATRIX_LR=0.02 \
    SCALAR_LR=0.02 \
    TIED_EMBED_LR=0.03 \
    WARMDOWN_ITERS=500 \
    TRAIN_SEQ_LEN=2048 \
    torchrun --standalone --nproc_per_node=1 ./train_gpt.py

    -------------------------------------------------------------------------------------------------------------

## Day 4

### Warmdown 400 experiment + sequence length 2048

    RUN_ID=seq2048_wd400 \
    DATA_PATH=./data/datasets/fineweb10B_sp1024/ \
    TOKENIZER_PATH=./data/tokenizers/fineweb_1024_bpe.model \
    VOCAB_SIZE=1024 \
    MAX_WALLCLOCK_SECONDS=600 \
    VAL_LOSS_EVERY=200 \
    TRAIN_LOG_EVERY=50 \
    MATRIX_LR=0.02 \
    SCALAR_LR=0.02 \
    TIED_EMBED_LR=0.03 \
    WARMDOWN_ITERS=400 \
    TRAIN_SEQ_LEN=2048 \
    torchrun --standalone --nproc_per_node=1 ./train_gpt.py
