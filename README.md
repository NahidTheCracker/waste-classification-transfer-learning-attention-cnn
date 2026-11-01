# Waste Image Classification Using Transfer Learning and an Attention-Enhanced Custom CNN: A Comparative Study

Course project for **CSE366 Artificial Intelligence**, Department of Computer Science and Engineering, East West University (Group 08).

## Overview

This project classifies photographs of single waste items into six categories (cardboard, glass, metal, paper, plastic and trash) using the public TrashNet dataset. It compares three pretrained CNNs (MobileNetV2, ResNet50, EfficientNetB0) with and without fine-tuning, a custom CNN trained from scratch, and the same custom CNN with one attention module added.

This is an image-classification study on a controlled benchmark. It does not locate multiple objects in a photo and it does not certify recyclability.

## Project status

| Stage | Content | Status |
|---|---|---|
| Submission 1 | Dataset information, EDA, related work | Done |
| Submission 2 | Pretrained models, with and without fine-tuning | Done |
| Submission 3 | Custom CNN from scratch | Planned |
| Submission 4 | Custom CNN with an attention module | Planned |

## Results so far (Submission 2)

Six runs on the same stratified split (1,768 train / 380 validation / 379 test images), 30 epochs each, one seed. The test set was used once per run, after restoring the best-validation-loss checkpoint.

| Model | Mode | Test accuracy | Macro-F1 |
|---|---|---|---|
| MobileNetV2 | Frozen | 84.17% | 0.821 |
| MobileNetV2 | Fine-tuned | 89.45% | 0.886 |
| ResNet50 | Frozen | 83.38% | 0.817 |
| **ResNet50** | **Fine-tuned** | **93.93%** | **0.938** |
| EfficientNetB0 | Frozen | 91.56% | 0.908 |
| EfficientNetB0 | Fine-tuned | 91.82% | 0.917 |

Frozen mode trains only the new classification head. Fine-tuned mode also unfreezes the last stage(s) of the backbone with a smaller learning rate. Curves, classification reports, confusion matrices and training and testing times for every run are in the Submission 2 notebook.

## Dataset

**TrashNet** by Gary Thung and Mindy Yang, created for Stanford CS 229 (Autumn 2016-17).

- Source: https://github.com/garythung/trashnet
- 2,527 images, six classes, all RGB JPEG, 512 x 384 pixels
- Class counts: cardboard 403, glass 501, metal 410, paper 594, plastic 482, trash 137
- Licence: MIT (stated in the original repository). The repository asks users of the dataset to cite it.

The images are **not** included in this repository. The notebooks download them automatically from the original repository.

## Repository contents

| File | Description |
|---|---|
| `CSE366_Submission1_Dataset_EDA_RelatedWork.ipynb` | Dataset information, EDA, sample images, findings, split manifest and related work |
| `CSE366_Submission2_Pretrained_Models.ipynb` | MobileNetV2, ResNet50 and EfficientNetB0 trained frozen and fine-tuned, with curves, classification reports, confusion matrices, timing and a comparison of all six runs |
| `split_manifest.csv` | Fixed stratified 70/15/15 split (seed 42) reused by all experiments |
| `requirements.txt` | Python packages needed to run the notebooks |

## How to run

**Submission 1** (no GPU needed):

```bash
pip install -r requirements.txt
jupyter notebook CSE366_Submission1_Dataset_EDA_RelatedWork.ipynb
```

Run all cells. The first run downloads the dataset into a local `trashnet_data/` folder.

**Submission 2** (GPU recommended): we ran it on Kaggle with a Tesla T4 GPU. Import `CSE366_Submission2_Pretrained_Models.ipynb` into a Kaggle or Colab notebook, turn on the GPU accelerator and Internet, and run all cells. The six runs take roughly 15-20 minutes on a T4. The notebook downloads TrashNet and `split_manifest.csv` automatically, so `split_manifest.csv` must stay in the root of this repository.

## Key findings

**From the EDA (Submission 1)**

- The dataset is imbalanced: trash has 137 images and paper has 594, a ratio of about 4.3 to 1.
- There are 6 exact duplicate files in 3 groups, and in every group the copies carry different labels. They are kept with their original labels and placed in the same split.
- All images were taken on a plain white background, so results on this benchmark may not carry over to cluttered real-world photographs.

**From the pretrained models (Submission 2)**

- Fine-tuning improved ResNet50 by 10.55 accuracy points and MobileNetV2 by 5.28 points, but changed EfficientNetB0 by only 0.26 points (one test image).
- Trash was the hardest class for the frozen models (F1 between 0.652 and 0.850); the fine-tuned ResNet50 raised it to 0.927.
- The fine-tuned models show a train-validation accuracy gap of about 8-10 points despite augmentation, dropout, weight decay and best-checkpoint selection.
- With only 379 test images (one image is 0.26 points), the order of the top runs should not be treated as certain.

## Team

Group 08: Sadia Afrin, Md. Nahid Howladar, Fahmida Kabir, Tanvir Ahmed

Supervised by Dr. Tania Sultana, Assistant Professor, Department of CSE, East West University.

## Citation

If you use the dataset, please cite the original repository:

G. Thung and M. Yang, "TrashNet: Dataset of images of trash," GitHub repository, https://github.com/garythung/trashnet
