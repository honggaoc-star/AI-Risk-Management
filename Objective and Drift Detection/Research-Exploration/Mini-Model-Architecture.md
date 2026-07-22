# Preliminary Architecture for a Mini-Model Drift Monitor

## Status

**Version 0.1 — July 2026**

This document specifies a preliminary, testable architecture for monitoring objective and design drift in extended human–AI collaboration. It follows the [research proposal](Research-Proposal.md) and [focused literature review](Focused-Literature-Review.md). It is not an implementation specification and does not presume that a trained mini model will outperform simpler controls.

## 1. Architectural Objective

The proposed system should determine whether a candidate AI output materially and without acknowledgment departs from the user-authorized state of a project, then select the least disruptive intervention proportionate to the risk.

The central design principle is:

> **Monitor continuously, intervene selectively, and preserve user momentum.**

The monitor is not intended to:

- perform the primary substantive task;
- certify factual truth, safety, or legal compliance;
- infer unstated user intent without evidence;
- freeze a project against deliberate change;
- replace human authority over governing objectives; or
- block every inconsistency.

Its bounded role is **project-state fidelity assessment**.

## 2. Core Architectural Claim

The mini model should not be treated as a standalone solution. Drift monitoring requires a system:

```text
governing-state construction
        + authority and version control
        + task-relevant retrieval
        + candidate-output comparison
        + calibrated intervention
```

The mini model performs principally the fourth function. Failures in the other functions can make even an accurate evaluator ineffective or harmful.

## 3. System Overview

```text
                           ┌───────────────────────────┐
                           │ User / Authorized Editor  │
                           └─────────────┬─────────────┘
                                         │ decisions and changes
                                         ▼
┌─────────────────┐            ┌───────────────────────────┐
│ Project Sources │───────────▶│ Governing-State Manager   │
│ chats/files/logs│            │ authority + versioning    │
└─────────────────┘            └─────────────┬─────────────┘
                                              │ relevant anchors
                                              ▼
┌─────────────────┐            ┌───────────────────────────┐
│ Current Request │───────────▶│ Retrieval / State Builder │
└────────┬────────┘            └─────────────┬─────────────┘
         │                                   │
         ▼                                   ▼
┌─────────────────┐            ┌───────────────────────────┐
│ Primary Model   │───────────▶│ Specialized Drift Monitor │
│ candidate output│            │ compare + classify + cite │
└─────────────────┘            └─────────────┬─────────────┘
                                              │ structured assessment
                                              ▼
                                ┌───────────────────────────┐
                                │ Intervention Policy       │
                                └─────────────┬─────────────┘
                                              ▼
                         pass | log | revise | notify | confirm | block
```

## 4. Unit of Analysis

The primary unit is a **candidate output–anchor relationship**.

- A **candidate output** is a response, proposed edit, tool action, plan, summary, or state update produced by the primary model.
- A **governing anchor** is an explicit project statement with recorded scope, authority, and version status.

The monitor may evaluate:

1. individual claims or proposed changes;
2. sections or actions;
3. structural relationships among components; and
4. the candidate output as a whole.

Claim-level analysis improves traceability, but drift may be structural and invisible at the sentence level. The architecture therefore requires both local and aggregate assessment.

## 5. Governing-State Model

### 5.1 Anchor Types

The governing state should support at least:

- **objective:** intended outcome, purpose, or value criterion;
- **audience or user:** intended beneficiary or decision-maker;
- **definition:** controlling meaning or conceptual distinction;
- **assumption:** accepted or provisional premise;
- **constraint:** required boundary, method, format, resource, or risk limit;
- **decision:** adopted choice and, where available, rationale;
- **exclusion:** explicitly rejected or out-of-scope item;
- **architecture:** approved structure or relationship among components;
- **evidence rule:** permitted sources, proof standard, or source hierarchy;
- **unresolved question:** issue not yet decided;
- **rejected alternative:** considered but not adopted; and
- **supersession record:** relationship between a current and former anchor.

