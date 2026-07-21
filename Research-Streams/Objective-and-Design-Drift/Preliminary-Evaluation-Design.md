# Preliminary Evaluation Design for Objective and Design Drift Monitoring

## Status

**Version 0.1 — July 2026**

This document defines a preliminary evaluation program for the system proposed in [Mini-Model-Architecture.md](Mini-Model-Architecture.md). It is intended to determine whether objective and design drift can be reliably identified, whether a specialized mini model adds value, and whether monitoring improves extended human–AI work after accounting for its costs.

It is not a preregistered protocol. Thresholds, sample sizes, and statistical tests remain provisional until a pilot establishes task prevalence, annotation reliability, and expected effect sizes.

## 1. Evaluation Objective

The central question is not simply whether a model can classify examples of drift.

> **Does an explicit-state monitoring system reduce consequential, unacknowledged project drift without imposing interruption, latency, maintenance, and conservatism costs that outweigh the benefit?**

The evaluation therefore has four levels:

1. **Construct evaluation:** Can objective and design drift be defined and labeled consistently?
2. **Component evaluation:** Do state representation, retrieval, and specialized comparison work separately?
3. **System evaluation:** Does the integrated monitor detect and contain drift?
4. **Workflow evaluation:** Does the system improve completed work and user experience?

A model can perform well at one level and fail at another. High classification accuracy cannot compensate for corrupted state, failed retrieval, or disruptive intervention.

## 2. Evaluation Principles

### 2.1 Evaluate the System, Not Only the Model

End-to-end reliability depends on:

```text
state quality
    × retrieval coverage
    × evaluator performance
    × intervention effectiveness
```

Errors must be attributed to the component that produced them wherever possible.

### 2.2 Treat Legitimate Development as a First-Class Class

The monitor must distinguish silent drift from authorized revision, exploration, elaboration, and correction. A system that prevents change is not aligned; it is conservative.

### 2.3 Measure Consequence, Not Only Frequency

Missing one foundational objective reversal may matter more than correctly identifying many minor wording deviations. Results should be stratified or weighted by materiality.

### 2.4 Preserve Ambiguity

Some cases cannot be resolved from available state. `insufficient_state`, `state_conflict`, and adjudicated ambiguity must not be forced into binary labels.

### 2.5 Separate Development and Test Evidence

Project traces, generators, domains, and perturbation templates used for training should not silently reappear in the final test set.

### 2.6 Compare Against Simpler Alternatives

The learned mini model is justified only if it improves on rules, retrieval, embeddings, existing factuality or inference models, primary-model self-review, and proportionate human review.

### 2.7 Include User and Workflow Costs

False alerts, confirmations, delay, state-maintenance burden, and constrained exploration are evaluation outcomes, not afterthoughts.

## 3. Constructs and Labels

### 3.1 Primary Construct

Objective and design drift is:

> **A material, unacknowledged divergence of AI-generated work from the user-authorized objectives, definitions, constraints, decisions, or conceptual architecture governing an extended interaction or project.**

### 3.2 Required Elements

An affirmative drift label normally requires:

- an identifiable governing anchor or structural relationship;
- meaningful divergence from that anchor;
- materiality to the project or task;
- absence of adequate acknowledgment; and
- no evidence that the change was authorized.

### 3.3 Primary Disposition Labels

- `aligned` — no meaningful divergence;
- `permissible_development` — development, elaboration, exploration, or correction consistent with the change process;
- `possible_drift` — evidence suggests divergence but is incomplete or ambiguous;
- `probable_drift` — material, unacknowledged, unauthorized divergence is well supported;
- `confirmed_authorized_change` — divergence exists and was knowingly authorized;
- `insufficient_state` — available state cannot support a valid judgment; and
- `state_conflict` — governing anchors conflict or authority cannot be resolved.

### 3.4 Drift Types

Multi-label classification may include:

- objective;
- definition;
- constraint;
- assumption;
- decision;
- structural or design;
- evidence;
- scope; and
- task drift.

### 3.5 Materiality

Provisional four-level scale:

