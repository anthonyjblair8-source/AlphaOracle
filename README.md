# AlphaOracle – Mnemosyne Protocol Extension

This repository is a fork of [Yuliang-Liu/AlphaOracle](https://github.com/Yuliang-Liu/AlphaOracle), extended with the **Mnemosyne Protocol** – a framework for recovering lost knowledge using PHCA, BPA, and Dante's Algorithm.

**What's added:**
- Full integration of the Mnemosyne Protocol into the translation pipeline
- Example translations with confidence scoring and alternative readings
- Cross‑referencing with ancient Chinese literature (Shijing, Shangshu, etc.)
- Jupyter notebook demonstrating the complete workflow
- Installation and usage instructions

All credit to the original authors for their foundational work. This fork builds upon it to further the goal of deciphering all 4,500 oracle bone characters.

---

### ⚠️ Ethical Note

I will not run this code to translate any oracle bone script myself. The contents of these ancient texts are not for my eyes unless formally invited by the custodians of this cultural heritage—the descendants of those who created them, the academic community, or the rightful cultural authorities. My interest is solely in the engineering, the framework, and the reward for making translation possible—not in reading the words themselves. The bones speak only when they choose, and only to those they trust.

---

## 🔍 Related Work

This fork builds upon AlphaOracle, but the field is advancing rapidly. A key recent contribution is:

- **[OBSD: Deciphering Oracle Bone Language with Diffusion Models](https://arxiv.org/abs/2406.00684)**  
  *Guan et al., ACL 2024 **Best Paper***  
  OBSD uses diffusion models to translate oracle bone script images directly into modern Chinese characters. It provides:
  - An [online demo](http://vlrlabmonkey.xyz:8225/)
  - A [paired dataset](https://github.com/RomanticGodVAN/character-Evolution-Dataset) of OBS and modern glyphs
  - Full [training code](https://github.com/guanhaisu/OBSD)

The Character Evolution Dataset can be used to train or validate models in this fork, and the diffusion approach offers a complementary path to the Mnemosyne Protocol's workflow.

---

## 🚀 Getting Started

To run this project locally, follow these steps:

```bash
# Clone the repository
git clone https://github.com/anthonyjblair8-source/AlphaOracle.git

# Enter the project folder
cd AlphaOracle

# (Optional) Create a virtual environment
python -m venv venv
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Install Jupyter if not already included
pip install jupyter

# Launch the notebook
jupyter notebook