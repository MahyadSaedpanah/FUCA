# FUCA: Factorized and Uncertainty-Aware Contrastive Alignment for Time Series Domain Adaptation
[![Anonymous Review](https://img.shields.io/badge/Status-Anonymous%20Review-lightgrey.svg)](#anonymity-notice)
[![Third-Party Licenses](https://img.shields.io/badge/Third--Party-Licenses-blue.svg)](#third-party-assets-and-licenses)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Official anonymous implementation of the paper:

**FUCA: Factorized and Uncertainty-Aware Contrastive Alignment for Time Series Domain Adaptation**

> **Anonymous Submission**
>
> This repository accompanies a paper currently under anonymous peer review.
> Author names, affiliations, contact information, and other identifying
> information are intentionally omitted to preserve anonymity.
> They will be restored after the review process.

## Overview

Unsupervised domain adaptation (UDA) for time series aims to transfer
knowledge from a labeled source domain to an unlabeled target domain.
However, domain shifts may affect temporal and frequency characteristics
differently.

FUCA addresses this problem through three main components:

- **Robust Temporal-Frequency Correlation Graph (RTFC-G):**
  models sample-specific interactions between temporal and frequency
  representations and performs adversarial alignment in the resulting
  structured correlation space.

- **Dynamic Uncertainty-Aware Teacher Selection (DUTS):**
  estimates branch reliability and dynamically selects the more reliable
  branch for target-domain cross-view knowledge transfer.

- **Factorization-Aware Gated Contrastive Learning (FGC):**
  separates instance-preserving and shared cross-view objectives and
  adaptively balances them to preserve view-specific information while
  promoting reliable cross-view alignment.

Experiments are conducted on six benchmark datasets covering human
activity recognition, gesture recognition, and motor-imagery
classification.

## Status

This repository is provided anonymously for peer review and
reproducibility.

The repository contains the source code, experimental configurations,
and instructions required to reproduce the experiments reported in the
paper.

## Datasets

The experiments use the following publicly available datasets:

- [UCIHAR](https://researchdata.ntu.edu.sg/dataset.xhtml?persistentId=doi:10.21979/N9/0SYHTZ)
- [HHAR-P](https://researchdata.ntu.edu.sg/dataset.xhtml?persistentId=doi:10.21979/N9/OWDFXO)
- [WISDM](https://researchdata.ntu.edu.sg/dataset.xhtml?persistentId=doi:10.21979/N9/KJWE5B)
- [HHAR-D](https://woods-benchmarks.github.io/hhar.html)
- [EMG](https://github.com/microsoft/robustlearn/tree/main/diversify)
- [PCL](https://woods-benchmarks.github.io/pcl.html)

The preprocessed datasets should follow the same directory organization
used by the experimental pipeline.

Example:

```text
.
└── data
    ├── UCIHAR
    │   ├── train_0.pt
    │   ├── test_0.pt
    │   ├── ...
    │   └── train_n.pt
    │
    ├── WISDM
    │   ├── train_0.pt
    │   ├── test_0.pt
    │   └── ...
    │
    ├── HHAR-P
    │   └── ...
    │
    ├── HHAR-D
    │   └── ...
    │
    ├── EMG
    │   └── ...
    │
    └── PCL
        └── ...
```

## Experimental Protocol

For each domain, the data are divided into an 80% training split and a
20% testing split.

For each source-to-target transfer scenario:

- labeled source training samples are used for supervised learning;
- target training samples are treated as unlabeled during adaptation;
- target training labels are never used by the adaptation algorithm;
- evaluation is performed on the held-out target test split.

Z-score normalization is computed using only the corresponding training
split statistics.

All methods are evaluated using the same preprocessing, source-target
scenarios, data splits, random seeds, evaluation metrics, and training
budget.

Each experiment is trained for **50 epochs** with a mini-batch size of
**32**.

Each source-target scenario is repeated **5 times** using random seeds:

```text
0, 1, 2, 3, 4
```

The reported metrics are **Accuracy** and **Macro-F1**.

## Requirements

The implementation is based on Python and PyTorch.

Please install the required packages using the dependency file included
in this repository:

```bash
pip install -r requirements.txt
```

## How to Run

All experiment scripts are provided in the `scripts/` directory.

A separate `.sh` script is provided for each dataset, containing the
dataset-specific hyperparameters and experimental settings used in the
paper.

For example, the UCIHAR experiments can be run using:

```bash
bash scripts/UCIHAR.sh
```

The remaining datasets can be executed in the same way using their
corresponding scripts in the `scripts/` directory.

Each script reproduces the experimental configuration reported in the
paper and supplementary material, including the dataset-specific
hyperparameters and five repeated runs with different random seeds.

Dataset-specific hyperparameters and source-target transfer scenarios are
provided in the configuration files included in this repository.

The main dataset-dependent settings include the learning rate, DUTS
parameters, and FGC parameters. Fixed augmentation and contrastive
learning settings are shared across transfer scenarios as described in
the supplementary material.

## Hardware

The experiments reported in the paper were conducted on a single
**NVIDIA GeForce RTX 4090 GPU with 24 GB of memory**.

## Third-Party Assets and Licenses

FUCA uses publicly available datasets and open-source research code.
The corresponding original sources and licenses should be respected when
using or redistributing these assets.

| Asset | Source / License Information |
|---|---|
| UCIHAR | Original UCI dataset: Creative Commons Attribution 4.0 International (CC BY 4.0) |
| HHAR-P | Processed dataset hosted by NTU Research Data; see the linked dataset record for its license and terms of use |
| WISDM | Processed dataset hosted by NTU Research Data; see the linked dataset record for its license and terms of use |
| HHAR-D | Open Data Commons Attribution License |
| EMG / DIVERSIFY code | Distributed through the Microsoft `robustlearn` repository; repository code is released under the MIT License |
| PCL | Constituent datasets are distributed under their respective open-data licenses, including ODC Attribution 1.0, No Rights Reserved, and CC0 1.0 |
| AdaTime | MIT License |

Users of these datasets and codebases are responsible for complying with
the terms specified by their respective original providers.

## Acknowledgements

This implementation builds upon and follows the experimental conventions
of several publicly available research codebases. We thank the authors
of the following projects for making their code and datasets available:

- [AdaTime](https://github.com/emadeldeen24/AdaTime)
- [ACON](https://github.com/mingyangliu1024/ACON)
- [WOODS](https://github.com/jc-audet/WOODS)
- [DIVERSIFY / robustlearn](https://github.com/microsoft/robustlearn)

## Anonymity Notice

To comply with the double-blind review policy, this repository does not
contain author names, institutional affiliations, personal webpages,
personal GitHub profiles, or other identifying information.

Please do not attempt to identify the authors during the review process.
