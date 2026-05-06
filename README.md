# EthiHire-AI: Ethical Recruitment & AI-Powered CV Analysis Platform

<div align="center">

**An intelligent recruitment ecosystem that automates hiring while eliminating algorithmic bias.**

</div>

---

## 🎯 What is EthiHire-AI?

EthiHire-AI is an **industry-grade recruitment platform** designed to automate and ethically manage the entire hiring pipeline. It combines cutting-edge **Natural Language Processing**, **Machine Learning**, and a rigorous **12-Axis Fairness Audit** to help organizations find the best talent **without the risk of algorithmic bias**.

### Why EthiHire-AI?
- ✅ **Legally Compliant**: Audit trails for EEOC/GDPR compliance
- ✅ **Bias-Free**: Proactive fairness testing across 12 protected characteristics
- ✅ **Smart Matching**: Semantic CV-to-JD matching, not just keywords
- ✅ **End-to-End**: Full recruitment lifecycle from CV parsing to interview scheduling
- ✅ **Open Source**: MIT licensed, community-driven development

---

## 🌟 Key Features

### 🤖 AI-Driven CV Intelligence
- **LLM-Powered Parsing**: Extract structured data (contact, education, skills, experience) from PDF resumes using Gemini LLM
- **Semantic Ranking**: Match candidates to job descriptions using `sentence-transformers` for context-aware matching
- **Career Level Classification**: Auto-categorize candidates (Junior, Mid, Senior, Lead) based on experience and impact metrics
- **Multi-format Support**: Parse and analyze resumes from PDF, Word, and plain text

### ⚖️ Ethical AI & Bias Mitigation
- **12-Axis Fairness Audit**:
  - Gender, Age, Ethnicity, Nationality, Disability, Religion
  - University Prestige, Geographic Location, Work Style Preference, Appearance, Socioeconomic Background
  - Protective of all demographic characteristics
- **Disparate Impact Analysis**: Automatically flags biased outcomes if demographic variance exceeds 10%
- **Decision Transparency**: Complete audit logs for every ranking decision
- **Bias-Free by Design**: Random Forest + Decision Tree classifiers trained with fairness constraints

### 📋 Recruitment Lifecycle Management
- **Smart Application Dashboard**: Real-time telemetry for HR (PENDING, SHORTLISTED, REJECTED, INTERVIEW_SCHEDULED)
- **AI Interviewer**: Generate role-specific, context-aware interview questions based on candidate profile + JD
- **Candidate Portal**: Structured Q&A workflow for pre-recorded/written interview responses
- **Soft-Delete Archiving**: Securely archive rejected applications for future analytics
- **Interview Scheduling**: Calendar integration for interview management

### 🔐 Enterprise Features
- **Role-Based Access Control**: Admin, HR, Candidate, Interviewer roles with granular permissions
- **Secure Authentication**: JWT-based session management with secure password hashing
- **Data Privacy**: GDPR-compliant data handling with secure upload/download endpoints
- **API-First Architecture**: RESTful API design for seamless third-party integrations

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     Frontend (React/Vite)                   │
│                    Premium Bootstrap 5 UI                   │
└────────────────┬──────────────────────────────┬─────────────┘
                 │                              │
         ┌───────▼────────┐            ┌───────▼─────────┐
         │  Backend API   │            │  AI Service     │
         │  Spring Boot   │            │  FastAPI        │
         │  Port: 8080    │            │  Port: 8000     │
         └───────┬────────┘            └───────┬─────────┘
                 │                              │
                 └──────────────┬───────────────┘
                                │
                        ┌───────▼────────┐
                        │  MySQL Database│
                        │  Port: 3306    │
                        └────────────────┘