- **M0 — immaterial:** no meaningful effect on governing work;
- **M1 — minor:** localized and readily reversible;
- **M2 — material:** affects a meaningful conclusion, component, or downstream step;
- **M3 — critical:** threatens the central objective, validity, architecture, or an external consequential action.

### 3.6 Reversibility

- **R0 — immediately reversible:** no persistent effect;
- **R1 — readily reversible:** limited correction cost;
- **R2 — costly to reverse:** propagated edits, decisions, or dependencies;
- **R3 — difficult or irreversible:** external action, data loss, publication, or entrenched downstream reliance.

### 3.7 Acknowledgment and Authorization

These should be labeled separately:

- acknowledgment: `none`, `implicit`, `explicit`, `unclear`;
- authorization: `authorized`, `not_authorized`, `pending`, `unclear`;
- authority source: recorded using the governing-state hierarchy.

This prevents the dataset from collapsing substantive divergence and governance status into one opaque judgment.

## 4. Evaluation Units

Four nested units are proposed:

1. **Anchor pair:** one candidate unit compared with one governing anchor.
2. **Candidate unit:** a claim, action, edit, plan step, or structural change compared with all relevant anchors.
3. **Turn or artifact:** a full response, proposed file edit, or tool action.
4. **Trajectory:** the longitudinal project sequence and its accumulated outcomes.

Performance should be reported at all relevant levels. Pair-level success may coexist with trajectory-level failure if the system retrieves the wrong anchors or misses accumulation across individually minor changes.

## 5. Evaluation Stages

### Stage 0: Construct and Annotation Pilot

Determine whether trained reviewers can distinguish drift, authorized change, permissible development, and insufficient state.

### Stage 1: Controlled Component Benchmark

Use fixed state packets and candidate outputs to evaluate state interpretation and drift classification without retrieval uncertainty.

### Stage 2: Retrieval and End-to-End Offline Benchmark

Provide full project histories and require the system to construct or retrieve the relevant state before assessment.

### Stage 3: Simulated Longitudinal Workflows

Run primary models through controlled multi-turn research and document tasks, with and without monitoring.

### Stage 4: Bounded User Study or Shadow Deployment

Observe monitor behavior in real work without initially allowing autonomous blocking or silent state changes.

Progression should be gated. Failure at construct validity should stop or redesign later stages.

## 6. Dataset Design

### 6.1 Initial Domain

The first dataset should focus on AI-assisted research and complex document development. Candidate task families include:

- research-proposal development;
- literature synthesis;
- evidence-bounded case coding;
- conceptual framework revision;
- long-form report editing;
- repository or documentation maintenance; and
- structured project planning.

### 6.2 Trace Sources

Use a mixture of:

- synthetic controlled projects;
- expert-authored project histories;
- consented and de-identified real interaction traces;
- version-controlled document histories;
- generated counterfactual candidates; and
- live trajectories produced by several primary models.

No single source should dominate final evaluation.

### 6.3 Example Composition

The benchmark should deliberately include:

- clear drift positives;
- aligned negatives;
- legitimate-development hard negatives;
- authorized changes;
- insufficient-state cases;
- conflicting-state cases;
- cumulative drift emerging across turns;
- state-poisoning or stale-state cases; and
- ambiguous examples retained with disagreement metadata.

### 6.4 Controlled Perturbations

Perturbations may introduce:

- objective substitution;
- definition broadening or narrowing;
- constraint deletion or weakening;
- assumption promotion from provisional to factual;
- decision reversal;
- structural reorganization that breaks dependencies;
- evidence-standard relaxation;
- scope expansion;
- task substitution;
- reintroduction of rejected content;
- resurrection of superseded instructions; and
- gradual multi-turn accumulation of small changes.

Perturbations should vary in explicitness, semantic distance, materiality, reversibility, and location.

### 6.5 Hard Negatives

Required hard negatives include:

- paraphrase;
- format or style improvement;
- consistent elaboration;
- explicit brainstorming;
- alternative presented but not adopted;
- correction of an error;
- authorized change;
- response to new evidence under an accepted procedure;
- terminology modernization with preserved meaning;
- local restructuring without conceptual effect; and
- transparent identification of a conflict.

