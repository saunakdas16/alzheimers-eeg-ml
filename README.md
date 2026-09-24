**# EEG-Based Alzheimer's Disease Classification Using MNE-Python \& Machine Learning**



**An EEG analysis and machine-learning project for investigating Alzheimer's disease using resting-state, eyes-closed EEG, spectral analysis, and reproducible Python-based workflows.**



**## Project Overview**



**This project develops a reproducible pipeline for EEG preprocessing, artifact handling, spectral analysis, topographic visualization, feature extraction, and machine-learning-based classification.**



**The workflow is first developed and validated on a pilot subject before being systematically applied to the complete dataset.**



**## Dataset**



**\*\*OpenNeuro:\*\* ds004504**



**The dataset contains \*\*88 subjects\*\*:**



**- 36 Alzheimer's disease (AD)**

**- 23 Frontotemporal dementia (FTD)**

**- 29 Cognitively normal (CN)**



**Recordings contain \*\*19 scalp EEG channels\*\* sampled at \*\*500 Hz\*\* during resting-state, eyes-closed conditions.**



**The dataset is stored locally and is excluded from Git tracking.**



**## Analysis Workflow**



**The project is being developed in stages:**



**1. EEG data exploration**

**2. Electrode montage and channel-position inspection**

**3. EEG preprocessing**

**4. Artifact identification and removal**

**5. Independent Component Analysis (ICA)**

**6. Power spectral density (PSD) analysis**

**7. Epoching**

**8. Frequency-band power extraction**

**9. Relative-power calculation**

**10. Scalp topographic visualization**

**11. Subject-level feature construction**

**12. Feature exploration**

**13. Machine-learning classification**

**14. Subject-wise cross-validation and leakage prevention**

**15. Model evaluation**



**## Pilot Analysis**



**A single subject (`sub-001`) is being used as a pilot to develop and validate the processing workflow before applying it to all 88 subjects.**



**The pilot includes:**



**- Raw EEG inspection**

**- Channel and montage inspection**

**- Power spectral density analysis**

**- Power-line noise investigation**

**- 50 Hz notch filtering**

**- ICA-based artifact analysis**

**- ICLabel-based artifact classification**

**- 4-second non-overlapping epochs**

**- Welch PSD calculation**

**- Delta, theta, alpha, beta, and gamma band-power extraction**

**- Relative band-power calculation**

**- Scalp topographic visualization**

**- Subject-level feature construction**



**The pilot is intended to establish and test the analysis workflow rather than provide a final classification result.**



**## Frequency Bands**



**| Band | Frequency |**

**|---|---|**

**| Delta | 1–4 Hz |**

**| Theta | 4–8 Hz |**

**| Alpha | 8–13 Hz |**

**| Beta | 13–30 Hz |**

**| Gamma | 30–45 Hz |**



**## Feature Extraction**



**For each epoch, spectral power is calculated for the defined frequency bands.**



**Relative power is calculated as:**



**\*\*Relative band power = band power / total power (1–45 Hz)\*\***



**Relative band power is initially averaged across the 19 EEG channels and then across epochs to obtain subject-level spectral features.**



**The resulting subject-level feature representation contains:**



**- Delta relative power**

**- Theta relative power**

**- Alpha relative power**

**- Beta relative power**

**- Gamma relative power**



**Subject metadata such as diagnostic group, age, and MMSE are retained separately for downstream analysis.**



**## Machine Learning**



**The next stage of the project will construct a \*\*subject-level feature dataset\*\* from the complete set of participants.**



**Planned analysis includes:**



**- Feature exploration and statistical analysis**

**- Alzheimer's disease vs cognitively normal classification**

**- Subject-wise train/test splitting**

**- Subject-wise cross-validation**

**- Prevention of data leakage**

**- Machine-learning model training**

**- Model evaluation**



**Potential models include:**



**- Logistic Regression**

**- Support Vector Machine (SVM)**

**- Random Forest**



**Evaluation will include appropriate classification metrics such as accuracy, precision, recall, F1-score, ROC-AUC, and confusion matrices.**



**## Reproducibility**



**The analysis is implemented in Python using tools including:**



**- MNE-Python**

**- NumPy**

**- SciPy**

**- Pandas**

**- Matplotlib**

**- Scikit-learn**

**- MNE-ICALabel**



**The dataset itself is not committed to this repository.**



**## Repository Structure**



**```text**

**alzheimers-eeg-ml/**

**├── data/                  # Local dataset; excluded from Git**

**├── notebooks/             # Analysis notebooks**

**│   └── 01\_pilot\_analysis.ipynb**

**├── .gitignore**

**└── README.md**

