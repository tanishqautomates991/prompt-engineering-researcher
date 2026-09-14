# Prompt Documentation

This document records the exact parameterized prompt templates utilized throughout the research lifecycle, establishing an audit trail from initial knowledge grounding through ERA baseline drafting, 4-step Chain of Verification (CoVe), and final assumption auditing under an explicit **September 2026** knowledge and data currency boundary.

---

## 1. Generated Knowledge Prompt

**Objective:** Ground the downstream generation process in verified technical specifications prior to drafting, mitigating baseline hallucination under an explicit data currency boundary.

**Template:**
```text
Act as a Principal Infrastructure Researcher. Before drafting any comparison or narrative, generate a comprehensive, structured technical background fact sheet for {{TECHNOLOGY_1}}, {{TECHNOLOGY_2}}, and {{TECHNOLOGY_3}}.

[KNOWLEDGE BOUNDARY ENFORCEMENT]
All architectural limits, cloud service pricing tiers (AWS, GCP, Azure), API support matrices, software lifecycle statuses, and industry survey statistics must strictly reflect the verified state as of {{KNOWLEDGE_BOUNDARY}}.

For each technology, extract and systematically compile:
1. Core Architecture: Underlying control plane components, node topology, clustering protocols, and consensus mechanisms.
2. Scalability Limits & Autoscaling Mechanics: Official upstream node maximums, concurrent pod/task limits, hyperscale thresholds, and autoscaling layers (node-level vs. container task-level autoscaling, including launch latency).
3. Setup Complexity: Bootstrapping workflows, configuration prerequisites (networking, storage, PKI, RBAC), and operational tooling.
4. Cost Structures: Master node / control plane licensing, managed service fees, compute billing increments, and storage overhead.
5. Raw Specifications & Documentation Facts: Key configuration directives, supported container runtimes, privilege boundaries, and isolation models.
6. Industry Statistics & Governance: Adoption survey metrics (explicitly identifying surveyed practitioner cohorts, e.g., CNCF annual survey respondents), active maintenance status, vendor governance, and production deployment trends.

Output raw specifications and objective technical documentation facts only. Do not provide narrative commentary or qualitative recommendations at this stage.
```

**Parameters:**
- `{{TECHNOLOGY_1}}`: Kubernetes
- `{{TECHNOLOGY_2}}`: Docker Swarm
- `{{TECHNOLOGY_3}}`: AWS Fargate
- `{{KNOWLEDGE_BOUNDARY}}`: September 2026

---

## 2. ERA Baseline Draft Prompt

**Objective:** Produce an initial baseline research report utilizing the Expectation-Role-Action (ERA) prompting framework, strictly operating upon the generated background fact sheet under the verified knowledge boundary.

**Template:**
```text
[EXPECTATION]
Write an authoritative, objective technology research report comparing container orchestration platforms. All technical claims, figures, and architectural details must be derived strictly from the provided background fact sheet, reflecting the {{KNOWLEDGE_BOUNDARY}} knowledge cutoff. Format the draft using exactly these H2 headers:
## Introduction
## Tech Overviews
## Detailed Comparison
## Final Verdict

[ROLE]
Act as a Senior {{ROLE_TITLE}} with expertise in cloud architecture, distributed systems, and container orchestration platforms.

[ACTION]
Using the verified background facts supplied in {{BACKGROUND_FACT_SHEET}}, draft a baseline comparative analysis of {{TECHNOLOGY_1}}, {{TECHNOLOGY_2}}, and {{TECHNOLOGY_3}}. Analyze each system across scalability, operational overhead, setup complexity, and total cost of ownership. Conclude with a decisive final verdict summarizing ideal adoption scenarios.
```

**Parameters:**
- `{{ROLE_TITLE}}`: Cloud Solutions Architect
- `{{BACKGROUND_FACT_SHEET}}`: [Inserted Generated Knowledge Background Fact Sheet]
- `{{TECHNOLOGY_1}}`: Kubernetes
- `{{TECHNOLOGY_2}}`: Docker Swarm
- `{{TECHNOLOGY_3}}`: AWS Fargate
- `{{KNOWLEDGE_BOUNDARY}}`: September 2026

---

## 3. Chain of Verification (CoVe) Prompts

The Chain of Verification workflow executes as three distinct prompts following the generation of the baseline draft, completing the full 4-step CoVe cycle (Draft -> Question Formulation -> Independent Verification -> Corrected Report).