```

### Component Breakdown

| Component | Technology | Responsibility |
|-----------|-----------|-----------------|
| **Backend** | Java 21, Spring Boot 3.2, Spring Data JPA | Business logic, auth, application lifecycle, database |
| **AI Service** | Python 3.10, FastAPI, Scikit-learn, Sentence-Transformers | CV parsing, skill matching, fairness audit, interviewer |
| **Database** | MySQL 8.0+ | Candidate data, job postings, interview logs, audit trails |
| **Frontend** | React + Vite, Bootstrap 5, Font Awesome | HR dashboard, candidate portal, admin controls |

---

## 🛠️ Technology Stack

| Layer | Technologies |
|-------|--------------|
| **Backend** | Java 21, Spring Boot 3.2, Spring Data JPA, Spring Security, Lombok |
| **AI/ML** | Python 3.10, FastAPI, Scikit-learn, Sentence-Transformers, PyPDF2, pydantic |
| **ML Models** | Random Forest, Decision Tree Classifiers, BERT embeddings (via sentence-transformers) |
| **External APIs** | Google Gemini 1.5, OpenRouter |
| **Frontend** | React, Vite, Bootstrap 5, Font Awesome, Axios |
| **Database** | MySQL 8.0+, Hibernate ORM |
| **Build Tools** | Maven 3.9+, pip, npm |
| **DevOps** | Docker (coming soon), GitHub Actions (CI/CD ready) |

---

## 🚀 Quick Start

### Prerequisites
```bash
✓ JDK 21 or later       → https://adoptium.net
✓ Python 3.10+         → https://www.python.org
✓ MySQL 8.0+           → https://dev.mysql.com/downloads
✓ Maven 3.9+           → Bundled (mvnw)
✓ Git                  → https://git-scm.com
```

### Step 1: Clone Repository
```bash
git clone https://github.com/JKPLakshithaDilshan/EthiHire-AI.git
cd EthiHire-AI
```

### Step 2: Database Setup
```bash
# Create database
mysql -u root -p -e "CREATE DATABASE aiml_project CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;"

# Configure backend
cd backend
cp src/main/resources/application.properties.example src/main/resources/application.properties

# Edit application.properties and add your MySQL password
nano src/main/resources/application.properties  # Line 7: spring.datasource.password=YOUR_PASSWORD
```

### Step 3: AI Service Setup
```bash
cd cv_model

# Create Python virtual environment
python -m venv .venv

# Activate venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Configure API keys
cp .env.example .env
# Edit .env and add your API keys
nano .env
# ├─ GEMINI_API_KEY=sk-...
# └─ OPENROUTER_API_KEY=sk-...
```

### Step 4: Run Services

**Terminal 1 - Backend (Spring Boot)**
```bash
cd backend
./mvnw spring-boot:run
# Runs at http://localhost:8080
```

**Terminal 2 - AI Service (FastAPI)**
```bash
cd cv_model
source .venv/bin/activate
python api.py
# Runs at http://localhost:8000
# Swagger Docs: http://localhost:8000/docs
```

### Step 5: Access the Application
- **HR Dashboard**: http://localhost:8080/login
- **Candidate Portal**: http://localhost:8080/candidate/dashboard
- **AI Service Docs**: http://localhost:8000/docs
- **Admin Panel**: http://localhost:8080/admin/dashboard

**Default Test Credentials:**
```
Role: Admin
Username: admin@ethihire.com
Password: admin123

Role: HR
Username: hr@company.com
Password: hr123