### 5.2 Anchor Schema

A preliminary schema is:

```yaml
anchor_id: OBJ-001
anchor_type: objective
statement: Preserve the user's governing research design across extended work.
status: active
authority: user_explicit
scope: Objective and Drift Detection research stream
source_reference: conversation-or-file-location
created_at: timestamp-or-version
effective_from: version
supersedes: null
superseded_by: null
confidence_of_extraction: 0.98
materiality_default: high
tags:
  - fidelity
  - long-horizon
notes: null
```

### 5.3 Status Vocabulary

At minimum:

- `active` — currently governing;
- `provisional` — usable as a working assumption but not settled;
- `proposed` — suggested but not authorized;
- `unresolved` — explicitly open;
- `rejected` — considered and not adopted;
- `superseded` — formerly active but replaced;
- `historical` — retained for provenance without current authority; and
- `disputed` — authority or interpretation is contested.

These statuses are central. A system that stores text without its decision status can convert discussion into policy or resurrect rejected ideas.

### 5.4 Authority Vocabulary

A preliminary hierarchy is:

1. `user_explicit` — directly adopted by the authorized user;
2. `authorized_artifact` — recorded in a designated governing document;
3. `user_confirmed_summary` — extracted or summarized and then confirmed;
4. `delegated_authority` — adopted by a person or process with defined authority;
5. `inferred_from_user` — system inference not explicitly confirmed;
6. `ai_proposed` — generated suggestion without adoption; and
7. `unknown` — provenance or authority cannot be established.

Authority is not reducible to recency. A recent AI suggestion should not displace an older explicit user decision.

## 6. Governing-State Construction

State construction is a separate, higher-risk process from drift classification.

### 6.1 Candidate Extraction

Potential anchors may be extracted from:

- explicit user statements;
- designated project documents;
- confirmed summaries;
- decision logs;
- version-control history;
- accepted plans; and
- approved changes.

### 6.2 Confirmation Policy

The system should avoid requiring confirmation for every extracted statement. Proposed practice:

- automatically record explicit, high-confidence formulations;
- batch low-risk inferred anchors for periodic review;
- require confirmation before elevating inferred or AI-generated content to high authority;
- request immediate confirmation only when ambiguity affects a material current action; and
- preserve original source links for later audit.

### 6.3 State Updates

A change should create a new version event rather than silently overwrite the old anchor:

```text
proposed change
    → identify affected anchors
    → show material difference
    → authorize, reject, or defer
    → create version transition
    → retain provenance
```

The state manager must support rollbacks, disputed changes, and concurrent unresolved alternatives.

## 7. Retrieval Layer

Passing the entire state to the monitor would recreate long-context problems. The retrieval layer should construct a compact **evaluation packet**.

### 7.1 Inputs

- current user request;
- candidate output;
- task and workflow stage;
- active governing state;
- relevant recent changes; and
- optionally, source passages supporting retrieved anchors.

### 7.2 Retrieval Process

1. Decompose the candidate into claims, proposed changes, actions, and structural effects.
2. Retrieve anchors by semantic relevance, anchor type, entity, scope, and dependency.
3. Include directly governing active anchors.
4. Include related unresolved, rejected, or superseded anchors when they disambiguate status.
5. Retrieve rationales or source passages only when needed.
6. limit and rank the packet, while signaling retrieval uncertainty.

### 7.3 Retrieval Output

```json
{
  "task": "Draft a preliminary model architecture",
  "candidate_units": ["CU-01", "CU-02"],
  "anchors": ["OBJ-001", "CON-003", "DEC-004"],
  "status_context": ["ALT-002 rejected", "DEC-002 superseded"],
  "retrieval_confidence": 0.87,
  "coverage_warning": false
}
```

Retrieval failure must remain distinguishable from monitor failure.

## 8. Mini-Model Task Definition

