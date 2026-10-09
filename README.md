# AI Risk Management

AI Risk Management (AIRM) is a developing research lab and publication collection for studying risks arising from artificial intelligence and practical ways to identify, evaluate, mitigate, monitor, and govern them. The repository contains completed and publicly released research, active or exploratory work, and historical records retained for provenance. These statuses are not interchangeable.

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

## Research and Publication Guide

The project status descriptions below retain the October 2026 portfolio review; current-edition links reflect the approved publication update. Each project record remains authoritative for its own claims, version, evidence, and limitations.

### Completed and Publicly Released Research

- **[Return-Weighted Risk (RWR)](./Return-Weighted-Risk/)** — [Working Paper v1.2, August 2026](./Return-Weighted-Risk/Return-Weighted-Risk-for-Navigating-an-Evolving-AI-Landscape-v1.2.pdf). This is the accepted working-paper version, and the core manuscript project is closed for now. Its small-business-lending example is hypothetical; empirical validation remains future work.
- **[An Analytical Framework for Error and Hallucination in Deployed Generative AI Systems](./Analytical-Framework-on-Model-Error/)** — [v1.3, September 2026](./Analytical-Framework-on-Model-Error/An-Analytical-Framework-for-Error-and-Hallucination-in-Deployed-Generative-AI-Systems-v1.3.pdf). The paper develops the authority-first framework for evaluating delivered-response discrepancies. It is conceptual, is available for public comment and critical review, and does not claim established practical or empirical value.
- **[Plausible Mechanisms for Hallucination in Generative AI Systems](./Plausible-Mechanisms-for-Hallucination-in-Generative-AI-Systems/)** — [v1.2, October 2026](./Plausible-Mechanisms-for-Hallucination-in-Generative-AI-Systems/Plausible-Mechanisms-for-Hallucination-in-Generative-AI-Systems-v1.2.pdf). The manuscript is complete and prepared for prospective arXiv submission. Its mechanism families and propositions remain hypotheses rather than universally established causes.
- **[AI Provenance and the Evaluation of Intellectual Work](./Essays/AI-Provenance-and-the-Evaluation-of-Intellectual-Work/README.md)** — [v1.1, September 2026](./Essays/AI-Provenance-and-the-Evaluation-of-Intellectual-Work/AI-Provenance-and-the-Evaluation-of-Intellectual-Work-v1.1.pdf). Version 1.1 is the current recommended publication edition. The paper is maintained in the [Essays](./Essays/) area and is not an active research initiative by placement alone.

Each linked project record identifies one current recommended edition, provides its PDF and editable Word copy, and retains earlier editions in version history.

Repository publication makes these works publicly available; it does not imply peer review, journal acceptance, operational certification, or empirical validation. Public arXiv links will be added only after the corresponding records have been issued.

### Active or Exploratory Research

- **[Objective and Design Drift Detection](./Objective-and-Design-Drift-Detection/)** remains at the concept-development and research-proposal stage. It studies whether consequential divergence from user-authorized project state can be detected with sufficiently low workflow cost. Its [research exploration](./Objective-and-Design-Drift-Detection/Research-Exploration/) includes a proposal, focused literature review, preliminary architecture, and evaluation design. No trained drift-monitoring model is currently provided.

### Prospective or Deferred Work

Public arXiv records for the authority-first and hallucination-mechanisms manuscripts remain prospective; the repository PDFs above are the current public copies. Empirical evaluation of RWR and any decision to build a bounded objective-and-design-drift prototype also remain future work rather than current release claims.

### Archived and Superseded Materials

These materials remain accessible for provenance and continuity; they are not the current versions of the work they precede.

