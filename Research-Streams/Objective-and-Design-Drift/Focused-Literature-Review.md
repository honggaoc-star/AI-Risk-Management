# Focused Literature Review: Objective and Design Drift in Extended Human–AI Collaboration

## Status

**Version 0.1 — July 2026**

This is a focused, problem-oriented review supporting the [research proposal](Research-Proposal.md). It is not a systematic review or meta-analysis. Its purpose is to determine whether the proposed problem has already been formulated, identify the closest technical precedents, and refine the proposed contribution before architecture and evaluation design proceed.

## 1. Review Question

The review asks:

> **What existing research explains or mitigates the gradual, unacknowledged departure of an AI system from a user's authorized objectives, definitions, constraints, decisions, or project design—and what gap, if any, remains for a specialized low-friction monitor?**

The proposed phenomenon is defined as:

> **Objective and design drift is a material, unacknowledged divergence of AI-generated work from the user-authorized objectives, definitions, constraints, decisions, or conceptual architecture governing an extended interaction or project.**

This definition differs from ordinary response error in three respects. It is longitudinal, relational, and authority-sensitive. Drift is determined not only by whether a statement is true or internally consistent, but by whether a proposed output remains faithful to a versioned project state and whether a departure has been acknowledged and authorized.

## 2. Scope and Method

The review concentrates on seven adjacent literatures:

1. hallucination origins and taxonomies;
2. autoregressive error propagation and recovery;
3. long-context use, retrieval, and memory;
4. multi-turn dialogue consistency and goal persistence;
5. agent objective, constraint, and tool drift;
6. factuality evaluators, small specialist models, and LLM judges; and
7. intervention, abstention, and human oversight.

Priority was given to peer-reviewed papers in the ACL Anthology and to directly relevant recent preprints where peer-reviewed coverage remains limited. Searches combined terms including *hallucination*, *factual consistency*, *long context*, *lost in the middle*, *dialogue consistency*, *goal persistence*, *objective drift*, *constraint drift*, *memory drift*, *LLM evaluator*, *small fact checker*, and *LLM as a judge*.

The review does not attempt comprehensive coverage of AI safety, alignment, agent security, human–computer interaction, requirements engineering, or organizational change control. Those fields may become relevant in later versions.

Because several directly adjacent papers appeared in 2025–2026, the novelty assessment should be treated as time-sensitive and provisional.

## 3. Summary Finding

The proposal has **not** emerged in an empty research space. Its components are strongly anticipated by existing work:

- hallucination research distinguishes model knowledge, generation, and context-related causes;
- exposure-bias research studies how generated prefixes can propagate or permit recovery from error;
- long-context research shows that nominal capacity does not guarantee effective use;
- dialogue research examines context, persona, intent, and topic consistency;
- agent research increasingly identifies objective, constraint, memory, and tool drift across trajectories;
- factuality research demonstrates that small specialist evaluators can compete with much larger general models on bounded verification tasks; and
- LLM-as-a-judge research documents the usefulness and biases of model-based evaluation.

The closest recent work materially narrows any broad novelty claim. Terms such as *objective drift*, *constraint drift*, *context drift*, and *memory-induced tool-drift* are now used in agent and multi-turn research.

The remaining candidate contribution is more specific:

> **A user-authority-centered system for monitoring the fidelity of candidate outputs to an explicit, evolving project state, with intervention determined jointly by divergence, materiality, authorization, reversibility, and workflow cost.**

No reviewed work was found that fully combines all of those elements for extended research or complex document development. This is a preliminary gap finding, not proof of novelty.

## 4. Hallucination: Definitions and Origins

Hallucination research most often concerns generated content that is false, unsupported, or inconsistent with source material. Surveys distinguish intrinsic and extrinsic hallucination, factuality and faithfulness, and causes associated with data, training, inference, and retrieval. Dziri et al. analyze hallucination in conversational models as a product of parametric knowledge, dialogue history, and response generation. McKenna et al. show how memorized sentences and corpus-level statistical patterns can distort inference behavior. Broader surveys by Huang et al. and others organize causes and mitigation across model development and deployment.

This literature supports the three-layer organizing framework in [A Three-Layer Framework for Generative-AI Error](../../Research-Notes/Three-Layer-Framework-for-Generative-AI-Error.md): representational limitation, generative-path instability, and operative-context limitation. The categories are a project synthesis, however, and should not be presented as an established three-part taxonomy.

