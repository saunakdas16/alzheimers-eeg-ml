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

**Pilot analysis completed on `sub-001` · Ready for full-dataset processing**

</div>

---

## 🔬 Project Overview

Alzheimer's disease is associated with alterations in brain activity that can be investigated using electroencephalography (EEG).

This project develops a reproducible computational pipeline for analyzing resting-state, eyes-closed EEG recordings and extracting quantitative spectral features for downstream machine-learning analysis.

The workflow covers the complete analysis path:

**Raw EEG → Quality Inspection → Preprocessing → Artifact Correction → ICA → Spectral Analysis → Epoching → Feature Extraction → Subject-Level Dataset → Machine Learning**

The analysis is being developed and validated on a single pilot participant before being scaled systematically to the complete dataset.

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

The pilot workflow uses:

- Infomax ICA
- Extended Infomax
- Rank-aware component selection after average referencing
- Reproducible random initialization
- ICLabel-based component classification

Components are evaluated for potential artifact categories such as ocular, muscular, cardiac, and other non-neural sources before cleaning the EEG signal.

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

**Relative Band Power**

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

The pilot feature vector contains:

- Delta relative power
- Theta relative power
- Alpha relative power
- Beta relative power
- Gamma relative power

Participant metadata such as:

- Diagnostic group
- Age
- MMSE

are retained separately for downstream statistical analysis and machine learning.

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

The pilot serves as a **method-development and validation stage** before applying the finalized workflow to all 88 participants.

> **Important:** The pilot is not treated as a final disease-classification result. Its purpose is to establish a reproducible preprocessing and feature-extraction pipeline.

---

## 🤖 Machine Learning

After validating the pilot workflow, the next stage is to construct a **subject-level feature matrix** from the complete dataset.

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
├── data/                         # Local EEG dataset (Git ignored)
│
├── notebooks/
│   └── 01_pilot_analysis.ipynb   # Complete pilot workflow
│
├── .gitignore
│
└── README.md