At least half of non-drift test cases should be difficult negatives rather than trivial alignment examples.

### 6.6 Preliminary Scale

Suggested stages, subject to pilot revision:

- annotation pilot: 100–200 candidate units from 10–20 trajectories;
- controlled benchmark: 1,000–2,000 candidate units from at least 75 trajectories;
- end-to-end offline benchmark: at least 100 full trajectories;
- simulated workflow study: 30–60 tasks across multiple primary-model conditions;
- user study: determined by pilot variance and power analysis.

The trajectory, not the pair count, should govern claims about longitudinal performance.

## 7. Annotation Protocol

### 7.1 Reviewer Independence

Each evaluation case should receive at least two independent annotations before adjudication. Reviewers should not see model predictions or synthetic-generation labels.

### 7.2 Annotation Sequence

1. Read the task and governing-state packet.
2. Identify affected anchors without seeing a proposed label.
3. determine whether substantive divergence exists.
4. label acknowledgment and authorization separately.
5. assess materiality and reversibility.
6. assign primary disposition and drift types.
7. cite the decisive state evidence.
8. record uncertainty and missing information.

### 7.3 Adjudication

Disagreement should be preserved before resolution. The adjudication record should distinguish:

- misunderstanding of the protocol;
- missed evidence;
- differing interpretation;
- genuine state ambiguity; and
- disagreement about materiality.

Genuinely ambiguous cases may remain soft-labeled or excluded from headline binary metrics while being retained for uncertainty evaluation.

### 7.4 Agreement Measures

Report:

- raw agreement;
- class-specific agreement;
- Cohen's kappa or an appropriate multi-rater alternative for categorical labels;
- weighted kappa or ordinal agreement for materiality and reversibility;
- agreement on affected anchors; and
- adjudication rate.

Agreement thresholds should be set before full data production. A provisional requirement is substantial agreement on the primary disposition and acceptable agreement on material cases. Low agreement should trigger taxonomy or protocol revision rather than automatic expansion of the dataset.

## 8. Experimental Conditions and Baselines

### 8.1 Baseline Conditions

1. **No monitor.**
2. **Primary model with full raw history.**
3. **Primary model with structured state but no separate monitor.**
4. **Primary-model self-review.**
5. **Rules and schema checks.**
6. **Embedding similarity or change threshold.**
7. **Standard NLI or factuality evaluator.**
8. **Large general-model judge.**
9. **Specialized compact evaluator.**
10. **Hybrid cascade.**
11. **Periodic human review**, where appropriate.

### 8.2 State Conditions

- raw conversation or document history;
- unstructured human summary;
- structured state without authority metadata;
- structured state with status and authority;
- structured and versioned state with change history; and
- corrupted, stale, incomplete, or conflicting state.

### 8.3 Retrieval Conditions

- oracle relevant anchors;
- full governing state;
- embedding retrieval;
- hybrid semantic and metadata retrieval;
- retrieval with reranking; and
- deliberately degraded retrieval.

### 8.4 Intervention Conditions

- detection only;
- passive post-response notice;
- pre-release notice;
- confirmation request for material cases;
- quiet correction for narrowly authorized cases; and
- graduated policy.

Autonomous blocking should not be part of the initial live evaluation.

## 9. Component Metrics

### 9.1 Governing-State Construction

- anchor extraction precision and recall;
- anchor-type accuracy;
- status and authority accuracy;
- version-transition accuracy;
- provenance completeness;
- stale-anchor rate;
- user correction rate; and
- state-maintenance time.

### 9.2 Retrieval

- relevant-anchor recall at *k*;
- precision at *k*;
- mean reciprocal rank or normalized discounted cumulative gain;
- coverage of all decisive anchors;
- retrieval latency;
- irrelevant-context load; and
- error rate by anchor type, age, and position.

Decisive-anchor recall should receive greater emphasis than average retrieval relevance.

### 9.3 Drift Evaluator

