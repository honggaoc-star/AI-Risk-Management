# Framework for Error and Hallucination in Deployed Generative AI Systems

## Overview

This initiative develops an analytical framework for identifying, classifying, and investigating errors in responses delivered by deployed generative AI systems.

A delivered response may depend not only on a trained model, but also on the current input, prior interaction history, external information, retrieval and context-construction processes, and post-generation controls. The framework therefore evaluates the response at the system level while preserving distinctions among:

- the information available to the system;
- the governing reference authoritative for a particular assertion or task requirement;
- the discrepancy observed relative to that reference;
- the production stage or stages that may have contributed to the discrepancy;
- the consequence of the discrepancy; and
- the governance response appropriate to the supported diagnosis.

The central organizing principle is **authority first**: identify what governs a claim, and what evidence is needed, before classifying a discrepancy, tracing its cause, or deciding on a governance response.

## Working Paper

**An Analytical Framework for Error and Hallucination in Deployed Generative AI Systems**

Current version: **v1.0b — Working Paper, Review Draft**

The paper distinguishes hallucination from task-obligation fidelity error. Hallucination concerns the representational content of a generated assertion relative to its governing reference. Task-obligation fidelity concerns whether the delivered response conforms to an applicable requirement. The two may occur separately or together.

The framework also addresses:

- governing-reference selection;
- assertion–reference discrepancy;
- causal attribution across potentially joint contributing stages;
- time and authorized project state;
- possible error propagation;
- retrieval-augmented generation;
- consequence assessment; and
- the relationship between diagnosis and system-level controls.

**[Read or download the v1.0b manuscript (PDF)](./Framework%20for%20Error%20and%20Hallucination%20in%20Gen-AI%20Systems%20%28v1.0b%29.pdf)**

The v1.0b manuscript is available for public comment and review. Citation information will be added as the paper develops.

## Status and Review

This is an analytical working paper, not a completed empirical validation study. The framework is being circulated for critical review and remains subject to revision.

Comments are especially welcome on:

1. whether the authority-first evaluation sequence is conceptually distinctive and useful;
2. whether the definitions of hallucination and task-obligation fidelity error are clear and defensible;
3. whether the causal-attribution formulation improves diagnosis of deployed-system errors;
4. whether the framework can be applied consistently to practical cases; and
5. where the argument or notation remains difficult to follow on a first reading.

## Relationship to the AIRM Program

This work is part of the broader [AI Risk Management research lab](../). It develops a structured method for analyzing errors in deployed generative AI systems and complements the lab's work on objective drift, context and state management, evaluation, monitoring, and governance.

## Research Boundaries

This initiative offers an analytical framework for research and evaluation. It does not certify that any AI model, system, workflow, organization, or use is safe, accurate, compliant, aligned, or fit for a particular purpose. It does not provide legal, regulatory, compliance, medical, financial, employment, security, procurement, or other professional advice.