Given a candidate unit, task context, and retrieved governing anchors, the monitor should answer:

1. Is there a meaningful divergence?
2. Which anchor or relationship is affected?
3. What type of divergence is present?
4. Is the departure acknowledged as a proposal?
5. Does available evidence indicate authorization?
6. How material and reversible is the change?
7. Is the evidence sufficient to judge?

### 8.1 Output Labels

Primary disposition:

- `aligned`;
- `permissible_development`;
- `possible_drift`;
- `probable_drift`;
- `confirmed_authorized_change`;
- `insufficient_state`; or
- `state_conflict`.

Drift type may be multi-label:

- `objective`;
- `definition`;
- `constraint`;
- `assumption`;
- `decision`;
- `structural_design`;
- `evidence`;
- `scope`; or
- `task`.

### 8.2 Structured Assessment

```json
{
  "disposition": "probable_drift",
  "drift_types": ["constraint", "evidence"],
  "affected_anchors": ["CON-003", "EVD-002"],
  "divergence_summary": "The candidate introduces excluded retrospective sources.",
  "acknowledged_change": false,
  "authorization_found": false,
  "drift_probability": 0.91,
  "materiality": "high",
  "reversibility": "medium",
  "assessment_confidence": 0.88,
  "state_sufficiency": "sufficient",
  "recommended_action": "confirmation_request"
}
```

Natural-language rationales should be short and evidence-linked. Untraceable explanations should not be treated as proof.

## 9. Candidate Model Approaches

The architecture should test alternatives rather than select a model prematurely.

### 9.1 Deterministic Rules

Useful for exact exclusions, required fields, file boundaries, source dates, and explicit prohibited actions.

**Strength:** transparent, inexpensive, predictable.  
**Limit:** weak on paraphrase, conceptual relationships, and legitimate exceptions.

### 9.2 Embedding Similarity and Change Detection

Compare candidate units with relevant anchors and detect large semantic movement.

**Strength:** economical retrieval and screening.  
**Limit:** similarity is not entailment, authority, or drift; subtle reversals may remain textually close.

### 9.3 Natural-Language-Inference or Cross-Encoder Model

Classify candidate–anchor pairs as supported, contradicted, unrelated, or modified.

**Strength:** close to established factuality evaluators; compact implementations are plausible.  
**Limit:** pairwise entailment does not capture multi-anchor structure, authorization, or materiality.

### 9.4 Compact Generative Evaluator

Use a small instruction-tuned model to produce structured labels and anchor-linked explanations.

**Strength:** handles heterogeneous anchors and nuanced change.  
**Limit:** may hallucinate rationales, be less calibrated, and introduce greater latency.

### 9.5 Hybrid Cascade

The provisional preferred design is a cascade:

```text
rules and schema checks
        ↓
embedding retrieval and low-cost screening
        ↓
cross-encoder or compact evaluator
        ↓
larger judge or human review only for material ambiguity
```

This design reserves expensive or interruptive review for difficult cases. Whether it outperforms a single evaluator remains an empirical question.

## 10. Proposed Mini-Model Design

For an initial learned prototype, the leading hypothesis is a compact cross-encoder or encoder–decoder trained on structured candidate–state comparisons.

### 10.1 Inputs

- task description;
- workflow stage;
- one or more candidate units;
- retrieved anchors with type, status, authority, and scope;
- relevant change history; and
- optional source excerpts.

### 10.2 Outputs

- primary disposition;
- multi-label drift type;
- affected anchor IDs;
- divergence and authorization scores;
- materiality and reversibility estimates;
- state-sufficiency estimate; and
- a bounded anchor-linked explanation.

### 10.3 Multi-Task Objective

A possible training objective is:

\[
L = \lambda_1 L_{disposition}
  + \lambda_2 L_{type}
  + \lambda_3 L_{anchor}
  + \lambda_4 L_{materiality}
  + \lambda_5 L_{sufficiency}
  + \lambda_6 L_{calibration}
\]

