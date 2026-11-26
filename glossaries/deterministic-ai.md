---
title: Deterministic Decisions in AI Systems — Glossary
version: 1.0
date: 2026-11-26
purpose: Shared vocabulary for separating deterministic, logic-based computation from probabilistic AI reasoning, and for keeping decision data trustworthy over time.
audience: Designers, engineers, product consultants, and LLM agents working on AI-assisted products.
usage_for_llms: Use these as the preferred meanings when a project adopts this lexicon. When a term is ambiguous in the wider industry, the "Watch out" note says how it is used here.
license: CC BY 4.0
---

# Deterministic Decisions in AI Systems — Glossary

## 1. The core distinction

| Deterministic / logical | Probabilistic / AI |
|---|---|
| Same input always gives the same output | Output can vary between runs; it is sampled |
| Symbolic AI, rule-based systems, expert systems | Statistical, connectionist, or neural AI (including LLMs) |
| Deductive reasoning: conclusions follow from stated rules | Inductive reasoning: patterns generalized from examples |
| Formal methods and formal verification (proof) | Empirical evaluation (testing on samples) |
| Explainable by construction | Explained after the fact (post-hoc) |

### Deterministic
- **Definition:** A process that always produces the same output for the same input and state.
- **Use it for:** Calculations, eligibility checks, policy enforcement, anything that must be repeatable and auditable.

### Probabilistic (stochastic)
- **Definition:** A process whose output is drawn from a probability distribution, so repeated runs can differ.
- **Use it for:** Language understanding, summarizing, drafting, classification of messy input, judgment calls.
- **Watch out:** Setting an LLM's temperature to 0 reduces variation but does not guarantee identical outputs. Model updates by the provider can also change behavior. Do not call an LLM step "deterministic."

## 2. Families of AI and how they combine

### Symbolic AI
- **Definition:** AI that represents knowledge as explicit symbols, rules, and logic, and reasons by applying them. Also called classical AI or GOFAI ("good old-fashioned AI").
- **Examples:** Rules engines, decision tables, expert systems, knowledge graphs with logical inference, constraint solvers.

### Statistical / neural AI
- **Definition:** AI that learns patterns from data and represents them as numeric weights. Includes machine learning and large language models (LLMs).

### Deductive vs. inductive reasoning
- **Deductive:** From general rules to a guaranteed conclusion. If the rules and facts are right, the answer is right.
- **Inductive:** From examples to a likely generalization. The answer is probably right, with some error rate.

### Neuro-symbolic AI
- **Definition:** Systems that combine neural models (for perception, language, and judgment) with symbolic components (for rules, logic, and exact calculation).
- **Common pattern:** The LLM interprets the request and proposes an action; a symbolic layer computes, checks constraints, and makes or blocks the final decision.
- **Short phrase:** "LLMs propose, deterministic systems dispose."

## 3. Architecture patterns that keep decisions deterministic

### Tool use (function calling)
- **Definition:** The LLM calls external code (a calculator, database query, API, or rules engine) instead of producing the answer itself.
- **Why:** Keeps math, lookups, and business rules out of the model. "Keep the LLM out of the math."

### Structured outputs / constrained decoding
- **Definition:** Forcing model output to match a defined schema (for example, JSON with required fields and allowed values) so it can be validated by code.

### Schema validation
- **Definition:** Code that checks data against a declared structure and rules (types, ranges, required fields) and rejects anything that does not fit.

### Rules engine / decision table
- **Definition:** Software that evaluates explicit if-then rules or a table of conditions and outcomes. DMN (Decision Model and Notation, an OMG standard) is a common notation for decision tables.

### Policy as code
- **Definition:** Writing policies (access, compliance, approval limits) as versioned, testable code rather than prose.

### Guardrails
- **Definition:** Checks placed around an AI component to prevent unsafe, invalid, or out-of-policy inputs and outputs.
- **Deductive (symbolic) guardrails:** Code or logic that enforces hard constraints. Deterministic.
- **Inductive (neural) guardrails:** A model judges another model's output, for example "LLM-as-judge." Probabilistic.
- **Watch out:** Some products sold as "deterministic guardrails" still use an LLM to generate or run the check. Ask which kind it is.

### Formal verification
- **Definition:** Mathematically proving that a system meets a specification, instead of only testing examples.

### Human-in-the-loop (HITL)
- **Definition:** A person reviews or approves at defined checkpoints, usually before consequential or irreversible actions.

## 4. Data governance and hygiene

### Data governance
- **Definition:** The policies, roles, and ownership that decide how data is collected, defined, accessed, and used.

### Data lineage / provenance
- **Definition:** A record of where each data point came from and every transformation it went through. Lets you trace a decision back to its sources.

### Data contract
- **Definition:** A formal agreement between a data producer and its consumers on schema, meaning, quality rules, and change process. Breaking changes are caught before they reach decisions.

### Data quality dimensions
- **Definition:** The standard criteria for judging data: **accuracy, completeness, consistency, timeliness, validity, uniqueness.**

### Master data management (MDM) / single source of truth
- **Definition:** Keeping one authoritative, agreed version of core entities (customers, products, accounts) that every system uses.