Hallucination literature also exposes a boundary. A response may be factually correct yet unfaithful to its source. Recent work on “harmful factuality” makes this conflict explicit: a model may alter supplied content in an attempt to correct it, producing a true but source-unfaithful output. That finding closely supports this project's distinction between factual correctness and fidelity, although source fidelity is narrower than fidelity to a governing project state.

### Implication

Objective and design drift should be positioned as a **fidelity failure**, not a replacement definition for hallucination. The broader term *model error* can connect them, but the proposed monitor should not claim to establish factual truth.

## 5. Autoregressive Generation, Propagation, and Recovery

Autoregressive models generate each token conditionally on the prompt and preceding generated tokens. This creates path dependence: an early mistaken premise or reinterpretation changes the context for later generation. Exposure-bias research has long examined the difference between training on correct prefixes and generating from model-produced prefixes at inference time.

He et al. complicate a simple snowballing account. Their experiments show that distortions do not necessarily accumulate monotonically and that models can exhibit self-recovery. The relevant mechanism is therefore not inevitable error propagation but **generative-path instability**: early commitments may amplify, conceal, redirect, or sometimes correct error.

Recent approaches intervene during generation. HALLUCANA, for example, uses internal factuality representations to detect and correct emerging factual hallucination with a “canary” lookahead. Other methods use familiarity, hidden-state probes, multiple samples, self-evaluation, or process-level verification.

### Implication

The proposed monitor need not wait until a project is complete. Candidate output can be checked before release or before it becomes accepted state. But internal hidden-state methods require access to the primary model and focus chiefly on factuality. An external project-fidelity monitor may be more portable across proprietary models, though potentially less informed about internal uncertainty.

## 6. Long Context: Capacity Is Not Competence

Longer context windows are an important but incomplete response to longitudinal drift. Liu et al.'s “Lost in the Middle” shows that model performance can vary substantially with the position of relevant information; information present in the middle of long contexts may be used less reliably than information near the beginning or end. Later work links this pattern to positional attention bias and develops calibration or segmentation methods.

Long-context workflows also create selection problems. Retrieval may omit controlling information, return stale or conflicting material, or fragment documents whose meaning depends on wider context. Recent findings indicate that decomposing long inputs can itself lose cross-section dependencies. Consequently:

\[
\text{nominal context capacity} \neq \text{effective context use}
\]

Simply placing an entire project history in the prompt does not establish which statements are authoritative, current, provisional, rejected, or superseded. Nor does it reliably make the correct subset operative at the moment of generation.

### Implication

The proposed system should maintain a structured governing state rather than treat raw conversation history as state. Retrieval quality must be evaluated as an independent component. Larger context windows may reduce omissions while increasing noise and authority ambiguity.

## 7. Dialogue Consistency, Intent, and Topic Drift

Multi-turn dialogue research addresses contextual coherence, persona consistency, intent trajectories, topic transitions, and task completion. ConsistentChat, for example, uses explicit intent trajectories and structural “skeletons” to reduce context drift in synthesized multi-turn instruction data. Topic-guiding systems model and control concept transitions, showing that conversational direction can be represented and influenced.

This work is relevant but not equivalent to the proposed problem. Topic continuity can be undesirable when a user intentionally changes topics, and topical similarity does not guarantee fidelity to objectives or decisions. Conversely, a project can drift while continuing to use the same vocabulary and topic.

Dialogue work typically treats coherence or intent as an attribute inferred from the interaction. The present proposal places greater weight on **authority**: which objective or definition did the user adopt, which alternative was rejected, and whether a change was consciously accepted.

### Implication

Intent trajectories and structural dialogue representations are useful precedents for governing-state design. Drift detection must nevertheless compare semantic and normative project roles, not only conversational similarity.

## 8. Agent Goal, Objective, Constraint, and Memory Drift

The closest conceptual neighbors appear in recent long-horizon agent research.

AgentLAB includes objective drifting, intent hijacking, memory poisoning, and other trajectory-level attacks. PushBench studies quantitative goal persistence, demonstrating that agents can make plausible local progress yet fail to persist until an externally verifiable objective is complete. ATBench evaluates safety failures across multi-step trajectories rather than only final responses.

