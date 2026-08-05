# An Analytical Framework for Error and Hallucination in Deployed Generative AI Systems

## Current Manuscript

Current version: **August 2026**

**[Read or download the current PDF](./An-Analytical-Framework-for-Error-and-Hallucination-in-Deployed-Generative-AI-Systems.pdf?raw=1)**

## Archived Working-Paper Version

Previously circulated version: **Working Paper v1.1, July 2026**

[Read or download the archived PDF](./Analytical-Framework-on-Model-Error-v1.1.pdf?raw=1)

## Abstract

Evaluation of errors in a deployed generative AI system presents two related problems. First, the information used to produce a response may differ from the information that should govern its evaluation. Second, identifying an error does not establish how the configured system produced it. This paper develops an authority-first framework that addresses these problems in sequence. For each assessable assertion, the framework identifies the governing reference and classifies the assertion as supported, contradicted, unsupported, or unresolved. In parallel, it compares the delivered response with applicable task obligations. These two evaluative branches support two related error classifications: hallucination, which concerns a representational claim contradicted by or lacking support required from its governing reference, and task-obligation fidelity error, which concerns failure to satisfy an applicable requirement. The framework then separates error classification from localization and causal attribution, and error occurrence from consequence. Applications to temporal change, continuing-project state, retrieval-augmented generation, and propagation show why evaluation and control selection should concern a configured system performing a specified task rather than a model name alone. The framework is conceptual, and its practical and empirical value remains to be tested.

## Status and Review

The current manuscript revises v1.0b, which was previously circulated for public review. The revision clarifies the paper's authority-first focus and its relationship to a separate working paper completed shortly after v1.0b, *Plausible Mechanisms for Hallucination in Generative AI Systems: A Response-Production Framework*. [View the related project and current manuscript](../Plausible-Mechanisms-for-Hallucination-in-Generative-AI-Systems/).

An arXiv link will be added after a public arXiv record has been issued.

## Relationship to the AIRM Program

This work is part of the broader [AI Risk Management research lab](../). It develops a structured method for analyzing errors in deployed generative AI systems and complements the lab's work on objective drift, context and state management, evaluation, monitoring, and governance.

## Research Boundaries

This initiative offers an analytical framework for research and evaluation. It does not certify that any AI model, system, workflow, organization, or use is safe, accurate, compliant, aligned, or fit for a particular purpose. It does not provide legal, regulatory, compliance, medical, financial, employment, security, procurement, or other professional advice.
