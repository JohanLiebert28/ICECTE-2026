# Falsifying Complexity: Non-Linear Interaction Features for ASD Classification

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](https://www.python.org/)
[![Status](https://img.shields.io/badge/Status-Published-success)](https://ieeexplore.ieee.org/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

## 📌 Overview
**Author:** Hazrot Ali (KUET)  
**Paper:** *Falsifying Complexity: A Non-Linear Interaction Feature Outperforms Canonical and PAC Features for EEG-Based ASD Classification*

This repository contains the official implementation of the research paper presented at **ICECTE-2026**. 

The study addresses the **"Curse of Dimensionality" ($n \ll p$)** in EEG-based Autism Spectrum Disorder (ASD) classification. Instead of relying on "kitchen sink" feature extraction or complex metrics like Phase-Amplitude Coupling (PAC), this work introduces a **falsification-based methodology**. We demonstrate that a simple, data-driven non-linear interaction (**v4-Invented**) significantly outperforms both literature-backed spectral ratios and computationally expensive complex features.

## 📄 Key Contributions
* **Solved Overfitting:** Reduced a 2,476-feature "kitchen sink" model (92.3% CV, 50% Test) to a stable 35-feature baseline (66.6% CV).
* **Methodological Falsification:** Rigorously tested and falsified the assumption that complex features (PAC) or canonical ratios (Theta/Beta) inherently add predictive value.
* **Novel Biomarker:** Identified `asymm_x_dfa` and `delta_beta_ratio` as superior predictors for ASD severity estimation.

## 📂 Repository Structure
| File Name | Description |
| :--- | :--- |
| `preprocessing-pipeline.ipynb` | **Step 1:** Raw EEG cleaning pipeline. Includes Downsampling (250Hz), Bandpass (0.5-45Hz), ICA Artifact Removal, Wavelet Denoising (db4), and AutoReject epoching. |
| `final-feature-extraction.ipynb` | **Step 2:** Extraction of 2,476 features across 7 domains (Spectral Power, Fractal Dimension, Entropy, Asymmetry, PAC, etc.). |
| `feature-aggregation-machine...` | **Step 3:** The core logic. Aggregates features into the v-Linear baseline and runs the comparative analysis (v-Invented vs. v-Literature vs. v-PAC) using 5 ML classifiers. |

## 📊 Dataset
This study utilizes the public **64-channel EEG dataset** from Wang et al. (2017).
* **Subjects:** 34 total (15 ASD, 19 TD).
* **Paradigm:** Passive viewing of visual stimuli (standard vs. deviant images).
* **Source:** [Early and late stage processing abnormalities in autism spectrum disorders](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0178542)

## 📈 Results (Falsification Analysis)
We compared four hypothesis-driven models using a Repeated Stratified K-Fold validation scheme.

| Model Version | Feature Set | Feature Count | Best Classifier | Accuracy (CV) | Adjusted P-Value |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **v-Linear** | Aggregated Baseline | 35 | LogReg | 66.62% | -- |
| **v-Invented (v4)** | **Baseline + Interaction** | **37** | **kNN** | **74.19%** | **0.0002** |
| v-Literature (v6) | Baseline + TBR/DAR | 38 | kNN | 71.29% | 0.0067 |
| v-PAC (v21) | Baseline + Lit + PAC | 62 | kNN | 70.57% | 0.109 |

> **Key Finding:** The complex v-PAC model failed to significantly outperform the simpler v-Invented model ($p=0.109$), proving that added computational complexity was redundant noise for this dataset.

## 🛠️ Installation & Usage
1. Clone the repository:
   ``bash
   git clone [https://github.com/JohanLiebert28/ICECTE-2026.git](https://github.com/hazrotali2003028/ICECTE-2026.git)
   cd ICECTE-2026
2. Install dependencies:
   pip install mne numpy pandas scipy scikit-learn xgboost shap

🔗 Citation
If you use this code or methodology, please cite our paper:
@inproceedings{ali2026falsifying,
  title={Falsifying Complexity: A Non-Linear Interaction Feature Outperforms Canonical and PAC Features for EEG-Based ASD Classification},
  author={Hazrot Ali and Monira Islam},
  booktitle={2026 International Conference on Electrical, Computer and Telecommunication Engineering (ICECTE)},
  year={2026},
  organization={IEEE}
}
