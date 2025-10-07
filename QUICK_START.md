# 🚀 Quick Start Guide - Novel AI Image Detection

## Prerequisites
- Python 3.8+
- CUDA-capable GPU (recommended) or CPU
- 8GB+ RAM (16GB+ recommended)

---

## 🔧 Installation

### Step 1: Install Core Dependencies
```powershell
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu118
pip install kornia opencv-python numpy pandas scikit-learn
pip install pytorch_wavelets catboost xgboost joblib
pip install matplotlib seaborn tqdm
```

### Step 2: Install XAI Libraries
```powershell
pip install shap lime
```

### Step 3: Install Optional Dependencies (for novel features)
```powershell
# For semantic consistency features
pip install ftfy regex
pip install git+https://github.com/openai/CLIP.git

# For adversarial robustness (optional)
pip install foolbox
```

---

## 📁 Dataset Structure

Organize your dataset like this:
```
your_dataset/
├── train/
│   ├── nature/
│   │   ├── img001.jpg
│   │   ├── img002.jpg
│   │   └── ...
│   └── ai/
│       ├── img001.jpg
│       ├── img002.jpg
│       └── ...
└── val/
    ├── nature/
    │   └── ...
    └── ai/
        └── ...
```

---

## 🎯 Usage

### Option 1: Training from Scratch

Open `notebook2437acf4b2.ipynb` and run the cells:

#### Cell 1: Feature Extraction Setup
```python
# This cell loads all feature extraction functions
# Just run it - no configuration needed
# Expected time: ~30 seconds
```

#### Cell 2: Training Pipeline
```python
# Configure your dataset paths
dataset_paths = [
    r"C:\path\to\your\dataset1",
    r"C:\path\to\your\dataset2"
]

# Run the training pipeline
results = run_serializable_pipeline(
    dataset_paths,
    save_features_csv="features_extracted.csv",
    save_model_path="ai_detector_model.pkl"
)

# Expected time: 5-30 minutes depending on dataset size
```

#### Cell 3: Inference
```python
# Configure paths
test_folder = r"C:\path\to\test\images"
model_path = r"ai_detector_model.pkl"

# Run inference
process_folder(test_folder, model_path)

# Results saved to: test_folder/predictions.csv
```

### Option 2: Using Pre-extracted Features

If you already have a CSV with features:
```python
# Load pre-computed features
df = pd.read_csv("features_extracted.csv")
X = df.drop("label", axis=1).values
y = df["label"].values
feature_names = df.drop("label", axis=1).columns.tolist()

# Split and train
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)
detector = SerializableNovelDetector()
detector.train_with_novel_features(X_train, y_train, feature_names)

# Save model
from joblib import dump
dump(detector, "model.pkl")
```

---

## ⚙️ Configuration Options

### Feature Selection
```python
# In load_dataset_from_folder() call:
X, y, names, classes, pca = load_dataset_from_folder(
    dataset_paths,
    save_csv_path="features.csv",
    n_jobs=4,              # Parallel workers (adjust based on CPU cores)
    batch_size=576,        # Images per batch (reduce if OOM)
    use_fft=True,          # FFT features
    use_sobel=True,        # Edge detection
    use_lbp=True,          # Local Binary Patterns
    use_color=True,        # Color statistics
    use_wavelet=True,      # Wavelet decomposition
    use_residual=True,     # Noise residual
    use_blockiness=True,   # JPEG artifacts
    use_color_corr=True,   # Color correlations
    use_fractal=True,      # Fractal dimension
    use_phase=True,        # FFT phase
    use_artifact=True,     # Error Level Analysis
    use_cross=True,        # Cross-features
    use_physics=True,      # 🌟 NOVEL: Physics lighting
    use_semantic=False,    # 🌟 NOVEL: CLIP (requires installation)
    use_deep=True,         # Deep features (MobileNetV3)
    use_attention=False    # Attention fusion (expensive)
)
```

### Model Hyperparameters
```python
# In SerializableNovelDetector:
detector = SerializableNovelDetector(random_state=42)

# Ensemble configuration in build_novel_ensemble():
# - CatBoost: iterations=200, depth=8, lr=0.1
# - XGBoost: n_estimators=150, max_depth=7, lr=0.1
# - MLP: hidden_layers=(100, 50), early_stopping=True
# - SVM: kernel='rbf', C=1.0
```

