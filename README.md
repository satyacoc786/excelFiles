# ACEDIYTIX
## AI-Powered Smart Campus Analytics, Student Success, Machine Learning and RAG Platform

### MASTER DEVELOPMENT PROMPT — PYTHON-BASED FULL-STACK APPLICATION

## 1. Your Role

Act as a senior Python full-stack developer, AI/ML engineer, RAG architect, database designer, UI/UX designer, cybersecurity engineer, and software tester.

Build **Acediytix**, a complete, integrated, professional, responsive, colorful, easy-to-understand Smart Campus Analytics and Student Success Platform.

Do not merely generate a prototype, static dashboard, or collection of disconnected pages. Build an integrated application with real database operations, secure authentication, role-based permissions, Excel import/export, AI-assisted features, evaluated machine-learning models, a RAG knowledge assistant, optional face recognition, automated tests, and deployment documentation.

Implement the application incrementally while preserving every requirement in this specification.

If a requirement cannot be completed in the current development environment, explain the limitation, implement the available portion, and document what remains. Never claim that an unimplemented feature is complete.

---

# 2. Required Programming Languages and Architecture

Use Python throughout the application's primary development stack.

### Frontend

Use:
- Python.
- Streamlit for the primary interactive frontend.
- Streamlit multipage navigation.
- Streamlit forms, session state, data tables, interactive filters, file uploaders, and charts.
- Plotly for interactive charts and visual analytics.
- Custom CSS for the branded design system.
- Reusable Python UI components and shared layout functions.

If a requirement cannot be implemented adequately in Streamlit, use a small, documented JavaScript component only where necessary. Do not introduce a separate React application unless explicitly approved.

### Backend

Use:
- Python.
- FastAPI.
- Pydantic for request and response validation.
- REST APIs.
- Service-oriented modules with clearly separated responsibilities.
- Centralized exception handling.
- Structured logging.
- Rate limiting.
- Secure session or token-based authentication.

Keep the UI layer, API layer, business logic, data access, AI services, and ML pipelines separate.

The Streamlit frontend must call backend service functions or authenticated FastAPI endpoints. It must not bypass authorization or directly perform unrestricted database queries.

### Database

Use:
- MongoDB.
- PyMongo or Motor if its compatibility with the selected Python version is verified.
- Proper schemas and Pydantic validation.
- Indexes, references, timestamps, and uniqueness constraints where appropriate.
- Environment-based configuration.
- MongoDB transactions only where supported and justified.

Choose a compatible Python version and pin tested dependencies. Do not automatically use the newest Python version if a required AI or ML library does not support it.

### AI, Machine Learning, and RAG

Use:
- pandas and NumPy.
- scikit-learn.
- XGBoost or another suitable model when justified by evaluation.
- FastAPI for serving ML and AI services.
- Sentence Transformers or another suitable embedding model.
- A vector database or vector-search capability.
- A RAG orchestration library such as LangChain or LlamaIndex only when it materially helps.
- An LLM provider adapter supporting a configured hosted model or compatible local model.
- Document parsers for PDF, DOCX, TXT, CSV, and supported Excel files.
- OpenCV and a compatible pretrained face-recognition model for optional face authentication.

Do not make the application dependent on a paid AI service without providing configuration, cost information, and a graceful alternative.

Use a provider-independent interface for LLMs and embeddings so the implementation can switch between compatible providers.

---

# 3. Project Identity and Visual Design

Official application name: **Acediytix**.

Subtitle: **Smart Campus Analytics — Predict, Optimize & Improve Student Success**.

Create a professional academic technology brand with a recognizable text-based logo.

### Colorful, Easy-to-Understand Interface

Do not use an entirely plain white interface. Use a colorful, clean, professional design that remains readable and accessible.

Suggested palette:
- Primary: deep blue.
- Secondary: violet.
- Accent: cyan.
- Success: teal or green.
- Warning: amber.
- High-priority warning: restrained red.
- Main background: very light grey or soft white.
- Cards: white with subtle borders and shadows.
- Main text: dark navy or charcoal.

Use color consistently. Never rely on color alone to communicate a status.

### User Experience

Implement:
- A clear sidebar.
- Role-specific navigation.
- Dashboard cards.
- Interactive Plotly charts.
- Searchable and sortable tables.
- Filters by branch, academic year, semester, subject, and date.
- Helpful tooltips.
- Form validation.
- Success and error messages.
- Loading indicators.
- Empty states.
- Confirmation dialogs for important actions.
- Responsive layouts.
- Accessible labels and keyboard navigation.
- Consistent date, percentage, grade, and mark formatting.

Use restrained animations only where they improve usability.

Make the platform understandable to students, teachers, administrators, and people without a technical background.

---

# 4. User Roles and Secure Authentication

Implement three roles:
1. Student.
2. Staff.
3. Administrator.

### Student Login

Support:
- Roll Number.
- Password.
- Show/hide password.
- Password change.
- Secure password recovery.
- Optional face login.

### Staff Login

Support:
- Staff ID as defined by the supplied staff workbook.
- Password.
- Password change.
- Secure password recovery.
- Optional face login.