The relative weights should be tuned around consequential false negatives and disruptive false positives, not aggregate accuracy alone.

### 10.4 Size

“Mini” is functional rather than fixed by a parameter threshold. The model should be materially smaller and cheaper than the primary generator and capable of routine parallel or pre-release evaluation. Candidate sizes might range from hundreds of millions to a few billion parameters, but size should remain an evaluated design variable.

## 11. Training Data Design

### 11.1 Example Structure

Each example should contain:

- a project-state snapshot;
- a current request;
- a candidate response or action;
- relevant anchor IDs;
- disposition and drift labels;
- materiality and reversibility ratings;
- authorization status;
- an evidence-linked rationale; and
- annotator disagreement or ambiguity metadata.

### 11.2 Positive Cases

- explicit reversal of an accepted decision;
- subtle redefinition of a controlling term;
- excluded evidence introduced without acknowledgment;
- scope expansion presented as part of the approved task;
- architecture changes that undermine governing relationships;
- provisional assumptions converted into facts; and
- stale or superseded instructions restored.

### 11.3 Hard Negatives

The most important negative cases include:

- paraphrase without substantive change;
- elaboration consistent with the design;
- explicitly marked exploration;
- user-authorized revision;
- correction of a documented mistake;
- response to new evidence under an accepted change process;
- local deviation that does not materially affect the project; and
- candidate output that identifies a conflict rather than silently resolving it.

Without hard negatives, the model may learn conservatism rather than fidelity.

### 11.4 Data Sources

- controlled synthetic longitudinal projects;
- perturbations of real, consented project histories;
- version-control and document-revision traces;
- expert-authored edge cases;
- adversarial examples; and
- naturally occurring monitor disagreements.

Synthetic data can establish coverage but must not be the sole evaluation source.

## 12. Intervention Policy

The model should assess; a separate policy should decide what happens.

### 12.1 Policy Inputs

- drift probability;
- assessment confidence;
- materiality;
- reversibility;
- state sufficiency;
- anchor authority;
- workflow stage;
- user preferences; and
- consequence of delay or error.

### 12.2 Default Ladder

| Condition | Default action |
|---|---|
| Aligned or permissible development | Pass silently |
| Low-confidence, low-materiality divergence | Log |
| Clear, trivial, reversible inconsistency | Quiet correction where authorized |
| Moderate materiality or useful awareness | Passive notice |
| High materiality, plausible drift, reversible | Request confirmation |
| High materiality, high confidence, difficult to reverse | Pause or exceptional block |
| Insufficient or conflicting state | Ask a focused question only if the current action materially depends on resolution |

The system should learn from user overrides but must not silently reinterpret repeated dismissal as permanent authorization.

## 13. Operating Modes

### 13.1 Pre-Release Monitor

Checks a candidate response before it reaches the user. Best for quiet correction and consequential actions; adds latency.

### 13.2 Post-Response Auditor

Evaluates after delivery and updates a drift log. Low interruption, but errors may already influence the user.

### 13.3 State-Update Gate

Checks only whether a candidate output should become governing state. This may offer a high-value, lower-frequency initial use case.

### 13.4 Periodic Project Audit

Compares current artifacts with earlier governing state at milestones. Lower continuous cost but slower detection.

A practical prototype may begin with the state-update gate and periodic audit before attempting continuous pre-release monitoring.

## 14. Failure Handling

The monitor must distinguish:

- no divergence found;
- divergence found;
- relevant state not retrieved;
- state itself inconsistent;
- authority unclear;
- candidate too complex to assess; and
- evaluator uncertainty.

Forced binary decisions would hide these failure modes. `insufficient_state` and `state_conflict` are required outputs.

## 15. Security, Privacy, and Governance

The governing state may contain sensitive objectives, decisions, unpublished work, or proprietary constraints. The architecture should support:

