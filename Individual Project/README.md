# Reproducibility Study: UNBench Task 3 — Draft Adoption Prediction

## Overview

This is a reproducibility study of [UNBench](https://arxiv.org/abs/2502.14122) (Liang et al., AAAI 2026), focusing on **Task 3: Draft Adoption Prediction** — a binary classification task where an LLM predicts whether a UN Security Council draft resolution will be adopted.

**Original paper:** [Benchmarking LLMs for Political Science: A United Nations Perspective](https://arxiv.org/abs/2502.14122)  
**Original repo:** [https://github.com/yueqingliang1/UNBench](https://github.com/yueqingliang1/UNBench)

## Repository Structure

```
Individual Project/
├── README.md                          # This file
├── data/
│   └── task3.json                     # 30-sample evaluation subset
├── notebooks/
│   ├── task3_replication_deepseek.ipynb    # Reproduction with DeepSeek-V3
│   └── task3_modification_gemini.ipynb     # Modification with Gemini-2.5-Pro
└── report/
    └── FTEC5660_individual_project.pdf    # Final report
```

## Setup & Installation

### 1. Clone the repository
```bash
git clone https://github.com/wsnddddddddddddddd/FTEC5660.git
cd "FTEC5660/Individual Project"
```

### 2. Install dependencies
```bash
pip install openai scikit-learn imbalanced-learn tqdm pandas
```

### 3. Configure API keys

**For reproduction (DeepSeek-V3):**
- Sign up at [https://platform.deepseek.com](https://platform.deepseek.com)
- Get an API key
- In the notebook, replace `"YOUR_API_KEY_HERE"` with your key

**For modification (Gemini-2.5-Pro):**
- Sign up at [https://aistudio.google.com](https://aistudio.google.com)
- Get an API key
- In the notebook, replace `"YOUR_API_KEY_HERE"` with your key

## How to Run

### Reproduction (DeepSeek-V3)
1. Open `notebooks/task3_replication_deepseek.ipynb` in Jupyter Notebook
2. Fill in your DeepSeek API key in Cell 2
3. Run all cells sequentially
4. Results will be printed in the final cell

### Modification (Gemini-2.5-Pro)
1. Open `notebooks/task3_modification_gemini.ipynb` in Jupyter Notebook
2. Fill in your Gemini API key in Cell 2
3. Run all cells sequentially
4. Repeat 5 times to collect variance data (results vary due to Gemini's safety filters)

## Key Results

| Metric | DeepSeek-V3 (Ours) | Gemini-2.5-Pro (Mean ± Std) | Paper (n=1,978) |
|--------|--------------------|-----------------------------|-----------------|
| Accuracy | 1.000 | 0.553 ± 0.122 | 0.966 |
| Bal. ACC | 1.000 | 0.479 ± 0.313 | 0.724 |
| F1 | 1.000 | 0.064 ± 0.088 | 0.585 |
| MCC | 1.000 | −0.014 ± 0.230 | 0.597 |

**Key finding:** Gemini-2.5-Pro's safety filters block geopolitical content in UN resolutions, causing frequent null responses and near-random performance. DeepSeek-V3 has no such restrictions and achieves perfect accuracy on the 30-sample subset.

## Changes from Original Repository

1. **API client switch:** Replaced `Together` library with `OpenAI` client for DeepSeek/Gemini compatibility
2. **Model change (modification):** Swapped DeepSeek-V3 → Gemini-2.5-Pro
3. **None-check fix:** Added null response handling for Gemini's safety filter

## Notes

- No API keys are committed in this repository
- The 30-sample subset is a representative sample; the full dataset (1,978 drafts) is available from the [original authors' Google Drive](https://drive.google.com/file/d/1tiBCCYPjeIN92TkO8Vt8vrpSKLmGb-6Y/view)
- Results on the 30-sample subset are not directly comparable to the paper's full-dataset results
