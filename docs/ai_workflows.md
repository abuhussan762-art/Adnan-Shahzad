# AI Workflows

## Resume Ingestion Workflow
1. Extract sections and entities from PDF/DOCX.
2. Normalize dates, roles, and company names.
3. Flag missing or ambiguous fields (e.g., missing dates, company location).
4. Generate clarification prompts only for missing/ambiguous data.

## JD Tailoring Workflow
1. Parse job description for required skills, responsibilities, and keywords.
2. Rank resume bullets by relevance to JD requirements.
3. Rewrite summary to align with JD using truthful content only.
4. Reorder work experience bullets without adding new facts.
5. Inject keywords naturally where appropriate.
6. Validate ATS rules and formatting constraints.

## ATS Scoring Workflow
- Compute match score based on:
  - Keyword coverage
  - Skill overlap
  - Responsibility alignment
  - Recentness and relevance of experience
- Provide red flags and suggestions.

## Red Flag Detection
- Employment gaps beyond configured threshold.
- Weak bullet points (no action verb or impact).
- Overused words (e.g., "responsible for", "hard-working").
- Inconsistent dates or missing locations.

## Ethical Guardrails
- Block any output that implies falsified experience or credentials.
- Provide a warning when the JD requests skills not present in user data.
- Require user confirmation for any significant rewording of claims.
