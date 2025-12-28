# GEE LULC Research Engine 🌍

![GEE](https://img.shields.io/badge/Google_Earth_Engine-4285F4?style=for-the-badge&logo=googleearthengine&logoColor=white)
![Status](https://img.shields.io/badge/Status-Research_Grade-success?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

## 📖 Overview
The **GEE LULC Research Engine** is a robust, automated dashboard built on Google Earth Engine (GEE) for performing supervised Land Use Land Cover (LULC) classification. 

Unlike standard scripts, this tool is designed for scientific reproducibility. It automates sensor selection, harmonizes data across different satellite generations, and implements rigorous accuracy assessment techniques like **K-Fold Cross-Validation** directly on the server side.

## ✨ Key Features

* **🛰️ Automated Sensor Logic**: Automatically selects **Sentinel-2** (10m) for dates after 2016, or falls back to harmonized **Landsat 5/7/8/9** (30m) for historical analysis.
* **🤖 Multi-Classifier Support**: Instantly toggle between **Random Forest**, **Support Vector Machine (SVM)**, and **CART** to compare model performance.
* **✅ Robust Validation**: Implements **K-Fold Cross-Validation (Server-Side)** for statistically valid accuracy assessment, avoiding the bias of simple train/test splits.
* **📊 Uncertainty Analysis**: Generates **Probability/Confidence Maps** (for RF/SVM) to visualize spatial uncertainty in classification results.
* **🔄 Harmonized Data**: Uses NASA/USGS harmonized collections to ensure consistent spectral signatures across Landsat generations.

## 🚀 How to Use

1.  **Open the Code**: Copy the contents of `LULC_Engine.js` into the Google Earth Engine Code Editor.
2.  **Define Classes**:
    * Draw 4 polygons using the geometry tools.
    * Rename the imports to: `water`, `vegetation`, `builtup`, `bare`.
    * *Note: The script handles the merging and class assignment automatically.*
3.  **Draw ROI**: Draw a polygon over your area of interest.
4.  **Run**: Click "Run Analysis" on the interface.

## 🛠️ Methodology

### 1. Image Pre-processing
The engine queries the `COPERNICUS/S2_SR_HARMONIZED` or `LANDSAT/C02/T1_L2` collections. For Landsat, scaling factors (`0.0000275 * pixel + -0.2`) are applied automatically to ensure surface reflectance values are consistent (0-1 range).

### 2. Cross-Validation
Instead of a static 70/30 split, this tool uses **K-Fold Cross-Validation**. The training data is split into $k$ subsets (folds). The model is trained on $k-1$ folds and validated on the remaining fold. This process is repeated $k$ times, and the mean accuracy is reported.

### 3. Feature Importance & Probability
* **Feature Importance**: Extracts Gini impurity reduction stats from the Random Forest model to identify the most predictive spectral bands.
* **Probability Mode**: Uses `classifier.setOutputMode('PROBABILITY')` to map pixel-level confidence, highlighting areas where the model is "confused" (e.g., mixed pixels).

## 📦 Dependencies
* Google Earth Engine Account
* GEE API (JavaScript)

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👤 Author
**Bipul Roy** *Forestry & GIS Researcher* [LinkedIn Profile](https://linkedin.com/in/your-profile-link)
