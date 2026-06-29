# ORCAS — Orchestrated Router-Council ASI System

A concept architecture for reliable, domain-specialised AI based on knowledge purity, epistemic honesty, and coordinated specialist models.

---

## What is ORCAS?

Current large language models are trained on internet-scale, unverified data. They hallucinate because their training objective rewards fluent text, not accurate text. Fine-tuning domain-specific models on top of this noisy foundation patches surface behaviour without fixing the underlying problem.

ORCAS proposes a different approach: instead of one generalised model trained on everything, build a council of domain-specialist models each trained from a clean, verified corpus, orchestrated by a dedicated routing model called Routey.

The result is a system that:
- Knows what it knows
- Knows what it does not
- Routes queries to the right specialist
- Asks for clarification when uncertain
- Returns structured, source-attributed outputs

---

## Architecture Overview

```
                        [ USER INPUT ]
                               │
                    ┌──────────▼──────────┐
                    │        ROUTEY        │
                    │  Orchestration Layer │
                    └──────────┬──────────┘
                               │
           ┌──────────────────┼──────────────────┐
           │                  │                  │
    ┌──────▼──────┐   ┌───────▼──────┐   ┌──────▼──────┐
    │   MEDICAL   │   │    LEGAL     │   │ ENGINEERING │  ...
    │  Specialist │   │  Specialist  │   │  Specialist │
    └──────┬──────┘   └───────┬──────┘   └──────┬──────┘
           └──────────────────┼──────────────────┘
                               │
                    ┌──────────▼──────────┐
                    │        ROUTEY        │
                    │    Assembly Layer    │
                    └──────────┬──────────┘
                               │
                        [ USER OUTPUT ]
```

Three components:

**Base Model** — pre-trained from scratch on a strictly curated corpus of verified sources. Provides linguistic and reasoning capability without domain knowledge contamination.

**The Council** — domain-specialist models built on the Base Model, each trained on a domain-pure verified corpus. Specialists are trained to return full answers, partial answers with explicit domain gaps, or referrals — not hallucinated responses.

**Routey** — a lean orchestration model that classifies queries, dispatches to the right specialists, asks the user for clarification when uncertain, and assembles structured specialist outputs into a coherent response.

---

## Why This Matters

| Property | General LLM | Fine-tuned LLM | ORCAS |
|---|---|---|---|
| Training data quality | Unverified | Unverified base | Curated and verified |
| Hallucination rate | High | Moderate | Low by design |
| Epistemic honesty | None | None | Trained core feature |
| Source auditability | None | None | Full |
| Regulated industry viability | Low | Low | High |
| Domain extensibility | Not modular | Not modular | Add specialist independently |

---

## Read the Whitepaper

The full concept paper is in [`ORCAS_whitepaper_v0.2.md`](./ORCAS_whitepaper_v0.2.md).

It covers the full architecture, training pipeline, comparison with existing approaches, target applications, implementation roadmap, and glossary.

---

## Status

This is a concept paper. No implementation exists yet. Published to establish the architecture publicly and invite feedback from the ML community.

If you have thoughts, criticism, or interest in this direction — open an issue or reach out.

---

## Licence

© 2026 [Ash Lost]. Licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).

Free to share and adapt for non-commercial purposes with attribution. Commercial use requires explicit permission.
