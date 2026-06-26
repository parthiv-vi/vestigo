# Vestigo Insurance CRM 

Welcome to the **Vestigo Insurance CRM** repository. This project is a comprehensive enterprise-grade Customer Relationship Management (CRM) and Reconciliation system tailored specifically for insurance brokers.

## 📖 Project Overview

Vestigo Insurance CRM is designed to streamline the operations of an insurance brokerage. A critical feature of this system is the **Brokerage Reconciliation Module**, which automates the tedious process of matching expected brokerages (calculated when a policy is sold) with the actual brokerages received from insurers (e.g., ICICI Lombard, HDFC Ergo) at the end of the month.

### Key Capabilities
- **Policy Management:** Track policies sold, premiums, and expected brokerages.
- **Automated Brokerage Reconciliation:** Upload CSV statements from insurers, and the system auto-matches payments against expected brokerages in the CRM.
- **Variance Detection & Approval:** Automatically highlights discrepancies (overpayments or underpayments) and routes them through an approval workflow.
- **Financial Integration:** Preparation for pushing reconciled amounts directly to Zoho Books for seamless accounting.

---

## 🛠 Tech Stack

### Backend
- **Framework:** Python, Django, Django REST Framework (DRF)
- **Database:** SQLite (default for dev) / PostgreSQL or MySQL (production ready)
- **Authentication:** JWT (JSON Web Tokens) via `djangorestframework-simplejwt`
- **Background Tasks:** Celery & Redis (configured in requirements)
- **Documentation:** Swagger/OpenAPI via `drf-yasg`

### Frontend
- **Framework:** React 19, Vite
- **Styling:** Tailwind CSS v4, Headless UI, Heroicons
- **State/Data Management:** React Query (`@tanstack/react-query`), Axios
- **Routing:** React Router DOM
- **Charts:** Recharts

---

## 📂 Project Structure

```
vestigo/
├── backend/                   # Django Backend Code
│   ├── vestigo_backend/       # Core Django project settings & routing
│   ├── core/                  # Core abstract models and utilities
│   ├── users/                 # Custom user models and authentication
│   ├── operations/            # Policy and core business logic
│   ├── reconciliation/        # Brokerage and Premium reconciliation logic
│   ├── bdm/, claims/, reports/ # Additional business modules
│   ├── requirements.txt       # Python dependencies
│   └── manage.py              # Django entry point
├── frontend/                  # React Frontend Code
│   └── vestigo_frontend/      # Vite project
│       ├── src/               # React source (components, services, views)
│       ├── package.json       # Node dependencies
│       └── vite.config.js     # Vite configuration
├── docs/                      # Documentation (if any)
├── infra/                     # Infrastructure & Deployment scripts
└── README.md                  # This file
```

---

## 🚀 Setup & Installation (Developer Guide)

### 1. Backend Setup
```bash
cd backend
python -m venv venv

# Windows
.\venv\Scripts\activate
# Mac/Linux
source venv/bin/activate

pip install -r requirements.txt

# Set up environment variables
cp .env.example .env
# Edit .env to add your database credentials and secret keys

# Run migrations
python manage.py migrate

# Start the development server
python manage.py runserver
```

### 2. Frontend Setup
```bash
cd frontend/vestigo_frontend

# Install dependencies
npm install

# Start the Vite development server
npm run dev
```

---

## 📝 Developer Handover Notes & Next Steps

If you are the next developer picking up this project, here are the immediate areas that need attention for production readiness:

1. **Environment Variables:** The frontend API service currently points to a hardcoded `localhost:8000`. This needs to be moved to a `.env` variable (e.g., `VITE_API_BASE_URL`).
2. **Backend Security:** Review `backend/vestigo_backend/settings.py`. Ensure `DEBUG` is strictly `False` in production, secure the `SECRET_KEY`, and properly configure `ALLOWED_HOSTS` and `CORS_ALLOWED_ORIGINS` via environment variables.
3. **Database Migration:** The system currently defaults to SQLite. Ensure the production environment is provisioned with PostgreSQL or MySQL and update the `DATABASES` configuration.
4. **Zoho Books Integration:** The API endpoints for pushing reconciled statements to Zoho Books are conceptually planned but require full implementation.
5. **Insurer Configurations:** Variance thresholds are currently hardcoded (e.g., tolerance of 1.00). This should be moved to a configurable UI model per insurer.

---

## 📚 Further Reading

For a deeper dive into the business logic and recent architecture changes, refer to:
- `project_comprehensive_summary.md` - Overall system progress and architectural decisions.
- `brokerage_reconciliation_story.md` - A complete business use-case story explaining the Brokerage Reconciliation module.
