# PS-15: Skin Lesion Classification (HAM10000)

**Name:** Anish Idhayan  
**Register No.:** RA2311026050078  
**Section:** B  
**Course:** Deep Learning, Challenge Based Learning (Image Classification Challenge)  
**Institution:** SRM Institute of Science and Technology, Tiruchirappalli

## Objective
Classify dermatoscopic images into 7 types of pigmented skin lesion (akiec, bcc, bkl, df, mel, nv, vasc). The dataset is highly imbalanced (nevi are about 67%) and some lesions have several images, so the split is done by `lesion_id` and models are judged by macro F1 instead of accuracy.

## Dataset
HAM10000 (Harvard Dataverse), 10,015 images: https://doi.org/10.7910/DVN/DBW86T  
The images are not included in this repository because of their size. Download them from the link above.

## Method
- Split by `lesion_id` into train 6,691 / validation 1,674 / test 1,650 images, with no lesion overlap (seed 42)
- ImageNet-pretrained ResNet18 and EfficientNet-B0, fine-tuned end to end
- Class-weighted cross-entropy loss for imbalance, with data augmentation and early stopping
- Backbones compared on validation macro F1, then the selected model (ResNet18) evaluated once on the test set
- Grad-CAM used to check that the model looks at the lesion

## Results (test set, ResNet18)
| Metric | Value |
|---|---|
| Accuracy | 0.82 |
| Macro F1 | 0.68 |
| Balanced accuracy | 0.66 |
| Melanoma recall | 0.56 |

## Files
| File | Description |
|---|---|
| `RA2311026050078_PS15.ipynb` | Notebook with all code and outputs |
| `RA2311026050078_PS15_Report.pdf` | Two-page report |
| `split_seed42.csv` | Saved train/val/test split for reproducibility |

## How to reproduce
1. Download HAM10000 (the two image zips and `HAM10000_metadata.csv`) and unzip the images into one folder.
2. Open the notebook in Google Colab with a T4 GPU.
3. Set `DATA_DIR` to that folder and run all cells. The seed is fixed at 42.

Library versions: PyTorch 2.11, torchvision 0.26, scikit-learn 1.6.1.

## Dataset citation
Tschandl P., Rosendahl C., Kittler H. "The HAM10000 dataset, a large collection of multi-source dermatoscopic images of common pigmented skin lesions." Scientific Data 5:180161 (2018).

## Declaration
An AI assistant (Claude) was used to help write the notebook code and draft the report. All results come from my own run.
