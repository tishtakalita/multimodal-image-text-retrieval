# Multimodal Image-Text Retrieval

## Overview
This project explores cross-modal retrieval — given an image, retrieve the most relevant captions, and given a caption, retrieve the most relevant image. Five experiments were conducted on the Flickr8k dataset, progressively upgrading encoder architectures from ResNet18+GRU to ViT-B/16+SBERT. All experiments were trained using symmetric contrastive loss and evaluated using Recall@K and t-SNE visualization.

## Experiments
| Exp | Image Encoder | Text Encoder |
|---|---|---|
| 1 | ResNet18 | GRU |
| 2 | ResNet18 | Bi-GRU |
| 3 | ResNet18 | Bi-GRU + Self-Attention |
| 4 | ResNet18 | Bi-GRU + BERT embeddings | 
| 5 | ViT (vit_base_patch16_224) | SBERT (all-MiniLM-L6-v2) |

## Data
Flickr8k — 8,000 images each with 5 captions (40,000 pairs total). Data is not included in this repository. Download from [Kaggle](https://www.kaggle.com/datasets/adityajn105/flickr8k) and place in `data/` as described in `data/README.md`.

## Methodology
- Same train/test split (80/20) across all experiments 
- Same embedding dimension (256)
- Same loss function across all experiments — symmetric contrastive loss
- Same evaluation metrics — Recall@1, Recall@5, Recall@10 for both Image-to-Text and Text-to-Image directions
- Controlled setup ensures differences in results are due to architecture choices only

## Checkpoints
The `checkpoints/` folder is empty by default. Model checkpoints are not included in this repository due to file size. When you run a notebook, the trained checkpoint will be saved locally to `checkpoints/` automatically.

## Results
| Exp | I→T R@1 | I→T R@5 | I→T R@10 | T→I R@1 | T→I R@5 | T→I R@10 |
|---|---|---|---|---|---|---|
| 1 — ResNet18 + GRU | 0.0068 | 0.0364 | 0.0784 | 0.0100 | 0.0435 | 0.0841 |
| 2 — ResNet18 + Bi-GRU | 0.1075 | 0.2804 | 0.3904 | 0.0791 | 0.2431 | 0.3465 |
| 3 — ResNet18 + Bi-GRU + Attention | 0.1365 | 0.3348 | 0.4497 | 0.1033 | 0.2855 | 0.3994 |
| 4 — ResNet18 + Bi-GRU + BERT | 0.1507 | 0.3589 | 0.4775 | 0.1211 | 0.3323 | 0.4621 |
| 5 — ViT + SBERT | 0.2174 | 0.4719 | 0.5954 | 0.2051 | 0.4562 | 0.5823 |