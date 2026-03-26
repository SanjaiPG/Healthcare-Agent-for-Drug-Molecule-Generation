# Healthcare Agent for Drug Molecule Generation

> A Generative AI system that designs novel drug-like molecules using a character-level LSTM trained on SMILES strings from the ChEMBL database.

**Team – 04**  
Sanjai P G – CB.SC.U4CSE23366  
G T Hemanth Kumar – CB.SC.U4CSE23760  
Course: Generative AI – 23CSE475

---

## Problem Statement

Drug discovery is slow, expensive, and takes years. Researchers must test thousands of compounds before finding viable candidates. This project uses Generative AI to automatically create new drug-like molecules by learning patterns from existing molecular data — reducing early-stage effort and speeding up research.

---

## What We Built

A character-level LSTM model trained on SMILES (Simplified Molecular Input Line Entry System) strings from the ChEMBL database. The model learns chemical structure patterns and generates new, novel, drug-like molecules. Generated molecules are validated using RDKit for chemical correctness and scored using QED and Lipinski's Rule of Five.

---

## Architecture

```
User Query → Retrieval Module (RAG) → Generative AI Model → Validation (RDKit) → Output
```

| Module | Description |
|---|---|
| User Input | Molecule request or query |
| Knowledge Base | ChEMBL SMILES dataset + stored chemical info |
| Retrieval Module | Converts query to embeddings, searches vector DB |
| Generative AI Model | LSTM trained on SMILES, generates new molecules |
| Validation Module | RDKit checks chemical validity, filters invalids |
| Output Layer | Displays valid molecules + similar known drugs |

---

## Tech Stack

| Library | Role |
|---|---|
| PyTorch | LSTM model, training loop, tensor ops |
| RDKit | SMILES validation, QED & Lipinski scoring |
| pandas | Loading and filtering ChEMBL dataset |
| matplotlib | Property distribution plots |
| Google Colab | GPU-accelerated training environment |

---

## Installation

```bash
pip install torch rdkit pandas matplotlib ipython
```

> For RDKit, conda is recommended:
> ```bash
> conda install -c conda-forge rdkit
> ```

---

## Dataset

**ChEMBL 36** – A large bioactivity database of drug-like molecules in SMILES format.

🔗 **Download:** https://ftp.ebi.ac.uk/pub/databases/chembl/ChEMBLdb/releases/chembl_36/

File used: `chembl_36_chemreps.txt` → extract the `canonical_smiles` column.

---

## How to Run

1. Download the ChEMBL dataset and place it in `data/raw/`
2. Open `notebooks/main.ipynb` in Google Colab or Jupyter
3. Run all cells — the notebook handles preprocessing, training, and generation

---

## Results

| Metric | Value |
|---|---|
| Training Accuracy (final) | 76.75% |
| Final Train Loss | 0.6848 |
| Final Val Loss | 0.7014 |
| Validity | 0.2 (20%) |
| Uniqueness | 1.0 (100%) |
| Novelty | 1.0 (100%) |
| Ro5 Pass Rate | 77% (37/48) |
| Mean QED | 0.586 |
| Mean MW | 320.8 Da |

---

## Limitations

- **Cannot generate molecules for a specific disease** — the model is trained only on molecular structures (SMILES), with no disease-to-drug relationship data. It generates chemically valid molecules in general, not targeted ones.
- **No disease-conditioned generation** — if you provide a disease name, the system cannot respond to it meaningfully.
- **Low validity rate (20%)** — some generated SMILES strings are chemically invalid; RAG integration was not fully implemented.
- **No real-time retrieval** — the RAG module described in the architecture is not yet connected in the current implementation.
- **Fixed dataset scope** — the model only knows patterns from the ChEMBL subset it was trained on; it cannot generalize to unseen chemical spaces.

---

## Future Scope

- Replace SMILES with **SELFIES** tokenization for guaranteed valid outputs
- Upgrade to a **Transformer (GPT-style)** architecture for better long-range dependencies
- Use **Graph Neural Networks (GNNs)** for native molecular graph generation
- Integrate **disease-drug datasets** (DrugBank, BindingDB) for conditional generation
- Build a **CLI tool** or **web app** for non-technical users

---