\# EEG-Based Alzheimer's Disease Classification Using MNE-Python \& Machine Learning



An EEG analysis and machine-learning project for investigating Alzheimer's disease using resting-state, eyes-closed EEG, spectral analysis, and reproducible Python-based workflows.



\## Project Overview



This project develops a reproducible pipeline for EEG preprocessing, artifact handling, spectral analysis, topographic visualization, feature extraction, and machine-learning-based classification.



The workflow is first developed and validated on a pilot subject before being systematically applied to the complete dataset.



\## Dataset



\*\*OpenNeuro:\*\* `ds004504`



The dataset contains \*\*88 subjects\*\*:



\- 36 Alzheimer's disease (AD)

\- 23 Frontotemporal dementia (FTD)

\- 29 Cognitively normal (CN)



Recordings contain \*\*19 scalp EEG channels\*\* sampled at \*\*500 Hz\*\* during resting-state, eyes-closed conditions.



The dataset is stored locally and is excluded from Git tracking.



\## Analysis Workflow



Raw EEG  

↓  

Signal \& metadata inspection  

↓  

Montage and electrode verification  

↓  

50-Hz power-line assessment  

↓  

50-Hz notch filtering  

↓  

ICA + ICLabel artifact assessment  

↓  

Artifact component removal  

↓  

4-second fixed-length epochs  

↓  

Welch Power Spectral Density (PSD)  

↓  

Frequency-band power  

↓  

Relative band power  

↓  

Topographic analysis  

↓  

Subject-level feature extraction  

↓  

Machine Learning  

↓  

Model Evaluation



\## Pilot Analysis



The preprocessing and feature-extraction pipeline was developed and validated using \*\*`sub-001`\*\*.



The pilot included:



\- EEG metadata and signal inspection

\- Electrode montage verification

\- Power spectral density analysis

\- Identification and removal of 50-Hz power-line interference

\- Investigation of a narrow 62.5-Hz spectral component

\- ICA-based artifact separation

\- ICLabel-based component classification

\- Removal of high-confidence ocular components

\- 4-second non-overlapping epoching

\- Welch PSD calculation from 1–45 Hz

\- Delta, theta, alpha, beta, and gamma band-power extraction

\- Relative-power calculation

\- Scalp topographic visualization

\- Subject-level feature generation and quality control



The pilot established and tested the processing workflow that will be applied to the full dataset.



\## Frequency Bands



| Band | Frequency |

|---|---|

| Delta | 1–4 Hz |

| Theta | 4–8 Hz |

| Alpha | 8–13 Hz |

| Beta | 13–30 Hz |

| Gamma | 30–45 Hz |



\## Machine Learning



The next stage of the project will construct a \*\*subject-level feature dataset\*\* from all 88 participants.



Planned analysis includes:



\- Feature exploration and statistical analysis

\- Alzheimer's disease vs cognitively normal classification

\- Subject-wise train/test splitting and cross-validation

\- Logistic Regression

\- Support Vector Machine (SVM)

\- Random Forest

\- Accuracy, precision, recall, F1-score, and ROC-AUC

\- Confusion matrices and model comparison



Subject-level separation will be maintained throughout the machine-learning workflow to reduce the risk of data leakage between training and test data.



\## Technologies



\*\*Python · MNE-Python · NumPy · SciPy · Pandas · Matplotlib · Scikit-learn · MNE-ICALabel · Git · GitHub\*\*



\## Repository Structure



&#x20;   alzheimers-eeg-ml/

&#x20;   ├── data/                         # Local dataset; not tracked by Git

&#x20;   ├── notebooks/

&#x20;   │   └── 01\_pilot\_analysis.ipynb

&#x20;   ├── .gitignore

&#x20;   └── README.md



\## Project Status



\### Completed



\- Project and GitHub repository setup

\- Dataset acquisition and organization

\- EEG data exploration

\- Montage and electrode inspection

\- Pilot preprocessing

\- 50-Hz power-line removal

\- ICA/ICLabel artifact assessment

\- Spectral feature extraction

\- Relative-power analysis

\- Topographic visualization

\- Subject-level pilot feature generation

\- Pilot documentation



\### Next



\- Apply the validated pipeline to all 88 subjects

\- Build the complete subject-level feature dataset

\- Perform statistical analysis

\- Develop machine-learning models

\- Evaluate classification performance

