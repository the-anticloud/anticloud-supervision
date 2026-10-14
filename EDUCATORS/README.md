# Educators — SUPERVISION

**Project:** SUPERVISION  
**Category:** SURVEILLANCE_CAMERA  
**Upstream:** https://github.com/roboflow/supervision  
**Pinned commit:** `f59aa0da3bc244d937f87b8f56fe7c893e55aab5`  
**Assurance:** 16/16 checks passing  
**Ledger head:** `ddd94bba3ac0a14c310a0713a93babd8fb55abd405a4cb9c4e085b55bce9e5d8`  
**Date:** October 2026

## Teaching with SUPERVISION

The project is usable as a worked example of offline-first packaging with a
cryptographic audit chain. It ships with the assurance suite, the evidence
register and the ledger, so students can verify claims rather than take them on
faith.

## Suggested exercises

1. Run `python tools/run_bench.py --out BENCH.json` and read the 16 results.
2. Recompute the SHA3-256 of a row's evidence file and compare to the register.
3. Walk the AIOSS chain from genesis to head `ddd94bba3ac0a14c310a0713a93babd8fb55abd405a4cb9c4e085b55bce9e5d8` and confirm every link.
4. Break one artifact and observe the chain fail to verify.

## Licence for teaching

Apache 2.0 terms apply to academic and teaching use. See `24_ANTICOMMONS_LICENSE`.
