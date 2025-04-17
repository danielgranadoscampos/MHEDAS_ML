# Cardiovascular Disease Classification from CMR Radiomics

*Machine‑learning project on the ACDC challenge dataset*

---

## 0. Reproducibility

```text
Python 3.12
numpy 1.26 · pandas 2.2 · scikit‑learn 1.5 · matplotlib 3.9 · seaborn 0.13 · shap 0.45
Random seed: 42
```

All experiments are executed through `main.py` so they can be reproduced end‑to‑end with

```bash
python main.py --model svm --selector none --cv 5
```

---

## 1. Exploratory Data Analysis (EDA)

| property | value |
|----------|-------|
| **Patients** | 100 |
| **Classes** | NORM · MINF · DCM · HCM · RV (20 each) |
| **Features** | 642 radiomics + *height*, *weight* |
| **Missing** | 0 |

### 1.1  Class distribution

Balanced (20 patients per class) – no re‑sampling required.

### 1.2  Height & Weight

* mean ± SD height: **???.? ± ?.? cm** · weight: **??.? ± ??.? kg**

### 1.3  Correlation heat‑map

Large clusters of >0.9 correlation among shape metrics and texture matrices indicate
redundancy – a signal that feature reduction/selection will be helpful.

### 1.4  Dimensionality reduction snapshot

| method | comps | variance | observation |
|--------|-------|----------|-------------|
| **PCA** | 2 | 55 % | poor visual separation of classes |
| **PCA** | 12 | 86 % | suitable for modelling |
| **PCA** | 16 | 90 % | diminishing returns |
| **LDA** | 4 | 100 % discrim. | better class clustering than PCA |

---

## 2. Training / Validation Split

| strategy | train | val | rationale |
|----------|-------|-----|-----------|
| Stratified **80 / 20** | 80 | 20 | quick benchmark; keeps class balance |
| Stratified **5‑fold CV** | 80 per fold | 20 per fold | reduces split variance – preferred |

**Results (RandomForest, default hyper‑params)**

```text
80/20 split  : accuracy 0.80
5‑fold CV    : 0.79 ± 0.08
```

Per‑class F1 ranged 0.75 – 0.89; RV best, DCM/MINF weakest.

---

## 3. Baseline Models  *(work in progress)*

| model | status | next steps |
|-------|--------|------------|
| **SVM** (RBF) | ☐ | grid‑search C, γ, class‑weight |
| **RandomForest** | ☑ basic | tune *n*‑trees, depth, mtry |
| **MLPClassifier** | ☐ | design 1–2 hidden layers, α, early‑stop |

Evaluation metrics: **macro‑F1**, **balanced accuracy**, confusion matrix (+ per‑class recall).

---

## 4. Feature Engineering & Model Enhancement  *(to do)*

* **Dimensionality reduction**: PCA (retain ≥ 90 % var.); LDA; Autoencoder.
* **Feature selection**: VarianceThreshold → MutualInformation; RFECV with SVM / RF.
* Combine in a `Pipeline` to avoid data‑leakage.

Outcome to log:
* number of retained features / components
* macro‑F1 ± 95 % CI
* computation time

---

## 5. Results Analysis  *(pending)*

* Pairwise Wilcoxon signed‑rank across folds, Bonferroni‑corrected.
* Plot SHAP summary for champion model; list top‑10 influential radiomics.
* Compare class‑wise recall before/after feature engineering.

---

## 6. Toward Clinical Adoption  *(outline)*

1. **External validation** on a multi‑centre cohort (domain shift).
2. **Calibration**: Brier score, reliability plots; consider Platt scaling.
3. **Explainability dashboard** for cardiologists (SHAP, counter‑factuals).
4. **Robustness**: 50× repeated CV to assess selection stability.
5. **Regulatory path**: CE/FDA SaMD, data‑governance (GDPR, HIPAA), quality‑management.

Key performance metric for deployment: **class‑specific sensitivity (>0.85)** to minimise
false negatives in diseased groups.

---

## 7. Repository Structure

```
acdc_project/
├── datasets/ACDC_radiomics.csv
├── class_notebooks
├── src/
│   ├── data_prep.py
│   ├── models.py
│   ├── evaluation.py
│   └── feature_analysis.py
├── main.py          # CLI runner for experiments
└── REPORT.md        # this file
```

---

## 8. Checklist / Next Actions

- [ ] Implement SVM & MLP pipelines with grid‑search.
- [ ] Add PCA & LDA branches to pipeline.
- [ ] Run RFECV for feature selection.
- [ ] Capture fold‑wise predictions for stats.
- [ ] Generate SHAP explanations for top model.
- [ ] Draft statistical test section in report.
- [ ] Polish figures, embed confusion matrices.

---

### References

ACDC project brief