- [Analytical Framework August 2026 manuscript](./Analytical-Framework-on-Model-Error/An-Analytical-Framework-for-Error-and-Hallucination-in-Deployed-Generative-AI-Systems.pdf);
- [Plausible Mechanisms August 2026 manuscript](./Plausible-Mechanisms-for-Hallucination-in-Generative-AI-Systems/Plausible-Mechanisms-for-Hallucination-in-Generative-AI-Systems.pdf);
- [Return-Weighted Risk v1.1, August 2026](./Return-Weighted-Risk/Return-Weighted-Risk-for-Navigating-an-Evolving-AI-Landscape.pdf), retained under its unversioned filename;
- AI Provenance v1.0, September 2026: [PDF](./Essays/AI-Provenance-and-the-Evaluation-of-Intellectual-Work/AI-Provenance-and-the-Evaluation-of-Intellectual-Work-v1.0.pdf) and [Word](./Essays/AI-Provenance-and-the-Evaluation-of-Intellectual-Work/AI-Provenance-and-the-Evaluation-of-Intellectual-Work-v1.0.docx);
- [Analytical Framework working paper v1.1, July 2026](./Analytical-Framework-on-Model-Error/Analytical-Framework-on-Model-Error-v1.1.pdf);
- [legacy analytical-framework v1.0b folder](./Framework%20for%20Error%20Analysis/), retained temporarily;
- [Hallucination Mechanisms working paper v1.0](./Plausible-Mechanisms-for-Hallucination-in-Generative-AI-Systems/Hallucination-Mechanisms-Working-Paper-v1.0.pdf); and
- [Model Error and Mitigation](./Objective-and-Design-Drift-Detection/Research-Notes/Model-Error-and-Mitigation.md), a superseded exploratory note retained in the objective-and-design-drift research record.

## Relationship to Prior Work

The AIRM lab builds on two existing projects while leaving their published versions independent and canonical.

