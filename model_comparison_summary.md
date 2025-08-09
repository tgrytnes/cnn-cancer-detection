# Model comparison – summary

**Best validation AUC:** **EffNet-B4 tuned best (17M)** (0.9905). Runner-up: **MobileNetV2 (2.3M)** (0.9360), ΔAUC = 0.0545.
**Highest validation accuracy:** EffNet-B4 tuned best (17M) (0.9600).

## Conclusions
- Prefer the model with the **highest AUC** for deployment; AUC is threshold-independent and robust to class imbalance.
- If screening use-case prioritizes **sensitivity**, consider the model with the highest positive-class recall and adjust the decision threshold accordingly.
- Verify that validation gains translate to the **public LB**; if not, recheck data leakage, augmentation, and thresholding.
- Keep the **Simple-CNN** as a sanity baseline; large deltas vs. baselines are a good sign your transfer models learn meaningful patterns.

## Next steps
- Calibrate thresholds using the validation ROC/PR curves to hit your target recall or precision.
- Run **bootstrap** or **DeLong** tests to check whether AUC differences are statistically significant.
- Log **confusion matrices** and **per-class metrics** (if multi-class in future) to catch asymmetric errors.
- Export a compact report (this table + curves) for stakeholders.