Other recent work explicitly formulates **constraint drift** in multi-agent systems: safety-critical constraints may be weakened or lost as they pass through memory, delegation, communication, tool use, and optimization. Proposed “constraint state governance” maintains constraints as explicit execution state. Work on memory-induced tool-drift shows that stored preferences can inappropriately influence tool parameters even when the memory is irrelevant to the current task.

These developments substantially overlap with the present proposal's claims that:

- the trajectory, not only the response, is the relevant unit;
- constraints must remain operative across handoffs and memory operations;
- explicit state and external verification can outperform prompt-only persistence; and
- locally reasonable actions can produce globally incorrect behavior.

Important differences remain. Much of the adjacent work emphasizes security attacks, safety constraints, tool calls, or completion of externally measurable goals. The present proposal begins with cooperative human–AI knowledge work, where governing objectives evolve legitimately, materiality is interpretive, and the system must distinguish silent drift from authorized conceptual development.

### Implication

The project must no longer imply that “drift” itself is a new AI-risk concept. Its contribution must be defined at the level of **project-state fidelity, authority tracking, and low-friction change governance**.

## 9. Factuality Evaluators and the Feasibility of a Mini Model

The strongest evidence for technical feasibility comes from specialized factuality evaluators.

AlignScore trains a 355-million-parameter alignment function across natural-language inference, question answering, fact verification, retrieval, semantic similarity, paraphrasing, and summarization. It reports performance comparable to or better than much larger general-model metrics across diverse factual-consistency datasets.

MiniCheck provides an even closer implementation precedent. Its 770-million-parameter best model was trained on structured synthetic factual errors and reached GPT-4-level accuracy on a unified grounding benchmark at substantially lower reported cost. The system checks whether claims are supported by grounding documents, including cases requiring information synthesis across sentences.

Other work uses lightweight probes over generator hidden states, small sequence-to-sequence models, decomposed verification, or multi-step claim/evidence pipelines. PROBE finds that hallucination detection improves when decomposed into claim identification, evidence finding, evidence evaluation, and localization rather than treated as a single judge prompt.

Together, this literature supports a limited proposition:

> A comparatively small model can be competitive with a large general model when the evaluation task, evidence relationship, and training distribution are sufficiently bounded.

It does not establish that a small model can detect objective or design drift. Factual grounding normally asks whether evidence supports a claim. Project fidelity may require comparing one output with multiple heterogeneous anchors, understanding their authority and version status, and distinguishing contradiction from permissible change.

### Implication

MiniCheck and AlignScore should be treated as architectural and baseline precedents, not as existing drift monitors. A first prototype should test whether their claim–evidence alignment paradigm transfers to candidate-output–governing-state alignment.

## 10. LLM-as-a-Judge: Capability and Dependence

Large models are widely used to evaluate relevance, correctness, style, safety, and preference. They offer flexible rubric following and natural-language rationales, making them an obvious baseline and possible synthetic-data generator.

However, model judges exhibit position, style, authority, distraction, and self-preference effects. Performance can be sensitive to prompt structure, task difficulty, response presentation, and the similarity between generator and judge. A same-family evaluator may share misconceptions or preferences with the primary model. Larger reasoning models do not eliminate these biases.

### Implication

The architecture should avoid assuming that an independent API call constitutes independent judgment. Evaluation should compare:

- same-model self-review;
- same-family and different-family judges;
- a specialized compact model;
- rule and retrieval baselines; and
- human judgments under an explicit annotation protocol.

Correlated errors are an empirical question. The monitor's independence should be measured, not asserted.

## 11. Intervention, Abstention, and Human Oversight

Most adjacent technical work focuses on detection accuracy or automatic correction. The proposed system additionally treats the cost of intervention as part of reliability. A detector that produces frequent false alerts can create automation fatigue, encourage reflexive overrides, constrain exploration, and ultimately reduce safety.

Selective prediction and abstention research provides a partial foundation: a system may act only above a confidence threshold or defer uncertain cases. Human-in-the-loop designs similarly allocate review according to uncertainty or consequence. Yet drift monitoring requires more than confidence. An intervention policy should also account for materiality, reversibility, workflow stage, and whether a departure is exploratory or operative.

The proposed ladder remains:

```text
pass
  → log
  → quiet correction
  → passive notice
  → confirmation request
  → exceptional block
```

### Implication

