# CNN Cancer Detection (Histopathologic Cancer Detection)

Identify metastatic cancer in small image patches. 

---

## Overview
- **Task:** Binary image classification (cancer vs. non-cancer)
- **Goal:** Establish a simple baseline, compare transfer-learning models, report validation metrics, and submit to Kaggle
- **Stack:** TensorFlow/Keras and W&B

---

## 📊 Results (validation split)
| Model                       | Params | Val AUC  | Val Acc |
|----------------------------|:------:|:--------:|:-------:|
| **EfficientNet-B4 (tuned)**| ~17M   | **0.9905** | **0.9600** |
| MobileNetV2                | ~2.3M  | 0.9360   | –       |
| Simple-CNN baseline        | <1M    | –        | –       |

*Prefer highest **AUC** (threshold-independent). Calibrate threshold via ROC/PR if sensitivity is prioritized.*