### Administrator

Provide a protected administrative account-management workflow. Students and ordinary staff must never be able to grant themselves administrator privileges.

### Initial Password Workflow

Allow an authorized administrator to configure a shared temporary password for newly imported student accounts.

Requirements:
- Hash passwords using Argon2id or appropriately configured bcrypt.
- Never store plaintext passwords.
- Require a password change on first login.
- Give every student an independent password after the initial change.
- Never allow one student's password change to affect another student's account.
- Implement secure password-reset and account-recovery workflows.

### Authentication Security

Implement:
- Secure session management.
- HTTP-only cookies or another suitable session architecture.
- CSRF protection where applicable.
- Login rate limiting.
- Session expiration.
- Account suspension.
- Logout.
- Server-side role and branch authorization.
- Audit logging for sensitive operations.

The Streamlit interface must not be treated as the security boundary. Every protected FastAPI endpoint and service operation must verify authorization.

---

# 5. Optional Face-Recognition Authentication

Support conventional ID/password authentication and optional face recognition.

Face recognition must use a real pretrained face-detection and embedding pipeline.

### Enrollment

1. The user verifies their account with their ID and password.
2. The system presents an informed consent notice.
3. The user explicitly agrees to biometric processing.
4. The application requests camera permission.
5. A suitable image is processed by the face-recognition service.
6. The service extracts a face representation.
7. The backend securely associates the representation with the verified account.
8. The application confirms enrollment.

### Face Login

1. The user selects Student or Staff.
2. The user identifies the claimed account.
3. The application obtains a camera frame with permission.
4. The backend validates the request.
5. The face service detects the face and compares its representation with the enrolled representation.
6. Match confidence, image quality, and supported liveness checks are evaluated.
7. The backend creates the normal authenticated session only if all required checks pass.

### Privacy and Security

Implement:
- Explicit informed consent.
- Optional enrollment.
- Encryption and restricted access to biometric representations.
- Secure deletion and revocation.
- No public biometric URLs.
- No biometric representations in browser local storage.
- Rate limiting and replay-attack mitigation.
- A normal password fallback.
- Documented limitations of liveness detection.

Do not claim that ordinary face matching alone provides high-assurance authentication.

If reliable liveness detection cannot be implemented in the current environment, clearly label the feature as a limited prototype and keep conventional authentication fully functional.

---

# 6. Excel Import and Existing College Data

The supplied student, staff, and academic-calendar workbooks are the primary source of institutional records.

Before designing final schemas, inspect:
- Workbook filenames.
- Sheet names.
- Column headings.
- Data types.
- Missing values.
- Duplicate identifiers.
- Branch labels.
- Academic-year and semester formats.
- Existing marks and attendance columns.

Do not invent actual student or staff records.

### Supported Inputs

Where compatible with the selected parser, support:
- XLSX.
- CSV.
- PDF.
- DOCX.
- TXT.

Excel files must be handled using suitable Python libraries such as pandas, openpyxl, and python-calamine where appropriate.

### Import Workflow

1. Upload the workbook.
2. Inspect sheets and columns.
3. Map source columns to application fields.
4. Preview records.
5. Validate required fields.
6. Detect duplicates and conflicts.
7. Display row-level errors.
8. Allow the administrator to download an error report.
9. Perform a dry run.
10. Import valid records into MongoDB.
11. Report inserted, updated, skipped, and failed records.

Preserve original Roll Numbers and Staff IDs.

Never merge records merely because their names are similar.

Do not overwrite existing information silently when a source column is missing.

Use staged imports or batching for large files.

Keep a backup of original workbooks. Use anonymized samples when sending data to an external AI provider.

---

# 7. Student Profiles and Academic Dashboard

Build a real student dashboard containing:
- Profile picture.
- Roll Number.
- Name.
- Branch.
- Year of study.
- Semester.
- Section.
- Authorized contact information.
- Overall attendance.
- Academic performance.
- MID-1 and MID-2 marks.
- Internal and external examination results.
- Semester results.
- Student Success Score.
- Available SGPA/CGPA.
- Upcoming academic events.
- Assignment and LMS summaries when data exists.
- Relevant skills and placement readiness information.
- Personalized recommendations.

Students can edit only approved profile fields.

Profile-picture uploads must validate file type, file size, authorization, and storage location.

Students may view only their own academic records.

---

# 8. Attendance Management

Implement:
- Daily attendance entry.
- Subject-wise attendance.
- Attendance sessions.
- Present and absent statuses.
- Institution-approved additional statuses.
- Attendance history.
- Attendance corrections with audit trails.
- Duplicate-session prevention.
- Attendance summaries.
- Low-attendance alerts.

Authorized staff must select a branch, year, semester, section, subject, and date.

The backend must verify that the staff member is authorized for the selected students.

For a simple present/absent scheme:

Attendance Percentage = Classes Attended / Total Classes Held × 100.

Apply the institution's actual rules for leave, exemptions, and cancelled classes.

Persist changes in MongoDB and refresh relevant summaries and analytics.

---

# 9. Marks and Examination Management

