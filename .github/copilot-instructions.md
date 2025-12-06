<!-- Copied style: concise, actionable, repo-specific guidance for AI coding agents -->
# Copilot instructions for VEP_Signal_Dec

Purpose
- Help an AI code assistant become immediately productive in this repository (analysis notebooks for VEP signals).

**High-level architecture / big picture**
- This repository is notebook-first: core analysis lives in Jupyter notebooks at the repository root (e.g., `01_npz.ipynb`, `02_ECOC_Lum_01.ipynb`, `03_ECOC_L_M_01.ipynb`, `04_ECOC_S_cone_01.ipynb`, `05_Results.ipynb`).
- Data ingestion and preprocessing are handled in `01_npz.ipynb` (creates and/or normalizes `.npz` data files used by later notebooks).
- Analysis experiments (ECOC variants) are implemented as separate notebooks named `02_*.ipynb`, `03_*.ipynb`, `04_*.ipynb`.
- `05_Results.ipynb` aggregates outputs and visualizations for reporting.

**Key developer workflows**
- Environment: the project uses an Anaconda environment named `mne` in developer shells. Common activation patterns observed in the workspace are:
  - `conda activate mne`
  - or (mac default) `source /opt/anaconda3/bin/activate mne`
- Interactive exploration: open the notebooks with `jupyter lab` or `jupyter notebook`.
- Headless execution (reproduce notebooks end-to-end) — examples:
  - `jupyter nbconvert --execute 01_npz.ipynb --to notebook --output executed-01_npz.ipynb`
  - Or, if `papermill` is installed: `papermill 01_npz.ipynb executed-01_npz.ipynb`
- When producing changes that should be reusable across experiments, extract code into a Python module rather than editing duplicated notebook cells.

**Project-specific conventions & patterns**
- Notebooks are the canonical source of truth — prefer updating or adding a notebook when adding an experiment.
- Naming: notebooks are ordered/prefixed by step number (01, 02, 03, 04, 05) — preserve ordering when adding new steps.
- Data artifact format: `.npz` is used for intermediate datasets (see `01_npz.ipynb`). Place generated `.npz` files in repository root or a `data/` folder and ensure notebook cells reference the same path.
- Results consolidation: keep final reporting and plots in `05_Results.ipynb` so downstream readers find a single summary notebook.

**Integration points & external dependencies**
- Conda env `mne` likely contains MNE, NumPy, SciPy, scikit-learn, matplotlib, and Jupyter — inspect your local environment for exact versions.
- No CI/test suite discovered in the repo; there are no `tests/` folders or `pytest` configs present.

**How to modify code safely**
- For small fixes to analysis logic, change the notebook cell and re-run that notebook end-to-end to ensure outputs update.
- For larger refactors (shared utilities or preprocessing), create a new top-level Python module (e.g., `vep_utils.py`) and import it from notebooks; this reduces duplicated edits across notebooks.
- When committing notebook changes, keep outputs either consistently present (if results should be archived) or cleared (if repository prefers diffs free of large output). Ask repository owner which they prefer.

**Examples (commands)**
- Activate environment:
  - ``conda activate mne``
  - or ``source /opt/anaconda3/bin/activate mne``
- Run a notebook headless and save executed copy:
  - ``jupyter nbconvert --execute 01_npz.ipynb --to notebook --output executed-01_npz.ipynb``

**Files you should look at first**
- `01_npz.ipynb` — data ingestion / .npz creation
- `02_ECOC_Lum_01.ipynb`, `03_ECOC_L_M_01.ipynb`, `04_ECOC_S_cone_01.ipynb` — experiment notebooks
- `05_Results.ipynb` — results aggregation and figures
- `Other/02_ECOC_Lum_old.ipynb` — older experiment; useful for historical reference

If anything here is unclear or you want the instructions expanded (for example, adding exact dependency versions or a recommended `requirements.txt`), tell me which part to inspect and I will update the file.
