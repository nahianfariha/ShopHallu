# ShopHallu

**ShopHallu: A Benchmark Dataset and Evaluation Framework for Detecting Hallucination in LLM-Generated Influencer-Style Product Reviews**

Nahian Fariha¹, Farzana Tasnim¹, Lutfun Nahar²
¹International Islamic University Chittagong · ²University of Newcastle, Australia

[Paper link — coming soon] · [Dataset]

---

## Overview

ShopHallu is a benchmark dataset and evaluation framework for detecting hallucination in LLM-generated influencer-style product reviews. It provides a rule-based analysis pipeline, human-annotated samples (Cohen's Kappa κ = 0.8278, 89.00% observed agreement), and an evaluation of multiple LLMs on the hallucination detection task.

<!-- TODO: paste 2-3 line abstract summary here -->

## Repository Structure

```
ShopHallu/
├── data/
│   ├── processed/          # Final dataset used in the paper
│   └── annotations/        # Annotator files + Cohen's Kappa samples
├── notebooks/
│   ├── 01_dataset_generation.ipynb
│   ├── 02_rule_based_analysis_for_annotation.ipynb
│   └── 03_evaluation.ipynb
├── figures/                 # Figures used in the paper
└── README.md
```

## Dataset

The base product review data is sourced from the [Amazon Reviews dataset](https://amazon-reviews-2023.github.io/) (categories: All Beauty, Cell Phones & Accessories, Grocery & Gourmet Food). Raw category files are **not** included in this repo due to size — see `docs/dataset_card.md` for download instructions.

The processed ShopHallu dataset (`data/processed/`) contains LLM-generated influencer-style reviews with rule-based and human-annotated hallucination labels.

## Setup

```bash
git clone https://github.com/nahianfariha/ShopHallu.git
cd ShopHallu
pip install -r requirements.txt
```

Run notebooks in order: `01_dataset_generation.ipynb` → `02_rule_based_analysis_for_annotation.ipynb` → `03_evaluation.ipynb`

## Results

<!-- TODO: fill in key numbers table — e.g. model comparison, hallucination detection accuracy -->

| Metric | Value |
|---|---|
| Cohen's Kappa (κ) | 0.8278 |
| Observed Agreement | 89.00% |

## Citation

This paper is currently under review. A formal citation (with journal, volume, DOI) will be added here once it is accepted/published. Until then, please cite this repository directly:

```bibtex
@misc{shophallu2026,
  title  = {ShopHallu: A Benchmark Dataset and Evaluation Framework for Detecting Hallucination in LLM-Generated Influencer-Style Product Reviews},
  author = {Nahian Fariha and Farzana Tasnim and Lutfun Nahar},
  year   = {2026},
  note   = {Under review},
  howpublished = {\url{https://github.com/nahianfariha/ShopHallu}}
}
```

## License

- **Code** (notebooks, scripts) is released under the [MIT License](LICENSE).
- **Dataset** (`data/`) is released under [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/) — you may use, share, and adapt it, provided appropriate credit is given.

See the `LICENSE` file in this repo for the full code license text.

## Contact

For questions, open an issue or contact nahianfariha.cs@gmail.com
