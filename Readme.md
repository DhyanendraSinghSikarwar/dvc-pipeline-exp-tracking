

# DVC Pipeline Experiment Tracking

This repository demonstrates how to set up and run machine learning experiments with **[DVC (Data Version Control)](https://dvc.org/)**, Git, and Python virtual environments.
It includes environment setup, dataset versioning, experiment tracking, and parameter tuning using DVC experiments.

---

## Prerequisites

* Python 3.x
* Git
* DVC
* Virtual environment (`venv`) or Conda

---

## Setup and Workflow

### 1. Create and Activate Virtual Environment

```bash
python3 -m venv myenv
source myenv/bin/activate
```

Creates an isolated Python environment and activates it.

---

### 2. Install Dependencies

```bash
pip install pandas numpy scikit-learn dvc
```

Installs core dependencies for data processing, model training, and DVC.

---

### 3. Initialize Git Repository

```bash
git init
git remote add origin https://github.com/DhyanendraSinghSikarwar/dvc-pipeline-exp-tracking.git
```

Initializes a Git repo and sets the remote origin.

---

### 4. Save Installed Packages

```bash
pip freeze > requirements.txt
```

Captures the exact package versions for reproducibility.

---

### 5. Create `.gitignore`

```bash
touch .gitignore
```

Prepares a `.gitignore` file to exclude unnecessary files from Git.

---

### 6. Initialize DVC

```bash
dvc init
```

Initializes DVC in the repo.

---

### 7. Stage and Commit Initial Files

```bash
git add .
git commit -m "initial commit"
```

Stages all files and commits them to Git.

---

### 8. View and Reproduce Pipeline

```bash
dvc dag
dvc repro
```

* `dvc dag` shows the pipeline dependency graph.
* `dvc repro` reproduces the pipeline steps based on `dvc.yaml`.

---

### 9. Install dvclive (for experiment logging)

```bash
pip install dvclive
```

Enables live metric logging during experiments.

---

### 10. Run and Show Experiments

```bash
dvc exp show
dvc exp run
```

* `dvc exp run` executes the pipeline as an experiment.
* `dvc exp show` displays experiment results in a table.

---

### 11. Compare Experiments

```bash
dvc exp diff risky-duad bardy-beep
```

Shows parameter and metric differences between two experiments.

---

### 12. Queue Multiple Parameter Variations

```bash
dvc exp run --queue -S model_training.n_estimators=8,16,32 -S model_training.max_depth=2,3,5
```

Queues multiple experiments with different `n_estimators` and `max_depth` values without running them immediately.

---

### 13. Run All Queued Experiments

```bash
dvc exp run --run-all
```

Executes all experiments in the queue.

---

### 14. Apply Best Experiment

```bash
dvc exp apply mangy-jill
```

Applies parameters and outputs from the chosen experiment to the workspace.

---

### 15. Track Data with DVC

```bash
dvc add data/processed/test_processed.csv
```

Adds a dataset to DVC for version control.

---

### 16. Commit DVC Changes

```bash
dvc commit -m 'best exp'
```

Commits updated DVC-tracked files.

---

### 17. Restore Staged Files (if needed)

```bash
git restore --staged data/raw/test.csv
git restore --staged data/raw/train.csv
```

Removes files from the staging area without deleting them locally.

---

### 18. Final Git Commit and Push

```bash
git commit -m "best exp"
git push origin master
```

Commits changes and pushes them to GitHub.

---

## Key DVC Experiment Command

The most important parameter sweep command in this workflow:

```bash
dvc exp run --queue -S model_training.n_estimators=8,16,32 -S model_training.max_depth=2,3,5
```

This queues **all combinations** of `n_estimators` and `max_depth` for later execution, allowing scalable hyperparameter tuning without running experiments immediately.

---

## References

* [DVC Documentation](https://dvc.org/doc)
* [dvclive](https://dvc.org/doc/dvclive)

---

I