[Practical AI Sense: Perspectives on AI](https://honggaoc-star.github.io/practical-ai-sense/perspectives-on-ai.html) provides the broader human-use and governance motivation. Its themes include capability expansion, active human judgment, responsible development, workflow redesign, skill evolution, institutional governance, and the difference between technical capability and successful diffusion.

[Evidence-Centered AI Evaluation](https://honggaoc-star.github.io/practical-ai-evaluation/working-paper.html) provides the more direct institutional foundation. It argues that AI assurance should evaluate a defined system and use—not merely a model—and should consider evidence sufficiency, system boundaries, human reliance, testing, monitoring, change management, and conditional acceptance of residual risk.

Together, these projects motivate a research program concerned with the practical management of AI risk across models, systems, workflows, users, and institutions.

## Related Practical Work

The following work addresses adjacent practical questions but remains independent of the research in this repository. These links are navigational: the projects do not share release claims, validation, or operating responsibilities, and no project below validates an AIRM paper or is validated by one.

- **[Practical AI Management (PAIM)](https://github.com/honggaoc-star/PAIM)** is a practitioner-oriented management system for bounded organizational uses of AI. [PAIM v0.1.0](https://github.com/honggaoc-star/PAIM/releases/tag/v0.1.0) is released under its own bounded validated claim as a local governed CLI and typed Python gateway. That validation does not establish real-world organizational effectiveness or authorize consequential production reliance.
- **AI Value Management (AIVM)** is identified in [PAIM's method boundary](https://github.com/honggaoc-star/PAIM#method-before-software) as an upstream analytical capability that can provide PAIM's Value leg. Risk remains a separate analytical leg, and PAIM remains responsible for its own management integration and decision record. The October 2026 public portfolio baseline does not identify a separate AIVM public release, so none is implied here.
- **[PAE Workbench](https://honggaoc-star.github.io/practical-ai-evaluation/)** is the interactive public preview associated with [Practical AI Evaluation](https://github.com/honggaoc-star/practical-ai-evaluation). It is an educational prototype for assembling draft review evidence, not approval, certification, validation, proof of safety, a compliance conclusion, or professional advice.

## Repository Structure

```text
AI-Risk-Management/
├── README.md
├── Essays/
│   ├── README.md
│   └── AI-Provenance-and-the-Evaluation-of-Intellectual-Work/
│       ├── README.md
│       ├── AI-Provenance-and-the-Evaluation-of-Intellectual-Work-v1.1.pdf   # current recommended edition
│       ├── AI-Provenance-and-the-Evaluation-of-Intellectual-Work-v1.1.docx
│       ├── AI-Provenance-and-the-Evaluation-of-Intellectual-Work-v1.0.pdf
│       └── AI-Provenance-and-the-Evaluation-of-Intellectual-Work-v1.0.docx
├── Return-Weighted-Risk/
│   ├── README.md
│   ├── Return-Weighted-Risk-for-Navigating-an-Evolving-AI-Landscape-v1.2.pdf   # current recommended edition
│   ├── Return-Weighted-Risk-for-Navigating-an-Evolving-AI-Landscape-v1.2.docx
│   └── Return-Weighted-Risk-for-Navigating-an-Evolving-AI-Landscape.pdf
├── Objective-and-Design-Drift-Detection/
│   ├── README.md
│   ├── Research-Exploration/
│   │   ├── README.md
│   │   ├── Research-Proposal.md
│   │   ├── Focused-Literature-Review.md
│   │   ├── Mini-Model-Architecture.md
│   │   └── Preliminary-Evaluation-Design.md
│   └── Research-Notes/
│       ├── README.md
│       ├── Three-Layer-Framework-for-Generative-AI-Error.md
│       └── Model-Error-and-Mitigation.md  # superseded historical note
├── Analytical-Framework-on-Model-Error/
│   ├── README.md
│   ├── An-Analytical-Framework-for-Error-and-Hallucination-in-Deployed-Generative-AI-Systems-v1.3.pdf   # current recommended edition
│   ├── An-Analytical-Framework-for-Error-and-Hallucination-in-Deployed-Generative-AI-Systems-v1.3.docx
│   ├── An-Analytical-Framework-for-Error-and-Hallucination-in-Deployed-Generative-AI-Systems.pdf
│   └── Analytical-Framework-on-Model-Error-v1.1.pdf   # archived working paper
├── Framework for Error Analysis/  # legacy v1.0b folder retained temporarily
│   ├── README.md
│   └── Framework for Error and Hallucination in Gen-AI Systems (v1.0b).pdf
└── Plausible-Mechanisms-for-Hallucination-in-Generative-AI-Systems/
    ├── README.md
    ├── Plausible-Mechanisms-for-Hallucination-in-Generative-AI-Systems-v1.2.pdf   # current recommended edition
    ├── Plausible-Mechanisms-for-Hallucination-in-Generative-AI-Systems-v1.2.docx
    ├── Plausible-Mechanisms-for-Hallucination-in-Generative-AI-Systems.pdf
    └── Hallucination-Mechanisms-Working-Paper-v1.0.pdf   # archived working paper
```

This structure is intentionally compact. New initiative, implementation, data, or evaluation folders should be added only when the work justifies them.

## Current Status

The October 2026 publication update identifies four current recommended research papers: Return-Weighted Risk v1.2 (August 2026), the authority-first model-error framework v1.3 (September 2026), the hallucination-mechanisms manuscript v1.2 (October 2026), and the AI provenance paper v1.1 (September 2026). Objective and Design Drift Detection remains active exploratory research. Earlier working papers and the superseded model-error note remain available as historical records.

These works address related questions but do not constitute a unified theory, and their conclusions do not transfer automatically from one project to another. Unless an individual project record states otherwise, the work is conceptual or exploratory and should not be read as empirical validation of a method, control, application, or organizational practice.

## Working Boundaries

This repository is exploratory research. It does not provide legal, regulatory, compliance, medical, financial, employment, security, procurement, or other professional advice. It does not certify that an AI model, system, workflow, organization, or use is safe, compliant, accurate, aligned, or fit for a particular purpose.

The concepts, architectures, terminology, and research priorities remain subject to refinement through literature review, technical development, empirical evaluation, and critical review.
