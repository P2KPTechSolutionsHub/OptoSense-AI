

# 📈 **OptoSense-AI: Neural Network–Powered pH Prediction and Visualization**

### 🧠 Overview

**OptoSense-AI** provides automated deep-learning tools for *pH estimation and spatial visualization* from optode RGB images.
It enables high-throughput and time-resolved analysis of chemical gradients in soil, water, and biological systems.

---

### 🔑 **Key Capabilities**

* Time-resolved, treatment-specific pH monitoring
* RGB-to-pH mapping using a trained neural network
* Quantifiable performance metrics (MSE-based)
* Two operational modes:

  * ⚡ **Fast Run Model** – For batch, multi-treatment datasets
  * 🔁 **Track History** – For single-sample, longitudinal monitoring

---

### 🚀 **Features**

* Neural network regression for RGB→pH conversion
* Dataset generation from standard calibration images
* Model persistence (`.keras`) for reuse
* Batch prediction and heatmap generation
* Export in `.tiff` and `.svg` formats
* Training loss visualization for performance assessment

---

### 📂 **Directory Structure**

```
.
├── main_model_fast_run.py       # Entry point for Fast Run
├── track_history.py             # Entry for single-sample mode
├── model.pk00.keras             # Trained model (auto-generated)
├── pHCalib/                     # Standard calibration images (e.g., 6_5.png)
├── experimental_data/           # Experimental input images (*.png)
├── ProcessedFigures/            # Fast Run output visualizations
├── outputs/                     # Track History results
└── README.md                    # This documentation
```

---

### 📦 **Dependencies**

Install all required packages:

```bash
pip install numpy tensorflow scikit-learn matplotlib opencv-python scikit-image pillow tqdm
```

---

### 📁 **Input Data Format**

**Calibration Images (`/pHCalib/`)**

* Format: `.png` or `.tiff`
* Filenames must encode pH value (e.g., `6_5.png` → pH 6.5)

**Experimental Images (`/experimental_data/`)**

* Organized by treatment, timepoint, and replicate
  Example:

  ```
  /experimental_data/
      └── Ctrl/
          ├── SD_1/
          │   ├── R1.png
          │   └── R2.png
  ```

---

### 🔬 **Methodology**

#### 1. Dataset Construction

`create_datasets_from_sample_ph()`

* Loads calibration images
* Crops, normalizes, and labels RGB pixels
* Output: `(N_pixels × N_images, 4)` → [R, G, B, pH]

#### 2. Model Architecture

| Layer | Type  | Units | Activation | Dropout |
| ----- | ----- | ----- | ---------- | ------- |
| 1     | Dense | 64    | ReLU       | 0.2     |
| 2     | Dense | 32    | ReLU       | 0.2     |
| 3     | Dense | 1     | Linear     | 0       |

* **Loss:** Mean Squared Error (MSE)
* **Optimizer:** Adam
* **Epochs:** 20
* **Batch Size:** 50
* **Split:** 90% Train / 10% Test

#### 3. Prediction & Visualization

* Normalize & flatten experimental images
* Predict pH values → reshape to 2D
* Export heatmaps as:

  * `.tiff` (numeric matrix)
  * `.svg` (colorized with `RdYlGn`, pH range 5.4–8.0)

#### 4. Loss Curve Plotting

* `matplotlib` plots training vs validation loss
* Used for evaluating convergence and accuracy

---

### ⚙️ **Execution**

#### **A. Fast Run — Batch Mode**

```bash
python main_model_fast_run.py
```

Performs:

* Dataset creation from `/pHCalib/`
* Model training/loading
* Prediction on all experimental datasets
* Outputs to `/ProcessedFigures/`

**Visualization layout:**
Rows → Raw → Predicted pH → Enhanced Raw → Enhanced pH
Columns → Replicates (R1–R4) × Days (1, 16, 64)

---

#### **B. Track History — Single Sample**

```bash
python track_history.py
```

Performs:

* Dataset creation
* Model training/loading
* Prediction on `.png` images
* Exports results to `/outputs/` as `.svg` and `.tiff`
* Displays final loss curve

---

### 🖼️ **Example Outputs**

* `sample_pre.svg` – Colorized pH heatmap
* `sample_pre.tiff` – Numeric pH matrix
* `training_curve.png` – Training loss trajectory

---

### 📊 **Performance**

* Typical validation loss: ~**0.0076 pH² units** (MSE)
* Resolves subtle spatial pH gradients in:

  * Environmental acidification
  * Biological assays
  * Chemical microreactors

---

### ⚠️ **Limitations**

* Calibration-dependent: valid within the trained pH range (e.g., 5.5–8.0)
* For other pH ranges, retrain with new calibration data

---

### 🧪 **Applications**

* Soil and environmental monitoring
* Biogeochemical visualization
* Microbial or root-zone acidification studies
* Educational demonstrations for colorimetric sensing

---

### 📚 **Citation & Contact**


> **OptoSense-AI:** Neural Network–Based pH Prediction and Visualization
> [Your Name(s)], [Your Institution], 2025.
> DOI / GitHub link: *[to be added]*

📧 Contact: [[your.email@domain.com](mailto:your.email@domain.com)]


