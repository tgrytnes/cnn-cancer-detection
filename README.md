# CNN Cancer Detection (Histopathologic Cancer Detection)

Problem. Identify metastatic cancer in small histopathology image patches — a binary classification task (tumor vs. non-tumor).

Why it matters. Assists pathologists with fast triage of suspicious regions, reducing review time and improving consistency. Emphasizes sensitivity/specificity trade-offs typical in medical imaging.

Objectives.
	•	Establish a baseline (simple CNN).
	•	Compare transfer-learning backbones (e.g., MobileNet/EfficientNet) with rationale.
	•	Tune key hyperparameters (learning rate, batch size, epochs, regularization, augmentation, decision threshold).
	•	Evaluate primarily with AUC (threshold-independent), plus accuracy/PR; analyze errors.
	•	Capture learnings, failures, and improvements with clear next steps.

Data at a glance. Small RGB patches with labels (1=tumor, 0=non-tumor) organized into train/validation/test splits. Apply the same preprocessing to all splits (e.g., normalization; model-specific preprocess_input when using transfer learning).

Plan (high level).
	1.	EDA: show class balance and sample tiles per class; inspect pixel-intensity distributions/artifacts.
	2.	Preprocessing: normalization; justify augmentations (flips/rotations, light color jitter) based on EDA.
	3.	Modeling: baseline CNN → transfer models; use early stopping / learning-rate scheduling.
	4.	Analysis: compare metrics in a results table; plot ROC/PR and learning curves.

---

## 📊 Results (validation split)
| Model                       | Params | Val AUC  | Val Acc |
|----------------------------|:------:|:--------:|:-------:|
| **EfficientNet-B4 (tuned)**| ~17M   | **0.9905** | **0.9600** |
| MobileNetV2                | ~2.3M  | 0.9360   | –       |
| Simple-CNN baseline        | <1M    | –        | –       |

*Prefer highest **AUC** (threshold-independent). Calibrate threshold via ROC/PR if sensitivity is prioritized.*
