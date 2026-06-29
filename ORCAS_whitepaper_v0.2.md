# Orchestrated Router-Council ASI System
## ORCAS — Concept Paper v0.2

*June 2026*

---

## Abstract

Large language models hallucinate because they are trained to. The dominant approach to AI development — training generalised models on internet-scale, unverified data — produces systems that generate fluent but unreliable outputs, an architectural consequence rather than an implementation bug. ORCAS proposes a fundamentally different paradigm: a hierarchical system of domain-specialised language models built on a clean, curated base, orchestrated by a dedicated routing model. Rather than pursuing artificial general intelligence through data volume and parameter scale, ORCAS pursues Artificial Specialised Intelligence through data purity, architectural honesty, and coordinated specialisation. The result is a system that knows what it knows, knows what it does not, and coordinates specialist knowledge to answer complex queries reliably.

---

## 1. Problem Statement

### 1.1 The Hallucination Problem

Large language models hallucinate because their training objective rewards them for doing so. Next-token prediction on internet-scale data teaches models to produce statistically plausible text, not factually accurate text. When a model encounters contradictory signals in its training corpus — which is inevitable at internet scale — it learns to interpolate between conflicting representations. The output is fluent, confident, and frequently wrong.

This is not a bug that can be patched. It is an emergent property of the training paradigm itself. Scaling parameters or adding more data does not solve the problem; it often compounds it by introducing more contradictions at greater scale and giving the model more conflicting signals to interpolate between.

### 1.2 The Generalisation Trap

The dominant assumption in current AI development is that generalisation — the ability to perform adequately across all domains — is the primary objective. This drives the AGI race: larger models, broader training data, more parameters. The result is systems that are mediocre across everything and exceptional at nothing, deployed in contexts that require genuine expertise.

For regulated industries — medicine, law, structural engineering, pharmacology — mediocre with confidence is not acceptable. A hallucinated drug interaction or a fabricated legal precedent carries real liability. Current LLMs cannot be deployed in these contexts without human oversight that largely negates their utility.

### 1.3 The Fine-Tuning Patch

The industry response to domain-specific unreliability is fine-tuning: taking a general base model and adapting it to a specific domain through additional training on domain data. This approach is cost-effective but fundamentally limited.

Fine-tuning adjusts the surface behaviour of a model without changing its underlying knowledge representation. The noisy, contradictory foundation remains intact. A model fine-tuned on medical literature still carries within it the unverified medical misinformation present in its original pre-training corpus. Domain-specific reliability cannot be guaranteed when the base model's internal representation was formed from unverified data.

Fine-tuning is a patch on a flawed foundation. ORCAS proposes replacing the foundation.

### 1.4 The Epistemic Dishonesty Problem

Current LLMs have no mechanism for refusing to answer. They are trained on a corpus where text always continues — there is no silence, no "I don't know," no referral. The result is a model architecturally incapable of recognising or expressing the limits of its own knowledge. When it reaches the boundary of its training, it keeps generating anyway.

This is not a personality flaw. It is a training objective flaw. Any system that will always attempt an answer is an unreliable system by definition. ORCAS treats epistemic honesty — the ability to say "not my domain" or "I only know part of this" — as a core trained capability rather than an emergent hope.

---

## 2. Proposed Architecture: ORCAS

ORCAS — Orchestrated Router-Council ASI System — is a three-tier architecture consisting of a clean base model, a council of domain specialists built on that base, and a dedicated orchestration model that manages query routing, specialist dispatch, and response assembly.

### 2.1 System Overview

```
╔══════════════════════════════════════════════════════════════╗
║                        USER INTERFACE                        ║
╚══════════════════════════════════════════════════════════════╝
                               │
                    ┌──────────▼──────────┐
                    │        ROUTEY        │
                    │   Classification &   │
                    │   Dispatch Layer     │
                    └──────────┬──────────┘
                               │
           ┌──────────────────┼──────────────────┐
           │                  │                  │
    ┌──────▼──────┐   ┌───────▼──────┐   ┌──────▼──────┐
    │   MEDICAL   │   │    LEGAL     │   │ ENGINEERING │  ...
    │  Specialist │   │  Specialist  │   │  Specialist │
    └──────┬──────┘   └───────┬──────┘   └──────┬──────┘
           │                  │                  │
           └──────────────────┼──────────────────┘
                               │
                    ┌──────────▼──────────┐
                    │        ROUTEY        │
                    │    Assembly Layer    │
                    └──────────┬──────────┘
                               │
╔══════════════════════════════▼═══════════════════════════════╗
║                        USER INTERFACE                        ║
╚══════════════════════════════════════════════════════════════╝
```

