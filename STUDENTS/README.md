# Students — SUPERVISION

**Project:** SUPERVISION  
**Category:** SURVEILLANCE_CAMERA  
**Upstream:** https://github.com/roboflow/supervision  
**Pinned commit:** `f59aa0da3bc244d937f87b8f56fe7c893e55aab5`  
**Assurance:** 16/16 checks passing  
**Ledger head:** `ddd94bba3ac0a14c310a0713a93babd8fb55abd405a4cb9c4e085b55bce9e5d8`  
**Date:** October 2026

## What this project gives you

A complete worked example of offline-first packaging with a cryptographic audit
chain: source pinned at `f59aa0da3bc244d937f87b8f56fe7c893e55aab5`, a 16-check assurance suite, an evidence register
with per-check hashes, and an AIOSS ledger chain ending at `ddd94bba3ac0a14c310a0713a93babd8fb55abd405a4cb9c4e085b55bce9e5d8`.

## Learn by verifying

```
python tools/run_bench.py --out BENCH.json
```

Then take any row from `ISOLATED_LAB_RESULTS/03_Result_Register.md`, recompute
the SHA3-256 of its evidence file, and confirm it matches. If it does not match,
the record has been altered — that is the whole point of the chain.

## Licence

Apache 2.0 terms apply to study and teaching use.
