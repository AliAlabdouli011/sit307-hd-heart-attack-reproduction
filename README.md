# SIT307 11.1 HD Task — Reproduction and Improvement

Reproduction and methodological improvement of Bhagat, Sharma & Agarwal (2025),
"An efficient stacking-based ensemble technique for early heart attack
prediction", *Multimedia Tools and Applications*, 84:36351-36375,
doi: 10.1007/s11042-024-19293-7.

This package contains **two notebooks**, run in sequence, plus the shared
dataset files both notebooks depend on.

## Files

| File | Purpose |
|---|---|
| `part1_reproduction.ipynb` | Part 1: faithful reproduction of the paper's described protocol (record-level split), plus the duplicate-record audit and critical analysis of discrepancies against the paper's own reported tables and figures. |
| `part2_improvement.ipynb` | Part 2: the proposed methodological improvement, a duplicate-group-aware evaluation protocol (applied to both the outer train/test split and the stacking ensemble's internal cross-validation), with group-level and repeated-split evaluation. **Depends on `part1_reproduction.ipynb` having been run first** (it reads the same dataset files and reuses Part 1's reported numbers for comparison; it does not import any variables directly from Part 1, but the notebooks are intended to be read and run in order). |
| `heart_disease_1025.csv` | The main dataset (1,025 rows, 14 columns), used by both notebooks. |
| `heart_disease_cleveland_303.csv` | A separately-labelled 303-row Cleveland-only file, used in Part 1 (Section 1) to check whether the 1,025-row dataset genuinely combines four databases as the paper describes. Not used by Part 2. |
| `requirements.txt` | Exact package versions used to produce every result in both notebooks. |
| `README.md` | This file. |

## Dataset

- **Source**: Kaggle, `johnsmith88/heart-disease-dataset` (the "Public Health
  Dataset" cited by the paper). Kaggle is not directly reachable from the
  environment this was built in, so this specific copy was obtained from a
  GitHub mirror that explicitly cites the same Kaggle dataset as its source:
  `https://github.com/halekpetigo/BIOF509/blob/main/heart.csv` (main file) and
  `https://github.com/halekpetigo/BIOF509/blob/main/heart%202.csv` (Cleveland-only file)
- **SHA-256 checksums**:
  - `heart_disease_1025.csv`: `ddb2996b2f4db2e00aad13f4518200179ff69f79093838e3c21ffa672ebec0f1`
  - `heart_disease_cleveland_303.csv`: `7c3014365675306819510a49ff289efbec1d1a6a666a2dc7652f1547b383d859`
- **Shape**: `heart_disease_1025.csv` is 1,025 rows x 14 columns (13 features + `target`);
  `heart_disease_cleveland_303.csv` is 303 rows x 14 columns

If re-downloading, verify checksums match before running either notebook,
since this specific dataset is known (see Part 1, Section 2) to contain
substantial exact-row duplication (723 of 1,025 rows), which is central to
both notebooks' findings, a differently-cleaned copy would not reproduce the
same results. If you have direct Kaggle access, cross-checking against the
live `johnsmith88/heart-disease-dataset` page directly is recommended where
possible; this mirror is a documented, checksummed substitute used because
Kaggle was not reachable from the build environment, not the authors'
original primary source.

## Environment

- Python 3.12.x
- Package versions pinned in `requirements.txt`; install with:

```
pip install -r requirements.txt
```

## Running

1. Place both CSV files in the same directory as both notebooks.
2. Run `part1_reproduction.ipynb` top to bottom first.
3. Run `part2_improvement.ipynb` top to bottom (it reads the same two CSV
   files independently; it does not need Part 1's notebook kernel or
   variables to still be running, but should be read as a continuation of
   Part 1's findings).

`random_state=42` is used for stochastic components where supported (train/
test splits, classifiers with a random element, the stacking cross-validation
folds), so results should be exactly reproducible on rerun with the pinned
package versions. A few components (e.g. Gaussian Naive Bayes) have no
stochastic element and so take no seed. Part 2's repeated-evaluation section
additionally sweeps seeds 0-9 deliberately, as part of its own experimental
design, not because the main result is seed-dependent.

Expected running time: Part 1 completes in under a minute on a standard
laptop CPU; Part 2's repeated-evaluation section (10 full pipeline reruns)
takes several minutes.

## Acknowledgement of GenAI Use

Generative AI was used to help tighten up my own writing across both
notebooks' explanations and this README. All code was run by me to produce
the results reported; see each notebook's own "Acknowledgement of GenAI Use"
section for the notebook-specific statement.
# sit307-hd-heart-attack-reproduction