### 3.1. CoVe Step 1: Verification Question Formulation Prompt
**Objective:** Identify falsifiable technical assertions, pricing assumptions, and boundary conditions in the baseline draft.

**Template:**
```text
Review the baseline research draft below:
"""
{{BASELINE_DRAFT}}
"""

Formulate exactly {{QUESTION_COUNT}} targeted, falsifiable verification questions designed to fact-check technical claims, cloud pricing models, operational constraints, and lifecycle maintenance statuses cited in the draft. Focus specifically on claims where general assumptions might diverge from official vendor documentation as of {{KNOWLEDGE_BOUNDARY}}.
```

**Parameters:**
- `{{BASELINE_DRAFT}}`: [Baseline Research Report Output]
- `{{QUESTION_COUNT}}`: 4
- `{{KNOWLEDGE_BOUNDARY}}`: September 2026

---

### 3.2. CoVe Step 2: Independent Question Answering Prompt
**Objective:** Answer each verification question independently against verified developer documentation, isolated from the baseline draft to prevent confirmation bias.

**Template:**
```text
Independently answer the following {{QUESTION_COUNT}} verification questions based on official documentation current as of {{KNOWLEDGE_BOUNDARY}}:
{{VERIFICATION_QUESTIONS}}

Requirements for each answer:
1. Cite the exact official developer documentation basis or vendor specifications (e.g., AWS Documentation, Kubernetes Upstream Docs, Mirantis Lifecycle Announcements, Moby Swarmkit Repository Release Logs, Docker Engineering Whitepapers).
2. State the precise verified technical facts, including numbers, billing increments, feature limitations, or vendor maintenance status.
3. For Docker Swarm claims, cite specific product lifecycle releases, Swarmkit repository maintenance records, or official scale benchmarks.
4. Do not consult or refer to the baseline draft text while generating these answers.
```

**Parameters:**
- `{{QUESTION_COUNT}}`: 4
- `{{VERIFICATION_QUESTIONS}}`: [List of 4 formulated questions from Step 1]
- `{{KNOWLEDGE_BOUNDARY}}`: September 2026

---

### 3.3. CoVe Step 3: Report Correction & Final Edit Prompt
**Objective:** Cross-examine the baseline draft against verified answers, generate an explicit correction mapping, and produce the final corrected report.

**Template:**
```text
Perform a rigorous cross-examination between the Baseline Draft and the Verified Answers:

Baseline Draft:
"""
{{BASELINE_DRAFT}}
"""

Verified Answers:
"""
{{VERIFIED_ANSWERS}}
"""

Execution Instructions:
1. Generate an explicit Correction Mapping table following the format:
   Question -> Verified Answer -> Corrected Statement
2. Produce the Final Edit of the research report, replacing all unverified assumptions, unqualified survey statistics, or imprecise autoscaling descriptions with verified documentation statements as of {{KNOWLEDGE_BOUNDARY}}.
3. Preserve the exact mandatory H2 headers:
   ## Introduction
   ## Tech Overviews
   ## Detailed Comparison
   ## Final Verdict
```

**Parameters:**
- `{{BASELINE_DRAFT}}`: [Baseline Research Report Output]
- `{{VERIFIED_ANSWERS}}`: [Documentation-grounded answers from Step 2]
- `{{KNOWLEDGE_BOUNDARY}}`: September 2026

---

## 4. Assumption Audit Prompt

**Objective:** Uncover latent biases, implicit operating environments, or unstated prerequisite assumptions in the final recommendation.

**Template:**
```text
Analyze the Final Verdict and architectural recommendations of the corrected report:
"""
{{FINAL_EDIT_TEXT}}
"""

Identify exactly {{BIAS_COUNT}} hidden latent biases or implicit operational assumptions embedded within the technology verdict (e.g., regarding cloud environments, capital scale, engineering team talent, or practitioner survey sampling biases as of {{KNOWLEDGE_BOUNDARY}}). For each item, state the assumption clearly, explain why it represents a potential failure mode, and label them 1, 2, and 3.
```

**Parameters:**
- `{{FINAL_EDIT_TEXT}}`: [Final Corrected Research Report Output]
- `{{BIAS_COUNT}}`: 3
- `{{KNOWLEDGE_BOUNDARY}}`: September 2026