# [MediNotes Pro — AI-Powered Medical Consultation Summaries](https://saas-aryan-mishras-projects-46628429.vercel.app/).

A modern healthcare application that converts raw consultation notes into structured medical summaries, actionable follow-ups, and patient-friendly messages — powered by AI.

## Table of Contents
- About
- Features
- Tech Stack
- Demo / Example Flow
- Installation
  - Backend
  - Frontend
- Environment Variables (exact names used in this repository)
- Usage
  - Development
  - Production / Deployment
- How It Works
- Security Considerations
- Potential Enhancements
- Contributing
- Contact

## About
MediNotes Pro helps clinicians convert consultation notes into:
- Professional medical summaries for clinical records
- Actionable next steps and follow-up items
- Patient-friendly email drafts explaining diagnosis and next steps
- Fast, validated data entry with date pickers and streaming AI output

## Features
- Structured consultation input (patient name, date, notes)
- Pydantic-driven strict validation
- AI-generated: summary, next steps, patient email
- JWT-protected routes and Clerk-based user management
- Streaming AI responses for live feedback

## Tech Stack
- Backend: FastAPI, Pydantic, fastapi-clerk-auth (Clerk integration), OpenAI
- Frontend: TypeScript (Next.js/React), secure client auth with Clerk, structured forms
- Deployment: Vercel (frontend + serverless Python backend)

## Demo / Example Flow 
1. Sign in
2. Open the consultation form
3. Enter:
   - Patient Name: Aryan Mishra
   - Date: Today
   - Notes: "Patient presents with persistent cough for 2 weeks. No fever. Chest clear. BP 120/80. Likely viral bronchitis. Prescribed rest and fluids. Follow up if symptoms persist beyond a week."
4. Result:
   - Medical summary
   - Actionable next steps
   - Patient-friendly email draft
To view the project demo video, [Click Here](https://drive.google.com/file/d/1rpB7A7jbRmEHMSc3wylKgF3M4doPXKCt/view?usp=drive_link)

## Installation
Prerequisites:
- Python 3.8+
- Node.js 16+ (if using the frontend)
- Vercel CLI (optional for deploy)

Backend (example)
1. Create & activate a virtual environment:
   - python -m venv .venv
   - source .venv/bin/activate  (Windows: .venv\Scripts\activate)
2. Install dependencies:
   - pip install -r requirements.txt
   - Ensure requirements.txt includes at minimum:
     - fastapi
     - uvicorn
     - openai
     - fastapi-clerk-auth
     - pydantic
3. Run development server:
   - uvicorn main:app --reload

Frontend (if separate)
1. Install node deps:
   - npm install
2. Start dev server:
   - npm run dev

## Environment Variables (exact names used in this repository)
Set these environment variables exactly as named below in vercel. The repo and documentation reference these names in code and deployment instructions.

- OPENAI_API_KEY
  - OpenAI API key used by the backend. Example: vercel env add OPENAI_API_KEY

- NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY
  - Clerk publishable key (client-side). Should be set in .env.local for local development and as a Vercel env var for preview/production.

- CLERK_SECRET_KEY
  - Clerk secret key used by the backend to verify sessions and webhooks.

- CLERK_JWKS_URL
  - Clerk JWKS URL used by the backend library to validate JWTs (see api/index.py which uses os.getenv("CLERK_JWKS_URL")).


Notes:
- Do NOT commit any of these values to source control. Use .env.local for local development and provider-native secret management (Vercel env vars, AWS Secrets Manager, etc.) in production.
- Example local file (.env.local) contents used in documentation:

  NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_...
  CLERK_SECRET_KEY=sk_test_...
  CLERK_JWKS_URL=https://...
  OPENAI_API_KEY=sk-...

- For server-only secrets (CLERK_SECRET_KEY, CLERK_JWKS_URL, OPENAI_API_KEY) ensure they are not exposed to the browser.

## Usage
Development
- Start backend: uvicorn main:app --reload
- Start frontend (if applicable): npm run dev
- Visit the frontend URL, authenticate with Clerk, and use the consultation form.

Production / Deployment
- Ensure the exact environment variables above are configured in your hosting provider (Vercel, AWS App Runner, etc.).
- To add to Vercel from your terminal, example commands:
  - vercel env add OPENAI_API_KEY
  - vercel env add NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY
  - vercel env add CLERK_SECRET_KEY
  - vercel env add CLERK_JWKS_URL

- Deploy the full application to Vercel:
  - vercel --prod

You can also visit the vercel deployed website by [clicking Here](https://saas-aryan-mishras-projects-46628429.vercel.app/).

## How It Works
1. Structured Input
   - Patient name, visit date, consultation notes.
2. Data Validation
   - Inputs validated via Pydantic models for types and formats.
3. AI-Generated Output
   - Backend calls OpenAI to produce:
     - Medical summary
     - Actionable next steps
     - Patient-facing email
   - Streaming responses support progressive rendering in the UI.
4. Security
   - Clerk and JWTs used for authentication/authorization (backend uses CLERK_JWKS_URL to configure the guard).

## Security Considerations (Important)
For clinical deployment, implement:
- HIPAA-compliant infrastructure and processes
- Encryption at rest and in transit
- Audit logs for all access and modifications
- Role-based access controls (doctor, admin, nurse)
- Data retention and deletion policies
- Patient consent management
- Penetration testing and regular security reviews

## Potential Enhancements
- Template library for common conditions
- Voice dictation for notes
- Multi-language patient communication
- EHR/EMR integration
- Analytics dashboard for consultation trends
- Shared templates for teams

## Contributing
- Open an issue to discuss changes or file a pull request.
- Include descriptive commit messages and update README/docs as needed.


## Contact
Maintainer: @Aryan-any
Project: MediNotes Pro — AI-Powered Medical Consultation Summaries
