# CNN Cancer Detection – Week-3 Notebook
*Kaggle Histopathologic Cancer Detection challenge*

**All experiments, code, and analysis are shown in the accompanying Jupyter notebook in this repository: cnn_cancer_detection.ipynb **

**Problem.** Identify metastatic cancer in small histopathology image patches — a binary classification task (tumor vs. non-tumor).

**Why it matters.** Assists pathologists with fast triage of suspicious regions, reducing review time and improving consistency. Emphasizes sensitivity/specificity trade-offs typical in medical imaging.

**Objectives**
- Establish a baseline (simple CNN).
- Compare transfer-learning backbones (e.g., MobileNet/EfficientNet) with rationale.
- Tune key models/hyperparameters.
- Evaluate primarily with **AUC** (threshold-independent), plus accuracy/PR; analyze errors.
- Capture learnings, failures, and improvements with clear next steps.

**Data at a glance.** Small RGB patches with labels (1=tumor, 0=non-tumor) organized into train/validation/test splits. Apply consistent preprocessing to all splits (e.g., normalization; model-specific `preprocess_input` for transfer models).

**Plan (high level)**
1. **EDA:** class balance; sample tiles per class; pixel-intensity distributions/artifacts.
2. **Preprocessing:** normalization; justify augmentations (flips/rotations, light color jitter) based on EDA.
3. **Modeling:** baseline CNN → transfer models; early stopping & learning-rate scheduling.
4. **Analysis:** compare metrics in a results table; plot ROC/PR and learning curves.

---

## Results (validation split)

| Metric         | Simple CNN   | MobileNetV2 | EfficientNetB4 (frozen) | EfficientNetB4 (fine-tuned) |
|----------------|--------------|-------------|---------------------------|-------------------------------|
| Train Acc      | 85.1%        | 84.9%       | 85.7%                    | 96.9%                         |
| Train AUC      | 92.3%        | 92.0%       | 92.6%                    | 99.44%                        |
| Val Acc        | 82.6%        | 85.6%       | 86.7%                    | 95.95%                        |
| Val AUC        | 90.0%        | 92.7%       | 93.58%                   | 99.00%                        |
| Val Loss       | 41.8%        | 33.5%       | 31.4%                    | 11.3%                         |

*Prefer the model with the highest **AUC** (threshold-independent). If sensitivity is prioritized, calibrate the decision threshold using ROC/PR analyses.*
