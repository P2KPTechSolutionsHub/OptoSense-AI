
# 📈 **OptoSense-AI: Neural Network–Powered pH Prediction**

**OptoSense-AI** is a Python tool for automated **pH estimation and visualization** from optode RGB images — enabling time-resolved and treatment-specific chemical gradient analysis.

---

## 🔑 Features

* Neural network regression (RGB → pH)
* Time-series and batch analysis modes
* Auto dataset creation from calibration images
* Fast model training & prediction (`.keras` model persistence)
* Heatmap export: `.tiff` (matrix) and `.svg` (color map)
* Built-in training loss visualization

---

## ⚙️ Usage

### 🧩 Fast Run (batch mode)

```bash
python main_model_fast_run.py
```

### 🔁 Track History (single sample)

```bash
python track_history.py
```

Outputs are saved to `/ProcessedFigures/` and `/outputs/`.

---

## 📁 Structure

```
main_model_fast_run.py     # Batch processing
track_history.py           # Single-sample tracking
pHCalib/                   # Calibration images
experimental_data/         # Input RGB datasets
ProcessedFigures/          # Fast Run outputs
outputs/                   # Track History outputs
```

---

## 📦 Dependencies

```bash
pip install numpy tensorflow scikit-learn matplotlib opencv-python scikit-image pillow tqdm
```

---

## 📊 Model Summary

| Layer | Units | Activation | Dropout |
| ----- | ----- | ---------- | ------- |
| Dense | 64    | ReLU       | 0.2     |
| Dense | 32    | ReLU       | 0.2     |
| Dense | 1     | Linear     | 0       |

**Loss:** MSE **Optimizer:** Adam **Epochs:** 20 **Batch:** 50

---

## 🖼️ Example Outputs

* `sample_pre.svg` → pH heatmap
* `sample_pre.tiff` → numeric pH matrix
* `training_curve.png` → loss trajectory

Typical validation loss: **~0.0076 pH² units**

---

## 🧪 Applications

* Optode-based pH analysis
* Biological and chemical microreactor visualization
* Educational demonstrations of colorimetric sensing

---

