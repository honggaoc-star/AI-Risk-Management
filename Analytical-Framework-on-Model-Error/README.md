# An Analytical Framework for Error and Hallucination in Deployed Generative AI Systems

## Working Paper

Current version: **Working Paper v1.1, July 2026**

**[Read or download the v1.1 manuscript (PDF)](./Analytical-Framework-on-Model-Error-v1.1.pdf)**

[Download the v1.1 manuscript in Word format](./Analytical-Framework-on-Model-Error-v1.1.docx)

## Abstract

Evaluation of errors in a deployed generative AI system is difficult when the system combines a trained model with designated sources, retrieved information, tools, prior interactions, and system controls. Under these conditions, an error in the response delivered to a user may not originate in the trained model. The information used to produce the response may also differ from the information that should govern its evaluation. To address these problems, this paper develops an authority-first evaluation framework. The framework first identifies the governing reference for each assessable claim and then classifies the relationship between the claim and that reference as supported, contradicted, unsupported, or unresolved. It treats hallucination and task-obligation fidelity error as related error classifications that may overlap. Hallucination concerns a representational claim that is contradicted by, or lacks support required from, its governing reference; task-obligation fidelity error concerns failure to satisfy an applicable requirement. The framework further separates identification of an error from its localization and causal attribution, and separates occurrence of the error from its consequences. Applications to temporal change, continuing-project state, retrieval-augmented generation, and error propagation illustrate why evaluation should begin with authority rather than with an assumed source of failure. This sequence may support more consistent evaluation and better-targeted controls, while keeping the cause of a response error unresolved when the available evidence does not support a firmer conclusion.


## Status and Review

This version revises v1.0b, which was previously circulated for public review. The revision clarifies the paper’s authority-first focus and its relationship to a separate working paper completed shortly after v1.0b, *Plausible Mechanisms for Hallucination in Generative AI Systems: A Production Response Framework*. [View the related working paper](../Plausible-Mechanisms-for-Hallucination-in-Generative-AI-Systems/).


## Relationship to the AIRM Program

This work is part of the broader [AI Risk Management research lab](../). It develops a structured method for analyzing errors in deployed generative AI systems and complements the lab's work on objective drift, context and state management, evaluation, monitoring, and governance.

## Research Boundaries

This initiative offers an analytical framework for research and evaluation. It does not certify that any AI model, system, workflow, organization, or use is safe, accurate, compliant, aligned, or fit for a particular purpose. It does not provide legal, regulatory, compliance, medical, financial, employment, security, procurement, or other professional advice.
