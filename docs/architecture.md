# System Architecture

## High-Level Components
1. **Client Application**
   - Resume editor UI, template selection, JD input, preview, and export.
2. **API Gateway**
   - Auth, rate limiting, tenant routing, audit logging.
3. **Ingestion Service**
   - PDF/DOCX parsing, layout normalization, entity extraction.
4. **Profile Service**
   - Stores structured resume profile with version history.
5. **JD Analysis Service**
   - Extracts keywords, skills, responsibilities, and ATS signals.
6. **Tailoring Service**
   - Rewrites summary and reprioritizes bullets without falsification.
7. **ATS Rules Engine**
   - Validates format rules and flags violations.
8. **Scoring & Insights Service**
   - ATS match score, keyword coverage, red flags, and suggestions.
9. **Export Service**
   - Generates DOCX and PDF with consistent formatting and ATS-friendly layout.

## Data Flow
1. User uploads resume.
2. Ingestion extracts data and produces a structured profile.
3. User edits or clarifies missing data.
4. JD analysis extracts requirements and keywords.
5. Tailoring engine aligns resume content to JD.
6. ATS rules engine validates final output.
7. Export service produces DOCX/PDF.
8. Versioning keeps original and customized snapshots.

## Security & Privacy
- Encrypt PII at rest and in transit.
- Minimize retention of raw files.
- Allow user data deletion and export.
- Audit logs for access and change history.
