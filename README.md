# Waste Image Classification Using Transfer Learning and an Attention-Enhanced Custom CNN: A Comparative Study

Course project for **CSE366 Artificial Intelligence**, Department of Computer Science and Engineering, East West University (Group 08).

## Overview

This project classifies photographs of single waste items into six categories (cardboard, glass, metal, paper, plastic and trash) using the public TrashNet dataset. It compares three pretrained CNNs (MobileNetV2, ResNet50, EfficientNetB0) with and without fine-tuning, a custom CNN trained from scratch, and the same custom CNN with one attention module added.

This is an image-classification study on a controlled benchmark. It does not locate multiple objects in a photo and it does not certify recyclability.

## Project status

| Stage | Content | Status |
|---|---|---|
| Submission 1 | Dataset information, EDA, related work | Done |
| Submission 2 | Pretrained models, with and without fine-tuning | Planned |
| Submission 3 | Custom CNN from scratch | Planned |
| Submission 4 | Custom CNN with an attention module | Planned |

No model results have been produced yet.

## Dataset

**TrashNet** by Gary Thung and Mindy Yang, created for Stanford CS 229 (Autumn 2016-17).

- Source: https://github.com/garythung/trashnet
- 2,527 images, six classes, all RGB JPEG, 512 x 384 pixels
- Class counts: cardboard 403, glass 501, metal 410, paper 594, plastic 482, trash 137
- Licence: MIT (stated in the original repository). The repository asks users of the dataset to cite it.

The images are **not** included in this repository. The notebook downloads them automatically from the original repository.

## Repository contents

| File | Description |
|---|---|
| `CSE366_Submission1_Dataset_EDA_RelatedWork.ipynb` | Dataset information, EDA, sample images, findings, split manifest and related work |
| `split_manifest.csv` | Fixed stratified 70/15/15 split (seed 42) reused by all later experiments |
| `requirements.txt` | Python packages needed to run the notebook |

## How to run

```bash
pip install -r requirements.txt
jupyter notebook CSE366_Submission1_Dataset_EDA_RelatedWork.ipynb
```

Run all cells. The first run downloads the dataset into a local `trashnet_data/` folder.

## Key findings from the EDA

- The dataset is imbalanced: trash has 137 images and paper has 594, a ratio of about 4.3 to 1.
- There are 6 exact duplicate files in 3 groups, and in every group the copies carry different labels. They are kept with their original labels and placed in the same split.
- All images were taken on a plain white background, so results on this benchmark may not carry over to cluttered real-world photographs.

## Team

Group 08: Sadia Afrin, Md. Nahid Howladar, Fahmida Kabir, Tanvir Ahmed

Supervised by Dr. Tania Sultana, Assistant Professor, Department of CSE, East West University.

## Citation

If you use the dataset, please cite the original repository:

G. Thung and M. Yang, "TrashNet: Dataset of images of trash," GitHub repository, https://github.com/garythung/trashnet