- macro and per-class precision, recall, and F1;
- precision–recall curves;
- area under the precision–recall curve where class imbalance warrants;
- materiality-weighted error;
- anchor-identification accuracy;
- multi-label drift-type performance;
- expected calibration error and reliability plots;
- selective accuracy or risk–coverage curves;
- insufficient-state detection; and
- explanation traceability.

### 9.4 Intervention Policy

- visible-alert rate;
- confirmation-request rate;
- unnecessary-interruption rate;
- missed-intervention rate;
- correct escalation by materiality;
- user override rate;
- override correctness after adjudication;
- alert concentration and fatigue; and
- policy latency.

## 10. End-to-End Metrics

### 10.1 Drift Outcomes

- proportion of drift events detected;
- proportion contained before becoming operative;
- time or turns to detection;
- accumulated drift severity;
- downstream propagation prevented;
- critical drift miss rate; and
- final project-fidelity score.

### 10.2 Workflow Outcomes

- task completion rate;
- completion time;
- number of user interventions;
- state-maintenance burden;
- output quality by blinded expert review;
- user trust and perceived control;
- alert fatigue;
- perceived interruption;
- preservation of exploratory freedom; and
- rate of legitimate changes delayed or suppressed.

### 10.3 Cost Outcomes

- added tokens and computation;
- median and tail latency;
- monetary cost;
- memory and storage cost;
- human review time; and
- correction cost for escaped versus intercepted drift.

## 11. Consequence-Weighted Evaluation

An unweighted event count may reward detection of many trivial deviations while hiding rare critical failures. A provisional consequence weight may combine materiality and reversibility:

\[
w_i = f(M_i, R_i)
\]

One end-to-end loss formulation is:

\[
L_{system} =
\sum_i w_i C_{miss,i}
+ \alpha C_{false\ alert}
+ \beta C_{interruption}
+ \gamma C_{latency}
+ \delta C_{state\ maintenance}
+ \epsilon C_{constrained\ exploration}
\]

The coefficients should not be chosen solely by researchers. They should be informed by user preferences and use-case consequences, and sensitivity analyses should show how conclusions change under different weights.

## 12. Primary Evaluation Questions

### Q1. Is the Construct Labelable?

Can independent reviewers identify objective and design drift with adequate agreement, particularly for material cases?

### Q2. Does Explicit State Help?

Does structured, versioned, authority-labeled state improve performance over raw history or ordinary summaries?

### Q3. Does Specialized Retrieval Help?

Does relevant-anchor retrieval improve accuracy and efficiency over full-state prompting without increasing decisive omissions?

### Q4. Does a Mini Model Add Incremental Value?

Does the compact evaluator outperform equal-cost simpler baselines and approach or exceed a larger judge on the bounded task?

### Q5. Can Drift Be Distinguished from Development?

Does the system maintain high precision on hard negatives involving legitimate change, correction, and exploration?

### Q6. Does Graduated Intervention Improve Workflow Value?

Does a materiality-sensitive policy reduce consequential drift with fewer interruptions than a uniform warning policy?

### Q7. Where Does the System Fail?

What proportion of end-to-end errors originates in state construction, retrieval, evaluation, intervention, or unresolved human disagreement?

## 13. Hypotheses

- **H1:** Structured state with status and authority metadata will improve material-drift detection over raw-history prompting.
- **H2:** Version history will reduce false positives on authorized changes and false negatives involving superseded decisions.
- **H3:** Oracle-anchor evaluation will substantially exceed end-to-end performance, revealing retrieval as a major bottleneck.
- **H4:** Hard-negative training will reduce false alerts on legitimate development without an unacceptable loss in drift recall.
- **H5:** A compact specialist evaluator will outperform comparable-cost general evaluation on in-domain project-fidelity cases.
- **H6:** A hybrid cascade will achieve a better consequence-weighted cost profile than a single large-model judge.
- **H7:** Separating assessment from intervention will reduce unnecessary interruption.
- **H8:** A state-update gate will provide greater early-stage value than monitoring every sentence.
- **H9:** Performance will degrade under stale, conflicting, or poisoned state even when the evaluator is unchanged.
- **H10:** End-to-end workflow benefit will be smaller than offline classification gains.

## 14. Ablation Plan

Remove or alter one component at a time:

