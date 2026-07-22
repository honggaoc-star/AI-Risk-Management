# AI Risk Management

AI Risk Management is a developing research program focused on practical ways to identify, evaluate, mitigate, and govern risks arising from artificial intelligence, particularly generative AI systems used in consequential or extended human–AI workflows.

The program begins from a simple premise: improving the underlying model is necessary, but model-level improvement alone may not address every risk that emerges when AI systems are used over time, within complex projects, and under evolving human objectives. Reliable AI use therefore requires attention not only to model capability, but also to system design, context management, monitoring, human judgment, and residual-risk control.

This repository will initially concentrate on one focused research stream:

> **Objective and design drift in extended human–AI collaboration, and the feasibility of a specialized, low-friction monitoring model.**

The repository does not currently attempt to provide a comprehensive treatment of all AI risks, establish compliance requirements, or claim that any single mechanism can solve AI hallucination or reliability problems.

## Initial Research Question

Extended interaction with generative AI creates a distinctive reliability problem. An AI response may remain fluent, factually plausible, and locally responsive while gradually departing from the user's original objectives, definitions, constraints, accepted decisions, or conceptual architecture.

This repository uses the following preliminary definition:

> **Objective and design drift is a material, unacknowledged divergence of AI-generated work from the user-authorized objectives, definitions, constraints, decisions, or conceptual architecture governing an extended interaction or project.**

The initial research asks:

> Can a specialized, comparatively small model monitor a primary generative model's proposed outputs against an explicit, evolving project state and detect consequential drift without materially interrupting the user's work?

## Conceptual Starting Point

The project began with a broad working definition of AI hallucination as model error. Three sources of error were identified as an initial organizing hypothesis:

1. **Representational limitation** — the model does not adequately encode or generalize the knowledge, relationships, or procedures required for a task.
2. **Generative-path instability** — autoregressive generation makes later outputs conditional on earlier generated outputs, allowing errors, recoveries, and path dependence to shape the response.
3. **Operative-context limitation** — relevant information is absent, truncated, displaced, distorted, or ineffectively used at inference time.

These factors are not presented as an exhaustive taxonomy. They organize the relationship between underlying model limitations, sequential generation, and the information available during use.

The discussion then identified a fourth requirement: **error detection and containment**. Even when an error originates in the underlying model, generative path, or operative context, a monitoring mechanism may prevent it from becoming embedded in subsequent work.

This creates a distinction between two important failure types:

- **Factual error:** the output is false, unsupported, or logically invalid.
- **Fidelity error:** the output may be individually reasonable but no longer serves the user's governing intent or established design.

The proposed monitoring model focuses primarily on the second category while remaining complementary to factuality, safety, and other AI-assurance controls.

## Proposed Monitoring Architecture

The preliminary design contains five interacting components:

1. **Primary generative model** — produces the substantive work.
2. **Governing-state manager** — maintains an explicit record of authorized objectives, definitions, assumptions, constraints, decisions, exclusions, unresolved questions, and changes.
3. **Retrieval layer** — selects the governing information relevant to the current task and proposed output.
4. **Specialized monitoring model** — compares the proposed output with the current task and governing state.
5. **Intervention policy** — determines whether the system should pass, log, quietly correct, notify, request confirmation, or—in narrowly defined circumstances—pause the action.

A simplified representation is:

```text
User request + governing state
            ↓
Primary model produces a candidate output
            ↓
Specialized monitor evaluates project fidelity
            ↓
Pass | log | revise | notify | confirm | exceptional block
```

The monitor is not intended to replace the primary model, independently solve the user's substantive problem, or certify that an output is true. Its narrower role is to identify possible divergence from an explicit, user-authorized project state.

## Complementary Role

The proposed monitor is not an alternative to improvements made by AI laboratories within foundation models. It is intended to complement advances in:

- training data and objectives;
- model architecture and representation;
- reasoning and planning;
- decoding and generative-path control;
- calibration and abstention;
- internal self-correction;
- context-window capacity and effective context use;
- retrieval, grounding, and factual verification.

Internal improvements seek to reduce the probability that errors originate. The proposed external monitoring layer seeks to reduce the probability that residual drift remains undetected and becomes embedded in the work.

## Low-Friction Design Principle

The proposed monitor must preserve the productivity, exploratory freedom, and cognitive leverage that motivate the use of AI tools.

Its governing design principle is:

> **Monitor continuously, intervene selectively, and preserve user momentum.**

Most aligned outputs and permissible developments should pass without visible interruption. Intervention should depend on the probability of drift, the materiality and reversibility of the departure, the monitor's confidence, the workflow stage, and the consequences of allowing the change to proceed.

The goal is not to prevent project evolution. It is to distinguish conscious, authorized development from silent drift.

## Intended Users

The initial audience is users and developers of long-horizon, stateful AI workflows, including:

- researchers, analysts, and writers developing complex bodies of work;
- software, engineering, policy, and professional teams;
- developers of research assistants, coding agents, document systems, and persistent AI assistants;
- organizations using AI in extended or structurally constrained workflows;
- model-risk, compliance, audit, and AI-governance functions;
- operators of multi-agent systems where errors or reinterpretations can propagate across handoffs.

