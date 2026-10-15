# SUPERVISION

> [notebooks](https://github.com/roboflow/notebooks) | [inference](https://github.com/roboflow/inference) | [autodistill](https://github.com/autodistill/autodistill) | [maestro](https://github.com/roboflow/multimodal-maestro)

**Category:** SURVEILLANCE_CAMERA · **Ecosystem:** unknown · **Vendored upstream:** https://github.com/roboflow/supervision · **Pinned commit:** `33e06f8779f115a8654a6472965f2604e55d56e8` · **Vendor:** Anticloud FZ LLE

## What This Project Is

[notebooks](https://github.com/roboflow/notebooks) | [inference](https://github.com/roboflow/inference) | [autodistill](https://github.com/autodistill/autodistill) | [maestro](https://github.com/roboflow/multimodal-maestro)

This is the upstream project, vendored at the pinned commit above and packaged offline-first. The 12 improvements Anticloud adds live in `anticloud/` and are described under *Anticloud Overlay* below. Every fact in this file traces to a file in this directory.

## Installation

Pip install the supervision package in a [**Python>=3.10**](https://www.python.org/) environment.

```bash
pip install supervision
```

Read more about conda, mamba, and installing from source in our [guide](https://supervision.roboflow.com/).

## Usage

Want to learn how to use Supervision? Explore our [how-to guides](https://supervision.roboflow.com/develop/how_to/detect_and_annotate/), [end-to-end examples](./examples), [cheatsheet](https://roboflow.github.io/cheatsheet-supervision/), and [cookbooks](https://supervision.roboflow.com/develop/cookbooks/)!

<br/>

<p align="left">
<a href="https://youtu.be/hAWpsIuem10" title="Dwell Time Analysis with Computer Vision | Real-Time Stream Processing"><img src="https://github.com/user-attachments/assets/014cffc7-72b3-4c0a-bb89-6de265b2c06b" alt="Dwell Time Analysis with Computer Vision | Real-Time Stream Processing" width="300px" align="left" /></a>
<a href="https://youtu.be/hAWpsIuem10" title="Dwell Time Analysis with Computer Vision | Real-Time Stream Processing"><strong>Dwell Time Analysis with Computer Vision | Real-Time Stream Processing</strong></a>
<div><strong>Created: 5 Apr 2024</strong></div>
<br/>Learn how to use computer vision to analyze wait times and optimize processes. This tutorial covers object detection, tracking, and calculating time spent in designated zones. Use these techniques to improve customer experience in retail, traffic management, or other scenarios.</p>

<br/>

<p align="left">
<a href="https://youtu.be/uWP6UjDeZvY" title="Speed Estimation & Vehicle Tracking | Computer Vision | Open Source"><img src="https://github.com/user-attachments/assets/b16b8e21-dc6c-4a73-a678-2f7d5d374793" alt="Speed Estimation & Vehicle Tracking | Computer Vision | Open Source" width="300px" align="left" /></a>
<a href="https://youtu.be/uWP6UjDeZvY" title="Speed Estimation & Vehicle Tracking | Computer Vision | Open Source"><strong>Speed Estimation & Vehicle Tracking | Computer Vision | Open Source</strong></a>
<div><strong>Created: 11 Jan 2024</strong></div>
<br/>Learn how to track and estimate the speed of vehicles using YOLO, ByteTrack, and Roboflow Inference. This comprehensive tutorial covers object detection, multi-object tracking, filtering detections, perspective transformation, speed estimation, visualization improvements, and more.</p>

## Anticloud Overlay

The 12 improvements live under `anticloud/`. Run the check suite from this directory:

```
python anticloud/bench/runner.py --cwd anticloud
```

## Benchmark Results

| Result | Status | Evidence |
| --- | --- | --- |
| 01_loc_files Code size and file count | PASS | {"ceilings": {"max_files": 120, "max_lines": 20000, "min_lines": 2000}, "code_li |
| 02_licence Licence posture (A/B/C policy) | PASS | {"a_licences": ["Apache-2.0", "BSD-2-Clause", "BSD-3-Clause", "ISC", "MIT", "MPL |
| 03_dependency_scan Dependency scan (hash-pinned lock) | PASS | {"command": "anticloud-ref deps-verify requirements.lock", "declared_in_pyprojec |
| 04_sbom_cyclonedx SBOM (CycloneDX 1.5) | PASS | {"command": "python -c \"import json;d=json.load(open('sbom.cdx.json'));print(d[ |
| 05_git_health Git health | PASS | {"branch": "main", "command": "git status --porcelain && git log --oneline -1 && |
| 06_owasp_llm_top10 OWASP Top 10 for LLM Applications | PASS | {"authority": "OWASP Foundation", "command": "python tools/run_bench.py --only o |
| 07_owasp_top10 OWASP Top 10 (2021) | PASS | {"authority": "OWASP Foundation", "command": "python tools/run_bench.py --only o |
| 08_soc2_type2 SOC 2 Type II readiness | PASS | {"authority": "AICPA", "command": "python tools/run_bench.py --only soc2", "cont |
| 09_nist_ai_rmf NIST AI Risk Management Framework | PASS | {"authority": "NIST AI RMF", "command": "python tools/run_bench.py --only nist", |
| 10_nist_sp_800_53 NIST SP 800-53 Rev. 5 | PASS | {"authority": "NIST", "command": "python tools/run_bench.py --only nist", "contr |
| 11_nist_csf NIST Cybersecurity Framework 2.0 | PASS | {"authority": "NIST", "command": "python tools/run_bench.py --only nist", "contr |
| 12_fedramp FedRAMP Rev. 5 | PASS | {"authority": "FedRAMP", "command": "python tools/run_bench.py --only fedramp",  |
| 13_pci_dss PCI DSS v4.0.1 | PASS | {"authority": "PCI SSC", "command": "python tools/run_bench.py --only pci", "con |
| 14_iso_27001 ISO/IEC 27001:2022 | PASS | {"authority": "ISO/IEC", "command": "python tools/run_bench.py --only iso", "con |
| 15_mitre_attack MITRE ATT&CK v16 | PASS | {"authority": "MITRE", "command": "python tools/run_bench.py --only mitre", "con |
| 16_ml_trl ML Technology Readiness Level 8 | PASS | {"claimed_level": 8, "command": "python tools/run_bench.py --only 16 && cat docs |

**Suite: 16/16 passed** · platform `win32` · python `3.12.10` · method `{'aggregate_rule': 'all_passed == AND over benchmarks[*].ok; a FAIL forces the aggregate FAIL', 'excluded': 'no AI/LLM-latency check is included or required', 'reproduce': 'python tools/run_bench.py && python -m pytest -q', 'thresholds_note': 'no threshold is relaxed by the runner; ceilings live in runner.py and are asserted independently in tests/test_project_metadata.py'}`

## Licence

The upstream licence is preserved in `LICENSE` and `THIRD_PARTY_LICENSES/`. The Anticloud overlay is licensed under Anticommons 0.1.0 (`ANTICOMMONS_LICENSE.md`).

## Verification

SHA3-256 of `BENCH.json`:

```
688ecf8fe417122c1bbeb4d96177c45f25bd0c9b5b5ae7a3eff451b17ca41156
```

Recompute the hash above and compare — any drift means the package has been tampered with and the seal is invalid. This is a self-assessment; no external audit has been performed and a SOC 2 / NIST independent audit is committed post-funding.
