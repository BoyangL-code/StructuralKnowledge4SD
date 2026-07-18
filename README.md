# StructuralKnowledge4SD

StructuralKnowledge4SD contains data files and Jupyter notebooks for malodor descriptor prediction using molecular structural information. The current repository is organized around four feature sources:

- `Malodors_data.xlsx`: original malodor dataset.
- `Morgan.csv`: Morgan fingerprint features.
- `Rule.xlsx`: rule-based structural features.
- `Malodors_StructKG_features.xlsx`: structural knowledge graph features.
- `Odor_label.xlsx`: odor descriptor label matrix.

The repository is currently notebook-based rather than a packaged Python library.

## Repository structure

```text
StructuralKnowledge4SD/
├── Feature_data/
│   ├── Malodors_StructKG_features.xlsx
│   ├── Morgan.csv
│   ├── Odor_label.xlsx
│   └── Rule.xlsx
├── Train2/
│   ├── ALL/
│   │   ├── AD/
│   │   │   ├── AD_HPSearch.ipynb
│   │   │   ├── AD_plot.ipynb
│   │   │   └── Tanimoto similarity.ipynb
│   │   ├── AP/
│   │   │   ├── laogangAD.ipynb
│   │   │   └── prediction.ipynb
│   │   ├── SHAP/
│   │   │   └── shap_heatmap_out/
│   │   │       ├── SHAP.ipynb
│   │   │       ├── SHAPtop20.ipynb
│   │   │       ├── SHAPtop30.ipynb
│   │   │       ├── SHAPtop40.ipynb
│   │   │       └── united.ipynb
│   │   ├── sulpplement/
│   │   │   ├── Morgan+ StructKG/
│   │   │   │   ├── Best_model.ipynb
│   │   │   │   └── Untitled.ipynb
│   │   │   ├── SHAP/
│   │   │   │   ├── Untitled.ipynb
│   │   │   │   ├── Untitled1.ipynb
│   │   │   │   └── Untitled2.ipynb
│   │   │   └── Train_M&R/
│   │   │       ├── Best_model.ipynb
│   │   │       └── Train_M&R.ipynb
│   │   └── ALL_Best_model.ipynb
│   ├── Rule+StructKG/
│   │   ├── Rule+StructKG.ipynb
│   │   └── Rule+StructKGBest_model.ipynb
│   ├── Rule/
│   │   ├── Best_model.ipynb
│   │   └── Rule.ipynb
│   ├── StructKG/
│   │   └── Best_model.ipynb
│   └── morgan/
│       ├── Best_model.ipynb
│       └── morgan.ipynb
└── Malodors_data.xlsx
```

> Note: directory names are kept exactly as they appear in the repository, including `sulpplement` and paths containing spaces or symbols.

## Project purpose

The repository supports structure-informed odor prediction by comparing and combining different molecular representations:

| Feature source | File / folder | Purpose |
|---|---|---|
| Morgan fingerprint | `Feature_data/Morgan.csv`, `Train2/morgan/` | Baseline molecular fingerprint modeling |
| Rule-based structural feature | `Feature_data/Rule.xlsx`, `Train2/Rule/` | Interpretable structural-rule modeling |
| Structural knowledge graph feature | `Feature_data/Malodors_StructKG_features.xlsx`, `Train2/StructKG/` | Knowledge-graph-based structural representation |
| Rule + StructKG | `Train2/Rule+StructKG/` | Fusion of rule features and StructKG features |
| All features | `Train2/ALL/` | Integrated modeling using multiple feature sources |
| Odor labels | `Feature_data/Odor_label.xlsx` | Multi-label odor descriptor targets |
| Original dataset | `Malodors_data.xlsx` | Source molecular odor data |

## Main workflows

### 1. Single-feature modeling

Use the notebooks under `Train2/` to train or evaluate models based on one feature type:

```text
Train2/morgan/morgan.ipynb
Train2/Rule/Rule.ipynb
Train2/StructKG/Best_model.ipynb
```

