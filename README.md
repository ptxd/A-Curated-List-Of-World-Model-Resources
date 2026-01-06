# 🌍 Awesome World Models
[![Awesome](https://awesome.re/badge.svg)](https://awesome.re) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

> **"The essence of intelligence is the ability to predict the future."**

A curated "Zero-to-Hero" roadmap and collection of resources for building **World Models**—AI systems that learn an internal simulation of their environment to reason, plan, and act. This repository covers the evolution from foundational RNN-based models to modern Diffusion and Transformer-based Foundation World Models.



---

## 📖 Table of Contents
- [The Taxonomy of World Models](#-the-taxonomy-of-world-models)
- [Curated Project List (0 to Hero)](#-curated-project-list)
  - [Level 0-1: Foundational (RSSM)](#-level-0-1-foundational--rl-centric)
  - [Level 2: Transformers & Discrete Tokens](#-level-2-transformer-based)
  - [Level 3: Diffusion & Generative (SOTA)](#-level-3-the-hero-tier-generative--diffusion)
- [Standard Datasets](#-standard-datasets-the-fuel)
- [Evaluation Metrics](#-evaluation-metrics-the-score)
- [Glossary of Terms](#-glossary)
- [Quick Start](#-quick-start)

---

## 🧠 The Taxonomy of World Models

Before choosing a repo, understand the three main architectural approaches currently dominating the field:



| Architecture Type | Mechanics | Pros | Cons | Example |
| :--- | :--- | :--- | :--- | :--- |
| **RSSM (Recurrent State-Space)** | Uses RNNs to predict both deterministic (world rules) and stochastic (uncertainty) states. | Extremely fast inference; great for control/robotics. | Struggles with high-fidelity visual generation. | *DreamerV3* |
| **JEPA (Joint-Embedding)** | Predicts abstract *features* of the future, not pixels. No generation, only understanding. | Highly scalable; ignores visual noise. | Cannot "dream" video (cannot visualize its thoughts). | *V-JEPA* |
| **Generative (Diffusion/Transformer)** | Generates full high-fidelity video of future states (Autoregressive or Diffusion). | "Matrix-like" simulation; high visual detail. | Computationally expensive; slow inference. | *Sora, Diamond* |

---

## 🏆 Curated Project List

### 🟢 Level 0-1: Foundational & RL-Centric
*Best for: Understanding the basics, Robotics, Control Systems.*

| Project Name | GitHub Repository | Paper / Docs | Arch | Compute | Key Innovation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **World Models** (Orig) | [**ha-schmidhuber/world-models**](https://github.com/ctallec/world-models) | [Paper](https://worldmodels.github.io/) | VAE + RNN | ⚡ Low | The seminal paper. Decoupled vision (V) and memory (M) to train a controller (C) in "dreams." |
| **DreamerV3** | [**danijar/dreamerv3**](https://github.com/danijar/dreamerv3) | [Paper](https://arxiv.org/abs/2301.04104) | RSSM | ⚡⚡ Med | **The Gold Standard.** Masters diverse domains (Atari to Minecraft) with fixed hyperparameters. |
| **TD-MPC2** | [**nicklashansen/tdmpc2**](https://github.com/nicklashansen/tdmpc2) | [Website](https://www.tdmpc2.com/) | TOLD | ⚡⚡ Med | Local trajectory optimization. Highly efficient for continuous control tasks (robot arms). |

### 🟡 Level 2: Transformer-Based
*Best for: Long-horizon reasoning, Discrete environments, Sample efficiency.*

| Project Name | GitHub Repository | Paper / Docs | Arch | Compute | Key Innovation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **IRIS** | [**eloialonso/iris**](https://github.com/eloialonso/iris) | [Paper](https://arxiv.org/abs/2209.00588) | Transformer | ⚡⚡ Med | Replaces the RNN with a Transformer to model discrete latent tokens. More sample efficient than DreamerV2. |
| **LWM** | [**LargeWorldModel/LWM**](https://github.com/LargeWorldModel/LWM) | [Website](https://largeworldmodel.github.io/) | RingAttention | ⚡⚡⚡ High | **Millions of tokens.** Uses RingAttention to model 1H+ video context. A true "Foundation World Model." |

### 🔴 Level 3: The Hero Tier (Generative & Diffusion)
*Best for: High-fidelity simulation, Video generation, Interactive Environments.*

| Project Name | GitHub Repository | Paper / Docs | Arch | Compute | Key Innovation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **DIAMOND** | [**eloialonso/diamond**](https://github.com/eloialonso/diamond) | [Website](https://diamond-wm.github.io/) | Diffusion | ⚡⚡⚡ High | **SOTA 2024.** The first RL agent trained entirely inside a *Diffusion* world model. Handles visual details better than discrete tokens. |
| **GenieRedux** | [**insait-institute/GenieRedux**](https://github.com/insait-institute/GenieRedux) | [Paper](https://arxiv.org/abs/2402.15391) | ST-Transformer | ⚡⚡⚡ High | Open reproduction of Google's **Genie**. Generates playable 2D platformer worlds from a single image prompt. |
| **V-JEPA** | [**facebookresearch/jepa**](https://github.com/facebookresearch/jepa) | [Hugging Face](https://huggingface.co/facebook/vjepa) | JEPA | ⚡⚡⚡ High | **Non-Generative.** Learns physics/semantics by predicting latent features, not pixels. Very scalable. |

---

## 🛢 Standard Datasets (The Fuel)

You cannot build a World Model without data. These are the industry-standard environments used to train and test these models.



| Dataset / Environment | Type | Difficulty | Why use it? |
| :--- | :--- | :--- | :--- |
| **DeepMind Control Suite** | Physics (Joints) | 🟢 Easy | Standard for testing continuous control (walking, running). |
| **Atari 100k** | 2D Pixel | 🟡 Medium | The benchmark for sample efficiency. Can your model learn Space Invaders in 2 hours? |
| **Minecraft (Contractors)** | 3D Voxel | 🔴 Hard | Open-ended, long-horizon, partial observability. The ultimate test for World Models (*see DreamerV3*). |
| **RealEstate10K** | Video Walkthroughs | 🔴 Hard | Used for Video Generative World Models to test 3D consistency and infinite view synthesis. |
| **CARLA** | Autonomous Driving | 🔴 Hard | High-fidelity driving simulator for safety-critical world modeling. |

---

## 📏 Evaluation Metrics (The Score)

How do you know if your World Model is "Hero" status?

1.  **FVD (Fréchet Video Distance):** Measures the visual quality of the "dreamed" rollout compared to real video. Lower is better.
2.  **Zero-Shot Generalization:** Can the model control an agent in a level it has never seen before, purely by planning?
3.  **Reconstruction Loss:** How accurately can the VAE/Encoder reproduce the current frame?
4.  **Imagination Horizon:** How many steps into the future can the model predict before the simulation collapses into noise?

---

## 📖 Glossary

* **Latent Space ($z$):** A compressed representation of the world. The model doesn't think in pixels; it thinks in compressed "concepts."
* **RSSM (Recurrent State-Space Model):** A hybrid network that uses a deterministic path (RNN) to remember history and a stochastic path (VAE) to account for multiple possible futures.
* **Posterior Collapse:** A failure mode where the model ignores the latent code and just guesses the average image.
* **Model-Based RL:** Reinforcement Learning where the agent learns a policy by imagining consequences in the World Model, rather than trial-and-error in the real world.

---

## ⚡ Quick Start

To get started with the most stable implementation (**DreamerV3**), run the following in Google Colab or your local GPU machine:

```bash
# Clone the repository
git clone [https://github.com/danijar/dreamerv3](https://github.com/danijar/dreamerv3)
cd dreamerv3

# Install dependencies
pip install -r requirements.txt

# Run training on a simple task (requires no heavy setup)
python3 main.py --logdir ./logdir/cartpole --configs gymnasium --task CartPole-v1