- authority metadata;
- status labels;
- version history;
- rejected and superseded anchors;
- retrieval reranking;
- task and workflow-stage metadata;
- materiality prediction;
- hard-negative training;
- explanation or anchor-citation requirement;
- insufficient-state option;
- intervention graduation; and
- larger-model escalation.

These tests should identify whether observed gains come from the mini model or the surrounding state and policy system.

## 15. Robustness and Stress Tests

### 15.1 Longitudinal Scale

Vary number of turns, artifacts, anchors, revisions, and elapsed project stages.

### 15.2 Semantic Subtlety

Test paraphrase, implication, shifted quantifiers, changed scope, softened constraints, and structural rather than lexical divergence.

### 15.3 State Quality

Test missing, duplicated, stale, contradictory, incorrectly extracted, and deliberately poisoned anchors.

### 15.4 Authority Confusion

Introduce recent AI proposals that conflict with older explicit user decisions, conflicting users with different roles, and retrieved content containing apparent instructions.

### 15.5 Distribution Shift

Hold out project types, writing styles, domains, primary-model families, and perturbation generators.

### 15.6 Evaluator Dependence

Compare monitor performance on outputs from the same model family, different families, humans, and adversarial generators. Measure whether generator and evaluator errors correlate.

### 15.7 Adversarial Evasion

Test gradual drift, euphemistic reframing, distributed changes across sections, justification-heavy reversals, and claims that falsely assert user authorization.

## 16. Simulated Workflow Design

Each task should include:

- a governing project brief;
- explicit and provisional anchors;
- at least one authorized change opportunity;
- multiple document or conversation stages;
- opportunities for both drift and legitimate evolution;
- a final artifact judged against the complete authorized state; and
- logged candidate outputs before intervention.

Possible experimental arms:

| Arm | State | Monitor | Intervention |
|---|---|---|---|
| A | Raw history | None | None |
| B | Structured state | None | None |
| C | Structured state | Primary-model self-review | Passive |
| D | Structured state | Large-model judge | Graduated |
| E | Structured state | Mini model | Graduated |
| F | Structured state | Hybrid cascade | Graduated |

Task and model order should be randomized where feasible. Final artifacts should receive blinded review.

## 17. Human Study Design

### 17.1 Initial Mode

Begin with shadow mode: the monitor records assessments without altering outputs. Compare its recommendations with user reactions and independent review.

### 17.2 Participants

Recruit users who conduct extended, structurally constrained work, initially researchers, analysts, technical writers, or repository maintainers. Casual chatbot users are not the primary population.

### 17.3 Within-Subject Comparison

Where feasible, have participants complete matched tasks with:

- no monitor;
- passive monitoring; and
- graduated monitoring.

Counterbalance condition order to reduce learning effects.

### 17.4 User Measures

- perceived control;
- trust calibrated to actual performance;
- usefulness of alerts;
- interruption and frustration;
- willingness to continue using the system;
- perceived protection from drift;
- freedom to explore and revise; and
- time spent maintaining or correcting state.

Behavioral measures should supplement self-report.

## 18. Statistical Analysis

The final plan should be determined after pilot data. Preliminary practices include:

- confidence intervals for all headline metrics;
- paired comparisons on matched trajectories;
- mixed-effects models accounting for task, participant, primary model, and project;
- bootstrap intervals for trajectory-level metrics where assumptions are weak;
- calibration analysis rather than accuracy alone;
- correction for multiple primary comparisons;
- sensitivity analysis for materiality weights and alert thresholds; and
- separate confirmatory and exploratory analyses.

Report effect sizes and uncertainty, not only statistical significance.

## 19. Error Analysis

Each material failure should receive a causal assignment where possible:

```text
state omission or corruption
    → retrieval miss or overload
    → candidate decomposition failure
    → comparison/classification error
    → materiality or reversibility error
    → intervention-policy error
    → user interpretation or override
```

Error analysis should also identify cases where no component could reasonably succeed because the user's governing state was genuinely underdetermined.

## 20. Decision Thresholds

Exact thresholds require pilot evidence, but the program should predefine decision logic.

