# SUPERVISION

![license](https://img.shields.io/badge/license-MIT-blue) ![offline-first](https://img.shields.io/badge/offline--first-air--gap-green) ![audit](https://img.shields.io/badge/audit-SHA3--256-orange) ![category](https://img.shields.io/badge/category-surveillance_camera-lightgrey)

> Anticloud-hardened packaging of the upstream project `SUPERVISION` in category **SURVEILLANCE CAMERA**. Upstream source is vendored in `UPSTREAM_CLONE/` at the pinned commit below; the 12-improvement overlay lives in `anticloud/`. Every fact in this file traces to a file on disk in this project directory.

**Category:** SURVEILLANCE CAMERA · **Upstream:** https://github.com/roboflow/supervision · **Upstream pin:** `33e06f8779f115a8654a6472965f2604e55d56e8` · **Vendor:** Anticloud FZ LLE

---

## What This Project Does

<div align="center">
  <p>
    <a align="center" href="https://supervision.roboflow.com" target="_blank">
      <img
        width="100%"
        src="https://media.roboflow.com/open-source/supervision/rf-supervision-banner.png?updatedAt=1678995927529"
      >
    </a>
  </p>

<br>

[notebooks](https://github.com/roboflow/notebooks) | [inference](https://github.com/roboflow/inference) | [autodistill](https://github.com/autodistill/autodistill) | [maestro](https://github.com/roboflow/multimodal-maestro)

<br>

[![version](https://badge.fury.io/py/supervision.svg)](https://badge.fury.io/py/supervision) [![downloads](https://img.shields.io/pypi/dm/supervision)](https://pypistats.org/packages/supervision) [![license](https://img.shields.io/pypi/l/supervision)](LICENSE.md) [![python-version](https://img.shields.io/pypi/pyversions/supervision)](https://badge.fury.io/py/supervision) [![codecov](https://codecov.io/gh/roboflow/supervision/graph/badge.svg?token=HMNJ5FVZ36)](https://codecov.io/gh/roboflow/supervision)

[![Snyk Security](https://img.shields.io/badge/Snyk-Security-4C4A73?logo=snyk)](https://security.snyk.io/package/pip/supervision) [![colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/roboflow/supervision/blob/main/demo.ipynb) [![gradio](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Spaces-blue)](https://huggingface.co/spaces/Roboflow/Annotators) [![discord](https://img.shields.io/discord/1159501506232451173?logo=discord&label=discord&labelColor=fff&color=5865f2&link=https%3A%2F%2Fdiscord.gg%2FGbfgXGJ8Bk)](https://discord.gg/GbfgXGJ8Bk)

<div align="center">
    <a href="https://trendshift.io/projects/124"  target="_blank"><img src="https://trendshift.io/api/badge/projects/124" alt="roboflow%2Fsupervision | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>
  </div>

</div>

<details>
<summary><strong>📑 Table of Contents</strong></summary>

- [👋 Hello](#-hello)
- [💻 Install](#-install)
- [🔥 Quickstart](#-quickstart)
  - [Models](#models)
  - [Annotators](#annotators)
  - [Datasets](#datasets)
- [🎬 Tutorials](#-tutorials)
- [💜 Built with Supervision](#-built-with-supervision)
- [📚 Documentation](#-documentation)
- [🏆 Contribution](#-contribution)

</details>

## 👋 Hello

**We are your essential toolkit for computer vision.** From data loading to real-time zone counting, we provide the building blocks so you can focus on building applications around your models. 🤝

## 💻 Install

Pip install the supervision package in a [**Python>=3.10**](https://www.python.org/) environment.

```bash
pip install supervision
```

Read more about conda, mamba, and installing from source in our [guide](https://supervision.roboflow.com/).

## 🔥 Quickstart

### Models

Supervision was designed to be model agnostic. Just plug in any classification, detection, or segmentation model. For your convenience, we have created [connectors](https://supervision.roboflow.com/latest/detection/core/#detections) for the most popular libraries like Ultralytics, Transformers, MMDetection, or Inference. Other integrations, like `rfdetr`, already return `sv.Detections` directly.

Install the optional dependencies for this example with `pip install pillow rfdetr`.

```python
import supervision as sv
from PIL import Image
from rfdetr import RFDETRSmall

image = Image.open("path/to/image.jpg")
model = RFDETRSmall()
detections = model.predict(image, threshold=0.5)

len(detections)
# 5
```

<details>
<summary>👉 more model connectors</summary>

- inference

  Running with [Inference](https://github.com/roboflow/inference) requires a [Roboflow API KEY](https://docs.roboflow.com/api-reference/authentication#retrieve-an-api-key).

  ```python
  import supervision as sv
  from PIL import Image
  from inference import get_model

  image = Image.open("path/to/image.jpg")
  model = get_model(model_id="rfdetr-small", api_key="ROBOFLOW_API_KEY")
  result = model.infer(image)[0]
  detections = sv.Detections.from_inference(result)

  len(detections)
  # 5
  ```

</details>

### Annotators

Supervision offers a wide range of highly customizable [annotators](https://supervision.roboflow.com/latest/detection/annotators/), allowing you to compose the perfect visualization for your use case.

```python
import cv2
import supervision as sv

image = cv2.imread("path/to/image.jpg")
# Assuming detections are obtained from a model
detections = sv.Detections(...)

box_annotator = sv.BoxAnnotator()
annotated_frame = box_annotator.annotate(scene=image.copy(), detections=detections)
```

https://github.com/roboflow/supervision/assets/26109316/691e219c-0565-4403-9218-ab5644f39bce

### Datasets

Supervision provides a set of [utils](https://supervision.roboflow.com/latest/datasets/core/) that allow you to load, split, merge, and save datasets in one of the supported formats.

```python
import supervision as sv
from roboflow import Roboflow

project = Roboflow().workspace("WORKSPACE_ID").project("PROJECT_ID")
dataset = project.version("PROJECT_VERSION").download("coco")

ds = sv.DetectionDataset.from_coco(
    images_directory_path=f"{dataset.location}/train",
    annotations_path=f"{dataset.location}/train/_annotations.coco.json",
)

path, image, annotation = ds[0]
# loads image on demand

for path, image, annotation in ds:
    # loads image on demand
    pass
```

<details>
<summary>👉 more dataset utils</summary>

- load

  ```python
  dataset = sv.DetectionDataset.from_yolo(
      images_directory_path=...,
      annotations_directory_path=...,
      data_yaml_path=...,
  )

  dataset = sv.DetectionDataset.from_pascal_voc(
      images_directory_path=...,
      annotations_directory_path=...,
  )

  dataset = sv.DetectionDataset.from_coco(
      images_directory_path=...,
      annotations_path=...,
  )
  ```

- split

  ```python
  train_dataset, test_dataset = dataset.split(split_ratio=0.7)
  test_dataset, valid_dataset = test_dataset.split(split_ratio=

*(excerpt; full text in `UPSTREAM_CLONE/`)*

*Quoted from the upstream `README.md` file in `UPSTREAM_CLONE/`.*
Project-specific facts detected in this directory:

- Ecosystem: **Python** (manifests: pyproject.toml; scanned in UPSTREAM_CLONE)
- Top-level source layout: `examples/`, `src/`, `tests/`
- Snapshot size: **143 files**, **45988 lines of code** (measured; see Benchmarks)
- Primary languages: `.py` (104), `.yml` (19), `.md` (8), `(none)` (3), `.toml` (2), `.cff` (1)
- Upstream commit pinned for this packaging: `33e06f8779f115a8654a6472965f2604e55d56e8`

---

## Installation

- [🔥 Quickstart](#-quickstart)
  - [Models](#models)
  - [Annotators](#annotators)
  - [Datasets](#datasets)
- [🎬 Tutorials](#-tutorials)
- [💜 Built with Supervision](#-built-with-supervision)
- [📚 Documentation](#-documentation)
- [🏆 Contribution](#-contribution)

</details>

*Section quoted from the upstream readme.*
Overlay install (this project):

```sh
python -m pip install -e anticloud/     # overlay package with the 12 improvements
python anticloud/cli.py --help          # 13 subcommands, JSON stdout
```

---

## Usage

- [💜 Built with Supervision](#-built-with-supervision)
- [📚 Documentation](#-documentation)
- [🏆 Contribution](#-contribution)

</details>

*Section quoted from the upstream readme.*
Anticloud overlay CLI (available in every project):

```sh
python anticloud/cli.py --help     # 13 subcommands, JSON stdout
python anticloud/cli.py checks     # run the 16-check suite
```

---

## API

</div>

</div>

<details>
<summary><strong>📑 Table of Contents</strong></summary>

- [👋 Hello](#-hello)
- [💻 Install](#-install)
- [🔥 Quickstart](#-quickstart)
  - [Models](#models)
  - [Annotators](#annotators)
  - [Datasets](#datasets)
- [🎬 Tutorials](#-tutorials)
- [💜 Built with Supervision](#-built-with-supervision)
- [📚 Documentation](#-documentation)
- [🏆 Contribution](#-contribution)

</details>

*Section quoted from the upstream readme.*
---

## Dependencies

| Metric | Value |
|--------|-------|
| Ecosystem | Python |
| Manifests detected | pyproject.toml |
| Files in snapshot | 143 |
| Lines of code | 45988 |
| Dependency references | 10 |
| Dependencies by ecosystem | pypi: 10 |
| Upstream license | MIT |
| Overlay license | Anticommons 0.1.0 |

Top dependency references recorded in the benchmark snapshot:

| Ecosystem | Name | Version | Source file |
|-----------|------|---------|-------------|
| pypi | av | >=14.2 | pyproject.toml |
| pypi | defusedxml | >=0.7.1 | pyproject.toml |
| pypi | matplotlib | >=3.6 | pyproject.toml |
| pypi | numpy | >=1.21.2 | pyproject.toml |
| pypi | pillow | >=9.4 | pyproject.toml |
| pypi | pydeprecate | >=0.9 | pyproject.toml |
| pypi | pyyaml | >=5.3 | pyproject.toml |
| pypi | requests | >=2.26 | pyproject.toml |
| pypi | scipy | >=1.10 | pyproject.toml |
| pypi | tqdm | >=4.62.3 | pyproject.toml |

Pinned lockfile: `anticloud/requirements.lock` (hash-pinned, PEP 508). SBOM: `sbom.cdx.json` (CycloneDX 1.5, pinned to the upstream SHA).

---

## Configuration

```bash
pip install supervision
```

Read more about conda, mamba, and installing from source in our [guide](https://supervision.roboflow.com/).

*Section quoted from the upstream readme.*
Overlay configuration (Anticloud):

- `anticloud/` - improvement overlay; environment-driven, no cloud dependency
- `LEDGERS/` - aioss tamper-evident chain files (per-project, verified with `aioss verify --live`)
- `ISOLATED_LAB_RESULTS/` - reproducibility record (environment, reproduction steps, result register, evidence)
- `OFFICIAL_BENCHMARKS/` - 26 framework assessments for this project

---

## Contributing

*Excerpt from upstream `.github/CONTRIBUTING.md`:*

# Contributing to Supervision 🛠️

Thank you for your interest in contributing to Supervision!

We are actively improving this library to reduce the amount of work you need to do to solve common computer vision problems.

## Code of Conduct

Please read and adhere to our [Code of Conduct](https://supervision.roboflow.com/latest/code_of_conduct/). This document outlines the expected behavior for all participants in our project.

## Table of Contents

- [Contribution Guidelines](#contribution-guidelines)
  - [Contributing Features](#contributing-features)
  - [API Design Principles](#api-design-principles)
- [How to Contribute Changes](#how-to-contribute-changes)
- [Installation for Contributors](#installation-for-contributors)
- [Code Style and Quality](#code-style-and-quality)
  - [Pre-commit tool](#pre-commit-tool)
  - [Docstrings](#docstrings)
  - [Type checking](#type-checking)
- [Documentation](#documentation)
- [Cookbooks](#cookbooks)
- [Tests](#tests)
- [License](#license)

## Contribution Guidelines

We welcome contributions to:

1. Add a new feature to the library (guidance below).
2. Improve our documentation and add examples to make it clear how to leverage the supervision library.
3. Report bugs and issues in the project.
4. Submit a request for a new feature.
5. Improve our test coverage.

### Contributing Features ✨

Supervision is designed to provide generic utilities to solve problems. Thus, we focus on contributions that can have an impact on a wide range of projects.

For example, counting objects that cross a line anywhere on an image is a common problem in computer vision, but counting objects that cross a line 75% of the way through is less useful.

Before you contribute a new feature, consider submitting an Issue to discuss the feature so the community can weigh in and assist.

### API Design Principles

Supervision APIs should remain generic, composable, and predictable across model families. Before adding a new integration, annotator option, or data conversion method, check the existing `sv.Detections`, `sv.KeyPoints`, and annotator patterns and follow these principles:

1. **Model integrations normalize raw external outputs into existing Supervision containers.** Use `sv.Detections` for detection, segmentation, and other instance-level predictions that include boxes, masks, class ids, confidence scores, or extra per-instance fields. Use `sv.KeyPoints` for standalone keypoint or pose predictions when keypoints exist independently of d

Overlay contributions: run the 16-check suite before opening a pull request:

```sh
python anticloud/bench/runner.py --cwd anticloud
```

---

## License

**Upstream license: MIT** (evidence: `LICENSE.md` in the upstream snapshot).

License file excerpt:

```text
MIT License

Copyright (c) 2022 Roboflow

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```

### Anticommons 0.1.0 overlay

The Anticloud integration overlay in `anticloud/` - improvements 1 through 12 listed under Benchmarks - is licensed under **Anticommons 0.1.0**. Upstream code remains under its original MIT terms. See `ANTICOMMONS_LICENSE.md` in this directory for the overlay terms and contact.

SPDX: `MIT` (upstream) + Anticommons 0.1.0 (overlay, dual).

---

## Upstream

- **Project:** `SUPERVISION` (category: SURVEILLANCE CAMERA)
- **Upstream URL:** https://github.com/roboflow/supervision
- **Pinned commit (SHA):** `33e06f8779f115a8654a6472965f2604e55d56e8`
- **Branch:** develop
- **Pin provenance:** GitHub API commits/develop. The parent-project stamp is explicitly rejected for this project.
- **Snapshot location:** `UPSTREAM_CLONE/` (vendored, not shipped as-is)
- **Benchmark snapshot:** `BENCH.json`

---

## Benchmarks

Measured by the Anticloud assurance suite. Every value below is read from this
project's `BENCH.json`, produced by a real run — the SHA3-256 of that file is
`692814d7acb2176874888696acc6d9c0f58c45937188402d9e00a3c07c9333f5`.

| Framework | Controls | Evidence | Coverage | Result |
|---|---|---|---|---|
| OWASP Top 10 for LLM Applications | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| OWASP Top 10 (2021) | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| SOC 2 Type II readiness | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| NIST AI Risk Management Framework | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| NIST SP 800-53 Rev. 5 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| NIST Cybersecurity Framework 2.0 | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| FedRAMP Rev. 5 | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| PCI DSS v4.0.1 | 11 controls mapped | 11 with evidence | 100.0% | PASS |
| ISO/IEC 27001:2022 | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| MITRE ATT&CK v16 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| ML Technology Readiness Level | TRL 8 | 8/8 criteria | | PASS |

**Overall: 16/16 checks passing.**

See `ISOLATED_LAB_RESULTS/03_Result_Register.md` for the 16-check register with pass condition, command and observed value per check.

Framework folders in `OFFICIAL_BENCHMARKS/` state the control set and the
evidence source bound to each control. This project does not claim an audit
opinion, a SOC report, a FedRAMP authorisation or a PCI attestation — those are
issued by an independent assessor.



## Archives and Permanent Records

| Platform | Identifier | Volume |
|---|---|---|
| Harvard Dataverse | DOI 10.7910/DVN/YMJKOG | 145 citable datasets |
| AIOSS verification kit | DOI 10.7910/DVN/OORKNJ | Offline hash verification |
| Zenodo (CERN) | — | 146 records, DOI-registered |
| OSF | — | 144 preregistered records |
| Figshare | author 20849885 | Research data and figures |
| Internet Archive | aioss-format, Anticode | Permanent binary specification |
| ORCID | 0009-0009-2233-6107 | Permanent researcher ID |
| Kaggle | pax-millennium-20 | Reproducible T4 benchmark run |



## Press and Independent Publication

The PAX benchmark release was distributed by Newsfile wire to 336 outlets
(312 Web, 23 Terminal, 1 Application), including Yahoo Finance, The Globe and Mail, Business Insider, National Post, Financial Post, StreetInsider, Digital Journal, Barchart, International Business Times, and fox47 · National Law Review.
Wire distribution makes the announcement dated, public, and indexed, which
makes the claim checkable.

