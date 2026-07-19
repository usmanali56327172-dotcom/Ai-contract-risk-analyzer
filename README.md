# AI Contract Risk Analyzer (Full-Stack Web Application)

A production-grade, enterprise-style Legal-Tech web application simulating an Ironclad/Lexion-style
Contract Risk Analysis platform, developed as a full-stack engineering portfolio project.
The system demonstrates practical use of a layered backend architecture, an async job queue,
a vector database, an LLM analysis pipeline, and a modern component-based frontend to manage
contracts, risk, compliance, negotiation, and billing.

---

## Features

### Authentication & Roles
- Sign up, login, logout with JWT (access token + rotating refresh token)
- Google and Microsoft OAuth login
- Role-based access: Owner, Admin, Member, Viewer (per organization)

### Contract Upload & Ingestion
- PDF and DOCX upload with text extraction
- Automatic OCR fallback for scanned/image-only PDFs
- Async processing via a dedicated BullMQ worker (separate from the API process)

### AI Contract Analysis
- Clause detection across 12 clause types (payment, termination, liability, IP, data privacy, etc.)
- Missing-clause detection
- 4-dimension risk scoring: legal, financial, operational, compliance
- Executive summary, recommendations, and confidence score
- Multi-language contract analysis (detects and analyzes non-English contracts)

### AI Redline Generator
- Rewrites high-risk clauses in place with a rationale and risk-reduction delta

### AI Negotiation Assistant
- Prioritized negotiation playbook per risky clause: position, counter-ask, fallback

### Contract Expiry Prediction
- Extracts effective/expiry dates, renewal type, and notice period
- Org-wide "expiring soon" view with automated notifications

### Compliance Checker
- Built-in GDPR, HIPAA, and ISO 27001 rule sets
- Custom, organization-defined compliance frameworks

### AI Chat with Contract (RAG)
- Retrieval-augmented Q&A grounded strictly in the uploaded document
- Chunked, embedded, and searched via Qdrant

### Contract Comparison
- Clause-by-clause diff between two contracts (added / removed / modified / unchanged)
- Exact risk-score delta between versions

### Risk Trend Dashboard
- Month-over-month risk trend across the organization's contracts
- Org-wide summary: total contracts, average risk, high-risk count, expiring soon

### Clause Library
- Reusable, organization-scoped clause templates with usage tracking

### E-Signature
- Adapter-based provider system (manual workflow works out of the box; DocuSign-ready)

### Export
- Download the full AI report as a PDF or Word (DOCX) document

### Notifications
- In-app notification center with unread count
- Scheduled daily check for contracts expiring soon

### Billing
- Stripe Checkout for subscriptions
- Stripe Billing Portal for plan management
- Signature-verified webhook handling

### Responsive Design & Theming
- "Ink & Brass" design system, mobile-friendly layout

---

## Tech Stack Used

| Layer | Technology | Purpose |
|---|---|---|
| Backend | Node.js, NestJS, TypeScript | REST API server |
| Database | PostgreSQL + Prisma ORM | Relational data storage, type-safe queries |
| Vector Store | Qdrant | Contract chunk embeddings for RAG chat |
| Queue | BullMQ + Redis | Async contract analysis (separate worker process) |
| Auth | JWT + bcrypt + Passport (Google/Microsoft OAuth) | Authentication |
| AI | OpenAI Responses API + `text-embedding-3-small` | Clause/risk analysis, chat, embeddings |
| OCR | tesseract.js + pdf-to-png-converter | Scanned PDF text recovery |
| Payments | Stripe Checkout + Billing Portal + Webhooks | Subscription billing |
| Export | pdfkit, docx | PDF/Word report generation |
| Frontend | Next.js 15, React 19, TypeScript | User interface |
| Styling | Tailwind CSS | Responsive, themeable UI |
| Charts | Recharts | Risk trend dashboard |
| Testing | Jest | Unit tests (auth, prompts, chunking, risk logic) |
| Containers | Docker + docker-compose | Local environment, deployment |
| CI | GitHub Actions | Lint, typecheck, build, test, Docker build |
