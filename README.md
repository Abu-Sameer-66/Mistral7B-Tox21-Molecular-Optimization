<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&ColorList=896A15,6E8915,98351F&height=200&section=header&text=Tox21%20Optimization%20%7C%20Mistral7B&fontSize=40&fontColor=DEE2D9&animation=fadeIn&fontAlignY=35&desc=LLM%20Fine-tuning%20%7C%20DeepChem%20GSoC%20'26%20&descAlignY=60&descAlign=50" width="100%"/>
</div>

<div align="center">
  <img 
    src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=32&pause=1000&color=DEE2D9&center=true&vCenter=true&width=1000&lines=Fine-tuning+Mistral-7B+on+Tox21+Dataset;Achieving+0.72+Mean+ROC-AUC;Solving+Gradient+Instability+with+fp32+Upcasting;8x+Oversampling+for+Imbalanced+Tox+Labels."
    alt="Typing SVG"
  />
</div>

<br/>













---

### 🧬 Project Overview
This repository contains the professional implementation of a **Mistral-7B** based molecular property predictor, optimized specifically for the **Tox21** dataset. Developed as a pre-proposal prototype for **Google Summer of Code 2026** with **DeepChem**, this project demonstrates how general-purpose LLMs can be adapted for high-accuracy chemical toxicity screening on consumer hardware.

---

### 🚀 Key Scientific Engineering

| Engineering Challenge | Proposed Solution | Technical Impact |
|:---|:---|:---|
| **Numerical Instability** | **fp32 Upcasting** for loss calculation & Gradient Clipping. | Eliminated **NaN Loss crashes** inherent in fp16 mixed-precision training. |
| **Memory Bottleneck** | **4-bit NF4 Quantization** & Gradient Checkpointing. | Enabled training on **16GB VRAM GPUs** (Google Colab T4) with under 6GB footprint. |
| **Class Imbalance** | Dynamic **8x Oversampling** for minority toxic classes. | Prevented model bias toward "Non-Toxic" majority labels, ensuring high sensitivity. |
| **Data Integrity** | Rigorous **Scaffold Splitting** methodology. | Validated out-of-distribution generalization, critical for drug discovery. |

---

### 📊 Performance Benchmarks (Tox21)

| Model | Dataset | Strategy | Mean ROC-AUC |
|:---|:---|:---|:---|
| **Mistral-7B** | **Tox21** | LoRA ($r=64$) + fp32 Upcasting | **0.7200** |



---

### 🛠️ Production Tech Stack

<div align="center">
  <img src="https://img.shields.io/badge/DeepChem-Scientific_AI-blue?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/HuggingFace-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black"/>
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white"/>
  <img src="https://img.shields.io/badge/LoRA-PEFT-green?style=for-the-badge"/>
  <br/>
</div>

---

### 📂 Repository Structure
- `scripts/tox21_benchmark.py`: Core training and evaluation pipeline.
- `requirements.txt`: Environment dependencies.
- `assets/`: Training curves and scientific validation plots.

### 💻 How to Run
1. **Clone the repository:**
   ```bash
   git clone [https://github.com/Abu-Sameer-66/Mistral7B-Tox21-Molecular-Optimization.git](https://github.com/Abu-Sameer-66/Mistral7B-Tox21-Molecular-Optimization.git)
