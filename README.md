# BioAltitude-Defender
An offline, Explainable AI (XAI) desktop application for early detection of High-Altitude Pulmonary Edema (HAPE) and Cerebral Edema (HACE) using Physiological & Genomic data. Designed for DRDO Defence Medical Applications.
# 🏔️ BioAltitude Defender (AltMedix AI)

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![Python](https://img.shields.io/badge/python-3.11%2B-yellow.svg)
![Platform](https://img.shields.io/badge/platform-Windows-lightgrey.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

**BioAltitude Defender** is an advanced, AI-powered biomedical desktop application designed for the **early detection of High-Altitude Pulmonary Edema (HAPE)** and **High-Altitude Cerebral Edema (HACE)**. It is specifically designed for high-altitude defence personnel, mountaineers, and medical researchers.

By fusing real-time physiological time-series data (SpO2, Heart Rate, Respiration) with genomic biomarkers, this tool provides an **Explainable AI (XAI)** risk assessment. It operates **completely offline**, making it ideal for deployment in remote, high-altitude environments where internet connectivity is unavailable.

---

## ✨ Key Features

*   🧠 **Multi-Modal AI Engine:** Combines physiological vitals with genomic profiles (DNA markers like STC1, MYLK, VCAM1) using a Random Forest algorithm to predict HAPE/HACE risk.
*   🌍 **Global Interoperability:** Supports both **National (ABDM/DISHA)** standards for India and **International (OMOP/HIPAA)** standards. Data can be loaded in either format.
*   🔍 **Explainable AI (SHAP):** Does not just give a score; it explains *why* a patient is at risk by highlighting the top contributing factors (e.g., SpO2 drop, elevated heart rate).
*   🛠️ **Smart CSV Converter:** Automatically detects, renames, and repairs raw CSV files from any medical device/software, converting them into the required format and synthesizing missing vital signs.
*   🔒 **Zero-Retention Architecture:** Patient data is loaded temporarily into RAM for analysis and is never saved to a local database, ensuring complete data privacy.
*   📄 **Automated PDF Reports:** Generates professional, audit-ready PDF reports containing the risk score, metadata (ABHA ID/Person ID), and SHAP explanations.

---

## 🛠️ Technology Stack

*   **Language:** Python 3.11+
*   **GUI Framework:** PyQt5
*   **Machine Learning:** Scikit-Learn, Pandas, NumPy
*   **Explainability:** SHAP
*   **PDF Generation:** ReportLab
*   **Packaging:** PyInstaller

---

## 📊 Datasets Utilized (For Research & Training)

This software integrates data from globally recognized biomedical repositories to train and validate its models:
*   **Physiological Data:** PhysioNet (BIDMC PPG and Respiration Dataset, Oxygen Saturation Variability).
*   **Genomic Data:** NCBI GEO (GSE52209, GSE103927, GSE46480) for HAPE and Acute Mountain Sickness (AMS) transcriptomic signatures.
*   **International Standards:** OMOP CDM, SNOMED CT, LOINC.
*   **National Standards (India):** ABDM, ICD-10, PM-JAY.

---

## 🚀 How to Use the Software (For End Users)

If you are using the pre-built executable (`BioAltitudeDefender.exe`), follow these steps:

1. **Launch the App:** Double-click `BioAltitudeDefender.exe`. No installation is required.
2. **Select Standard:** Choose **National (ABDM)** or **International (OMOP)** from the top-left dropdown.
3. **Import Data:**
   * Click **📂 Import CSV** to load a pre-formatted vitals file.
   * Click **🧬 Import Genomic** to load a patient's genomic profile.
   * *(Optional)* Click **🛠️ Smart Import** if you have a raw, unformatted CSV from a medical device. The AI will auto-fix it.
4. **Analyze:** Click **🔍 Predict Risk**. The app will display the risk percentage (LOW, MODERATE, HIGH) and explain the contributing factors.
5. **Export:** Click **📄 Export PDF Report** to save the assessment for medical records.

---

## 💻 Developer Setup (How to Run from Source)

To run the source code, clone the repository and follow these steps:

### 1. Install Requirements
```
python -m venv venv_win
venv_win\Scripts\activate   # On Windows
pip install -r requirements.txt
```
### 2. Generate Processed Data
```
python src/data_loader.py
```
### 3. Run the Application
```
python main.py
```
### 4. Build Standalone EXE
To create a portable Windows executable:
```
python -m PyInstaller --noconfirm --clean --onefile --windowed --name "BioAltitudeDefender" --icon "icon.png" --exclude-module cupy --collect-all shap --collect-all sklearn --collect-all scipy --collect-all joblib --collect-all numba --collect-all llvmlite --collect-all reportlab --hidden-import "src.smart_converter" --hidden-import "src.risk_model" --hidden-import "src.config_loader" --add-data "config.yaml;." --add-data "icon.png;." --add-data "models/risk_model.pkl;models" --add-data "models/feature_names.json;models" --add-data "data/processed/Patient_National_ABDM.csv;data/processed" --add-data "data/processed/Patient_International_OMOP.csv;data/processed" --add-data "data/processed/Patient_Vitals_TimeSeries.csv;data/processed" --add-data "data/processed/Patient_Genomic_Profile.csv;data/processed" main.py
```
⚠️ Disclaimer
This software is a Research Prototype and is NOT a clinically validated medical device. The AI models are trained on synthetic and public research datasets. Do not use this tool for real-world medical diagnosis or treatment without proper validation from regulatory bodies (such as CDSCO or FDA) and collaboration with medical institutions like DRDO-DIPAS or ICMR.
```
```
👨‍💻 Developer: Rohit Ekka

Email: ekkar5092@gmail.com

GitHub: @mrglitchbz2

Developed as a research prototype for Defence Medical Applications (DRDO).