All components — the Base Model, each Specialist, and Routey — share a common lineage from the same clean pre-training base, ensuring consistent linguistic behaviour across the system while maintaining genuine knowledge isolation between specialists.

### 2.2 The Base Model

The foundation of ORCAS is a language model pre-trained from scratch on a strictly curated corpus. Unlike existing general-purpose models, this base is not trained on web-crawled data. The training corpus consists exclusively of verified, high-quality sources:

- Peer-reviewed academic literature (methodology and reasoning examples, not domain conclusions)
- Formal logic and mathematical literature
- Philosophy of language and linguistics
- Verified encyclopaedic references
- Structured argumentation and rhetoric
- Primary source documents and official publications

The goal of the base model is not domain knowledge but linguistic and reasoning capability: grammar, syntax, logical inference, structured argumentation, uncertainty expression, and instruction following. Domain knowledge is deliberately excluded at this stage and introduced only at the specialist layer.

This separation is critical. A base model contaminated with domain-specific but unverified content passes that contamination to every specialist built on it. A clean base ensures that all domain knowledge in the system is entirely attributable to the verified specialist training corpus, not to noise inherited from pre-training.

### 2.3 The Council — Specialist Models

Built on the clean base, each Council member is a domain-specialist model trained further on a curated, domain-pure corpus. The corpus for each specialist contains only verified material relevant to that domain.

**Example Council configuration:**

| Specialist | Primary Corpus Sources |
|---|---|
| Medical | Clinical literature, pharmacological databases, clinical practice guidelines, drug interaction databases, verified case studies |
| Legal | Legislation, case law, legal commentary, jurisdictional documentation, legal reference works |
| Engineering | Technical standards, engineering literature, material specifications, verified technical reference |
| Scientific | Peer-reviewed research, experimental methodology, verified datasets, replication studies |
| Financial | Regulatory filings, accounting standards, verified financial reference, audited reports |
| Historical | Primary source archives, peer-reviewed historical scholarship, verified chronological records |

Each specialist is trained with three explicit response types as core capabilities:

**Full Response** — the query falls entirely within the specialist's domain and competence. A complete structured answer is returned with confidence score and source attribution.

**Partial Response** — the query spans the specialist's domain and one or more other domains. The specialist answers its portion fully and explicitly labels the remaining parts as requiring input from other specialists, identifying which domains those are and what the outstanding questions are.

**Referral** — the query falls outside the specialist's domain entirely. The specialist returns a structured referral signal identifying which domains are likely relevant and why, rather than attempting an answer.

This is epistemic honesty trained as a feature. Specialists are not rewarded for always generating an answer. They are rewarded for accurate self-assessment of their own competence boundaries. A specialist that correctly says "I don't know" is functioning correctly.

**Structured Output Format**

Specialist responses are structured outputs, not raw prose. Every specialist response conforms to the following schema:

```
{
  response_type:    FULL | PARTIAL | REFERRAL
  content:          [answer text for in-domain portions]
  confidence:       [0.0–1.0 score]
  source_refs:      [list of training corpus references]
  domain_gaps:      [list of topics outside this specialist's scope]
  referral_targets: [list of recommended specialists for gap topics]
  gap_queries:      [reformulated sub-questions for each gap topic]
}
```

This structure allows Routey to assemble multi-specialist responses deterministically. The assembly operation is compositional, not generative — Routey does not synthesise a new response from specialist outputs, it organises and presents them with clear provenance.

### 2.4 Routey — The Orchestration Model

Routey is the orchestration layer responsible for query classification, dispatch, response assembly, and user-facing communication. Unlike the specialists, Routey does not need to be large. Its task is well-defined and learnable: understand what the user is asking, determine which specialists are relevant, dispatch accordingly, and assemble structured outputs into a coherent response.

Routey does not need to know medicine, law, or engineering. It needs to know the boundaries of each specialist's domain well enough to route reliably. This is a significantly simpler and more auditable training objective than general competence.

**Routey's Operational Flow:**

