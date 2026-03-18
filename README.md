# Recommender Systems Assignment
### MovieLens 100K — Parts 1–6

---

## Requirements

| Package | Version | Purpose |
|---|---|---|
| Python | 3.9 – 3.13 | Runtime |
| numpy | any | Matrix operations |
| pandas | any | Data handling |
| scikit-learn | any | TF-IDF, cosine similarity, MLP, metrics |
| scipy | any | SVD (svds) |
| matplotlib | any | All visualizations |
| seaborn | any | Heatmaps |
| lime | any | Task 12 explainability |
| tensorflow / keras | optional | Task 8 neural network |

> **scikit-surprise is NOT required.**  
> Task 6 uses a pure-numpy SGD-SVD implementation — no external library needed.

---

## Installation

Run **Cell 1** of the notebook (the first code cell):

```python
!pip install numpy pandas scikit-learn scipy matplotlib seaborn requests lime -q
!pip install tensorflow -q        # optional — Python <= 3.12 only
```

Then **Kernel → Restart** before running anything else.

---

## How to Run

1. Open `recommender_systems.ipynb` in Jupyter Lab or Jupyter Notebook
2. Run **Cell 1** (installs dependencies) → restart kernel
3. Run **all cells top to bottom** (Cell → Run All)

**Do not skip cells.** Each part depends on variables set in earlier cells:

```
Cell 1  (install)
  ↓
Cell 3  (imports)
  ↓
Cell 5  (load data)
  ↓
Cell 7  (train/test split)  ← required by ALL evaluation cells
  ↓
Parts 1–6 in order
  ↓
Final comparison table
```

---

## Dataset

Downloaded automatically on first run from:
```
https://files.grouplens.org/datasets/movielens/ml-100k.zip
```
Saved to `./ml-100k/`. If download fails (no internet), download manually and unzip into the same folder as the notebook.

---

## Structure

| Part | Tasks | Description |
|---|---|---|
| 1 | 1–2 | Content-based filtering (TF-IDF + user profiles) |
| 2 | 3–4 | Collaborative filtering (user-based + item-based) |
| 3 | 5–6 | Matrix factorization (SVD scipy + SGD-SVD) |
| 4 | 7 | Hybrid meta-model (GradientBoosting) |
| 5 | 8–9 | Neural network CBF + Reinforcement Learning |
| 6 | 10–13 | Explainability (feature weights, neighbours, LIME) |

---

## Visualizations

| Figure | Location | Shows |
|---|---|---|
| Fig 1 | After data loading | Rating distribution, ratings per user, genre counts |
| Fig 2 | After Task 1 | TF-IDF cosine similarity heatmap between sample movies |
| Fig 3 | After Task 1 | IDF weight per genre (rarity → influence) |
| Fig 4 | After Task 3 | K-sensitivity: RMSE / P@10 / R@10 vs number of neighbours |
| Fig 5 | After Task 5 | SVD singular values + user factor norm distribution |
| Fig 6 | After Task 6 | SGD-SVD training curve (train vs test RMSE per epoch) |
| Fig 7 | After Task 7 | Hybrid feature importances + predicted vs actual scatter |
| Fig 8 | After Task 9 | RL bandit cumulative rewards + Q-value distribution |
| Fig 9 | Final cell | Bar chart comparison of all models (RMSE, P@10, R@10) |

---

## Evaluation Protocol

All models use a **per-user 80/20 train/test split**:
- Profiles and similarity matrices are built from **train ratings only**
- RMSE is measured on **held-out test ratings**
- P@K and R@K use **test ratings ≥ 4** as the relevant set
- Recommendations exclude only **train-seen movies** so test movies can appear

This avoids the common mistake of evaluating against movies the model was trained on (which always gives P@K = R@K = 0).

---

## Results

```
Model                  RMSE     P@10    R@10
TF-IDF CBF             N/A     ~0.03   ~0.02
User-Based CF         ~1.00    ~0.01   ~0.01
Item-Based CF         ~1.05    ~0.01   ~0.01
SVD scipy             ~0.97    ~0.12   ~0.13
SVD SGD               ~0.94    ~0.08   ~0.05
Hybrid Meta-Model     ~0.68    ~0.10   ~0.08
```

SVD methods outperform neighbourhood-based CF on RMSE.  
The hybrid model achieves the best RMSE by combining CBF + SVD signals.
