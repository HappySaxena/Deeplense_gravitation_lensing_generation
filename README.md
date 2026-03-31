# GSoC 2026 ML4SCI Evaluation Tasks - DeepLense 🚀

**Deep Learning for Strong Gravitational Lensing: Classification, Physics-Informed Neural Networks (PINNs), and Equivariant Diffusion Models.**

This repository contains the code, experiments, and results for the official evaluation tasks for the Google Summer of Code (GSoC) 2026 project under the **ML4SCI** umbrella (DeepLense).

The objective of these tasks is to explore and benchmark advanced deep learning architectures on astrophysical data. The project spans architectural benchmarking for classification, the integration of continuous physical constraints (e.g, Lens Equation) via Physics-Informed Neural Networks (PINNs), and the generation of highly realistic physical tensor fields using $E(2)$-Steerable Denoising Diffusion Probabilistic Models (DDPMs).

---

## 📦 Datasets & Pretrained Weights

**Note:** Due to GitHub's file size limitations, all optimized model weights (`.pth` files) and large generated datasets have been hosted externally.

🔗 [https://drive.google.com/file/d/1cJyPQzVOzsCZQctNBuHCqxHnOY7v7UiA/view?usp=sharing](#) *(taskviii dataset)*

🔗 [https://drive.google.com/file/d/1ZEyNMEO43u3qhJAwJeBZxFBEYc_pVYZQ/view](#) *(Commontask & task vii dataset)*

🔗 [https://drive.google.com/drive/folders/1QoDiosI5NxA9qdOUWjQ_GM5R6juUEIRX?usp=drive_link](#) *(Weights)*

To run inference or resume training, please download the respective weights from the Drive link above and place them in the root directory, or update the weight paths inside the respective Jupyter notebooks.

---

## 📂 Repository Structure

The repository is divided into three primary modules based on the evaluation tasks. Each directory contains modular Jupyter Notebooks for training pipelines and a dedicated `Results/` folder for visualizations.

```text
Deeplense_gravitation_lensing_generation/
│
├── common_task/
│   ├── Results/                          # ROC curves, loss trajectories, parameter comparisons
│   ├── common-task-custom.ipynb          # Custom baseline architecture experiments
│   └── common_task_classification_multiple_models_comparision.ipynb # Benchmarking ViTs, ConvNeXt, ResNet
│
├── specific_task vii/                    # Physics-Informed Classification
│   ├── physics-block-implementation.ipynb# Core differentiable optics module (Lens Equation)
│   ├── task_vii_pinn_1st approach.ipynb  # PINN Approach 1: Source concatenation
│   ├── taskvii-pinn-2nd approach.ipynb   # PINN Approach 2: Source-only classification
│   └── *.png                             # ROC curves for PINN approaches
│
└── specific_task viii/                   # Generative Diffusion Models
    ├── result-1st approach/              # DDIM sampling, SLERP interpolations, epoch progressions
    ├── result-2nd approach/              # Equivariant model generation outputs
    ├── taskviii-1st-approach.ipynb       # Baseline DDPM implementation for lensing generation
    └── taskviii-2nd-equivariant-approach.ipynb # Advanced E(2)-Steerable Generative Engine\
```
## Links
- [GSOC 2026 Project Description](https://ml4sci.org/gsoc/2026/proposal_DEEPLENSE8.html)
- [Deep Learning the Morphology of Dark Matter Substructure](https://arxiv.org/abs/1909.07346)
