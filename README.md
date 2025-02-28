[![author](https://img.shields.io/badge/Author-Francisco&nbsp;Bustamante-red.svg)](https://www.linkedin.com/in/flsbustamante/)
[![Project generated with PyScaffold](https://img.shields.io/badge/-PyScaffold-005CA0?logo=pyscaffold)](https://pyscaffold.org/)
[![](https://img.shields.io/badge/Python-3.13+-blue.svg)](https://www.python.org/)

# Credit Card Fraud Detection

> Catch Fraud Before It Happens – Powered by Data Science.

Welcome to the Credit Card Fraud Detection project. This repository presents a
comprehensive data science solution designed to tackle fraud detection in an imbalanced
dataset.

The project demonstrates a complete pipeline — from preprocessing, through stratified
cross-validation and model training with class weight adjustments, to model evaluation
using metrics such as average precision (AUPRC), recall, and AUROC.

![fluxogram](reports/figures/fraud.png)

In addition to implementing various machine learning algorithms, the project emphasizes
model interpretability, providing actionable insights for real-world decision making.

This work serves as a practical example of how advanced data science techniques can be
applied to improve fraud detection systems in the financial sector.

I wrote an article about this project on my portfolio webpage. You can check it out
[here](https://franciscobustamante.com.br/portfolio/2022-01-project_credit_card_fraud/).

## Main results

The study was divided into five main parts, each one with its own notebook in the
[`notebooks`](notebooks/) folder:

1. **Data cleansing and feature engineering**: The dataset was cleaned and transformed
   to improve the performance of the machine learning models.
   [Notebook 1](notebooks/01-flsb-data_cleansing.ipynb).
2. **Exploratory data analysis**: The dataset was analyzed to understand the distribution
   of the features and the target variable.
   [Notebook 2](notebooks/02-flsb-eda.ipynb).
3. **Model training and evaluation**: Several machine learning models were trained and
   evaluated using cross-validation.
   [Notebook 3](notebooks/03-flsb-classification-models.ipynb).
4. **Resampling techniques**: The dataset was balanced using resampling techniques to
   improve the performance of the machine learning models.
   [Notebook 4](notebooks/04-flsb-classification-models-resampling.ipynb).

The project's pipeline can be summarized as follows:

![pipeline](reports/figures/pipeline_full.png)

The final model, a Support Vector Machine (SVM) with a radial basis function kernel,
with preprocessing and resampling, has the following metrics:

|AUROC|AUPRC|
|-------------------------------------|-------------------------------------|
| ![AUROC](reports/figures/auroc.png) | ![AUPRC](reports/figures/auprc.png) |

| Metric              | Score    | Std Dev   |
|---------------------|----------|-----------|
| Accuracy            | 0.999680 | 0.000046  |
| Balanced Accuracy   | 0.914688 | 0.011774  |
| F1                  | 0.906547 | 0.014236  |
| Precision           | 1.000000 | 0.000000  |
| Recall              | 0.829375 | 0.023549  |
| ROC AUC             | 0.940962 | 0.008235  |
| Average Precision   | 0.865117 | 0.026657  |
| F1 Weighted         | 0.999665 | 0.000050  |



## Installation

In order to set up the necessary environment:

1. review and uncomment what you need in `environment.yml` and create an environment `fraud` with the help of [conda]:
   ```
   conda env create -f environment.yml
   ```
2. activate the new environment with:
   ```
   conda activate fraud
   ```
3. install the package in editable mode with:
   ```
   pip install -e .
   ```
   This will install the package in editable mode, so you can modify the source code and
   directly import the package in Python.

> **_NOTE:_**  The conda environment will have fraud installed in editable mode.
> Some changes, e.g. in `setup.cfg`, might require you to run `pip install -e .` again.


Optional and needed only once after `git clone`:

4. install several [pre-commit] git hooks with:
   ```bash
   pre-commit install
   # You might also want to run `pre-commit autoupdate`
   ```
   and checkout the configuration under `.pre-commit-config.yaml`.
   The `-n, --no-verify` flag of `git commit` can be used to deactivate pre-commit hooks temporarily.

5. install [nbstripout] git hooks to remove the output cells of committed notebooks with:
   ```bash
   nbstripout --install --attributes notebooks/.gitattributes
   ```
   This is useful to avoid large diffs due to plots in your notebooks.
   A simple `nbstripout --uninstall` will revert these changes.


Then take a look into the `src` and `notebooks` folders.

### MLFlow setup

The notebooks have all the consolidated results of the models, with the numerical results
and visualizations. If you want even more detailed results, you can use MLFlow to track
the experiments. To set up MLFlow, you need to:

1. Open the `.env` file present in the `src/fraud` folder.
2. Set the `MLFLOW_ON` variable to True.
3. Run the code of the classification notebook.
4. A folder called `mlruns` will be created in the `notebooks` folder.
5. To see the results, you need to run the following command in the terminal:
   ```bash
   mlflow ui
   ```



## Dependency Management & Reproducibility

1. Always keep your abstract (unpinned) dependencies updated in `environment.yml` and eventually
   in `setup.cfg` if you want to ship and install your package via `pip` later on.
2. Create concrete dependencies as `environment.lock.yml` for the exact reproduction of your
   environment with:
   ```bash
   conda env export -n fraud -f environment.lock.yml
   ```
   For multi-OS development, consider using `--no-builds` during the export.
3. Update your current environment with respect to a new `environment.lock.yml` using:
   ```bash
   conda env update -f environment.lock.yml --prune
   ```
## Project Organization

```
├── AUTHORS.md              <- List of developers and maintainers.
├── CHANGELOG.md            <- Changelog to keep track of new features and fixes.
├── CONTRIBUTING.md         <- Guidelines for contributing to this project.
├── LICENSE.txt             <- License as chosen on the command-line.
├── README.md               <- The top-level README for developers.
├── data
│   ├── external            <- Data from third party sources.
│   ├── interim             <- Intermediate data that has been transformed.
│   ├── processed           <- The final, canonical data sets for modeling.
│   └── raw                 <- The original, immutable data dump.
├── docs                    <- Directory for Sphinx documentation in rst or md.
├── environment.yml         <- The conda environment file for reproducibility.
├── models                  <- Trained and serialized models
├── notebooks               <- Jupyter notebooks. Naming convention is a number (for
│                              ordering), the creator's initials and a description,
│                              e.g. `1.0-fw-initial-data-exploration`.
├── pyproject.toml          <- Build configuration. Don't change! Use `pip install -e .`
│                              to install for development or to build `tox -e build`.
├── references              <- Data dictionaries, manuals, and all other materials.
├── reports                 <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures             <- Generated plots and figures for reports.
├── setup.cfg               <- Declarative configuration of your project.
├── setup.py                <- [DEPRECATED] Use `python setup.py develop` to install for
│                              development or `python setup.py bdist_wheel` to build.
├── src
│   └── fraud               <- Actual Python package where the main functionality goes.
├── tests                   <- Unit tests which can be run with `pytest`.
├── .coveragerc             <- Configuration for coverage reports of unit tests.
├── .isort.cfg              <- Configuration for git hook that sorts imports.
└── .pre-commit-config.yaml <- Configuration of pre-commit git hooks.
```

## Citing

If you use this project in a scientific publication or in classes, please consider
citing as

F. L. S. Bustamante, Credit card fraud detection, 2022 - Available at:
https://github.com/chicolucio/credit_card_fraud

## My Links

- [LinkedIn](https://www.linkedin.com/in/flsbustamante/)
- [Portfolio](https://franciscobustamante.com.br/portfolio)
- [Curriculum Vitae](https://franciscobustamante.com.br/about/)

<!-- pyscaffold-notes -->

## Note

This project has been set up using [PyScaffold] 4.6 and the [dsproject extension] 0.7.2.

[conda]: https://docs.conda.io/
[pre-commit]: https://pre-commit.com/
[Jupyter]: https://jupyter.org/
[nbstripout]: https://github.com/kynan/nbstripout
[PyScaffold]: https://pyscaffold.org/
[dsproject extension]: https://github.com/pyscaffold/pyscaffoldext-dsproject
