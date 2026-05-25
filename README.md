# Multimodal Image-Text Retrieval (Flickr8k)

## Overview
This project explores cross-modal retrieval — given an image, retrieve the most relevant captions, and given a caption, retrieve the most relevant image. Six experiments were conducted on the Flickr8k dataset, progressively upgrading encoder architectures from a simple GRU baseline to a ViT + SBERT setup. All experiments were trained using symmetric contrastive loss and evaluated using Recall@K and t-SNE visualization.

## Experiments
1. Image encoder: ResNet18, Text encoder: GRU
2. Image encoder: ResNet18, Text encoder: Bi-GRU
3. Image encoder: ResNet18, Text encoder: Bi-GRU with self attention
4. Image encoder: ResNet18, Text encoder: Bi-GRU with BERT embedding
5. Image encoder: ViT (vit_base_patch16_224), Text encoder: BERT (SBERT (all-MiniLM-L6-v2))
6. Prompting techniques 

## Data
Flickr8k — 8,000 images each with 5 captions (40,000 pairs total). Data is not included in this repository. Download from [Kaggle](https://www.kaggle.com/datasets/adityajn105/flickr8k) and place in `data/` as described in `data/README.md`.

## Methodology
- Same train/test split (80/20) across all experiments using `random_state=42`
- Same loss function across all experiments — symmetric contrastive loss
- Same evaluation metrics — Recall@1, Recall@5, Recall@10 for both Image→Text and Text→Image directions
- Same embedding dimension (256) for fair comparison
- Controlled setup ensures differences in results are due to architecture choices only

## Results
| Exp | I→T R@1 | I→T R@5 | I→T R@10 | T→I R@1 | T→I R@5 | T→I R@10 |
|---|---|---|---|---|---|---|
| 1 — ResNet18 + GRU | | | | | | |
| 2 — ResNet18 + Bi-GRU | | | | | | |
| 3 — ResNet18 + Bi-GRU + Attention | | | | | | |
| 4 — ResNet18 + Bi-GRU + BERT | | | | | | |
| 5 — ViT + SBERT | | | | | | |
| 6 — BLIP-2 | | | | | | |

## Notebooks
- `01_resnet18_gru.ipynb` — Baseline experiment with ResNet18 image encoder and GRU text encoder
- `02_resnet18_bigru.ipynb` — Upgrades text encoder to Bi-GRU for bidirectional context
- `03_resnet18_bigru_attention.ipynb` — Adds self-attention over Bi-GRU hidden states
- `04_resnet18_bigru_bert.ipynb` — Replaces learned embeddings with frozen BERT representations
- `05_vit_sbert.ipynb` — Upgrades both encoders to pretrained ViT and SBERT
- `06_blip2_prompting.ipynb` — Explores few-shot, chain-of-thought, and self-consistency prompting with BLIP-2

## Status
- [x] Experiment 1 — Complete
- [ ] Experiment 2
- [ ] Experiment 3
- [ ] Experiment 4
- [ ] Experiment 5
- [ ] Experiment 6