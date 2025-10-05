# DA5401 — Assignment 5

- **Name**: Soumya Ranjan Patel  
- **Roll Number**: DA25M029




## Repository Structure

```
DA5401-assignment-4-patelsoumyaranjan04/
├── DA5401_A5.ipynb
└──yeast.arff
└── README.md 
```

# 🧬 Yeast Gene Expression — Manifold Visualization and Data Veracity Analysis

This repository explores the **structure and data quality (veracity)** of the **Yeast gene expression dataset** using two nonlinear dimensionality reduction techniques:

- **t-SNE** → for **local neighborhood structure**
- **Isomap** → for **global manifold geometry**

Our goal is to investigate whether **functional categories** of genes form meaningful clusters or manifolds in low-dimensional space — and to identify potential **noisy labels**, **outliers**, and **hard-to-learn samples**.

---

## 📊 Dataset Overview

- **Dataset**: Yeast gene expression  
- **Features**: 103 standardized expression values per sample  
- **Labels**: 14 functional categories (multi-label)  
- **Task**: Analyze whether the data naturally separates into meaningful structures when projected into 2D using manifold learning methods.

---



## 🌀 t-SNE Analysis

We applied t-SNE with different perplexities (0.5, 30, 50, 100):

| Perplexity | Visualization Summary |
|-----------|-------------------------|
| **0.5** | Produces concentric elliptical patterns — likely a projection artifact. |
| **30–100** | Stable structure: a **single dense overlapping cloud** with heavy mixing between categories. |

### 📌 Example: Perplexity = 30

<img width="746" height="584" alt="image" src="https://github.com/user-attachments/assets/6a067415-cdab-4e83-8779-e3b1b36be86e" />


- **No clear clusters** corresponding to functional categories.
- Some **localized pockets** of one category (`Other`), but generally **high overlap**.
- Indicates that the feature space **does not naturally separate categories**.

---

## 🧭 Isomap Analysis

We applied Isomap with neighborhood sizes **k = 10, 15, 30**:

| k | Visualization Summary |
|---|-------------------------|
| 10 / 15 / 30 | All show similar results: a **single blob-like structure** with overlapping categories and no evident manifold curvature. |

### 📌 Example: k = 15
<img width="744" height="570" alt="image" src="https://github.com/user-attachments/assets/c53498c0-a010-4a87-8993-51640618ba0d" />


- No clear clusters or curved manifold structure are observed.
- Isomap does **not reveal additional global structure** beyond what t-SNE shows.

---

## 🔍 Veracity Inspection

### 1. Noisy / Ambiguous Labels
Neighborhood purity analysis highlights samples whose neighbors belong to multiple categories:

<img width="737" height="639" alt="image" src="https://github.com/user-attachments/assets/feceb887-ac69-443a-b590-7f8f23da6d10" />


- Many **low-purity points** scattered across the embedding.
- Indicates **widespread label overlap** or ambiguity.

---

### 2. Outliers
Isolation Forest identifies unusual expression patterns:

<img width="821" height="664" alt="image" src="https://github.com/user-attachments/assets/d0309d5d-f375-44f6-af84-50f8316c1068" />


- Outliers are **scattered** rather than forming distinct isolated groups.
- May correspond to **rare biological conditions** or **measurement errors**.

---

### 3. Hard-to-Learn Samples
- Extensive **color mixing** indicates regions where no simple decision boundaries can separate categories.
- Classifiers will require **highly non-linear** decision functions or noise-robust methods.

---

## 📝 Final Insights

| Aspect                 | t-SNE                         | Isomap                        |
|-------------------------|--------------------------------|--------------------------------|
| **Focus**              | Local neighborhood structure  | Global manifold geometry      |
| **Structure**          | Some localized pockets, but no clear clusters | Single blob, no curvature |
| **Label Overlap**      | High                          | High                          |
| **Outliers**           | Scattered, few                | Scattered, few                |
| **Best For**           | Spotting noisy / ambiguous samples | Assessing overall manifold shape |

### Key Takeaways

- Neither t-SNE nor Isomap reveals **distinct or separable clusters** for functional categories.
- The dataset appears **highly overlapping, noisy**, and does **not lie on a simple low-dimensional manifold**.
- Classification is likely to be **intrinsically difficult** due to data ambiguity, not just algorithm choice.
- Robust, nonlinear classifiers and potential **label cleaning** or **uncertainty modeling** may be necessary for good performance.

---

## 🧪 Methods Summary

| Method   | Role                        | Key Insight |
|---------|-------------------------------|-------------|
| **t-SNE**  | Local structure exploration  | Reveals scattered ambiguous samples, no clear clusters |
| **Isomap** | Global manifold unfolding   | Shows no meaningful manifold structure |

---