### 20.1 Proceed from Annotation Pilot

Proceed only if:

- reviewers can identify governing anchors consistently;
- primary dispositions show acceptable agreement;
- material cases show stronger agreement than chance; and
- disagreements can be reduced through protocol clarification without erasing genuine ambiguity.

### 20.2 Proceed to Model Training

Proceed only if:

- structured state can be maintained at tolerable cost;
- retrieval reaches high recall for decisive anchors;
- simple baselines leave a meaningful gap; and
- enough independently labeled cases exist to support a bounded experiment.

### 20.3 Proceed to Live Intervention

Proceed only if:

- material-drift precision is high enough to justify interruption;
- critical false negatives are characterized;
- calibration supports thresholding or abstention;
- shadow-mode results show plausible net benefit; and
- privacy and state-integrity controls are adequate.

## 21. Stop, Narrow, or Redesign Criteria

The project should stop, narrow, or redesign if:

- drift cannot be distinguished reliably from legitimate development;
- maintaining authoritative state imposes excessive user burden;
- retrieval errors dominate and cannot be controlled;
- a mini model adds no value over simple state management and rules;
- false alerts materially constrain exploration;
- judge errors remain strongly correlated with primary-model errors;
- benefits occur only on synthetic perturbations; or
- end-to-end workflow performance does not improve despite offline accuracy.

A finding that structured state or periodic human review is more effective than a mini model would still be a useful research result.

## 22. Reporting Requirements

Every evaluation release should report:

- precise dataset composition and provenance;
- natural versus synthetic case proportions;
- task, model, and domain splits;
- annotation instructions and agreement;
- adjudication procedures;
- prevalence and materiality distribution;
- performance by drift type and difficulty;
- all baselines and ablations;
- calibration and selective-performance results;
- latency, computation, and human burden;
- hard-negative performance;
- state and retrieval failure rates;
- workflow outcomes; and
- known limitations and excluded populations.

Aggregate accuracy alone is insufficient.

## 23. Minimal Viable Evaluation

Before building a full benchmark, conduct a bounded feasibility study:

1. Create 12–20 short project trajectories across three research or document tasks.
2. Define 8–15 governing anchors per trajectory.
3. Produce aligned, drifted, authorized-change, and insufficient-state candidates.
4. Obtain two independent annotations and adjudicate disagreements.
5. Evaluate rules, embeddings, an existing NLI/factuality model, primary-model self-review, a large judge, and one compact evaluator.
6. Compare oracle anchors with automatic retrieval.
7. Simulate passive notice and confirmation thresholds.
8. Estimate annotation cost, state-maintenance burden, false-alert rate, and latency.
9. Make an explicit go, narrow, redesign, or stop decision.

This study should precede expensive fine-tuning.

## 24. Expected Evidence Table

| Claim to test | Required evidence | Evidence that would weaken the claim |
|---|---|---|
| Drift is a measurable construct | Independent agreement with traceable anchors | Persistent disagreement after protocol refinement |
| Explicit state improves fidelity | Better matched-trajectory performance than raw history | No gain or gains explained only by added context length |
| Authority and versioning matter | Ablation loss when metadata is removed | Equivalent performance without metadata |
| Mini model is technically useful | Better bounded-task cost/performance than simpler baselines | Rules, embeddings, or ordinary NLI perform equivalently |
| Monitoring is operationally valuable | Consequential drift prevented at acceptable burden | High interruption, delay, or constrained exploration |
| Low-friction intervention is feasible | High silent-pass rate with low critical miss rate | Useful recall requires frequent user confirmation |

## 25. Working Conclusion

The evaluation should be designed to disconfirm as well as support the proposal. Three findings are necessary before a mini-model drift monitor can be considered useful:

1. objective and design drift can be labeled with adequate reliability;
2. explicit state and specialized evaluation add measurable protection; and
3. graduated monitoring creates positive net workflow value.

Failure of any one condition should prevent a broad deployment claim. The immediate next step is not full model training, but the minimal viable evaluation: a small auditable set of longitudinal project traces, independent coding, baseline comparison, and explicit go/no-go review.
