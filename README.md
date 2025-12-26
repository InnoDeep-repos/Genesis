# Genesis: Energy-Aware Sparse Routing Outperforms Mixture-of-Experts at Scale

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![ArXiv](https://img.shields.io/badge/arXiv-2505.xxxxx-b31b1b.svg)](https://arxiv.org/abs/2505.xxxxx)
[![Python](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Pytorch](https://img.shields.io/badge/pytorch-2.1+-orange.svg)](https://pytorch.org/)

> **"The future of efficient AI lies not just in sparsity, but in energy-centric design principles."**

**Genesis** is a novel sparse Mixture-of-Experts (MoE) architecture governed by a bio-physical energy functional. Unlike standard routers (Mixtral, DeepSeek) that optimize for loss or FLOPs, Genesis explicitly minimizes **routing stress** and maximizes **semantic cohesion**.

The result? A model that is **faster, greener, and more stable** than the current state-of-the-art.

---

## 🏆 Key Results (7B Scale on H200)

We compared Genesis against **Mixtral (Top-2)** and **DeepSeek (Shared + Top-2)** on an NVIDIA H200 GPU.

| Model | Time (s) | Energy (kJ) | Speedup | Energy Savings |
| :--- | :--- | :--- | :--- | :--- |
| Mixtral (Top-2) | 265.8 | 101.5 | 1.0x | -- |
| DeepSeek (Shared+Top2) | 242.9 | 99.7 | 1.09x | -1.8% |
| **Genesis (Energy-Aware)** | **150.4** | **80.1** | **1.77x** | **-21.1%** |

![Genesis Results](Genesis_vs_Mixtral_DeepSeek_7B_PRO_BarChart.png)

## 🧬 How It Works

Genesis treats the routing process as a physical system seeking a low-energy state.
$$ H = E_{bind} + E_{entropy} + E_{cost} $$
*   **$E_{bind}$ (Binding Energy):** Tokens are attracted to experts with matching semantic centroids.
*   **$E_{entropy}$ (Stability):** Penalizes uncertain routing decisions.
*   **$E_{cost}$ (Load Balancing):** Penalizes expert overload (buffer overflows).

This allows the model to naturally evolve specialized experts without the need for complex auxiliary load-balancing losses.

## 🚀 Quick Start

### Installation

```bash
git clone https://github.com/yourusername/genesis.git
cd genesis
pip install -r requirements.txt
```

### Run the 7B Experiment

You can reproduce the 7B scale experiment (Genesis vs Mixtral vs DeepSeek) using the provided script.

```bash
# Run Genesis (Default)
python train_7b.py --mode genesis

# Run Mixtral Baseline
python train_7b.py --mode mixtral

# Run DeepSeek Baseline
python train_7b.py --mode deepseek
```

### Use in Your Own Code

Genesis is designed as a modular drop-in replacement for LLaMA MLPs.

```python
from genesis import inject_router

# Load your LLaMA model
model = LlamaForCausalLM.from_pretrained("meta-llama/Llama-2-7b-hf")

# Inject Genesis Router (Energy-Aware)
model = inject_router(model, mode="genesis")

# Train as usual!
```

## 🧪 Isoflopic Validation (1B Scale)

We also provide the code for the **Isoflopic Validation** (Section 4.3 of the paper), proving that Genesis's gains come from superior routing, not just FLOP reduction.

```bash
python V15_Isoflopic_Experiment.py
```

## 📜 Citation

If you use Genesis in your research, please cite our paper:

```bibtex
@article{mustapha2025genesis,
  title={Genesis: Energy-Aware Sparse Routing Outperforms Mixture-of-Experts at Scale},
  author={Mustapha, Hamdi},
  journal={arXiv preprint arXiv:2505.xxxxx},
  year={2025}
}
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
