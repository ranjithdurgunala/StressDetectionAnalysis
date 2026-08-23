# Leakage-Audited Cross-Corpus Evaluation of Social Media Stress Detection

This repository contains the executed research notebook and reproducibility materials for:

> **A Leakage-Audited Cross-Corpus Evaluation Framework for Social Media Stress Detection: Quantifying Construct Divergence Across Four Public Corpora**

The study examines whether poor cross-corpus generalisation in social-media stress detection is primarily explained by evaluation leakage, topical/domain variation, annotation/construct differences, community shortcuts, or label noise.

## Main experiments

| ID | Experiment | Main purpose |
|---|---|---|
| A | Structural leakage audit | Verify whether Dreaddit train/test partitions share parent posts. |
| B | Protocol comparison | Compare random segment-level and post-grouped evaluation. |
| C | In-domain validation | Establish that the transformer pipeline reaches the expected Dreaddit performance range. |
| D | Cross-corpus transfer | Measure transfer among Dreaddit, SAD, IRF, and MultiWD. |
| E | Cross-domain control | Measure topical variation within Dreaddit while holding the annotation scheme fixed. |
| F | Construct-validity probe | Measure how strongly community identity predicts the harmonised label. |
| G | Masking intervention | Compare community-specific masking with frequency-matched random masking. |
| H | Label-noise ceiling | Test whether higher-agreement Dreaddit labels improve external transfer. |

## Manuscript-aligned headline results

- **4 public corpora; 17,095 instances** after preprocessing.
- **Official Dreaddit parent-post overlap: 0.**
- Maximum protocol effect: **0.0052 macro-F1**, with no comparison significant at α = 0.05.
- RoBERTa-base positive-class F1: **83.34%**.
- MentalRoBERTa positive-class F1: **83.46%**.
- BERT-base positive-class F1: **82.40%**.
- MentalBERT positive-class F1: **82.67%**.
- Mean grouped in-domain macro-F1: **0.767**.
- Mean cross-corpus macro-F1: **0.476**.
- Overall transfer gap: **0.291**.
- Two of twelve transformer transfer conditions are at or below the strict majority-class macro-F1 baseline of approximately **0.343**.
- Dreaddit-anchored topical cost: **0.008**.
- Dreaddit-anchored between-corpus cost: **0.287**, representing **97.2%** of the anchored transfer gap.
- Three-corpus sensitivity gap excluding SAD: **0.240**.
- Oracle community-prior macro-F1: **0.600**.
- Community-specific masking effect: **−0.004**.
- Higher-agreement training changes external transfer by at most **0.004 macro-F1**.

These values are reproduced in `results/manuscript_reported_results.md`.

## Repository contents

```text
stress-detection-cross-corpus-evaluation/
├── Objective1_CrossCorpus_StressDetection_Final.ipynb
├── README.md
├── requirements.txt
├── LICENSE
├── CITATION.cff
├── protocol_specification.md
├── .gitignore
├── data/
│   └── README.md
├── docs/
│   └── reproducibility_checklist.md
├── results/
│   ├── README.md
│   └── manuscript_reported_results.md
└── figures/
    └── README.md
```

## Software requirements

The notebook is designed for a CUDA-enabled Kaggle or Colab runtime. A GPU is strongly recommended for the transformer experiments.

Install the Python dependencies with:

```bash
pip install -r requirements.txt
```

The notebook also checks the runtime environment and installs only missing packages when necessary.

## Execution order

Run the notebook from top to bottom.

1. **Section 0:** verify the environment and define the experimental configuration.
2. **Section 1:** download and harmonise the four corpora.
3. **Experiment A:** perform the structural leakage audit.
4. **Experiment B:** compare evaluation protocols.
5. **Experiment C:** run the four-encoder in-domain validation.
6. **Experiment D:** run cross-corpus transfer and grouped in-domain evaluation.
7. **Experiment E:** run the within-Dreaddit topical control.
8. **Experiments F/G:** run the community-identifiability and masking analyses.
9. **Experiment H:** run the label-noise ceiling analysis.
10. **Section 10:** calculate the manuscript-aligned decomposition.
11. **Section 11:** generate the publication figures.
12. **Section 12:** export tables, result files, and archives.

The notebook contains the outputs from the completed experimental run so that the public repository preserves the executed research record.

## Data

The four corpora are **not redistributed** here.

The notebook downloads the source files from repositories associated with the original resources. Users should consult and comply with the original dataset licences and terms.

The study uses:

- Dreaddit
- SAD
- IRF
- MultiWD

See `data/README.md` for details.

## Hugging Face models

The transformer comparison includes:

- `roberta-base`
- `bert-base-uncased`
- MentalRoBERTa
- MentalBERT

The domain-adapted mental-health checkpoints may require accepting their model licences and authenticating with a Hugging Face read token.

**Never commit a Hugging Face token or any other credential to GitHub.**

## Reproducibility and manuscript consistency

The notebook is deliberately aligned with the manuscript. In particular, the primary decomposition is **Dreaddit-anchored**, rather than the earlier exploratory all-corpus decomposition.

The repository therefore reports:

```text
Dreaddit grouped in-domain       0.835
Leave-one-domain-out mean       0.827
Dreaddit → other corpora        0.540
Topical cost                    0.008
Between-corpus cost             0.287
Between-corpus share            97.2%
```

The strict majority-class macro-F1 baseline is approximately **0.343**. The separate value **0.45** is not treated as the majority-class baseline.

## Code and result licence

The original code in this repository is released under the MIT License.

This licence applies to the repository's original code and documentation only. It does **not** grant rights to third-party datasets or pretrained model weights.

## Responsible use

The experiments concern automated analysis of mental-stress-related language. The models are research tools and should not be interpreted as clinical diagnostic systems. The results should not be used to diagnose an individual or make high-stakes decisions about a person's mental health.

## Citation

If you use this repository or the benchmark protocol, please cite the associated manuscript once the final bibliographic information is available.

See `CITATION.cff` for the repository citation metadata.
