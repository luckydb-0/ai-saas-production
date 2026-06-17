# MediNotes Pro

MediNotes Pro is an exercise project built while following the Udemy course
[AI Engineer Production Track: Deploy LLMs & Agents at Scale](https://www.udemy.com/course/generative-and-agentic-ai-in-production/).

The project explores a production-style AI SaaS architecture deployed on Vercel: users authenticate with Clerk, access a subscription-gated product page, submit healthcare consultation notes, and receive an AI-generated doctor summary, next-step checklist, and patient-friendly email draft streamed from an authenticated Python API.

## Features

- Clerk authentication and user management
- Clerk subscription gating and pricing UI
- Consultation form with patient name, visit date, and clinical notes
- Authenticated FastAPI endpoint for healthcare note summarization
- Streaming OpenAI responses using Server-Sent Events (SSE)
- Markdown rendering for generated summaries and email drafts
- Responsive interface styled with Tailwind CSS

## Tech Stack

- Next.js 16 Pages Router, React 19, and TypeScript
- FastAPI and Python
- OpenAI API
- Clerk authentication and billing
- React Datepicker
- Tailwind CSS
- Vercel deployment

## Project Structure

```text
api/index.py        Authenticated FastAPI streaming endpoint
pages/index.tsx     Public landing page and sign-in flow
pages/product.tsx   Subscription-gated consultation assistant
pages/_app.tsx      Clerk provider and global application setup
styles/globals.css  Global and Markdown styles
week1/              Course notes and exercises
```

## Prerequisites

- Node.js 20.9 or newer
- Python 3
- OpenAI and Clerk accounts
- A Clerk plan with the key `premium_subscription`

## Setup

Install the frontend dependencies:

```bash
npm install
```

Create a Python virtual environment and install the API dependencies:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Create `.env.local` with the required credentials:

```dotenv
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
CLERK_SECRET_KEY=your_clerk_secret_key
CLERK_JWKS_URL=your_clerk_jwks_url
OPENAI_API_KEY=your_openai_api_key
```

Do not commit `.env.local` or any real credentials.

## Development

Run the Next.js frontend locally:

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

The backend is implemented as a Python function in `api/index.py`, rather than a Next.js API route. The frontend sends authenticated `POST /api` requests with the consultation payload and renders the streamed Markdown response. The complete frontend-to-API flow is designed to run on Vercel, which detects both the Next.js application and the Python function.

Useful checks:

```bash
npm run lint
npm run build
```

## Deployment

Link the repository to a Vercel project and configure these environment variables for the appropriate environments:

- `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY`
- `CLERK_SECRET_KEY`
- `CLERK_JWKS_URL`
- `OPENAI_API_KEY`

Deploy a preview:

```bash
npx vercel
```

Deploy to production:

```bash
npx vercel --prod
```

## Learning Resources

- [Course: AI Engineer Production Track](https://www.udemy.com/course/generative-and-agentic-ai-in-production/)
- [Next.js Pages Router documentation](https://nextjs.org/docs/pages)
- [Clerk documentation](https://clerk.com/docs)
- [FastAPI documentation](https://fastapi.tiangolo.com/)
- [OpenAI API documentation](https://platform.openai.com/docs)

## Disclaimer

This repository is an educational exercise, not a production-ready healthcare product. It should not be used with real patient data. Privacy, compliance, medical review, security controls, usage limits, audit logging, data retention, pricing, and operational safeguards would need substantial work before any real launch.