The relevant outcome is not maximum alerts. It is consequential drift prevented at acceptable cognitive and operational cost. This appears less developed in the closest evaluator literature and is a plausible area of contribution.

## 12. Comparative Map

| Research area | Governing reference | Typical failure | Typical method | Remaining gap for this project |
|---|---|---|---|---|
| Hallucination and factuality | World knowledge or supplied evidence | False or unsupported claim | Retrieval, verification, calibration, decoding | Correctness does not establish fidelity to user-authorized design |
| Long-context research | Information in a long prompt or corpus | Omission, position bias, ineffective use | Longer windows, retrieval, calibration, segmentation | Presence and relevance do not establish authority or version status |
| Dialogue consistency | Conversation history, persona, or inferred intent | Incoherence, topic or persona inconsistency | Intent modeling, memory, dialogue-state tracking | Topic consistency is not project fidelity; user authorization is underrepresented |
| Agent safety and persistence | Goal, policy, constraint, or task completion rule | Objective loss, constraint weakening, premature completion | State tracking, verification, trajectory benchmarks | Often security- or task-oriented; less attention to legitimate evolving design |
| Factuality evaluator | Claim–evidence pair | Lack of entailment or support | NLI, alignment models, decomposed checking | Project anchors are heterogeneous, versioned, and authority-sensitive |
| LLM-as-a-judge | Rubric or preference prompt | Mis-scoring and evaluator bias | General LLM evaluation | Cost, bias, correlated errors, and weak specialization |
| Proposed drift monitor | Explicit evolving governing state | Material unacknowledged divergence | Retrieval + specialist comparison + graduated intervention | Must demonstrate labelability, incremental value, and low-friction operation |

## 13. Refined Research Gap

The literature supports neither a sweeping novelty claim nor abandonment of the project. It points toward a narrower and more defensible gap.

Existing work separately provides:

- theories and benchmarks for factual hallucination;
- evidence that context can be present but ineffectively used;
- methods for dialogue and goal continuity;
- trajectory-level formulations of objective and constraint drift;
- explicit state-tracking defenses;
- small models for bounded evidence alignment; and
- general model judges for flexible evaluation.

The proposed research asks whether these components can be adapted and integrated for a different governing relationship:

```text
candidate AI output
        ↕
explicit, versioned, user-authorized project state
        ↓
materiality-sensitive intervention
```

The candidate gap has five parts:

1. **Project-state scope:** objectives, definitions, assumptions, decisions, evidence rules, exclusions, and architecture are monitored together.
2. **Authority and versioning:** the system distinguishes adopted, provisional, rejected, superseded, and unresolved positions.
3. **Change awareness:** legitimate development is separated from silent substitution.
4. **Specialized economical evaluation:** a compact evaluator is tested against simpler and larger alternatives.
5. **Workflow-value optimization:** false alerts, interruptions, latency, and constrained exploration are treated as first-order costs.

The focused review did not identify a mature system or standard benchmark covering this complete combination. A broader systematic search could still locate closer work, particularly in requirements engineering, process compliance, change management, and human–AI interaction.

## 14. Consequences for the Research Proposal

The literature suggests five revisions or cautions for subsequent work:

1. Do not claim that objective, context, or constraint drift is newly identified.
2. Define the contribution as user-authorized project-state fidelity rather than drift detection in general.
3. Treat the monitor as one component of a state-governance system, not a standalone solution.
4. Use small factuality evaluators as feasibility precedents while acknowledging the added difficulty of authorization and legitimate change.
5. Make low-friction intervention and workflow value central evaluation targets.

The central research question remains viable, but its answer is uncertain. The most difficult components may be state construction, authority labeling, and change adjudication rather than model classification.

## 15. Architecture Requirements Derived from the Review

The companion architecture should include:

- a structured, versioned governing-state schema;
- explicit status and authority metadata;
- retrieval of only task-relevant anchors;
- comparison at both proposition and structural levels;
- multi-label drift classification;
- separate estimates of divergence, materiality, and confidence;
- traceable anchor citations;
- an “insufficient state” outcome rather than forced classification;
- protection against stale or poisoned state;
- baselines using rules, embeddings, NLI, general LLM judges, and compact evaluators; and
- a graduated intervention policy external to the classifier.

## 16. Evaluation Requirements Derived from the Review

Evaluation should include:

