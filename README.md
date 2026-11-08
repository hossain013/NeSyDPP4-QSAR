# NeSyDPP4-QSAR

> A neuro-symbolic AI (Logic Tensor Network) QSAR model that discovers potent DPP-4 inhibitors for type 2 diabetes treatment.

[![DOI](https://img.shields.io/badge/DOI-10.3389%2Ffbinf.2025.1603133-blue)](https://doi.org/10.3389/fbinf.2025.1603133)
[![Journal](https://img.shields.io/badge/Frontiers%20in%20Bioinformatics-2025-green)](https://www.frontiersin.org/journals/bioinformatics/articles/10.3389/fbinf.2025.1603133)
[![License: CC BY](https://img.shields.io/badge/License-CC%20BY-lightgrey)](https://creativecommons.org/licenses/by/4.0/)

## Overview

Dipeptidyl peptidase-4 (DPP-4) is an FDA-approved target for type 2 diabetes mellitus (T2DM), but current DPP-4 inhibitors can cause gastrointestinal issues, severe joint pain, nasopharyngitis, hypersensitivity, and nausea, and *in vivo* screening is costly and often impractical. **NeSyDPP-4** combines neural learning with symbolic, logic-based reasoning to predict DPP-4 bioactivity — accurately, and in a more interpretable way than a black-box model alone.

## Method — in short

- **Data:** 6,563 bioactivity records (SMILES compounds with IC50 values) from ChEMBL, PubChem, BindingDB, and GTP, after deduplication and thresholding.
- **Features:** CDK Extended descriptors (PaDEL), Morgan fingerprints, ChemBERTa-2 and LLaMA 3.2 embeddings, and physicochemical properties.
- **Model:** Logic Tensor Network (LTN) — a neuro-symbolic approach that integrates first-order logic / domain knowledge with neural learning — compared against deep neural network (DNN) and Transformer baselines.
- **Validation:** internal test set, plus external validation on the Drug Target Commons (DTC) dataset.

## Results

Best configuration — LTN with CDK Extended + Morgan fingerprints:

| Metric | Internal test | External (DTC) |
|---|---:|---:|
| Accuracy | **0.9725** | **0.9579** |
| F1-score | **0.9723** | **0.9577** |
| ROC AUC | **0.9719** | **0.9565** |
| MCC | **0.9446** | **0.9171** |

NeSyDPP-4 outperformed the DNN and Transformer baselines and existing state-of-the-art methods, and generalised to the external DTC dataset — supporting its use for virtual screening and prioritisation of new DPP-4 inhibitor candidates.

## Repository contents

| Notebook | What it does |
|---|---|
| `1_DPP4-External-Data-Collection & Feature Extraction.ipynb` | External data collection and feature extraction |
| `2_DPP4-Features-Exatraction.ipynb` | Feature extraction |
| `3_DPP4-LTN-Training-CDKExetended-ECFP(Morgan).ipynb` | LTN training — CDK Extended + Morgan (ECFP) |
| `3_DPP4-LTN-Training-CDKExetended-ECFP-HP.ipynb` | LTN training — hyperparameter variant |
| `4_DPP4-LTN-Evaluation-CDKExetended-ECFP.ipynb` | LTN evaluation |
| `DPP4-DNN-Training-CDKExetended-ECFP.ipynb` / `DPP4-DNN-Evaluation-CDKExetended-ECFP.ipynb` | DNN baseline — training / evaluation |
| `Transformer-DPP4.ipynb` / `DPP4-Transformer-Evaluation.ipynb` | Transformer baseline — training / evaluation |
| `environment.yml` | Conda environment (`dpp4_env`, Python 3.10) |

## Quick start

```bash
conda env create -f environment.yml
conda activate dpp4_env
jupyter notebook
```

Run the notebooks in order, starting with `1_` (data collection / features), then `3_` (LTN training), then `4_` (evaluation).

## Data card / Data availability

- **Dataset used in the study:** https://drive.google.com/file/d/1SGiYOyuSiirueZR3F6K0d7aHcPT43PYw/view
- **Sources:** ChEMBL, PubChem, BindingDB, and GTP (6,563 records); external validation on Drug Target Commons (DTC).
- **Code:** this repository — https://github.com/hossain013/NeSyDPP4-QSAR

This is the dataset link given in the Data Availability Statement of the published article.