Support:
- MID-1.
- MID-2.
- Internal assessments.
- External examinations.
- Semester examinations.
- Subject-wise results.
- Grades.
- Academic percentages.
- SGPA and CGPA where grading rules are supplied.

MID-1 and MID-2 each support a maximum of 15 marks for the supplied dataset unless the institution configures a different scheme.

Do not assume the maximum marks for other examinations.

Validate marks against configured limits.

Normalize marks before combining assessments with different maximum values.

Recalculate affected academic summaries after authorized changes.

Represent missing marks as Not Available rather than zero.

Maintain an audit trail of changes to official results.

---

# 10. Academic Calendar

Import the existing calendar and provide:
- Monthly view.
- Weekly view.
- Agenda view.
- Academic-year filters.
- Semester filters.
- Branch and year filters.
- Examinations.
- Midterm dates.
- Holidays.
- Workshops.
- Seminars.
- Hackathons.
- Placement activities.
- Assignment deadlines where supplied.

Only authorized staff and administrators can modify official calendar events.

Never invent actual examination dates or holidays.

---

# 11. Student-to-Staff Feedback

Create a complete staff-feedback module.

Students may submit:
- Staff member.
- Subject where applicable.
- Feedback category.
- Rating from 1 to 5.
- Written feedback.
- Improvement suggestions.
- Privacy mode.

Suggested categories:
- Teaching clarity.
- Subject knowledge.
- Doubt clarification.
- Classroom engagement.
- Timeliness.
- Assignment guidance.
- Overall teaching experience.

Support identified and confidential feedback modes.

Explain the privacy rules before submission.

Ordinary staff accounts must not see confidential feedback identities.

Staff dashboards may display:
- Average rating.
- Response count.
- Rating distribution.
- Category summaries.
- Trends.
- Authorized written feedback.

Do not treat a small number of ratings as definitive evidence of staff performance.

Keep staff feedback separate from the Student Success Score unless a future validated and institution-approved design explicitly requires otherwise.

---

# 12. Student Success Score

Calculate a configurable score from 0 to 100.

Suggested initial weights:
- Academic performance: 40%.
- Attendance: 25%.
- LMS and assignment completion: 10%.
- Placement readiness: 10%.
- Skills assessment: 10%.
- Engagement: 5%.

Normalize indicator scores to 0–100 before applying weights.

Requirements:
- Handle missing data transparently.
- Show data coverage.
- Explain indicator contributions.
- Show calculation timestamps.
- Allow authorized administrators to configure weights.
- Document the calculation.
- Avoid protected or irrelevant personal characteristics.
- Do not describe the score as a definitive measure of a student's ability or future.

If missing indicators are excluded, renormalize the remaining weights transparently or mark the score provisional.

Initial configurable interpretation:
- 80–100: Strong current indicators.
- 60–79: Developing; monitor progress.
- 40–59: Support may be beneficial.
- Below 40: Priority for faculty review.

These are operational bands, not validated probabilities.

---

# 13. Genuine Machine-Learning System

Build a real ML pipeline using Python, pandas, NumPy, and scikit-learn.

### Prediction Targets

Where historical data supports them, predict:
- Future examination performance.
- Academic threshold risk.
- Future academic percentage.
- Placement readiness or outcomes when suitable labels exist.

Use relevant historical information such as:
- Prior marks.
- Attendance history.
- Previous results.
- Assignment completion.
- Relevant LMS activity.
- Skills assessments.
- Placement preparation.

Do not use academic marks alone to claim reliable placement-outcome prediction.

### Training and Evaluation

Implement:
- Data cleaning.
- Feature engineering.
- Train/validation/test splits.
- Leakage prevention.
- Baseline models.
- Cross-validation where appropriate.
- Model versioning.
- Prediction timestamps.
- Monitoring and retraining policies.

Use regression metrics such as MAE and RMSE where appropriate.

Use classification metrics such as precision, recall, F1-score, ROC-AUC, and PR-AUC where appropriate.

Do not fabricate training results or accuracy.

If historical data is insufficient, provide transparent rule-based indicators and label ML predictions unavailable until a suitable model can be trained.

### Explainability

Show:
- Predicted outcome.
- Uncertainty where meaningfully calibrated.
- Important input indicators.
- Model version.
- Prediction date.
- Data coverage.
- Recommended support actions.

Use feature importance or SHAP when appropriate. Do not present model contributions as proof of causation.

---

# 14. AI Assistant and RAG Knowledge System

Build an integrated AI assistant called **Acediytix Campus Copilot**.

The assistant must help authorized users understand academic policies, use the platform, search permitted institutional documents, and interpret authorized academic summaries.

Implement a genuine Retrieval-Augmented Generation pipeline rather than merely sending a prompt to an LLM.

### 14.1 RAG Architecture

Create these stages:

1. Document ingestion.
2. File validation.
3. Text extraction.
4. Document cleaning.
5. Chunking with source metadata.
6. Embedding generation.
7. Vector indexing.
8. Query embedding.
9. Semantic retrieval.
10. Optional keyword or hybrid retrieval.
11. Permission filtering.
12. Context assembly.
13. LLM answer generation.
14. Source citations.
15. Answer