- longitudinal rather than isolated examples;
- natural and deliberately introduced drift;
- hard negatives representing legitimate project evolution;
- independent annotation and adjudication;
- per-type and per-materiality performance;
- calibration and abstention;
- retrieval and state-quality ablations;
- cross-model and out-of-domain tests;
- evaluator-error correlation analysis;
- interruption and false-confirmation rates; and
- end-to-end user and workflow outcomes.

## 17. Selected References

- Chen, Jiawei, et al. [“ConsistentChat: Building Skeleton-Guided Consistent Multi-Turn Dialogues for Large Language Models from Scratch.”](https://aclanthology.org/2025.emnlp-main.424/) *EMNLP*, 2025.
- Dziri, Nouha, et al. [“On the Origin of Hallucinations in Conversational Models.”](https://aclanthology.org/2022.naacl-main.387/) *NAACL*, 2022.
- He, Tianxing, et al. [“Exposure Bias versus Self-Recovery: Are Distortions Really Incremental for Autoregressive Text Generation?”](https://aclanthology.org/2021.emnlp-main.415/) *EMNLP*, 2021.
- Hsieh, Cheng-Yu, et al. [“Found in the Middle: Calibrating Positional Attention Bias Improves Long Context Utilization.”](https://aclanthology.org/2024.findings-acl.890/) *Findings of ACL*, 2024.
- Huang, Lei, et al. [“A Survey on Hallucination in Large Language Models: Principles, Taxonomy, Challenges, and Open Questions.”](https://arxiv.org/abs/2311.05232) 2023; subsequently published in *ACM Transactions on Information Systems*.
- Li, Tianyi, et al. [“HALLUCANA: Fixing LLM Hallucination with a Canary Lookahead.”](https://aclanthology.org/2025.findings-naacl.12/) *Findings of NAACL*, 2025.
- Liu, Nelson F., et al. [“Lost in the Middle: How Language Models Use Long Contexts.”](https://aclanthology.org/2024.tacl-1.9/) *Transactions of the Association for Computational Linguistics* 12, 2024, 157–173.
- McKenna, Nick, et al. [“Sources of Hallucination by Large Language Models on Inference Tasks.”](https://aclanthology.org/2023.findings-emnlp.182/) *Findings of EMNLP*, 2023.
- Tang, Liyan, Philippe Laban, and Greg Durrett. [“MiniCheck: Efficient Fact-Checking of LLMs on Grounding Documents.”](https://aclanthology.org/2024.emnlp-main.499/) *EMNLP*, 2024.
- Zha, Yuheng, et al. [“AlignScore: Evaluating Factual Consistency with a Unified Alignment Function.”](https://aclanthology.org/2023.acl-long.634/) *ACL*, 2023.
- Zhang, et al. [“PROBE: Process-Based Benchmark for Hallucination Detection.”](https://aclanthology.org/2026.findings-acl.2099/) *Findings of ACL*, 2026.

### Recent Directly Adjacent Preprints

The following recent works are included because of their direct conceptual relevance; their claims should be treated according to their publication status:

- Cai, Yuandao, et al. [“Push Your Agent: Measuring and Enforcing Quantitative Goal Persistence in Long-Horizon LLM Agents.”](https://arxiv.org/abs/2605.23574) 2026.
- Dabas, Mahavir, et al. [“Memory-Induced Tool-Drift in LLM Agents.”](https://arxiv.org/abs/2605.24941) 2026.
- Jiang, Tanqiu, et al. [“AgentLAB: Benchmarking LLM Agents against Long-Horizon Attacks.”](https://arxiv.org/abs/2602.16901) 2026.
- Li, Tianxiao, et al. [“Safe Multi-Agent Behavior Must Be Maintained, Not Merely Asserted: Constraint Drift in LLM-Based Multi-Agent Systems.”](https://arxiv.org/abs/2605.10481) 2026.

## 18. Working Conclusion

The literature supports the practical concern that extended AI systems can lose, distort, or inappropriately apply goals, constraints, context, and memory. It also supports the feasibility of small specialist evaluators for bounded evidence-comparison tasks. It does not yet establish that a compact monitor can reliably distinguish consequential project drift from authorized evolution at sufficiently low operational cost.

That unresolved question justifies the next stage: a preliminary architecture that treats the mini model as one component of explicit project-state governance and defines testable alternatives rather than presuming that model training is the answer.
