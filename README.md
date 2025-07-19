# ASR4SCBD

This repository contains the scrubbed codebase for my MSc thesis project regarding the use of deep ASR models in the space of side-channel analysis.
Specifically utilizing wav2vec 2.0 with CTC loss to perform side-channel based disassembly (SCBD) of power-traces.

## Structure

```
asr4scbd/
├── README.md                       
├── code/                           
│   ├── evaluation.ipynb            # Model evaluation and metrics
│   ├── finetune.ipynb              # Fine-tuning pre-trained models
│   ├── pretrain.ipynb              # Pre-training from scratch
│   └── visualization.ipynb         # Data visualization and analysis
├── configs/                        
│   └── *.yaml                      # Training configuration files
├── datasets/                       
├── docker/                         # Workspace container
├── figures/                        # Generated plots and visualizations
└── runs/                           # Model checkpoints and experiment outputs
```

## Development Environment

A local development environment is configured in the ```.devcontainer``` dir, which can be connected to via the VS Code extension Dev Containers.

## Datasets

Datasets can be generated using the ```riscv-power-tools``` repository.
Existing datasets are also available on HuggingFace in the [asr4scbd collection](https://huggingface.co/collections/Duedahl/asr4scbd-687aad716a174f148e88ddb1).

The datasets can be cloned via git:

```bash
git lfs install &&
git clone https://huggingface.co/datasets/Duedahl/full_rvi_mdb datasets/full_rvi_mdb
```

You will need to update the paths used to reference the traces for the existing tooling to work.
E.g. like so:
```bash
cd datasets/full_rvi_mdb &&
fullpath=$(pwd) &&
sed -i "s|\"traces\": \"\./|\"traces\": \"${fullpath}/|g" *.json
```

Similarly, if you want to fetch our best existing model:

```bash
git lfs install &&
git clone https://huggingface.co/Duedahl/wav2vec2_ctc_rvi_mdb runs/wav2vec2_ctc_rvi_mdb
```

## How to Use

The repository is primarily structures around Jupyter Notebooks to allow for interactive testing, but these
notebooks can be converted to regular python scripts like so:

```bash
jupyter nbconvert --no-prompt --to python ./code/pretrain.ipynb &&
jupyter nbconvert --no-prompt --to python ./code/finetune.ipynb
```

The environment required to run these scripts is configured in the fairseq docker container.
To build it run:

```bash
docker compose -f docker/docker-compose.yaml build --no-cache
```

To run pretraining with a specific config, run as below:

```bash
python3 ./code/pretrain.py config=./configs/pretrain-full-a.yaml
```

Analogously, for finetuning run as below:

```bash
python3 ./code/finetune.py config=./configs/finetune-full-a.yaml
```
