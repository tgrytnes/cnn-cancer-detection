CNN Cancer Detection (Histopathologic Cancer Detection)

Identify metastatic cancer in small image patches from digital pathology slides.
This repository contains my Week-3 mini-project for the Histopathologic Cancer Detection Kaggle challenge, structured for clarity, reproducibility, and peer review.

This project aligns with the course deliverables (notebook/report, public GitHub repo, and leaderboard screenshot) and grading rubric covering problem description, EDA, model architecture, results/analysis, conclusion, and organized deliverables.  ￼

⸻

🧭 Project Overview
	•	Task: Binary image classification (cancer vs. non-cancer).
	•	Objective: Build a robust CNN baseline and compare transfer-learning models, report validation metrics, and submit to Kaggle.
	•	Frameworks: TensorFlow/Keras, Weights & Biases (optional).

⸻

📦 Repository Structure

.
├─ notebooks/                 # Jupyter notebooks (EDA, training, evaluation)
├─ src/                       # Minimal helpers (datasets, training loops, utils)
├─ submissions/               # Kaggle CSV submissions
├─ assets/                    # Figures, leaderboard screenshot
├─ requirements.txt
├─ README.md
└─ LICENSE

Large datasets are not tracked in Git. Place data under data/ (ignored) or set DATA_DIR in notebooks.

⸻

⚙️ Setup
	1.	Python environment

python -m venv .venv && source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt

	2.	(Optional) W&B logging

export WANDB_PROJECT=cancer-detection
export WANDB_MODE=online   # or 'offline'

	3.	Kaggle data (CLI)

kaggle competitions download -c histopathologic-cancer-detection -p data/
unzip -q data/histopathologic-cancer-detection.zip -d data/histopathologic-cancer-detection


⸻

🧪 How to Run
	•	EDA: open notebooks/01_eda.ipynb
	•	Training (examples):
	•	notebooks/02_train_simple_cnn.ipynb
	•	notebooks/03_train_mobilenetv2.ipynb
	•	notebooks/04_train_efficientnetb4.ipynb
	•	Inference & submission: notebooks/05_infer_and_submit.ipynb → writes submissions/<timestamp>_submission.csv

Reproducibility
Key seeds used across notebooks:

SEED = 42  # tf, np, python


⸻

📊 Results

Validation (held-out split)

Model	Params	Val AUC	Val Acc	Notes
EfficientNet-B4 (tuned)	~17M	0.9905	0.9600	Best model; strong regularization & LR schedule
MobileNetV2	~2.3M	0.9360	–	Lightweight baseline
Simple-CNN baseline	<1M	–	–	Sanity check model to validate pipeline

Takeaways
	•	Prefer the model with the highest AUC for threshold-independent screening.
	•	Tune threshold using ROC/PR curves if sensitivity is prioritized.
	•	Keep Simple-CNN to guard against data/label issues and regressions.

Kaggle
	•	Competition: Histopathologic Cancer Detection
	•	Screenshot: assets/leaderboard.png (top submission for this repo).
	•	Note: The public leaderboard may be static if the competition is closed; a screenshot is included per the assignment.  ￼

⸻

🏗️ Methods
	•	Data pipeline: TFRecords / tf.data with caching, prefetch, and batched resizing.
	•	Preprocessing: Model-specific preprocessing (e.g., EfficientNet), basic augmentation.
	•	Training:
	•	Optimizers: Adam/AdamW
	•	Loss: Binary Cross-Entropy
	•	Metrics: AUC (primary), Accuracy (secondary)
	•	Callbacks: EarlyStopping (AUC), ModelCheckpoint (val AUC), ReduceLROnPlateau
	•	Hyperparameters (typical starting point):
	•	IMG_SIZE=(224,224), BATCH_SIZE=128, EPOCHS=10, SEED=42

⸻

🚀 Reproduce Best Result
	1.	Train EfficientNet-B4 notebook (04_train_efficientnetb4.ipynb).
	2.	Export the best checkpoint (.h5).
	3.	Run inference notebook (05_infer_and_submit.ipynb) to create submissions/<...>.csv.
	4.	Submit to Kaggle:

kaggle competitions submit -c histopathologic-cancer-detection \
  -f submissions/<your_file>.csv -m "EffNetB4 tuned"


⸻

🧾 Report & Rubric Mapping
	•	Problem & Data → 01_eda.ipynb (brief description + sample exploration).
	•	EDA → Distribution plots, basic cleaning, split rationale.
	•	Model Architecture → Simple-CNN, MobileNetV2, EfficientNet-B4 with justification and hyperparams.
	•	Results & Analysis → Tables/figures, what improved performance, what didn’t, troubleshooting, and tuning summary.
	•	Conclusion → Key learnings, limitations, and future work.
	•	Deliverables → Public repo (this), notebook(s)/pdf report, and leaderboard screenshot.  ￼

⸻

🧰 Practical Notes
	•	Compute: Training was done on GPU; adjust batch size if using CPU.
	•	Class imbalance: Monitor PR curve; consider focal loss or class weights if needed.
	•	Ethics: This is a learning project; clinical deployment would require rigorous validation and oversight.



⸻

If you want, send me your exact notebook filenames and I’ll customize the “How to Run” and “Reproduce Best Result” sections to match your repo.