```
Query received
       │
       ▼
  Classify query
       │
  ┌────┴────┐
  │confident?│
  └────┬────┘
       │
     YES │ NO
       │   │
       │   ▼
       │  Present best-guess domain options to user
       │  Receive user domain confirmation
       │   │
       └───▼
  Identify target specialist(s)
       │
  ┌────┴────┐
  │  single  │  multiple
  │ domain?  │
  └────┬────┘
       │
  single ▼      multiple ▼
  Dispatch      Parallel dispatch
  to one        to all relevant
  specialist    specialists
       │              │
       └──────┬───────┘
              ▼
    Receive structured outputs
              │
    ┌─────────┴──────────┐
    │  any referrals or   │
    │  domain gaps?       │
    └─────────┬──────────┘
              │
           YES │  NO
              │   │
              ▼   ▼
     Dispatch   Assemble
     to gap      final
    specialists  response
              │   │
              └───▼
         Deliver to user
```

**Routey's Three Operating Modes:**

**Confident Routing** — Routey classifies the query with sufficient confidence and dispatches directly to the relevant specialist or specialists without user interaction.

**Uncertain Routing** — Routey cannot classify the query with confidence. Rather than misrouting silently, Routey presents the user with its best-guess domain candidates as selectable options. The user can select one or more. This models real-world expert referral: a knowledgeable receptionist who is unsure which department handles a query asks rather than guessing. Crucially, Routey still attempts classification before asking — it presents options ranked by confidence, not an open-ended question.

**Multi-domain Dispatch** — For queries spanning multiple confirmed domains, Routey dispatches to all relevant specialists simultaneously. Each returns a structured partial response. Routey assembles these deterministically — not generatively — into a unified response, maintaining clear domain attribution for each portion.

### 2.5 The Self-Improving Feedback Loop

Every interaction generates training signal for Routey without requiring specialist retraining:

- Specialist referral signals that are confirmed correct by subsequent routing become positive routing examples
- Misroutes identified through specialist feedback (a specialist receiving a query outside its domain and returning a referral) are negative examples and corrective training data for Routey
- User-provided domain clarifications become labelled examples of ambiguous query patterns
- Multi-domain queries resolved through clarification label the linguistic features that correlate with cross-domain complexity

Over production use, Routey's routing accuracy improves organically. The clarification requests that characterise early deployment decrease as Routey learns the pattern space of ambiguous queries. The specialist layer remains stable while the orchestration layer continuously improves.

---

## 3. Training Pipeline

The ORCAS system is built in four sequential phases. Each phase depends on the outputs of the previous one.

