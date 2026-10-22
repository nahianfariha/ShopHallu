# ShopHallu

**ShopHallu: An Automatically Labelled and Human-Validated Dataset of Unsupported Claims in LLM-Generated Influencer-Style Product Reviews**

**Authors:** Nahian Fariha, Farzana Tasnim, and Lutfun Nahar

- Nahian Fariha — Independent Researcher, Bangladesh
- Farzana Tasnim — International Islamic University Chittagong, Bangladesh
- Lutfun Nahar — The University of Newcastle, Australia

[Paper](#paper) · [Dataset](#dataset) · [Methodology](#methodology) · [Results](#key-findings) · [Citation](#citation)

---

## Overview

ShopHallu is a dataset for analysing unsupported claims in large language model (LLM)-generated influencer-style product reviews. It investigates how prompt templates, language models, generation temperatures, product categories, and customer-review evidence relate to unsupported claims in generated promotional content.

The dataset contains **4,455 generated paragraphs** for 99 Amazon products across three product categories. Each paragraph is paired with five held-out customer reviews, resulting in **22,275 paragraph–review pairs**. The pairs are automatically labelled as `Hallucinated`, `Supported`, or `Neutral` relative to the corresponding held-out review.

The study also evaluates agreement between automatic labels and a human annotator on a subset of 500 pairs and examines whether rule-based signals can help identify unsupported claims.

## Research Questions

This study addresses three research questions:

- **RQ1:** How do the prompt template, the model, and the temperature shape the style and promotional language of LLM-generated influencer-style product reviews?
- **RQ2:** How are the prompt template, the model, the product category, the temperature, and the evidence review associated with unsupported claims in these reviews?
- **RQ3:** How closely do the automatic labels and the rule-based signals agree with the judgement of a human annotator?

## Key Statistics

| Item | Value |
|---|---:|
| Products | 99 |
| Product categories | 3 |
| Generated paragraphs | 4,455 |
| Paragraph–review pairs | 22,275 |
| Automatically labelled pairs | 22,275 |
| Pairs included in the main analysis | 13,178 |
| Human-labelled pairs | 500 |
| Products in the human-labelled subset | 12 |
| Human–automatic observed agreement | 89.0% |
| Cohen's kappa | 0.83 |

## Dataset

### Source

The source data comes from **Amazon Review Data (2018)** by Ni et al. (UCSD), using the 5-core subsets.

Source: [Amazon Review Data (2018)](https://nijianmo.github.io/amazon/index.html)

The study uses reviews from the following categories:

- All Beauty
- Grocery and Gourmet Food
- Cell Phones and Accessories

Products were selected from the source data according to the study's eligibility criteria. Three customer reviews per product were used as generation context, while five held-out reviews per product were used as evidence for evaluating the generated paragraphs.

### Dataset construction

ShopHallu was constructed in three stages:

1. **Influencer-style paragraph generation:** Three LLMs generated paragraphs using three prompt templates and five temperature settings.
2. **Automatic labelling:** Each generated paragraph was paired with five held-out customer reviews. Claude Sonnet 4.6 assigned a coarse-grained label, with rule-based signals supplied as hints.
3. **Human–automatic comparison:** A subset of 500 pairs from 12 products was manually labelled by one human annotator and compared with the automatic labels.

### Label definitions

- **Hallucinated:** The generated paragraph contains content that is not supported by the paired evidence review, according to the study's labelling procedure.
- **Supported:** The paired evidence review supports the generated content.
- **Neutral:** The pair is assigned neither of the other two labels under the labelling procedure.

These labels are relative to the selected evidence review. An unsupported claim is not necessarily proven false; the evidence review may simply not establish whether the claim is true.

## Methodology

### Models

The generation stage evaluates three models:

- GPT-4o-mini
- Llama-3.1-8B-Instruct
- Gemini-3.5-Flash

Claude Sonnet 4.6 is used for automatic labelling.

### Experimental settings

| Parameter | Settings |
|---|---|
| Prompt templates | Strict, Neutral, Persuasive |
| Temperature | 0.0, 0.3, 0.5, 0.7, 1.0 |
| Products | 99 |
| Context reviews per product | 3 |
| Held-out evidence reviews per product | 5 |
| Generated paragraphs per setting | 1 |

### Rule-based signals

The automatic labelling procedure uses signals including:

- Sentence-BERT semantic similarity
- Keyword overlap
- Non-overlapping terms
- A promotional-language lexicon

These signals are provided as hints to the automatic labelling model. They should not be interpreted as independently verified ground-truth labels.

## Key Findings

The paper reports the following findings:

- Among the **13,178 analysed pairs**, 55.46% were labelled `Hallucinated`.
- The hallucination rate ranged from **34.74% under the Strict prompt template to 75.49% under the Persuasive template**.
- The difference between models depended on the prompt template.
- Evidence for an effect of generation temperature was weak.
- The hallucination rate was associated with the length of the evidence review.
- The same generated paragraph could be labelled `Supported` against one evidence review and `Hallucinated` against another.
- Automatic labels agreed with the human annotator on 89.0% of the 500 manually labelled pairs, with Cohen's kappa of 0.83.
- The evaluated surface-level signals did not outperform a majority-class baseline against the human labels.

These findings should be interpreted in light of the dataset construction, evidence selection, automatic labelling procedure, and limitations of the human-labelled subset.

## Repository Structure

The following is a suggested repository layout. Keep the entries that correspond to files actually included in the public repository.

```text
ShopHallu/
├── data/
│   ├── processed/
│   └── annotations/
├── notebooks/
│   ├── 01_dataset_generation.ipynb
│   ├── 02_rule_based_analysis_for_annotation.ipynb
│   └── 03_evaluation.ipynb
├── figures/
│   └── shophallu_framework.png
├── docs/
│   └── dataset_card.md
├── requirements.txt
├── LICENSE
└── README.md
```

## Framework Figure

If the paper's Figure 1 is included in the repository, it can be displayed here.

![ShopHallu framework](figures/shophallu_framework.png)

*Figure 1. Overview of the ShopHallu dataset construction and evaluation pipeline. Source: Figure 1 of the paper.*

## Reproducibility

To clone the repository:

```bash
git clone https://github.com/nahianfariha/ShopHallu.git
cd ShopHallu
```

If `requirements.txt` is included, install the dependencies:

```bash
pip install -r requirements.txt
```

Run the notebooks in the documented order, if they are present:

1. `01_dataset_generation.ipynb`
2. `02_rule_based_analysis_for_annotation.ipynb`
3. `03_evaluation.ipynb`

Reproduction may require access to the source review data, model APIs, and the prompts and settings used in the experiments. The repository should document the exact model identifiers, prompts, data-processing steps, and any unavailable intermediate files. Do not commit API keys or credentials.

## Limitations

ShopHallu has several limitations:

- The study covers 99 products across three Amazon categories and three evaluated LLMs.
- The human-labelled subset contains 500 pairs from 12 products and was labelled by one human annotator.
- The labels are based on individual held-out customer reviews rather than authoritative product specifications or independent fact verification.
- Fine-grained hallucination categories are exploratory and have substantially lower human–automatic agreement than the coarse-grained labels.
- The findings may not generalise to other languages, product categories, models, or prompting strategies.

Please consult the paper for the complete methodology, statistical analyses, and discussion.

## Paper

**Title:** ShopHallu: An Automatically Labelled and Human-Validated Dataset of Unsupported Claims in LLM-Generated Influencer-Style Product Reviews

**Authors:** Nahian Fariha, Farzana Tasnim, and Lutfun Nahar

**Preprint:** Add the arXiv link after the paper has been successfully submitted and its public record is available.

## Citation

If you use ShopHallu in your research, please cite the paper. Until a stable preprint identifier is available, the following provisional BibTeX entry can be used:

```bibtex
@misc{fariha2026shophallu,
  title  = {ShopHallu: An Automatically Labelled and Human-Validated Dataset of Unsupported Claims in LLM-Generated Influencer-Style Product Reviews},
  author = {Fariha, Nahian and Tasnim, Farzana and Nahar, Lutfun},
  year   = {2026},
  note   = {Preprint}
}
```

Update this entry with the verified arXiv identifier or publication details when available.

## License

**Code:** Specify the code license in the repository's `LICENSE` file.

**Dataset:** Check the source dataset's terms and the redistribution rights for every included component before specifying a dataset license. A license for your own code or annotations does not automatically grant permission to redistribute third-party customer-review text.

## Contact

For questions or research-related enquiries, contact:

**Nahian Fariha** — nahianfariha.cs@gmail.com
