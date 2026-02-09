# Data Model

## ResumeProfile
- id
- user_id
- original_file_id
- created_at
- updated_at

### PersonalInfo
- full_name
- title
- email
- phone
- location
- linkedin_url
- portfolio_url

### ProfessionalSummary
- summary_text
- summary_version

### WorkExperience[]
- role
- company
- location
- start_date
- end_date
- is_current
- achievements[]

### Skills
- technical[]
- soft[]
- tools[]
- software[]
- keywords_bank[]

### Education[]
- degree
- institution
- location
- start_date
- end_date
- grade_or_gpa (optional)

### Certifications[]
- name
- issuer
- issued_date
- expiration_date (optional)
- credential_id (optional)

### Projects[] (optional)
- name
- role
- description
- technologies[]
- outcomes[]

## JobDescriptionAnalysis
- id
- resume_profile_id
- job_title
- company
- location
- required_skills[]
- preferred_skills[]
- responsibilities[]
- keywords[]
- ats_signals[]
- created_at

## ResumeVersion
- id
- resume_profile_id
- job_description_id (optional)
- version_label
- summary_text
- work_experience[] (ordered)
- skills_snapshot
- education_snapshot
- certifications_snapshot
- created_at

## Insights
- resume_version_id
- ats_score
- keyword_match_percent
- red_flags[]
- suggestions[]