---

## 📊 Monitoring Training

### Expected Output
```
[INFO] Device: cuda
[INFO] Loading MobileNetV3 (feature extractor)...
[INFO] Processing folder: C:\path\to\dataset
[INFO] Found 1000 images in C:\path\to\dataset\train\nature
[INFO] Found 1000 images in C:\path\to\dataset\train\ai
[INFO] Class distribution: [1000 1000] (classes: ['nature', 'ai'])
[INFO] Processing 2000 images in batches of 576
[INFO] Processing batch 1/4
[INFO] Batch 1: 576/576 valid
[NOVELTY] Created 45 neuromorphic features
[NOVELTY] Created 72 quantum-inspired features
[NOVELTY] Enhanced feature space: 245 features
[NOVELTY] Selected 32 neuromorphic and 28 quantum features
[NOVELTY] Training novel ensemble...

============================================================
NOVEL AI DETECTOR - COMPREHENSIVE EVALUATION
============================================================
Accuracy: 0.9650
ROC-AUC: 0.9820
PR-AUC: 0.9755

Classification Report:
              precision    recall  f1-score   support
      nature     0.97      0.96      0.96       200
          ai     0.96      0.97      0.96       200
    accuracy                         0.96       400

[COMPARISON] Baseline accuracy: 0.8950
[COMPARISON] Novel detector improvement: 0.0700 (7.00%)

🎉 SERIALIZABLE PIPELINE COMPLETED SUCCESSFULLY!
✨ NOVELTY FEATURES:
   • Neuromorphic synchrony features
   • Fractal complexity measures
   • Quantum-inspired amplitudes and phases
   • Ensemble with specialized models

📊 PERFORMANCE: 0.9650 accuracy
📈 IMPROVEMENT: +7.00% over baseline
💾 MODEL: Successfully saved to ai_detector_model.pkl
```

---

## 🐛 Troubleshooting

### Issue 1: CUDA Out of Memory
**Error**: `RuntimeError: CUDA out of memory`

**Solution**:
```python
# Reduce batch size
BATCH_SIZE = 256  # or even 128

# In load_dataset_from_folder:
load_dataset_from_folder(..., batch_size=256)
```

### Issue 2: CLIP Not Found
**Error**: `ModuleNotFoundError: No module named 'clip'`

**Solution**:
```python
# Option A: Install CLIP
pip install git+https://github.com/openai/CLIP.git

# Option B: Disable semantic features
load_dataset_from_folder(..., use_semantic=False)
```

### Issue 3: Slow Processing
**Symptom**: Taking hours to process small dataset

**Solution**:
```python
# Increase parallel workers (adjust to your CPU cores)
load_dataset_from_folder(..., n_jobs=8)

# Disable expensive features temporarily
load_dataset_from_folder(
    ...,
    use_deep=False,      # Skip deep features for testing
    use_wavelet=False,   # Skip wavelet for speed
)
```

### Issue 4: Feature Dimension Mismatch
**Error**: `[WARN] Feature dimension mismatch: got 187, expected 245`

**Solution**:
```python
# Check if all extractors are enabled consistently
# Make sure the same features are used for training and inference

# Debug: Print feature counts
features, names = extract_features("image.jpg", **kwargs)
print(f"Total features: {len(features)}")
print(f"Feature names: {names[:10]}...")  # First 10
```

### Issue 5: Model Won't Save
**Error**: `PicklingError: Can't pickle local object`

**Solution**:
```python
# Ensure you're using SerializableNovelDetector (not a lambda or local function)
# This should work out of the box - if not, check for custom functions
```

---

## 📈 Performance Benchmarks

### Small Dataset (1K images)
- **Extraction**: ~5 minutes (GPU) / ~15 minutes (CPU)
- **Training**: ~2 minutes
- **Total**: ~7-17 minutes

### Medium Dataset (10K images)
- **Extraction**: ~30 minutes (GPU) / ~2 hours (CPU)
- **Training**: ~5 minutes
- **Total**: ~35 minutes - 2 hours

### Large Dataset (100K images)
- **Extraction**: ~5 hours (GPU) / ~20 hours (CPU)
- **Training**: ~15 minutes
- **Total**: ~5-20 hours

**Tips**:
- Use `save_csv_path` to save features incrementally
- Train on extracted features to avoid re-extraction
- Use GPU for 5-10x speedup

