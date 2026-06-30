# Personalized Financial Wellness & Tax AI Agent

This is a prototype for an AI-powered employee financial assistant that helps employees manage their payroll, simulate tax savings, and interact with an AI grounded in their personal financial data.

## Features
- **Secure Authentication**: JWT-based login using employee IDs. Data isolation is strictly enforced.
- **Payslip Upload & OCR**: Upload PDF/images to extract payroll data. Uses mocked OCR logic for the prototype.
- **Grounded AI Chat**: Ask questions about your salary, deductions, and HRA. The AI only responds using your specific context.
- **Tax Simulator**: Predict your tax savings by inputting potential 80C investments.
- **Investment Checklist**: Track which proofs (PAN, Rent Receipts, 80C) are submitted, pending, or missing.

## Tech Stack
- **Frontend**: React 18, Vite, Material UI (MUI), React Router, Axios.
- **Backend**: Python, FastAPI, Pydantic, python-jose (JWT).
- **Data**: Local mock JSON files simulating database and OCR outputs (`data/` directory).

## Folder Structure
```
financial-ai-agent/
├── backend/
│   ├── api/routes.py           # API endpoints
│   ├── services/               # Core business logic (AI, Tax, Auth, OCR)
│   ├── security/jwt_handler.py # JWT utilities
│   ├── models/schemas.py       # Pydantic schemas
│   ├── data/                   # Mock JSON databases
│   ├── ocr/                    # Mock OCR outputs
│   └── main.py                 # FastAPI Entrypoint
└── frontend/
    ├── src/
    │   ├── components/         # Reusable UI (Sidebar, ChatWidget)
    │   ├── pages/              # Views (Dashboard, Upload, Chat)
    │   ├── services/api.js     # Axios API integration
    │   └── context/            # Global Auth Context
    ├── package.json
    └── vite.config.js
```

## How to Run

### Backend Setup
1. Navigate to the `backend` directory: `cd backend`
2. Create and activate a virtual environment (recommended on macOS):
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```
3. Install dependencies: `pip3 install -r requirements.txt`
4. Run the FastAPI server: `python3 main.py` (Runs on http://localhost:8000)

### Frontend Setup
1. Navigate to the `frontend` directory: `cd frontend`
2. Install dependencies: `npm install`
3. Run the Vite development server: `npm run dev` (Runs on http://localhost:3000)

## Environment Variables
- **Backend**: 
  - `JWT_SECRET`: Secret key for signing JWTs (defaults to local string).
  - `LLM_API_URL`: The URL of the wrapper AI API.

## Mock Data Explanation
The prototype uses `backend/data/employees.json` for valid logins. You can log in using Employee ID: **E1001** (Rahul) or **E1002** (Jane). Only E1001 has full mocked payroll data in this prototype.

## Security Assumptions
- User isolation is achieved by enforcing the `employee_id` retrieved directly from the JWT token via dependency injection in FastAPI.
- Files uploaded are placed in an isolated directory specific to the JWT's subject identifier.

## Future Improvements
- Replace JSON files with a real relational database (e.g. PostgreSQL).
- Integrate actual Tesseract or Textract OCR pipelines.
- Integrate standard OpenAI API rather than mock responses.
- Add comprehensive error handling for malformed payslips.
