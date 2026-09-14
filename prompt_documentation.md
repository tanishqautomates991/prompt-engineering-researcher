# Prompt Documentation

## 1. Generated Knowledge Prompt
**Template:** Provide 3 core architectural facts, 3 primary use cases, and the underlying cost models for {{TECHNOLOGY_1}}, {{TECHNOLOGY_2}}, and {{TECHNOLOGY_3}}. Ensure these facts are verified before drafting.

## 2. ERA Baseline Draft Prompt
**Expectation:** Write an authoritative, objective technology research report comparing container orchestration platforms based on the verified facts above.
**Role:** Act as a Senior {{ROLE_TITLE}}.
**Action:** Draft a baseline comparison of {{TECHNOLOGY_1}}, {{TECHNOLOGY_2}}, and {{TECHNOLOGY_3}}.
**Constraint:** Format the draft using exactly these H2 headers: ## Introduction, ## Tech Overviews, ## Detailed Comparison, ## Final Verdict.

## 3. CoVe (Chain of Verification) Prompt

**Step 1:** Formulate exactly {{QUESTION_COUNT}} specific verification questions to fact-check the technical claims made in the draft.

**Step 2:** Answer those {{QUESTION_COUNT}} questions independently.

**Step 3:** Generate a Final Edit of the report (using the exact same H2 headers) correcting any inaccuracies identified.

## 4. Assumption Audit Prompt
**Action:** Run an Assumption Audit on the Final Edit. Identify exactly {{BIAS_COUNT}} hidden latent biases or hidden assumptions embedded in the final verdict. Label them 1, 2, and 3.