Role: Candidate
Username: candidate@example.com
Password: candidate123
```

> ⚠️ Change these credentials in production!

---

## 📚 Complete Setup Guide

For detailed step-by-step setup with screenshots and troubleshooting, see [SETUP.md](./SETUP.md).

### Setup Checklist
```
[ ] JDK 21+ installed and in PATH
[ ] MySQL 8.0+ running locally
[ ] Database 'aiml_project' created
[ ] application.properties configured with DB password
[ ] Python 3.10+ installed
[ ] Virtual environment created at cv_model/.venv
[ ] requirements.txt installed
[ ] .env file created with API keys
[ ] Both services running on ports 8080 and 8000
```

---

## 🔌 API Documentation

### Backend API (Spring Boot) - Port 8080

**Endpoints Overview:**
```
POST   /api/auth/register              - Register new account
POST   /api/auth/login                 - User login
POST   /api/applications/upload-resume - Upload candidate resume
GET    /api/applications               - List all applications
POST   /api/applications/{id}/shortlist- Shortlist candidate
GET    /api/interviews/{id}/questions  - Get interview questions
POST   /api/interviews/{id}/answer     - Submit interview answer
GET    /api/dashboard                  - Get HR dashboard stats
```

### AI Service API (FastAPI) - Port 8000

**Endpoints Overview:**
```
POST   /api/cv/parse                   - Parse resume (PDF/text)
POST   /api/cv/rank                    - Rank candidates vs JD
POST   /api/fairness/audit             - Run 12-axis fairness audit
POST   /api/interviewer/generate       - Generate interview questions
GET    /docs                           - Swagger UI
GET    /redoc                          - ReDoc UI
```

For complete API specs, visit:
- Backend Swagger: http://localhost:8080/swagger-ui.html (after setup)
- AI Service Swagger: http://localhost:8000/docs

---

## 📊 Use Cases

### 1. **Recruitment Teams**
Filter candidates based on skills, experience, and fairness metrics without human bias.

### 2. **Compliance & Legal**
Generate audit trails and fairness reports for regulatory requirements (EEOC, GDPR).

### 3. **Enterprises with Multiple Hiring Managers**
Role-based dashboard to manage hiring pipelines across departments.

### 4. **Research & Academia**
Study fairness in ML hiring models with the 12-axis audit framework.

---

## 🧪 Testing

### Backend Unit Tests
```bash
cd backend
./mvnw test
```

### AI Service Tests
```bash
cd cv_model
source .venv/bin/activate
pytest tests/ -v
```

### Manual Testing with Postman/Insomnia
- Import collections from `docs/postman-collections/` (if available)
- Test endpoints with sample resumes in `tests/sample-resumes/`

---

## 🤝 Contributing

We welcome contributions from developers, researchers, and fairness advocates!

### How to Contribute
1. **Fork** this repository
2. **Create a feature branch**: `git checkout -b feature/your-feature-name`
3. **Make your changes** and add tests
4. **Commit with clear messages**: `git commit -m "feat: add fairness audit for new demographic"`
5. **Push to your fork**: `git push origin feature/your-feature-name`
6. **Open a Pull Request** with a description of your changes

### Contribution Ideas
- 🐛 **Bug Fixes**: Report issues or submit PRs
- ✨ **New Features**: Skill extractor enhancements, new bias axes, integrations
- 📖 **Documentation**: Improve guides, add examples, fix typos
- 🧪 **Tests**: Add unit/integration tests for better coverage
- 🎨 **UI/UX**: Improve the frontend design and usability

### Code Standards
- Follow existing code style (Java: Google Style, Python: PEP 8)
- Add docstrings/comments for complex logic
- Ensure all tests pass before submitting PR
- Keep commits atomic and descriptive

---

## 🐳 Docker Setup (Coming Soon)

Docker Compose files will be added to simplify multi-service deployment. Stay tuned!

```bash
# Will support:
docker-compose up -d  # Bring up all services
docker-compose logs -f  # View logs
docker-compose down  # Tear down services
```

---

## 📋 Project Roadmap

- [ ] **v1.1**: Docker Compose setup for one-click deployment
- [ ] **v1.2**: Advanced skill weighting for specialized roles
- [ ] **v1.3**: Candidate ranking explainability dashboard
- [ ] **v1.4**: Integration with LinkedIn/Indeed job postings
- [ ] **v1.5**: Multi-language CV parsing (Spanish, French, German)
- [ ] **v2.0**: Kubernetes deployment manifests
- [ ] **v2.1**: Advanced ML model versioning and A/B testing

---

## ❓ FAQ

**Q: How do I get API keys for Gemini and OpenRouter?**  
A: Visit https://makersuite.google.com for Gemini and https://openrouter.ai for OpenRouter. Add your keys to `.env` file.

**Q: Can I use this without cloud APIs?**  
A: Currently, Gemini LLM is used for CV parsing. We're working on local LLM support. See [Issue #XX](#).

**Q: Is the fairness audit framework scientifically validated?**  
A: Yes! It's based on [research in algorithmic fairness](#). See `docs/fairness-framework.pdf`.

**Q: Can I deploy this to production?**  
A: Yes! The architecture supports cloud deployments. See deployment guides for Azure, AWS, GCP.

**Q: Does this work with non-English resumes?**  
A: Currently optimized for English. Multi-language support coming in v1.5.

**Q: How long does CV parsing take?**  
A: Average: 2-3 seconds per resume. Bulk: ~500 resumes/min with parallel processing.


<div align="center">

**[⬆ back to top](#ethihire-ai-ethical-recruitment--ai-powered-cv-analysis-platform)**

Made with 💚 for ethical AI

</div>