### Taxonomy, ontology, knowledge graph
- **Taxonomy:** A controlled, hierarchical set of categories for classifying things consistently.
- **Ontology:** A richer model of concepts and the relationships between them, with defined meanings.
- **Knowledge graph:** Data stored as entities and relationships, often based on an ontology, that both people and machines can query and reason over.

### Data validation vs. drift detection
- **Data validation:** Is this data well-formed and within the rules? (A per-record or per-batch check.)
- **Drift detection:** Has the data or the world changed compared with what the system was built on? (A comparison over time.)
- **Watch out:** These are often confused. They have different causes and different fixes.

## 5. Drift

### Data drift (covariate shift)
- **Definition:** The distribution of inputs changes, P(X), while the relationship between inputs and outcomes stays the same.

### Concept drift
- **Definition:** The relationship between inputs and the outcome changes, P(y|X). The same inputs now mean something different.
- **Watch out:** "Concept drift" and "data drift" are used interchangeably in some literature, and "concept drift" is sometimes an umbrella term. Define which one you mean.

### Label drift (prior shift)
- **Definition:** The mix of outcomes changes, P(y), for example a rare event becoming common.

### Model drift
- **Definition:** The general business term for a model's performance degrading over time, usually caused by one of the drifts above.

### Behavior drift (LLM systems)
- **Definition:** An AI system's outputs change because the underlying model, prompt, retrieved content, or tools changed, even when inputs did not.
- **Mitigation:** Pin model versions, version prompts, and rerun a fixed evaluation set after any change.

### Drift patterns
- **Sudden:** An abrupt change.
- **Gradual:** The old pattern fades as the new one appears.
- **Incremental:** A slow, steady shift.
- **Recurring:** Earlier patterns return, for example seasonally.

## 6. Reliability practices

### Reproducibility
- **Definition:** Data, code, model, prompt, and settings are all versioned, so a past decision can be rerun and gives the same result.

### Idempotency
- **Definition:** Running an operation more than once has the same effect as running it once. Prevents duplicate actions on retries.

### Versioning and pinning
- **Definition:** Recording exact versions of data snapshots, code, models, and prompts, and fixing (pinning) them in production so nothing changes silently.

### Evaluations (evals) and golden datasets
- **Eval:** A repeatable test that scores an AI system's outputs against expected results.
- **Golden dataset:** A fixed, curated set of inputs with known correct answers, used to detect regressions.

### Backtesting / replay
- **Definition:** Running a decision process over past data to see what it would have decided, before changing it in production.

### Pre-registered decision rule
- **Definition:** Writing down how a choice will be made (the metric and threshold) before seeing the results, so the outcome cannot be rationalized after the fact.

### Observability and monitoring
- **Definition:** Logging and measuring data, decisions, and model behavior in production so problems show up quickly.

### Audit trail
- **Definition:** A tamper-evident record of what was decided, when, by which version of which component, and from which data.

### Explainability (XAI)
- **By construction:** The decision logic is readable (rules, tables, formulas).
- **Post-hoc:** Techniques that estimate why a model produced an output after the fact.

## 7. Umbrella disciplines and frameworks

- **MLOps:** Practices for building, deploying, monitoring, and retraining machine learning models reliably.
- **LLMOps:** MLOps adapted to LLM systems: prompt and model versioning, evals, guardrails, cost and latency monitoring.
- **DataOps:** Applying agile and DevOps practices to data pipelines and data quality.
- **Decision intelligence:** Treating decisions as something to design, model, measure, and improve, combining data, rules, and AI.
- **AI governance frameworks:** NIST AI Risk Management Framework (AI RMF 1.0) and ISO/IEC 42001 (AI management systems).

## 8. Talking points

- "We use AI where judgment and language help, and deterministic logic where decisions must be correct, repeatable, and auditable."
- "The model proposes; rules and calculations decide."
- "Every decision traces back to versioned data and explicit rules."
- "We monitor for drift so the system doesn't quietly degrade."
- "We write the decision rule down before we see the results."

## Sources
- How neurosymbolic AI can transform enterprise decision-making — InfoWorld: https://www.infoworld.com/article/4243405/how-neurosymbolic-ai-can-transform-enterprise-decision-making.html
- Autonomous Business System via Neuro-symbolic AI — arXiv: https://arxiv.org/pdf/2601.15599
- Don't Make Models Guess: Symbolic Guardrails for Domain-Specific AI Agents — arXiv: https://arxiv.org/pdf/2604.15579
- PL-Guard: Probabilistic Logic Reasoning for LLM Guardrails — arXiv: https://arxiv.org/pdf/2608.15673
- Understanding and adapting to data drift — Microsoft: https://learn.microsoft.com/ai/playbook/capabilities/ml-lifecycle-management/drift-and-adaptation/drift-overview
- Data Drift vs. Concept Drift — Deepchecks: https://deepchecks.com/data-drift-vs-concept-drift-what-are-the-main-differences/
- Time to Retrain? Detecting Concept Drifts in Machine Learning Systems — arXiv: https://arxiv.org/pdf/2410.09190