```
PHASE 1: BASE MODEL
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 Curated corpus assembly
 (logic, linguistics, encyclopaedic, formal reasoning)
                  │
                  ▼
      Pre-training from scratch
                  │
                  ▼
         Clean Base Model ✓
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

PHASE 2: SPECIALIST TRAINING (parallelisable)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 Domain corpus curation (per specialist)
                  │
                  ▼
  Continued training on Clean Base Model
                  │
                  ▼
  Boundary recognition training
  (in-domain / partial / referral response types)
                  │
                  ▼
  Structured output format training
                  │
                  ▼
    Specialist Model (per domain) ✓
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

PHASE 3: ROUTEY TRAINING
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 Query classification dataset assembly
 Domain boundary mapping (from specialists)
                  │
                  ▼
  Continued training on Clean Base Model
                  │
                  ▼
  Routing logic training
  (confident / uncertain / multi-domain modes)
                  │
                  ▼
  Assembly logic training
  (deterministic composition of structured outputs)
                  │
                  ▼
           Routey Model ✓
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

PHASE 4: INTEGRATION AND VALIDATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 End-to-end routing accuracy testing
 Cross-domain query handling validation
 Structured output schema compliance verification
 Feedback loop initialisation
                  │
                  ▼
           ORCAS System ✓
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Phase 2 can be parallelised across multiple specialists once the Base Model is available. Adding a new specialist to the Council at any point after initial deployment requires only Phase 2 for that specialist and a Routey update to include its domain boundaries — it does not require retraining the existing Council or rebuilding the Base.

---

## 4. Comparison with Existing Approaches

| Property | General LLM | Fine-tuned LLM | Mixture of Experts | **ORCAS** |
|---|---|---|---|---|
| Training data quality | Web-crawled, unverified | Unverified base + domain data | Web-crawled, unverified | Curated and verified at every layer |
| Hallucination rate | High | Moderate | High | Low by design |
| Domain reliability | Low | Moderate | Low–Moderate | High |
| Epistemic honesty | None by architecture | None by architecture | None by architecture | Trained core feature |
| Knowledge isolation | None | Surface only | Architectural only | Real (separate training corpora) |
| Cross-domain queries | Generative (unreliable) | Generative (unreliable) | Generative (unreliable) | Structured specialist assembly |
| Source auditability | None | None | None | Full (structured output + corpus refs) |
| Regulated industry viability | Low | Low | Low | High |
| Self-improvement without retraining | No | No | No | Yes (Routey improves in production) |
| Domain extensibility | Not modular | Not modular | Not modular | Add specialist without rebuilding |
| Open source viability | Partial | Partial | Partial | Full (independently deployable components) |

The fundamental distinction is that ORCAS is the only architecture in which the specialists' knowledge comes exclusively from verified sources. Every other approach either trains on unverified data at the base level or layers domain adaptation on top of an unverified foundation.

---

## 5. Target Applications

ORCAS is most valuable where accuracy is non-negotiable and confident errors carry real consequences. The following represent primary target contexts.

### 5.1 Medical and Clinical

A Medical Specialist trained on peer-reviewed clinical literature, pharmacological databases, and clinical guidelines can assist practitioners with drug interaction checking, differential diagnosis support, literature synthesis, and clinical guideline lookup. The structured output format with confidence scores allows practitioners to assess the certainty of any given response. The source attribution allows them to verify against primary literature.

Current LLMs cannot be used in clinical settings without medical professional oversight because their hallucination rate in medical contexts is clinically dangerous. ORCAS's architecture makes this deployment viable.

### 5.2 Legal

A Legal Specialist trained on jurisdiction-specific legislation, case law, and legal commentary can provide genuine legal research assistance. Because specialist training corpora are jurisdiction-specific, the same architecture can produce distinct specialists for different legal systems — a Polish legal specialist and a German legal specialist are separate training projects on the same base, not one model asked to know all laws everywhere.

### 5.3 Scientific Research

A Scientific Specialist trained on peer-reviewed research across a field can synthesise literature, identify methodological patterns, flag contradicting findings, and assist with research design. The source attribution is particularly valuable here — a research assistant that can point to the specific papers behind any claim is substantially more useful than one that summarises without attribution.

### 5.4 Engineering and Technical Standards

An Engineering Specialist trained on technical standards, material specifications, and engineering literature can assist with compliance checking, design verification against standards, and technical calculation support. Engineering errors are often catastrophic; a system that knows when it is uncertain and refuses to guess is substantially safer than one that answers confidently from noisy training data.

### 5.5 Education

An Educational deployment of ORCAS benefits from the same reliability properties but in a different way: a system that accurately represents the limits of its own knowledge models good epistemic practice for students. Current LLMs teach students that confident answers are always forthcoming. ORCAS teaches that some questions require specialist knowledge, some require multiple perspectives, and some are genuinely uncertain.

---

## 6. Advantages Over Existing Approaches

### 6.1 Over General-Purpose LLMs

ORCAS does not attempt to answer everything with one model. Specialist models trained on verified domain corpora produce responses with fundamentally lower hallucination rates because their training data contains fewer contradictions and no unverified sources. The routing architecture ensures that queries reach models with genuine, verified competence in the relevant domain.

### 6.2 Over Fine-Tuned Domain Models

Fine-tuning patches surface behaviour without changing the underlying knowledge representation. A fine-tuned medical model is still fundamentally a web-trained model that has been redirected, not a model whose medical knowledge comes from verified medical sources. ORCAS specialists are built on a clean base with domain knowledge introduced at training time from curated, verified corpora. The domain knowledge is foundational, not superficial.

### 6.3 Over Mixture-of-Experts Architectures

Current mixture-of-experts architectures route between expert parameter sets within a single model trained on the same data. All experts share the same noisy training foundation. ORCAS routes between genuinely distinct models with genuinely distinct training corpora. The knowledge isolation is real, not architectural. A Council member's domain knowledge cannot be contaminated by another Council member's training corpus because they are separate models.

### 6.4 Viability for Regulated Industries

The structured output format — with confidence scores and source attribution traceable to a verified training corpus — provides the auditability that regulated industries require. A medical institution can trace a specialist's response to its training corpus. A legal firm can verify the jurisdictional basis of a legal response. A pharmaceutical company can audit a drug interaction output against its source literature.

This traceability is architecturally impossible with current black-box generalist models, and it is precisely the property that makes AI deployment viable in high-liability contexts.

---

## 7. Challenges and Mitigations

### 7.1 Data Acquisition and Quality

High-quality curated data is scarce relative to web-crawled data. Peer-reviewed literature, clinical guidelines, and verified technical documentation exist in far smaller volumes than internet text. This limits the scale at which specialists can be trained.

**Mitigation:** Smaller, denser, higher-quality models are preferable to large models trained on noisy data. A 7B parameter specialist trained on a pure domain corpus is likely to outperform a 70B generalist in its domain while hallucinating substantially less. ORCAS does not require massive scale — it requires data purity. Scale without purity is the problem ORCAS is designed to solve.

Much of the ideal training data is held behind commercial paywalls by academic publishers. Open access repositories, public domain literature, government publications, and institutional partnerships can partially mitigate this. The long-term alignment of ORCAS with the open access movement is structural — this architecture is most powerful when knowledge is freely accessible, and it provides an institutional incentive for contributing to open access.

### 7.2 Cross-Domain Query Complexity

Some queries are deeply interdisciplinary and cannot be cleanly partitioned between specialists. The assembly of partial responses may produce outputs that are locally correct in each domain but globally incoherent at their interface.

**Mitigation:** Specialists are trained to produce structured partial responses with explicit interface labels — the boundaries between their output and adjacent specialists' outputs are marked and typed, including specific gap queries reformulated for the receiving specialist. Routey's assembly operation respects these boundaries. Where integration is incomplete or interface points between specialist outputs are semantically incompatible, Routey flags this to the user explicitly rather than producing a silently incoherent response.

### 7.3 Base Model Reasoning Capability

A base model trained only on clean, domain-neutral data may lack the emergent reasoning capabilities that appear to arise from large-scale diverse training. Some reasoning capabilities in current frontier models are partly a product of training data diversity.

**Mitigation:** The base model corpus, while curated for quality and domain-neutrality, can be deliberately diverse in subject matter. Mathematical literature, formal logic, philosophy of language, linguistics, encyclopaedic references, and structured argumentation provide reasoning-relevant training signal without introducing domain-specific noise or unverified content.

### 7.4 Compute and Development Cost

Pre-training from scratch is significantly more expensive than fine-tuning an existing base model. This is a genuine economic barrier to initial development.

**Mitigation:** The modular architecture means specialists can be trained and deployed incrementally. A viable first version with two or three specialists can be developed before scaling the Council. Each specialist is an independent training project. The long-term compute cost is offset by commercial value in regulated industries where current LLMs cannot be deployed — markets that are currently inaccessible to all existing AI products represent a significant commercial opportunity. Once the Base Model exists, each additional specialist is a substantially smaller investment.

### 7.5 Routey Failure Modes

When Routey misroutes, the user receives a response from a specialist without genuine competence in the query's domain. Unlike a generalist model, the specialist will return a referral or partial response rather than a hallucinated answer — so misrouting is self-correcting to a degree. However, a misrouted query still creates latency and friction.

**Mitigation:** Routey's uncertain routing mode exists precisely to handle low-confidence classification. Misroutes that are corrected by specialist referrals generate training data for Routey automatically. The failure mode of ORCAS under misrouting — a specialist returning "not my domain" — is substantially less harmful than the failure mode of a generalist LLM under the same conditions — a confident hallucinated answer.

---

## 8. Open Architecture

ORCAS is proposed as an open architecture. Specialist model weights, training corpora where legally distributable, routing protocols, structured output schemas, and Council interface specifications should be publicly available.

This is both an ethical position and a strategic one. An open architecture attracts academic and developer contribution, accelerating improvement across the Council. It builds trust with regulated industries that cannot deploy or audit closed systems. It enables jurisdictional and institutional adaptation: a legal specialist can be retrained for a different legal system by any institution with access to the relevant corpus; a medical specialist can be specialised further for a specific clinical context.

Openness also distributes the data acquisition problem. Academic institutions, hospitals, legal bodies, and research organisations can contribute curated domain corpora to improve specialists in their field, with reciprocal access to the resulting models. The architecture incentivises knowledge sharing in a way that closed commercial models structurally cannot.

The modular design means that open source contributions can target specific components. A university hospital might contribute to the Medical Specialist training corpus. A law school might contribute to a Legal Specialist for a specific jurisdiction. A standards body might contribute to an Engineering Specialist. None of these contributions require access to the full system — they are independent, targeted, and directly beneficial to the contributing institution.

---

## 9. Implementation Roadmap

### Phase 1 — Foundation (Months 1–6)
- Corpus curation methodology and quality standards defined
- Base Model training corpus assembled and verified
- Base Model pre-training
- Structured output schema finalised and documented
- Council interface specification published

### Phase 2 — First Council (Months 6–12)
- Two to three initial specialists selected based on corpus availability and commercial viability
- Specialist training corpora assembled and verified
- Specialist training on Base Model
- Boundary recognition and structured output training validated
- Internal end-to-end testing

### Phase 3 — Routey and Integration (Months 12–18)
- Routey training corpus assembled from Phase 2 outputs
- Routey trained on Base Model
- Full system integration
- Routing accuracy benchmarking
- Limited external deployment for feedback collection
- Feedback loop validation

### Phase 4 — Council Expansion (Months 18+)
- Additional specialists trained and integrated
- Routey retrained on expanded domain boundary map
- Open source release of architecture specification and initial weights
- Community contribution framework established

Each phase produces usable outputs independently. Phase 2 produces specialist models that can be evaluated in isolation before integration. The system does not require full completion before generating value or feedback.

---

## 10. Conclusion

ORCAS proposes a fundamental reorientation of AI development priorities: from generalisation at scale to specialisation at quality. The hallucination problem is not an implementation failure — it is an architectural consequence of training objectives that prioritise fluency over accuracy and data volume over data verifiability.

By separating linguistic capability from domain knowledge, building specialists on verified corpora, training epistemic honesty as a core feature, and orchestrating specialist coordination through a purpose-built routing model, ORCAS aims to produce AI systems that are genuinely reliable in the domains where reliability matters most.

The modularity of the architecture means that no single failure point compromises the whole system. A specialist that performs poorly in its domain does not affect other specialists. Routey's routing errors are self-correcting through specialist referral signals. The Base Model is trained once and shared across all components, making the foundational investment reusable.

The AGI race optimises for impressive capability demonstrations across all domains simultaneously. ORCAS optimises for trustworthy answers in specific domains one at a time. In medicine, law, and engineering, trustworthy answers are worth more than impressive ones.

The system knows what it knows. It knows what it does not. It asks when it is uncertain. These are properties we expect from reliable experts. They should be properties we expect from reliable AI.

---

## Glossary

**ASI (Artificial Specialised Intelligence)** — AI systems designed for deep competence in specific domains rather than broad generalisation across all domains. Distinct from the common usage of ASI as "Artificial Superintelligence."

**Base Model** — The clean, domain-neutral language model at the foundation of ORCAS, pre-trained from scratch on curated, verified data. All specialists and Routey are built from this shared foundation.

**Boundary Recognition** — The trained capability of a specialist to accurately identify whether a given query falls within its domain, partially within its domain, or outside its domain entirely.

**Council** — The collective of domain-specialist models in the ORCAS system. Each Council member is independently trained on a domain-pure corpus and communicates with Routey through a standardised structured output format.

**Domain Gap** — A portion of a query that falls outside a specialist's domain, identified and labelled by the specialist in a partial response and passed to Routey for dispatch to the appropriate specialist.

**Epistemic Honesty** — The capacity of a model to accurately represent the limits of its own knowledge. In ORCAS, epistemic honesty is a trained feature of every specialist, not an emergent property.

**Hallucination** — The generation of fluent, confident text that is factually incorrect. A consequence of training on contradictory or unverified data where the model learns to interpolate between conflicting signals.

**Mixture of Experts (MoE)** — An existing architecture in which a single model contains multiple expert parameter sets and routes internally between them. Distinguished from ORCAS in that all MoE experts share the same training data and are not independently trained models.

**ORCAS (Orchestrated Router-Council ASI System)** — The complete system described in this document, comprising the Base Model, the Council of specialists, and the Routey orchestration layer.

**Partial Response** — A specialist response type indicating that the query spans the specialist's domain and one or more other domains. The specialist answers its portion and explicitly labels the remainder as requiring other specialists.

**Referral** — A specialist response type indicating that the query falls entirely outside the specialist's domain. The specialist returns a structured signal identifying likely relevant domains rather than attempting an answer.

**Routey** — The orchestration model responsible for query classification, specialist dispatch, response assembly, and user-facing communication. Routey is lean by design; its task is routing, not knowing.

**Structured Output** — The typed, schema-compliant response format used by all ORCAS specialists. Includes response type, answer content, confidence score, source attribution, domain gap labels, referral targets, and gap queries.

---

*ORCAS — Orchestrated Router-Council ASI System*
*Concept Paper v0.2 — June 2026*

*This work is licensed under Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0).
https://creativecommons.org/licenses/by-sa/4.0/*