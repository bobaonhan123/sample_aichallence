# Copilot / Agent Instructions — pytorch_sample

Purpose: provide short, actionable guidance so an AI coding agent can be immediately productive editing and running this repository.

Overview
- This repo is a collection of standalone Jupyter notebooks demonstrating small ML / visualization examples. Key files: `matplotlib.ipynb`, `xgboost.ipynb`, `pillow.ipynb`, `spectral_clustering.ipynb`, `cv_classification.ipynb`, `data_balance.ipynb`.
- There are no service backends, CI configs, or package manifests in the repository root. Treat changes as documentation/demo edits unless a new packaging/requirements file is added.

What to preserve when editing
- Notebooks: keep existing `metadata.id` values for existing cells and preserve `metadata.language`. New cells do not need an id. Follow the repository's notebook JSON style (cells are simple code/markdown arrays).
- Do not change user-visible cell IDs in messages. When referring to cells in user-facing output, use cell numbers (1-based).

Common patterns and examples (use when editing or creating notebooks)
- Reused imports: notebooks commonly import NumPy and Matplotlib. Example from `matplotlib.ipynb`:

  - Top cell (example): `import matplotlib.pyplot as plt` and `import numpy as np` before plotting.

- Plotting pattern: compute arrays with `np.linspace` or `np.random.*`, then call `plt.plot`/`plt.scatter` and `plt.show()` in the same cell. Prefer small, self-contained cells for plots.

Developer workflows (explicit, reproducible steps)
- Run or execute a notebook locally (Windows PowerShell):

```powershell
# create a venv (if needed)
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install jupyter numpy matplotlib scikit-learn xgboost pillow torch

# to execute a notebook in-place (simple verification):
python -m pip install --upgrade nbconvert
jupyter nbconvert --to notebook --execute "matplotlib.ipynb" --inplace
```

- If adding permanent dependencies, add a `requirements.txt` at repo root. Use `pip freeze > requirements.txt` from the activated environment that reproduces the notebook runtime.

Conventions and repo-specific rules
- Keep notebooks self-contained: imports + dataset generation or a single `data/` reference at the top of the notebook. If you add external data, document the path in the notebook's top markdown cell.
- Language / comments: some notebooks use Vietnamese headings for section titles — retain or translate only on explicit request.
- Avoid changing plot styling globally; prefer local cell-level style parameters (linestyle, color) as used in `matplotlib.ipynb`.

Integration points / external deps
- Notebooks rely on common PyData and ML libs: NumPy, Matplotlib, scikit-learn, XGBoost, Pillow, and PyTorch (repo folder suggests PyTorch examples). There are no remote APIs or service accounts in the repo.

Editing guidance for agents
- Make minimal, incremental changes with clear commit messages.
- When changing notebooks programmatically, preserve cell order and existing ids. If you must reformat JSON, ensure the `metadata.language` fields remain present.
- When adding examples, include a short markdown cell at the top describing inputs, outputs, and required packages.

What NOT to do
- Don't add or call external network services or credentials. There are no CI secrets or service integrations in the repo.
- Don't remove or rewrite existing cell `metadata.id` values unless the user asks explicitly to rebase/clean the notebook.

If you need clarification
- Ask the user whether they want new requirements committed to `requirements.txt`, or prefer ephemeral guidance (commands only).
- Ask if they want notebooks converted to Python scripts (we'll preserve the notebook canonical form unless asked otherwise).

----
If anything in this instruction file is unclear or incomplete, tell me which section to expand (examples, run commands, or notebook JSON rules) and I will iterate.
