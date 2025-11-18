# AFML CamVid Semantic Segmentation Project  
Fast-SCNN Baseline + BiSeNetV2-Lite Improved Model

This repository contains two complete semantic segmentation pipelines using the CamVid dataset.  
Both notebooks are fully automated — just place the dataset ZIP files in the project root and run all.

---

## 1. Environment Setup

### Create virtual environment

**Windows**
```
python -m venv venv
venv\Scripts\activate
```

**Linux/Mac**
```
python3 -m venv venv
source venv/bin/activate
```

### Install dependencies
```
pip install -r requirements.txt
```

---

## 2. Required Libraries (Short Explanations)

| Library | Purpose |
|--------|---------|
| torch | Deep learning training/inference |
| torchvision | Pretrained MobileNetV2 backbone |
| numpy | Array/mask operations |
| Pillow | Image I/O |
| cv2 | Detection bounding box extraction |
| matplotlib | Comparison image generation |
| sklearn | Dataset splitting |
| tqdm | Progress bars |

---

## 3. Download CamVid Dataset

Place these two ZIP files **in the project root**:

- 701_StillsRaw_full.zip  
- LabeledApproved_full.zip  

### Kaggle  
```
https://www.kaggle.com/datasets/carlolepelaars/camvid
```

### Official UCL Links  
Images ZIP:  
```
http://web4.cs.ucl.ac.uk/staff/g.brostow/MotionSegRecData/files/701_StillsRaw_full.zip  
```

Labels ZIP:  
```
http://web4.cs.ucl.ac.uk/staff/g.brostow/MotionSegRecData/data/LabeledApproved_full.zip  
```
---

## 4. Folder Structure After Running Notebooks

```
AFML_PROJECT/
│
├── 701_StillsRaw_full.zip              # Official CamVid raw images (place here)
├── LabeledApproved_full.zip            # Official CamVid raw labels (place here)
├── requirements.txt                    # Python dependencies
├── mapping.txt                         # Class → RGB mapping
│
├── CamVid_Baseline_FastSCNN.ipynb      # Baseline segmentation notebook (Fast-SCNN)
├── CamVid_Improved_BiSeNetV2.ipynb     # Improved segmentation notebook (BiSeNetV2-Lite)
│
├── camvid/
│   ├── images/                         # Extracted + renamed images
│   ├── labels/                         # Extracted + renamed colored labels
│   ├── labels_processed/               # Auto-generated class-ID masks
│   ├── splits/                         # Train/val/test text files (auto-created)
│   ├── raw_images/                     # Raw extracted zip folder (unused after preprocessing)
│   ├── raw_labels/                     # Raw extracted zip folder (unused after preprocessing)
│   └── mapping/                        # JSON mapping saved during preprocessing
│
└── outputs/
    ├── checkpoints/                    # Fast-SCNN trained weights
    ├── comparisons/                    # Baseline: Image | GT | Prediction
    ├── detection/                      # Baseline: simple bounding-box demo (for understanding only)
    ├── bisenet_checkpoints/            # BiSeNetV2-Lite trained weights
    ├── bisenet_comparisons/            # BiSeNetV2: Image | GT | Prediction
    └── bisenet_predictions/            # BiSeNetV2 predicted masks

```

Everything is generated automatically (splits, processed labels, outputs…).

---

## 5. Running the Project

### Fast-SCNN Baseline  
Open **CamVid_Baseline_FastSCNN.ipynb** → Run All.

Outputs stored in:
```
outputs/checkpoints/
outputs/comparisons/
outputs/detection/
```

**Results**
- Best Val mIoU: ~0.5236  
- Test mIoU: ~0.4964  

---

### BiSeNetV2-Lite (Improved Model)  
Open **CamVid_Improved_BiSeNetV2.ipynb** → Run All.

Outputs stored in:
```
outputs/bisenet_checkpoints/
outputs/bisenet_comparisons/
outputs/bisenet_predictions/
```

**Results**
- Best Val mIoU: ~0.6209  
- Test mIoU: ~0.6197  

---

## 6. Model Descriptions

### Fast-SCNN (Baseline)
- Lightweight architecture  
- Fast downsampling + shallow decoder  
- Good speed and moderate accuracy  

### BiSeNetV2-Lite (Improved)
- Two-branch architecture  
- Detail branch → spatial detail  
- Semantic branch → context  
- Uses MobileNetV2 pretrained backbone  
- Higher accuracy than baseline  

---

## 7. Notes
- Both notebooks are **run-all ready**  
- All preprocessing steps are automated  
- No manual renaming or label conversions needed  
- All results appear inside the **outputs/** folder  

---

## 8. License  
CamVid dataset belongs to original authors.  
This project is for academic and research use.

---

