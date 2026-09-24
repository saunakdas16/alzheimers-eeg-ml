<div align="center">

# 🧠 EEG-Based Alzheimer's Disease Classification

### MNE-Python • Signal Processing • ICA • Spectral Analysis • Machine Learning

An end-to-end EEG analysis pipeline for investigating Alzheimer's disease from resting-state, eyes-closed EEG using reproducible Python workflows.

<br>

![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python&logoColor=white)
![MNE-Python](https://img.shields.io/badge/MNE--Python-1.13.2-orange)
![NumPy](https://img.shields.io/badge/NumPy-2.x-013243?logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?logo=pandas&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-F7931E?logo=scikitlearn&logoColor=white)
![OpenNeuro](https://img.shields.io/badge/Dataset-OpenNeuro-8A2BE2)

<br>

**Pilot analysis completed on `sub-001` · Full-dataset feature extraction completed**

</div>

---

## 🔬 Project Overview

Alzheimer's disease is associated with alterations in brain activity that can be investigated using electroencephalography (EEG).

This project develops a reproducible computational pipeline for analyzing resting-state, eyes-closed EEG recordings and extracting quantitative spectral features for downstream machine-learning analysis.

The workflow covers the complete analysis path:

**Raw EEG → Quality Inspection → Preprocessing → Artifact Correction → ICA → Spectral Analysis → Epoching → Feature Extraction → Subject-Level Dataset → Machine Learning**

The analysis was first developed and validated on a single pilot participant and was then systematically applied to the complete dataset of 88 participants.

---

## 📊 Dataset

**Dataset:** [OpenNeuro ds004504](https://openneuro.org/datasets/ds004504)

The dataset contains **88 participants**:

| Group | Subjects |
|---|---:|
| Alzheimer's disease (AD) | 36 |
| Frontotemporal dementia (FTD) | 23 |
| Cognitively normal (CN) | 29 |
| **Total** | **88** |

### EEG Recording

- **19 scalp EEG channels**
- **500 Hz** sampling frequency
- Resting-state
- Eyes-closed condition
- Continuous EEG recordings
- 10-20 electrode placement system
- Original recordings stored as EEGLAB `.set` files

The dataset is stored locally and is intentionally **excluded from Git tracking** because of its size.

---

## ⚙️ Analysis Pipeline

### 01. Data Exploration

Initial inspection of:

- Participant demographics
- Diagnostic groups
- EEG recording metadata
- Channel names
- Sampling frequency
- Recording duration
- EEG amplitude
- Channel information
- Electrode montage and spatial positions

### 02. Signal Quality & Preprocessing

The preprocessing workflow includes:

- Raw EEG inspection
- Power-line noise investigation
- 50 Hz notch filtering
- Preparation of data for ICA
- Artifact identification
- ICA-based artifact analysis

### 03. Independent Component Analysis

Independent Component Analysis (ICA) is used to separate statistically independent signal sources from the multichannel EEG recording.

The ICA workflow uses:

- Extended Infomax ICA
- Rank-aware component selection after average referencing
- Reproducible random initialization
- ICLabel-based component classification

ICLabel classifications are used for automated artifact handling. Components classified as `eye blink` with a predicted probability of at least 0.80 are excluded before reconstructing the cleaned EEG signal.

### 04. Epoching

Continuous EEG is segmented into:

**4-second non-overlapping epochs**

This produces shorter, approximately stationary segments suitable for spectral analysis and feature extraction.

### 05. Frequency-Domain Analysis

Power Spectral Density (PSD) is estimated using **Welch's method**.

The analysis focuses on the following frequency bands:

| Band | Frequency Range |
|---|---:|
| Delta | 1–4 Hz |
| Theta | 4–8 Hz |
| Alpha | 8–13 Hz |
| Beta | 13–30 Hz |
| Gamma | 30–45 Hz |

### 06. Relative Power

For each epoch and channel:

<div align="center">

```math
\text{Relative Band Power}
=
\frac{\text{Band Power}}
{\text{Total Power}_{1-45\,\text{Hz}}}
```

</div>

Relative power provides a normalized representation of the contribution of each frequency band to the overall spectral power.

### 07. Spatial Analysis

Topographic representations are used to visualize the spatial distribution of spectral power across the scalp.

This provides a bridge between:

**numerical EEG features ↔ anatomical electrode distribution**

### 08. Subject-Level Features

The epoch-level spectral features are aggregated across the 19 EEG channels and across epochs to obtain subject-level representations.

The subject-level feature vector contains:

- Delta relative power
- Theta relative power
- Alpha relative power
- Beta relative power
- Gamma relative power

Participant metadata such as:

- Diagnostic group
- Age
- MMSE

are retained alongside the EEG features for downstream statistical analysis and machine learning.

---

## 🧪 Pilot Analysis

The first complete workflow was developed and validated using:

**Participant:** `sub-001`

The completed pilot includes:

✅ Raw EEG inspection  
✅ Channel and montage inspection  
✅ Electrode-position visualization  
✅ PSD analysis  
✅ Power-line noise investigation  
✅ 50 Hz notch filtering  
✅ ICA-based artifact analysis  
✅ ICLabel-based artifact classification  
✅ 4-second non-overlapping epoching  
✅ Welch PSD estimation  
✅ Frequency-band power extraction  
✅ Relative-power calculation  
✅ Scalp topographic visualization  
✅ Subject-level feature construction  

The pilot served as a **method-development and validation stage** before the finalized workflow was applied to all 88 participants.

> **Important:** The pilot is not treated as a final disease-classification result. Its purpose is to establish a reproducible preprocessing and feature-extraction pipeline.

---

## 🚀 All-Subject Feature Extraction

The workflow established during the pilot was successfully automated and applied independently to the **complete dataset of 88 participants**.

### Automated Workflow

For each participant, the pipeline performs:

- EEG loading
- 50 Hz notch filtering
- ICA preparation and Extended Infomax ICA
- ICLabel-based artifact classification
- Automatic exclusion of high-confidence eye-blink components
- ICA-based signal reconstruction
- 4-second non-overlapping epoching
- Welch PSD estimation
- Frequency-band power extraction
- Relative-power calculation
- Averaging across EEG channels
- Averaging across epochs
- Subject-level feature construction

### 📊 Final Feature Dataset

The automated pipeline produced a complete subject-level feature matrix containing:

**88 participants × 9 columns**

with **one row representing one participant**.

The dataset includes:

- Subject ID
- Diagnostic group
- Age
- MMSE
- Delta relative power
- Theta relative power
- Alpha relative power
- Beta relative power
- Gamma relative power

The final feature table is saved locally as:

`data/all_subjects_features.csv`

This dataset serves as the input for the subsequent **machine-learning stage**.

---

## 🤖 Machine Learning

The complete subject-level feature matrix has now been generated from all 88 participants. The next stage is to use this dataset for machine-learning analysis.

Planned analyses include:

### Classification

Primary planned comparison:

**Alzheimer's disease (AD) vs Cognitively Normal (CN)**

Potential models:

- Logistic Regression
- Support Vector Machine (SVM)
- Random Forest

### Evaluation

Model performance will be assessed using appropriate metrics including:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- Confusion matrix

### 🔒 Preventing Data Leakage

Because multiple EEG epochs originate from the same participant, epochs from a single subject must **not** be randomly divided between training and test sets.

The machine-learning stage will therefore use:

**subject-wise train/test splitting and subject-wise cross-validation**

This ensures that the model is evaluated on participants whose EEG data were not used during training.

---

## 🧬 Scientific Rationale

EEG-based neurodegenerative disease research often investigates changes in spectral organization and large-scale brain activity.

This project therefore focuses initially on relative spectral power across conventional EEG frequency bands.

Particular attention is given to the distribution of:

**Delta → Theta → Alpha → Beta → Gamma**

rather than relying only on raw amplitude values.

The resulting features can then be investigated statistically and used as inputs for machine-learning models.

---

## 🛠️ Technology Stack

| Tool | Purpose |
|---|---|
| **Python** | Core programming language |
| **MNE-Python** | EEG loading, preprocessing and analysis |
| **NumPy** | Numerical computation |
| **SciPy** | Scientific and signal-processing operations |
| **Pandas** | Metadata and feature-table handling |
| **Matplotlib** | Visualization |
| **Scikit-learn** | Machine learning and evaluation |
| **MNE-ICALabel** | ICA component classification |
| **Jupyter Notebook** | Interactive analysis |
| **Git / GitHub** | Version control and reproducibility |

---

## 📁 Repository Structure

```text
alzheimers-eeg-ml/
│
├── data/                                  # Local EEG dataset (Git ignored)
│
├── notebooks/
│   ├── 01_pilot_analysis.ipynb            # Complete pilot workflow
│   ├── 02_all_subjects_features.ipynb     # Automated feature extraction
│   
├── .gitignore
│
└── README.md
```