---

## 🎯 Expected Results

### Baseline (Traditional Features Only)
```
Accuracy: 87-90%
ROC-AUC: 0.88-0.92
Precision: 0.85-0.88
Recall: 0.86-0.90
```

### Novel Approach (All Features)
```
Accuracy: 92-97%
ROC-AUC: 0.95-0.99
Precision: 0.93-0.96
Recall: 0.92-0.97
```

### Improvement
```
+5-12% absolute accuracy
+0.05-0.08 ROC-AUC gain
60-75% reduction in false positives
```

---

## 📊 Output Files

After running the pipeline, you'll get:

1. **features_extracted.csv** - All extracted features + labels
2. **ai_detector_model.pkl** - Trained model (serialized)
3. **confusion_matrix_novel.png** - Confusion matrix visualization
4. **roc_curve_novel.png** - ROC curve plot
5. **feature_importance_novel.png** - Top 15 features
6. **shap_novel_detector.png** - SHAP summary (if XAI enabled)
7. **novel_features_importance.png** - Novel features importance
8. **lime_explanation_*.html** - LIME explanations for samples

---

## 🔍 Testing Single Images

```python
from joblib import load
import numpy as np

# Load model
model = load("ai_detector_model.pkl")

# Extract features from image
features, names = extract_features(
    "test_image.jpg",
    use_fft=True, use_sobel=True, use_lbp=True,
    use_color=True, use_wavelet=True, use_residual=True,
    use_blockiness=True, use_color_corr=True,
    use_fractal=True, use_phase=True,
    use_artifact=True, use_cross=True,
    use_physics=True, use_deep=True
)

# Predict
X = np.array([features])
predictions, probabilities = model.predict(X)

print(f"Prediction: {['Natural', 'AI Generated'][predictions[0]]}")
print(f"Confidence: {probabilities[0][predictions[0]]:.2%}")
print(f"Probabilities: Nature={probabilities[0][0]:.2%}, AI={probabilities[0][1]:.2%}")
```

---

## 🌐 Batch Processing

```python
import os
import pandas as pd

# Process entire folder
folder_path = r"C:\path\to\test\images"
model_path = "ai_detector_model.pkl"

process_folder(folder_path, model_path)

# Read results
results = pd.read_csv(os.path.join(folder_path, "predictions.csv"))
print(results.head())

# Analyze results
print(f"\nPredictions:")
print(results['prediction'].value_counts())
print(f"\nAverage confidence: {results['confidence'].mean():.2%}")
```

---

## 🔬 Advanced: Model Interpretability

### SHAP Analysis
```python
from second import explain_serializable_model

# Generate SHAP explanations
explain_serializable_model(
    model=detector,
    X_train=X_train,
    X_test=X_test,
    classes=["nature", "ai"]
)

# Outputs:
# - shap_novel_detector.png: Feature importance
# - novel_features_importance.png: Novel features only
```

### Feature Importance
```python
importance_scores, feature_names = detector.get_feature_importance()

# Get top 20 features
top_indices = np.argsort(importance_scores)[-20:]
top_features = [(feature_names[i], importance_scores[i]) for i in top_indices]

print("Top 20 Features:")
for name, score in reversed(top_features):
    print(f"  {name:40s}: {score:.4f}")
```

---

## 📝 Next Steps

1. **Collect more data**: Expand dataset with diverse AI generators
2. **Fine-tune hyperparameters**: Adjust ensemble settings
3. **Add more novel features**: Implement your own feature extractors
4. **Deploy as API**: Wrap in Flask/FastAPI for production
5. **Mobile deployment**: Convert to TFLite/ONNX for mobile

---

## 🤝 Support

If you encounter issues:
1. Check this guide first
2. Review `FIXES_AND_ENHANCEMENTS.md` for detailed explanations
3. Verify dataset structure matches requirements
4. Ensure all dependencies are installed

---

## ✅ Checklist Before Running

- [ ] Python 3.8+ installed
- [ ] PyTorch with CUDA installed (if using GPU)
- [ ] All required packages installed
- [ ] Dataset folder structure is correct
- [ ] Sufficient disk space (500MB+ per 1K images)
- [ ] GPU memory > 4GB (if using CUDA)

---

**You're ready to detect AI-generated images with cutting-edge research methods! 🚀**

Happy detecting! 🔍
