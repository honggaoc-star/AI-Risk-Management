# AI Risk Management

AI Risk Management (AIRM) is a developing research lab for studying risks arising from artificial intelligence and practical ways to identify, evaluate, mitigate, monitor, and govern them.

The lab is concerned particularly with generative AI systems used in consequential, extended, or structurally complex human–AI workflows. Its scope is not limited to any single risk category, model type, technical mechanism, or institutional setting.

The program begins from a simple premise: improving the underlying model is necessary, but model-level improvement alone may not address every risk that emerges when AI systems are used over time, within complex projects, and under evolving human objectives. Reliable AI use therefore requires attention not only to model capability, but also to system design, context management, evaluation, monitoring, human judgment, organizational processes, governance, and residual-risk control.

## Research Scope

The repository may support bounded studies of topics including:

- model and system reliability;
- objective, constraint, and design fidelity;
- AI evaluation and assurance;
- human–AI collaboration and oversight;
- context, memory, and state management;
- error detection, mitigation, and containment;
- monitoring and intervention design;
- multi-agent coordination and failure propagation;
- organizational and institutional AI risk;
- governance, accountability, and residual-risk acceptance.

This list defines a research domain rather than a commitment to pursue every topic. New studies should be added only when they have a distinct question, sufficient conceptual development, and a clear relationship to the broader AIRM program.

## Research Approach

The lab uses focused research initiatives rather than treating AI risk management as a single undifferentiated problem. Each initiative should define:

1. a bounded problem and research question;
2. the relevant system, use, and risk boundaries;
3. its relationship to adjacent literature and prior work;
4. a proposed analytical, technical, or institutional approach;
5. an evaluation strategy;
6. important limitations, tradeoffs, and residual risks.

The program favors practical, evidence-centered work. A proposed control should be evaluated not only on whether it reduces a target risk, but also on the costs, new risks, workflow effects, and governance requirements it introduces.

## Active Research Initiatives

### Objective and Drift Detection

[Objective and Drift Detection](./Objective%20and%20Drift%20Detection/) is the first research initiative in the AIRM lab.

It studies objective and design drift in extended human–AI collaboration and the feasibility of specialized, low-friction monitoring. The initiative asks whether AI-generated work can remain locally plausible while materially departing from user-authorized objectives, definitions, constraints, decisions, or conceptual architecture—and whether consequential departures can be detected without materially interrupting the user's work.

The initiative includes:

- [Research Exploration](./Objective%20and%20Drift%20Detection/Research-Exploration/), containing the proposal, focused literature review, preliminary architecture, and evaluation design;
- [Research Notes](./Objective%20and%20Drift%20Detection/Research-Notes/), containing the supporting three-layer framework for generative-AI error and the superseded exploratory note from which it developed.

Additional initiatives may be added when justified by the research.

## Relationship to Prior Work

The AIRM lab builds on two existing projects while leaving their published versions independent and canonical.

[Practical AI Sense: Perspectives on AI](https://honggaoc-star.github.io/practical-ai-sense/perspectives-on-ai.html) provides the broader human-use and governance motivation. Its themes include capability expansion, active human judgment, responsible development, workflow redesign, skill evolution, institutional governance, and the difference between technical capability and successful diffusion.

[Evidence-Centered AI Evaluation](https://honggaoc-star.github.io/practical-ai-evaluation/working-paper.html) provides the more direct institutional foundation. It argues that AI assurance should evaluate a defined system and use—not merely a model—and should consider evidence sufficiency, system boundaries, human reliance, testing, monitoring, change management, and conditional acceptance of residual risk.

Together, these projects motivate a research program concerned with the practical management of AI risk across models, systems, workflows, users, and institutions.

## Repository Structure

```text
AI-Risk-Management/
├── README.md
└── Objective and Drift Detection/
    ├── README.md
    ├── Research-Exploration/
    │   ├── README.md
    │   ├── Research-Proposal.md
    │   ├── Focused-Literature-Review.md
    │   ├── Mini-Model-Architecture.md
    │   └── Preliminary-Evaluation-Design.md
    └── Research-Notes/
        ├── README.md
        ├── Three-Layer-Framework-for-Generative-AI-Error.md
        └── Model-Error-and-Mitigation.md  # superseded historical note
```

This structure is intentionally compact. New initiative, implementation, data, or evaluation folders should be added only when the work justifies them.

## Current Status

AI Risk Management is at an early research-development stage. The current work concentrates on the first initiative, Objective and Drift Detection. The broader lab structure is intended to support future AI-risk-management studies without presuming their topics, methods, or conclusions in advance.

## Working Boundaries

This repository is exploratory research. It does not provide legal, regulatory, compliance, medical, financial, employment, security, procurement, or other professional advice. It does not certify that an AI model, system, workflow, organization, or use is safe, compliant, accurate, aligned, or fit for a particular purpose.

The concepts, architectures, terminology, and research priorities remain subject to refinement through literature review, technical development, empirical evaluation, and critical review.