The corresponding `Best_model.ipynb` notebooks appear to store best-model training or selection experiments for each feature setting.

### 2. Feature-fusion modeling

Use the following notebooks for feature combination experiments:

```text
Train2/Rule+StructKG/Rule+StructKG.ipynb
Train2/Rule+StructKG/Rule+StructKGBest_model.ipynb
Train2/ALL/ALL_Best_model.ipynb
Train2/ALL/sulpplement/Morgan+ StructKG/Best_model.ipynb
Train2/ALL/sulpplement/Train_M&R/Train_M&R.ipynb
```

Recommended comparison order:

```text
Morgan
Rule
StructKG
Rule + StructKG
Morgan + StructKG
Morgan + Rule
All features
```

### 3. Applicability domain analysis

Applicability domain and similarity-based analysis notebooks are stored in:

```text
Train2/ALL/AD/
```

Main notebooks:

```text
AD_HPSearch.ipynb
AD_plot.ipynb
Tanimoto similarity.ipynb
```

These notebooks are intended for hyperparameter search, AD visualization, and molecular similarity analysis.

### 4. Prediction on external or application data

Prediction-related notebooks are stored in:

```text
Train2/ALL/AP/
```

Main notebooks:

```text
laogangAD.ipynb
prediction.ipynb
```

### 5. SHAP interpretation

SHAP-related notebooks are stored in:

```text
Train2/ALL/SHAP/shap_heatmap_out/
```

Main notebooks:

```text
SHAP.ipynb
SHAPtop20.ipynb
SHAPtop30.ipynb
SHAPtop40.ipynb
united.ipynb
```

These notebooks are used for feature-importance analysis and visualization of important structural features.

## Installation

Create a Python environment:

```bash
conda create -n structural4sd python=3.9 -y
conda activate structural4sd
```

Install common packages used in molecular-feature and machine-learning notebooks:

```bash
pip install numpy pandas scikit-learn scipy matplotlib seaborn openpyxl tqdm jupyter shap xgboost
```

Install RDKit if molecular fingerprint calculation or SMILES processing is required:

```bash
conda install -c conda-forge rdkit -y
```

If some notebooks require additional packages, install them according to the import errors reported by Jupyter.

## Usage

### Step 1. Open Jupyter

```bash
jupyter notebook
```

or:

```bash
jupyter lab
```

### Step 2. Check input files

Before running notebooks, confirm that these files exist:

```text
Feature_data/Morgan.csv
Feature_data/Rule.xlsx
Feature_data/Malodors_StructKG_features.xlsx
Feature_data/Odor_label.xlsx
Malodors_data.xlsx
```

### Step 3. Run baseline models

Run single-feature notebooks first:

```text
Train2/morgan/morgan.ipynb
Train2/Rule/Rule.ipynb
Train2/StructKG/Best_model.ipynb
```

### Step 4. Run feature-fusion models

Run the combined-feature notebooks:

```text
Train2/Rule+StructKG/Rule+StructKG.ipynb
Train2/ALL/ALL_Best_model.ipynb
```

### Step 5. Run AD and SHAP analysis

After model training, run:

```text
Train2/ALL/AD/AD_HPSearch.ipynb
Train2/ALL/AD/AD_plot.ipynb
Train2/ALL/SHAP/shap_heatmap_out/SHAP.ipynb
```

## Reproducibility notes

For reproducible modeling, set a fixed random seed in all notebooks:

```python
RANDOM_STATE = 42
```

For scikit-learn style models:

```python
random_state = RANDOM_STATE
```

For cross-validation experiments, save:

```text
train/test split indices
model hyperparameters
feature file versions
label file version
evaluation metrics
```


## Citation

If this repository is used in a publication, cite the associated manuscript or project as:

```text
StructuralKnowledge4SD: Structural Knowledge Enhanced Molecular Odor Descriptor Prediction
```
