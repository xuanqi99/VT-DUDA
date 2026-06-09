# VT-DUDA: Visual Token Conditioning for Diffusion-guided Unsupervised Domain Adaptation

Official project page repository for:

**VT-DUDA: Visual Token Conditioning for Diffusion-guided Unsupervised Domain Adaptation**

**Authors:**
Xuan Qi, Daniele Berardini, Dario Serez, Vito Paolo Pastore, Vittorio Murino

**Affiliations:**
AI for Good (AIGO), Istituto Italiano di Tecnologia
University of Genoa
University of Verona

**Venue:** Transactions on Machine Learning Research, 2026

---

## Project Page

Project page:

```text
https://xuanqi99.github.io/VT-DUDA/
```

OpenReview page:

```text
https://openreview.net/forum?id=Y956680PCe
```

Paper PDF:

```text
https://openreview.net/pdf?id=Y956680PCe
```

---

## Overview

Unsupervised domain adaptation (UDA) aims to learn a target-domain classifier from labeled source data and unlabeled target data under distribution shift. Recent diffusion-based UDA methods synthesize labeled target-style images and use them as training data for downstream adaptation.

VT-DUDA studies the role of conditioning specificity in diffusion-guided UDA. Instead of relying only on text prompts, VT-DUDA introduces a visual-token conditioning interface that uses source images to provide instance-level visual context for target-style synthesis.

The core idea is to map each image into a compact sequence of visual tokens and concatenate these tokens with text embeddings along the cross-attention context dimension of a latent diffusion model. This provides instance-dependent conditioning beyond text alone while preserving the standard diffusion objective and keeping the diffusion backbone unchanged.

---

## Method

VT-DUDA contains three main stages:

1. **Token-conditioned diffusion training**
   We jointly train domain-specific diffusion adapters and an image-to-token encoder using labeled source images and unlabeled target images.

2. **Target-style data generation**
   For each labeled source image, VT-DUDA extracts visual tokens, combines them with the class prompt, and synthesizes target-style images under the target-domain adapter branch.

3. **Downstream UDA training**
   A classifier is trained on the generated labeled target-style dataset, optionally together with an unsupervised target regularizer.

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

* Experiments on Office-31, Office-Home, and VisDA-2017 show that VT-DUDA improves average target-domain accuracy over strong discriminative and diffusion-based UDA baselines.

---

## Figures

The project page uses the following paper figures:

```text
static/images/1.pdf
static/images/2.pdf
static/images/3.pdf
```

Figure descriptions:

* **Figure 1:** Overview of VT-DUDA.
* **Figure 2:** Token-strength scaling for target-style synthesis.
* **Figure 3:** Token-subset manipulation under translation-based augmentation.

---

## Main Results

### Full VT-DUDA Configuration

The full configuration combines pure-noise target-style synthesis with inversion-based translation.

| Method        | Office-Home Avg | Office-31 Avg | VisDA-2017 Mean |
| ------------- | --------------: | ------------: | --------------: |
| MCC           |           72.24 |         89.61 |           83.32 |
| ELS           |           71.84 |         90.21 |           83.40 |
| MCC + VT-DUDA |           76.58 |         92.23 |           87.48 |
| ELS + VT-DUDA |       **77.34** |     **92.84** |       **88.42** |

### Inversion-free Protocol

The inversion-free protocol uses only pure-noise target-style generation.

| Method        | Office-Home Avg | Office-31 Avg | VisDA-2017 Mean |
| ------------- | --------------: | ------------: | --------------: |
| MCC + VT-DUDA |           73.50 |         91.37 |           86.92 |
| ELS + VT-DUDA |       **73.72** |     **91.92** |       **87.56** |

---

## Datasets

VT-DUDA is evaluated on three standard UDA benchmarks:

* **Office-31**
* **Office-Home**
* **VisDA-2017**

The reported metric is target-domain classification accuracy.

---

## Implementation Notes

The paper instantiates VT-DUDA on top of Stable Diffusion XL (SDXL). The VAE and text encoders are frozen, and lightweight adapter parameters are trained together with the image-to-token encoder.

Main implementation settings:

* Diffusion backbone: SDXL
* Adapter type: LoRA-style domain-specific adaptation
* Image-to-token encoder: ResNet-18
* Default visual token count: `M = 10`
* Office-31 / Office-Home generation budget: 50 images per class
* VisDA-2017 generation budget: 1000 images per class

---

## Repository Structure

This repository currently hosts the project page.

```text
VT-DUDA/
├── index.html
├── README.md
├── .nojekyll
└── static/
    ├── css/
    ├── js/
    └── images/
        ├── 1.pdf
        ├── 2.pdf
        ├── 3.pdf
        └── favicon.ico
```

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

The project page is based on the Academic Project Page Template, which was adapted from the Nerfies project page.

* Academic Project Page Template: https://github.com/eliahuhorwitz/Academic-project-page-template
* Nerfies: https://nerfies.github.io/

---

## Website License

This project page follows the license of the Academic Project Page Template.

The website source is licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.

```text
https://creativecommons.org/licenses/by-sa/4.0/
```
