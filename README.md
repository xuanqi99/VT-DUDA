# VT-DUDA: Visual Token Conditioning for Diffusion-guided Unsupervised Domain Adaptation

Official project page for:

**VT-DUDA: Visual Token Conditioning for Diffusion-guided Unsupervised Domain Adaptation**

**Xuan Qi, Daniele Berardini, Dario Serez, Vito Paolo Pastore, Vittorio Murino**

AI for Good (AIGO), Istituto Italiano di Tecnologia  
University of Genoa  
University of Verona

**Transactions on Machine Learning Research (TMLR), 2026**

---

## Overview

Unsupervised domain adaptation (UDA) aims to learn a target-domain classifier from labeled source data and unlabeled target data under distribution shift. Recent diffusion-based UDA methods synthesize labeled target-style images and use them as training data for downstream adaptation.

VT-DUDA studies the role of conditioning specificity in diffusion-guided UDA. Instead of relying only on text prompts, VT-DUDA introduces a visual-token conditioning interface that uses source images to provide instance-level visual context for target-style synthesis.

The core idea is to map each image into a compact sequence of visual tokens and concatenate these tokens with text embeddings along the cross-attention context dimension of a latent diffusion model. This provides instance-dependent conditioning beyond text alone while preserving the standard diffusion objective and keeping the diffusion backbone unchanged.

---

## Method

VT-DUDA contains three main stages:

1. **Token-conditioned diffusion training**
2. **Target-style data generation**
3. **Downstream UDA training**

The same token-conditioned interface supports both:

* Pure-noise target-style synthesis
* DDIM-inversion-based target-style translation

Because the visual guidance is represented as an explicit token sequence, VT-DUDA also allows inference-time token manipulation through token selection and token-strength adjustment.

---

## Key Contributions

* We propose **VT-DUDA**, a visual-token conditioning framework for diffusion-guided unsupervised domain adaptation.

* VT-DUDA augments the standard cross-attention interface of an adapter-based latent diffusion model with instance-dependent visual tokens.

* The method enriches source-side class prompts and target-side generic prompts without modifying the diffusion backbone, VAE, or denoising objective.

* We study two token-conditioned routes for constructing synthetic target-style training data:

  * Pure-noise target-style synthesis
  * DDIM-inversion-based target-style translation

* Experiments on Office-31, Office-Home, and VisDA-2017 demonstrate consistent improvements over strong discriminative and diffusion-based UDA baselines.

---

## Main Results

### Full VT-DUDA Configuration

| Method        | Office-Home Avg | Office-31 Avg | VisDA-2017 Mean |
| ------------- | --------------: | ------------: | --------------: |
| MCC           |           72.24 |         89.61 |           83.32 |
| ELS           |           71.84 |         90.21 |           83.40 |
| MCC + VT-DUDA |           76.25 |         91.53 |           87.48 |
| ELS + VT-DUDA |       **76.74** |     **92.04** |       **88.42** |

### Inversion-free Protocol

| Method        | Office-Home Avg | Office-31 Avg | VisDA-2017 Mean |
| ------------- | --------------: | ------------: | --------------: |
| MCC + VT-DUDA |           73.50 |         91.37 |           86.92 |
| ELS + VT-DUDA |       **73.72** |     **91.92** |       **87.56** |

---

## Datasets

VT-DUDA is evaluated on:

* Office-31
* Office-Home
* VisDA-2017

Target-domain classification accuracy is used as the evaluation metric.

---

## Citation

```bibtex
@article{qi2026vtduda,
  title={VT-DUDA: Visual Token Conditioning for Diffusion-guided Unsupervised Domain Adaptation},
  author={Qi, Xuan and Berardini, Daniele and Serez, Dario and Pastore, Vito Paolo and Murino, Vittorio},
  journal={Transactions on Machine Learning Research},
  year={2026},
  url={https://openreview.net/forum?id=Y956680PCe}
}
```

---

## Acknowledgments

This project page is built upon the Academic Project Page Template and the Nerfies project page.

* Academic Project Page Template: https://github.com/eliahuhorwitz/Academic-project-page-template
* Nerfies: https://nerfies.github.io/
