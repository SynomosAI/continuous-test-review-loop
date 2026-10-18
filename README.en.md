# continuous-test-review-loop · Continuous Test-Review-Improve Loop

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE.md)
[![Agent Skill](https://img.shields.io/badge/Agent%20Skill-SKILL.md-blue.svg)](SKILL.md)
[![Test-Review-Improve Loop](https://img.shields.io/badge/loop-test%20%7C%20review%20%7C%20improve-brightgreen.svg)](SKILL.md)

SynomosAI four-pillar system: **Identity · Traceability · Governance · Symbiosis**.

> This repo is part of the [SynomosAI](https://github.com/SynomosAI) skill ecosystem.

**Keywords**: continuous testing · review · improvement loop · regression retest · fixed test checklist · pre-publish scan · quality gate

Makes "test -> review -> improve -> retest" a standing mechanism: a fixed test checklist, a review template, an improvement loop, and each round's report archived. Run one round after every major change (new scheme / skill release / tool upgrade), or weekly on a schedule.

## Quick Start

Prerequisite: place this directory in your agent skills folder. External scripts (`ai_gateway.py doctor`, `pre_publish_scan.py`) are marked as external dependencies.

```bash
git clone https://github.com/SynomosAI/continuous-test-review-loop.git
cd continuous-test-review-loop
cat SKILL.md
```

```text
Triggers: test · review · improve · polish · real run · verify a scheme
```

## What it covers

- **Four-step loop**: 1 test (fixed checklist, record raw evidence) -> 2 review (passes / findings / corrected beliefs / disposal) -> 3 improve (fix internal items now; external/security items ask first) -> 4 retest for no regression.
- **Fixed checklist 5+1**: gateway doctor + real call, local compute chain (Ollama + DSH probe), pre-publish scan (0 hits), end-to-end package run, page render + sensitive-word grep, queued items.
- **Disposal rules**: docs stale -> fix now; small script bug -> fix + retest; release-package code -> careful; external/security/credentials -> do not touch, flag for owner.

## Review report example (excerpt)

```text
Round N, 2026-08-28
  1 gateway doctor: PASS, real call returned
  2 local chain:   WARN qwen3.5:4b thinking ate tokens with num_predict=40
                   -> fix: pass "think": false (fixed this round, retest PASS)
  3 pre-publish scan: PASS, 0 hits
  loop status: item 2 cleared, no carry-over
```

## License

MIT License. © 2026 注册老炮@MedXpert. See [LICENSE.md](LICENSE.md).

## Disclaimer

Theoretical-positioning and tooling exploration. External scripts and standards are paraphrased from public sources; verify independently before formal citation.