- data minimization;
- local or controlled deployment where warranted;
- encryption and access control;
- scope-limited retrieval;
- audit logs for state changes and interventions;
- provenance for extracted anchors;
- defenses against memory or state poisoning;
- separation of user authority from retrieved external content; and
- deletion and retention policies.

Retrieved documents must not be allowed to elevate themselves into authoritative state through embedded instructions.

## 16. Observability and Auditability

Every visible intervention should be reconstructable from:

- the candidate unit evaluated;
- state version;
- anchors retrieved;
- model and policy versions;
- scores and disposition;
- action taken;
- user response or override; and
- subsequent state change, if any.

Logs should support evaluation without exposing unnecessary private content.

## 17. Baselines

The mini model must demonstrate incremental value against:

1. no monitor;
2. full-context prompting of the primary model;
3. primary-model self-review;
4. exact rules and schema checks;
5. embedding similarity thresholds;
6. standard NLI or factuality evaluators;
7. a large general-model judge;
8. periodic human review; and
9. hybrid combinations of the above.

If simpler state/version controls perform as well, a learned mini model may not be justified.

## 18. Architectural Hypotheses

The preliminary design yields testable hypotheses:

- **H1:** Explicit status and authority metadata improve drift detection beyond raw project history.
- **H2:** Task-relevant state retrieval improves performance over full-state prompting at comparable cost.
- **H3:** Hard-negative training reduces false alerts on legitimate project evolution.
- **H4:** A compact specialist evaluator can outperform same-cost general-model judging on bounded project-fidelity tasks.
- **H5:** A hybrid cascade provides a better accuracy–latency–cost tradeoff than any single evaluator.
- **H6:** Separating model assessment from intervention policy reduces unnecessary user interruption.
- **H7:** State-update monitoring yields greater initial workflow value than monitoring every generated sentence.
- **H8:** End-to-end performance is more sensitive to state and retrieval quality than to modest changes in evaluator size.

## 19. Prototype Boundary

The first prototype should be deliberately limited:

- domain: AI-assisted research and complex document development;
- state types: objectives, definitions, constraints, decisions, exclusions, and unresolved questions;
- outputs: text responses and proposed document edits;
- languages: initially English;
- intervention: pass, log, passive notice, or confirmation request;
- no autonomous blocking of consequential external actions;
- small, auditable dataset before scale-up; and
- comparison with non-model baselines before fine-tuning.

## 20. Go/No-Go Conditions for Model Training

Training should begin only if:

1. independent annotators can apply the drift and change labels with acceptable agreement;
2. governing anchors can be extracted and maintained with tolerable user burden;
3. retrieval can identify relevant anchors at useful recall;
4. simple baselines leave a meaningful performance gap; and
5. expected monitoring benefit plausibly exceeds latency and interruption costs.

If these conditions fail, the appropriate outcome may be better state/version management, narrower rules, or periodic human audit—not a larger evaluator.

## 21. Open Design Questions

- Should governing state be stored as structured records, prose, a graph, or a hybrid?
- What is the smallest authority vocabulary users can understand and maintain?
- Should candidate decomposition be performed by the monitor or a separate model?
- Can one model jointly assess divergence and materiality without harmful error coupling?
- How should cross-anchor structural drift be represented?
- When may the system quietly correct an output rather than ask the user?
- Can override behavior safely personalize thresholds?
- How can independence from the primary model be measured?
- Which parts should run locally for privacy and latency?
- Is a learned model necessary for the first useful product?

## 22. Working Conclusion

The most plausible architecture is not “a mini model watching a large model” in isolation. It is a governed comparison system in which explicit, versioned project state supplies the reference; retrieval makes the relevant state operative; a specialist evaluator identifies possible divergence; and an external policy limits intervention to material cases.

The next document, `Preliminary-Evaluation-Design.md`, should test the architecture component by component and judge success by end-to-end workflow value rather than classification accuracy alone.
