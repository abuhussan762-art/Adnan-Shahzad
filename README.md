# AI-Powered ATS-Friendly Resume & CV Builder

This repository contains the product and technical specification for an AI-powered resume/CV builder focused on ATS compliance, professional HR standards, and global hiring practices (GCC, Europe, UK, USA, and multinational companies).

## Product Goals
- Preserve factual correctness from uploaded resumes (PDF/DOCX) with no hallucinations.
- Provide JD-based tailoring that is truthful and optimized for ATS parsing.
- Export ATS-friendly PDF and editable DOCX with consistent formatting.
- Provide versioning, scoring, and guidance for continuous improvement.

## Core Modules
1. **Ingestion & Extraction**
   - PDF/DOCX parsing, section detection, entity extraction.
   - Human-in-the-loop clarification for missing/ambiguous data.
2. **Structured Resume Profile**
   - Normalized schema for summary, experience, education, skills, certifications, projects, and keywords.
3. **JD Tailoring Engine**
   - Keyword extraction, responsibility mapping, relevance scoring.
   - Rewrites summaries and reprioritizes bullets without fabricating content.
4. **ATS Rules Engine**
   - Validation for formatting rules, fonts, sections, and layout.
5. **Template System**
   - Minimal, professional templates (Corporate, Engineering, HSE, IT, Fresh Graduate).
6. **Versioning & Comparison**
   - Save original, customized versions, diffing, re-edit, and re-export.
7. **Scoring & Insights**
   - ATS match score, keyword coverage, red flags, and improvement suggestions.

## Documentation
- [Product Requirements](docs/product_requirements.md)
- [System Architecture](docs/architecture.md)
- [Data Model](docs/data_model.md)
- [AI Workflows](docs/ai_workflows.md)
- [Templates & Formatting Standards](docs/templates.md)

## Ethics & Compliance
- No fabricated experience, education, or certifications.
- User privacy and data minimization.
- All AI output must be professional, factual, and recruiter-grade.
