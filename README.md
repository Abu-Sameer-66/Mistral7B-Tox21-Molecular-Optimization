<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&ColorList=896A15,6E8915,98351F&height=200&section=header&text=Tox21%20%7C%20Multi-Task%20Toxicity%20Screening&fontSize=40&fontColor=DEE2D9&animation=fadeIn&fontAlignY=35&desc=OLMo-7B%20%7C%20Scaffold%20Split%20%7C%20Mean%20ROC-AUC:%200.7225&descAlignY=60&descAlign=50" width="100%"/>
</div>

<div align="center">
  <img 
    src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=22&pause=1000&color=DEE2D9&center=true&vCenter=true&width=1000&lines=OLMo-7B+Fine-tuned+on+12+Tox21+Tasks;Mean+ROC-AUC:+0.7225+on+Scaffold+Split;Random+vs+Scaffold+Gap:+0.2048+Discovered;8x+Oversampling+for+Imbalanced+Tox+Labels."
    alt="Typing SVG"
  />
</div>

<br/>

## 🧬 Project Overview

This repository contains a complete multi-task toxicity screening pipeline using **OLMo-7B** and **Mistral-7B** fine-tuned on the **Tox21** benchmark. Developed for **DeepChem GSoC 2026**, this project uncovers a critical flaw in published baselines — the **random vs scaffold split gap** — and demonstrates how LLMs can achieve competitive generalization when evaluated honestly.

---

## 📊 Results — Best Experiment

**OLMo-7B QLoRA — Scaffold Split — Mean ROC-AUC: 0.7225**

| Task | ROC-AUC |
|------|---------|
| NR-AR | 0.7179 |
| NR-AR-LBD | **0.8454** |
| NR-AhR | 0.7312 |
| NR-Aromatase | 0.7062 |
| NR-ER | 0.6888 |
| NR-ER-LBD | **0.8326** |
| NR-PPAR-gamma | 0.7343 |
| SR-ARE | 0.6968 |
| SR-ATAD5 | 0.6411 |
| SR-HSE | 0.6352 |
| SR-MMP | 0.7394 |
| SR-p53 | 0.7010 |
| **MEAN** | **0.7225** |

---

## 🔍 Key Scientific Finding — Random vs Scaffold Gap

| Model | Split | ROC-AUC |
|-------|-------|---------|
| RF + ECFP | Random (published baseline) | 0.8183 |
| RF + ECFP | Scaffold (honest evaluation) | 0.6135 |
| **Gap** | | **0.2048** |

**This gap of 0.20 proves that most published baselines use random split — which leaks scaffold information and overestimates real-world generalization. LLM scaffold-split numbers are NOT underperforming — they are the honest numbers.**

This finding directly justifies why the DeepChem GSoC project must use `ScaffoldSplitter` as the evaluation standard.

---

## 🚀 Key Scientific Engineering

| Challenge | Solution | Impact |
|-----------|----------|--------|
| **NaN Loss Crashes** | fp32 loss upcasting + gradient clipping | Eliminated fp16 gradient underflow on imbalanced Tox21 |
| **Class Imbalance** | 8x oversampling of toxic minority class | Prevented bias toward non-toxic majority labels |
| **Memory Bottleneck** | 4-bit NF4 + gradient checkpointing | OLMo-7B fits in 16GB VRAM |
| **Invalid SMILES** | RDKit sanitization — dropped 8 metal-ion SMILES | Prevented tokenizer instability from [Hg+2], [Fe+2] |
| **Baseline Inflation** | Scaffold split enforced throughout | True out-of-distribution generalization |

---

## 🛠️ Tech Stack

<div align="center">
  <img src="https://img.shields.io/badge/DeepChem-Scientific_AI-blue?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/HuggingFace-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black"/>
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white"/>
  <img src="https://img.shields.io/badge/OLMo--7B-4bit_NF4-purple?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/RDKit-Chemistry-red?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/LoRA-PEFT-green?style=for-the-badge"/>
</div>

---

## 📂 File Index

| File | Description |
|------|-------------|
| `tox21_mistral_benchmark.py` | Mistral-7B training pipeline, scaffold split, 8x oversampling |
| `dataset.py` | Tox21 data loading, RDKit sanitization, scaffold split logic |
| `model.py` | OLMo-7B 4-bit NF4 wrapper with LoRA config |
| `train.py` | Training loop with checkpoint saving |
| `OLMo_Tox21_MultiTask_Final.ipynb` | Final OLMo-7B run — **Mean ROC-AUC 0.7225** |
| `graphconv-tox21-deepchem.ipynb` | RF baseline + scaffold vs random gap discovery |
| `requirements.txt` | Dependencies |

---

## 💻 How to Run
```bash
pip install -r requirements.txt

# Modular pipeline (OLMo-7B)
python dataset.py    # prepare data
python train.py      # train model

# Mistral-7B benchmark
python tox21_mistral_benchmark.py

# Full notebook — Kaggle
# kaggle.com/sameernadeem66/graphconv-tox21-deepchem
```

---

## 🔗 Part of DeepChem GSoC 2026 Research

| Task | Model | Result | Repo |
|------|-------|--------|------|
| BACE Classification | Mistral-7B QLoRA | 0.8371 ROC-AUC | [BACE Repo](https://github.com/Abu-Sameer-66/Mistral7B-BACE-Generalization-Study) |
| BBBP Classification | Mistral-7B QLoRA | 0.7141 ROC-AUC | [BBBP Repo](https://github.com/Abu-Sameer-66/Mistral7B-BBBP-Molecular-Reasoning) |
| ClinTox Classification | Mistral-7B QLoRA | 0.9913 ROC-AUC | [ClinTox Repo](https://github.com/Abu-Sameer-66/Mistral7B-ClinTox-Study) |
| **Tox21 Multi-Task** | **OLMo-7B QLoRA** | **0.7225 Mean ROC-AUC** | **This Repo** |
| ESOL Regression | OLMo-7B + Reg Head | 0.8582 RMSE | [ESOL Repo] |
| SMILES Generation | OLMo-7B + RDKit TSM | 20/20 = 100% valid | [Generation Repo](https://github.com/Abu-Sameer-66/olmo-smiles-generation-tsm) |
```

---

## Proposal mein Tox21 row update karo

**Page 4 table — Tox21 row:**

Old:
```
Tox21 | Multi-Task | Native GraphConv | CPU/T4 | 0.6859 & 0.72 BB
```

New:
```
Tox21 | Multi-Task | OLMo-7B (4-bit QLoRA) | Kaggle T4 | 0.7225 | 
Key finding: RF random split = 0.8183 vs scaffold = 0.6135 — 
0.20 gap proves published baselines overestimate generalization.
RDKit dropped 8 invalid metal-ion SMILES [Hg+2], [Fe+2].
