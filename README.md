# ShetiRakshak / शेतीरक्षक

> **समजतं. करता येतं. साथ आहे.**  
> *Understand. Can act. Supported.*

ShetiRakshak is a Maharashtra-first, Marathi-first, voice-first, cotton-first agricultural decision-support application delivered as a PWA.

It keeps **पहारा — The Watch** over critical farming decision moments (weather, spraying windows, crop anomalies, scheme deadlines, market windows).

---

## Architecture at a Glance

- **Frontend:** React + Vite + Tailwind CSS + Lucide React (`frontend/`)
- **Backend:** Node.js + Express (ES Modules) (`backend/`)
- **Database & Auth:** Supabase PostgreSQL + Auth + Storage
- **External Services:** WeatherAPI.com (Weather) + Gemini API (Bounded explanation)
- **Voice:** Web Speech API (Input) + SpeechSynthesis (Output)

---

## Directory Structure

```text
/
├── frontend/          # React + Vite frontend application
├── backend/           # Node.js + Express API backend
├── docs/              # Specifications, architecture, guides, and logs
│   ├── source/        # Preserved source documents (Brand Bible, Tech Stack, Playbook)
│   ├── DEVELOPMENT_STATUS.md # Single source of truth for phase progress
│   ├── ARCHITECTURE.md
│   ├── DECISION_LOG.md
│   ├── API.md
│   ├── DATABASE.md
│   ├── TESTING.md
│   ├── SECURITY.md
│   ├── AI_GUIDELINES.md
│   ├── VOICE.md
│   ├── OFFLINE.md
│   └── RELEASE.md
├── .env.example       # Template environment variables
├── .gitignore
├── .nvmrc             # Node LTS v20.18.0
└── package.json       # Root orchestration scripts
```

---

## Getting Started

### Prerequisites

- Node.js `v20.18.0` LTS or higher
- npm `v10.8.2` or higher

### Environment Setup

Copy `.env.example` to `.env` and fill in necessary keys when ready:

```bash
cp .env.example .env
```

### Installation

Install dependencies in both services:

```bash
cd frontend && npm install
cd ../backend && npm install
```

### Running Locally

From the root repository:

```bash
# Start backend API (http://localhost:5000)
npm run dev:backend

# Start frontend dev server (http://localhost:5173)
npm run dev:frontend
```

### Testing & Building

```bash
# Run backend tests
npm test

# Build frontend production bundle
npm run build:frontend
```