Casual, isolated AI interactions are not the initial target. The monitoring value is expected to be greatest when work extends across many interactions, documents, decisions, or system components.

The first bounded use case will be **AI-assisted research and complex document development**. This setting provides explicit objectives, evolving definitions, identifiable design decisions, observable revisions, and realistic opportunities to distinguish legitimate development from drift.

## Relationship to Prior Work

This program builds on two existing projects while leaving their published versions independent and canonical.

### Practical AI Sense

[Practical AI Sense: Perspectives on AI](https://honggaoc-star.github.io/practical-ai-sense/perspectives-on-ai.html) provides the broader human-use and governance motivation. Its themes include capability expansion, active human judgment, responsible development, workflow redesign, skill evolution, institutional governance, and the difference between technical capability and successful diffusion.

This perspective informs a central requirement of the present project: a reliability control creates value only if it improves AI-assisted work without imposing review costs that defeat the purpose of using AI.

### Practical AI Evaluation

[Evidence-Centered AI Evaluation](https://honggaoc-star.github.io/practical-ai-evaluation/working-paper.html) provides the more direct institutional foundation. It argues that AI assurance should evaluate a defined system and use—not merely a model—and should consider evidence sufficiency, system boundaries, human reliance, testing, monitoring, change management, and conditional acceptance of residual risk.

The proposed drift monitor can be understood as one concrete monitoring control within that broader evidence-centered framework. It does not automatically approve or reject an AI use. It produces decision-relevant evidence about whether proposed work remains faithful to its authorized state.

Together, the projects form the following progression:

```text
Responsible and capability-enhancing AI use
                    ↓
Evidence-centered evaluation of a defined AI use
                    ↓
Specialized monitoring of objective and design fidelity
```

## Planned Repository Structure

```text
AI-Risk-Management/
├── README.md
├── PROGRAM-OVERVIEW.md
├── PRIOR-AND-RELATED-WORK.md
├── Research-Streams/
│   └── Objective-and-Design-Drift/
│       ├── README.md
│       ├── Research-Proposal.md
│       ├── Focused-Literature-Review.md
│       ├── Mini-Model-Architecture.md
│       └── Preliminary-Evaluation-Design.md
├── Research-Notes/
│   ├── Three-Layer-Framework-for-Generative-AI-Error.md
│   └── Model-Error-and-Mitigation.md  # superseded historical note
├── REFERENCES.md
├── ROADMAP.md
└── LICENSE
```

This structure is intentionally compact. Additional research streams or technical implementation folders should be added only when the work justifies them.

## Initial Evaluation Priorities

The monitoring concept should be evaluated on more than detection accuracy. A useful system must balance drift prevention against the costs it introduces.

Initial evaluation dimensions include:

- detection of objective, definition, assumption, scope, structural, decision, evidence, and task drift;
- distinction between drift and legitimate project evolution;
- precision, recall, calibration, and false-positive rates;
- interruption and unnecessary-confirmation rates;
- latency and computational cost;
- user overrides and alert fatigue;
- traceability to the specific governing anchor;
- performance across long interaction histories;
- effect on task completion, workflow speed, and exploratory freedom;
- resistance to incorrect, stale, or adversarial state information.

The relevant value proposition is therefore not simply "more drift detected." It is consequential drift prevented at an acceptable cost to the user and workflow.

## Principal Technical Challenges

The preliminary design recognizes several major hurdles:

- constructing an accurate and current governing state;
- distinguishing authoritative user decisions from tentative discussion or AI-generated proposals;
- representing superseded, rejected, and unresolved positions;
- detecting conceptual rather than merely textual divergence;
- distinguishing productive change from unauthorized drift;
- measuring materiality and reversibility;
- obtaining realistic, expert-labeled longitudinal training and evaluation data;
- enabling small models to reason effectively over retrieved long-horizon context;
- reducing correlated errors between the primary model and monitor;
- calibrating interventions to avoid false positives and alert fatigue;
- controlling latency, cost, privacy, and security risks.

The project therefore treats the mini model as one part of a larger system:

```text
State management
    + authority and version control
    + relevant retrieval
    + specialized evaluation
    + graduated intervention
```

## Current Status

The project is at the concept-development and research-proposal stage. The immediate priorities are to:

1. consolidate the initial proposal;
2. complete a focused review of adjacent literature and existing evaluator models;
3. formalize the governing-state and drift taxonomy;
4. define a preliminary model and system architecture;
5. construct representative drift and non-drift cases;
6. develop an evaluation design centered on both detection performance and workflow value;
7. determine whether a bounded prototype is justified.

No trained drift-monitoring model is currently provided by this repository.

## Working Boundaries

This repository is exploratory research. It does not provide legal, regulatory, compliance, medical, financial, employment, security, procurement, or other professional advice. It does not certify that an AI system is safe, compliant, accurate, aligned, or fit for a particular use.

The concepts, architecture, and terminology remain subject to refinement through literature review, technical development, empirical evaluation, and critical review.
