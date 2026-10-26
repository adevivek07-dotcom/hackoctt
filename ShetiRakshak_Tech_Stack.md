# ShetiRakshak — Technology Stack Specification

**Project:** ShetiRakshak  
**Product direction:** Maharashtra-first · Marathi-first · Cotton-first · Built to scale  
**Architecture goal:** Keep the codebase simple, maintainable, and easy to develop while supporting the Brand Bible's core requirements: clear next steps, Marathi/voice-first interaction, weak-network support, verified information, confidence signals, and human expert escalation.

---

## 1. Final Recommended Tech Stack

| Layer | Technology | Purpose |
|---|---|---|
| Frontend | **React + Vite** | Main web application UI |
| Styling | **Tailwind CSS** | Fast, consistent implementation of Brand Bible design tokens |
| Icons | **Lucide React** | Lightweight, accessible interface icons |
| Backend | **Node.js + Express** | Simple REST API and server-side business logic |
| Database | **Supabase PostgreSQL** | Farmer, crop, case, expert, scheme and market data |
| Authentication | **Supabase Auth** | User authentication without building a custom auth system |
| File Storage | **Supabase Storage** | Crop/problem photos and other user-uploaded files |
| Weather | **WeatherAPI.com** | Weather and forecast data |
| AI | **Gemini API** | Explanation, conversational assistance and language generation |
| Voice Input | **Web Speech API initially** | Speech-to-text without adding a dedicated speech backend |
| Voice Output | **Browser SpeechSynthesis initially** | Text-to-speech for early MVP |
| Location | **Browser Geolocation API** | Farmer location for weather and nearby-help use cases |
| Offline | **PWA + IndexedDB** | App shell and last-known information for weak/no connectivity |
| Frontend Hosting | **Vercel** | Simple frontend deployment |
| Backend Hosting | **Render** | Simple Node/Express deployment |
| Version Control | **Git + GitHub** | Source control and collaboration |
| Primary Language | **JavaScript initially** | Keep the initial codebase straightforward |

### Stack in one line

> **React + Vite + Tailwind CSS + Node/Express + Supabase + WeatherAPI + Gemini + Web Speech API + Vercel/Render**

---

## 2. Architecture Philosophy

The first version should deliberately avoid unnecessary infrastructure.

### Do NOT start with

- Microservices
- Kubernetes
- Kafka
- Redis
- Docker
- Separate Python AI service
- Vector database
- LangChain
- Complex AWS infrastructure
- Multiple backend services

### Preferred model

```text
One frontend
    ↓
One backend
    ↓
One database
    ↓
A small number of external APIs
```

The architecture should mirror the product philosophy: **simple, calm, focused and useful**.

---

## 3. High-Level Architecture

```text
                    🌾 SHETIRAKSHAK
                           │
                           ▼
                  ┌─────────────────┐
                  │ React + Vite    │
                  │ Tailwind CSS    │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │ Node + Express  │
                  │ REST API        │
                  └────────┬────────┘
                           │
             ┌─────────────┼─────────────┐
             ▼             ▼             ▼
        ┌─────────┐   ┌──────────┐   ┌─────────┐
        │Supabase │   │WeatherAPI│   │ Gemini  │
        │Postgres │   │          │   │   API   │
        └─────────┘   └──────────┘   └─────────┘
             │
             ├── Farmer data
             ├── Farm/crop data
             ├── Expert cases
             ├── Uploaded photos
             └── Cached/verified information
```

---

## 4. Frontend

### React + Vite

Use React for the application UI and Vite for development/build tooling.

### Why this choice

- Simple project structure
- Fast local development
- Good fit for an interactive application
- Easy component reuse
- No need to introduce server-side rendering complexity for the initial MVP

### Suggested frontend structure

```text
frontend/
├── src/
│   ├── components/
│   │   ├── Button.jsx
│   │   ├── Card.jsx
│   │   ├── VoiceButton.jsx
│   │   ├── TrustStrip.jsx
│   │   └── Watchline.jsx
│   │
│   ├── pages/
│   │   ├── Home.jsx
│   │   ├── Weather.jsx
│   │   ├── Crop.jsx
│   │   ├── Schemes.jsx
│   │   ├── Market.jsx
│   │   └── ExpertHelp.jsx
│   │
│   ├── services/
│   │   ├── weather.js
│   │   ├── ai.js
│   │   ├── crop.js
│   │   └── expert.js
│   │
│   ├── hooks/
│   │   ├── useWeather.js
│   │   └── useVoice.js
│   │
│   ├── utils/
│   ├── data/
│   ├── App.jsx
│   └── main.jsx
│
├── public/
└── package.json
```

---

## 5. UI and Design System

### Tailwind CSS

Tailwind should implement the existing ShetiRakshak Brand Bible tokens rather than creating an unrelated visual system.

### Core colors

```css
--color-ink: #17323A;
--color-bg: #FAF7F0;
--color-surface: #FFFFFF;
--color-border: #E4DCC8;

--color-accent: #F2A900;
--color-info: #2563A8;
--color-success: #2E7D4F;
--color-warning: #C77700;
--color-error: #B3261E;
```

### Typography

```text
Font:
Mukta
Fallback:
Noto Sans Devanagari
Noto Sans

Body:
18px / 28px

H1:
26px / 34px

Caption:
15px / 22px

Button:
18px / 24px
```

### UI principles to preserve

- One screen, one decision
- Next step before more detail
- Marathi first
- Voice when typing is difficult
- Visible uncertainty
- Source and date
- Human help one tap away
- Weak-network support
- Calm, uncluttered interface
- Never promise what the system cannot control

---

## 6. Backend

### Node.js + Express

Use one Express backend for:

- API endpoints
- External API calls
- AI orchestration
- Data validation
- Business rules
- Expert-case creation
- Server-side API-key protection

### Suggested backend structure

```text
backend/
├── routes/
│   ├── weather.js
│   ├── crop.js
│   ├── ai.js
│   ├── schemes.js
│   ├── market.js
│   └── experts.js
│
├── services/
├── middleware/
├── utils/
├── server.js
└── package.json
```

Keep external API keys on the backend whenever the provider requires secret credentials.

---

## 7. Database

### Supabase PostgreSQL

Use Supabase as the initial backend platform for:

- PostgreSQL database
- Authentication
- File storage
- Security policies

### Initial database tables

```text
users
farmers
farms
crops
crop_stages
weather_cache
crop_cases
experts
expert_requests
schemes
market_prices
notifications
```

Do not create a large enterprise schema before the product actually needs it.

---

## 8. Authentication

Use **Supabase Auth**.

The first experience should not force a farmer to register before receiving basic help.

Potential flow:

```text
Open App
   ↓
Choose Language
   ↓
Allow/enter Location
   ↓
See Weather / Basic Guidance
   ↓
Create account only when needed
```

Account can become necessary for:

- Saving a farm
- Tracking a crop
- Sending an expert case
- Saving history
- Personalised information

---

## 9. Weather System

### Provider

**WeatherAPI.com**

### Recommended flow

```text
Farmer
   ↓
React
   ↓
Express API
   ↓
WeatherAPI
   ↓
Verified weather data
   ↓
Application rules
   ↓
Marathi explanation
   ↓
Farmer
```

### Important rule

Do not simply expose raw weather numbers.

Example:

```text
Raw data:
Rain probability = 70%

        ↓

Interpretation:
"उद्या दुपारनंतर पावसाची शक्यता आहे."

        ↓

Next step:
"फवारणीचं नियोजन करताना हे लक्षात ठेवा."
```

Weather data is an input to a decision-support experience, not the final user-facing answer.

---

## 10. AI Architecture

### Provider

**Gemini API**

Use AI primarily for:

- Explaining information in simple Marathi
- Conversational responses
- Summarising verified information
- Translating/rewriting approved content where appropriate
- Structuring farmer questions
- Generating clear next-step wording

### Do NOT make AI the source of truth

Preferred:

```text
Verified Data
     ↓
Application Rules
     ↓
Gemini
     ↓
Clear Explanation
     ↓
Farmer
```

Not:

```text
Gemini
   ↓
Makes everything up
   ↓
Farmer
```

### Important safety principles

AI must not:

- Claim perfect crop diagnosis
- Guarantee protection
- Guarantee profit
- Guarantee prices
- Guarantee harvest
- Guarantee scheme approval
- Invent treatment doses
- Hide uncertainty

When confidence is low, the system should offer expert help.

---

## 11. Voice

### Initial implementation

**Input:** Web Speech API  
**Output:** Browser SpeechSynthesis API

### Flow

```text
🎙️ Farmer presses voice button
          ↓
"बोला, मी ऐकतोय."
          ↓
Farmer speaks Marathi
          ↓
Speech → Text
          ↓
ShetiRakshak processing
          ↓
Marathi answer
          ↓
Text → Speech
```

### Later upgrade

If browser voice recognition/synthesis is insufficient for regional Marathi requirements, introduce a dedicated speech provider.

Do not add a dedicated voice infrastructure before it is needed.

---

## 12. Crop Problem / Photo Flow

Initial architecture:

```text
Farmer
   ↓
Camera / Photo
   ↓
Upload
   ↓
Supabase Storage
   ↓
Backend
   ↓
AI / application analysis
   ↓
Confidence level
   ↓
If uncertain → Expert
```

Example response style:

```text
"ही एक संभाव्य समस्या आहे.
खात्री करण्यासाठी तज्ज्ञांना विचारा."
```

Avoid presenting uncertain AI analysis as a confirmed diagnosis.

---

## 13. Human Expert Escalation

Human escalation is a core product capability, not an optional error state.

### MVP approach

Do not build a complicated expert marketplace initially.

Start with a simple case system:

```text
Farmer
   ↓
"तज्ज्ञांना विचारा"
   ↓
Create Case
   ↓
Photo
+ Crop
+ Location
+ Question
+ AI context
   ↓
Expert Dashboard
   ↓
Expert Response
```

### `expert_requests` concept

```text
id
farmer_id
crop_id
question
photo_url
location
status
created_at
expert_response
```

Possible statuses:

```text
pending
assigned
in_review
answered
closed
```

---

## 14. Location

Use the browser's **Geolocation API** initially.

```text
Latitude
Longitude
    ↓
Weather service
    ↓
Local weather
```

Later, a maps/places provider can be added for:

- Nearest Krushi Seva Kendra
- Nearby experts
- Local agricultural services

Do not introduce a maps platform until this functionality is actually required.

---

## 15. Market Prices

Market information should be handled as verified data.

Recommended architecture:

```text
Verified Market Source
        ↓
Backend
        ↓
Database / Cache
        ↓
Farmer
```

AI can explain the data, but should not invent prices.

User-facing market information should include:

- Price
- Source
- Date/time
- Relevant market/centre
- Context where available

Avoid presenting a market price as a guaranteed future price.

---

## 16. Government Schemes

Use official government sources as the source of truth.

Architecture:

```text
Official Government Source
          ↓
ShetiRakshak
          ↓
Plain Marathi explanation
          ↓
Eligibility
Documents
Deadline
Official link
```

The AI layer can simplify and explain the information, but should not become the authoritative source for scheme eligibility or deadlines.

---

## 17. Offline / Weak Network

The MVP should support a practical offline-first direction without building a complicated offline system.

Use:

```text
PWA
+
Service Worker
+
IndexedDB
```

Initially cache:

- App shell
- Last weather information
- Last crop information
- Important recent advice
- Relevant timestamps

Example:

> **"इंटरनेट नाही. शेवटची माहिती दाखवत आहोत."**

Always show when the information was last updated.

---

## 18. Hosting

### Frontend

**Vercel**

Use for:

- React/Vite production build
- Easy deployment
- Git-based deployments

### Backend

**Render**

Use for:

- Node.js/Express API
- Environment variables
- Simple deployment

### Database

**Supabase**

This keeps the infrastructure small:

```text
Vercel
  ↓
Frontend

Render
  ↓
Backend

Supabase
  ↓
Database + Auth + Storage
```

---

## 19. Environment Variables

Example:

```text
# Frontend
VITE_SUPABASE_URL=
VITE_SUPABASE_ANON_KEY=

# Backend
WEATHER_API_KEY=
GEMINI_API_KEY=
```

### Security rules

- Never commit `.env` files
- Never expose secret backend API keys in React
- Keep `.env` in `.gitignore`
- Use environment variables in production
- Use server-side calls for secret API credentials

---

## 20. Suggested Core App Sections

The first version should focus on:

```text
🌾 ShetiRakshak

├── 🏠 Home
├── 🌦️ Weather
├── 🌱 My Crop
├── 📷 Crop Problem
├── 🎙️ Voice
├── 🏛️ Schemes
├── 💰 Market
└── 👨‍🌾 Expert Help
```

The Home screen should prioritize:

```text
1. Today's One Thing
2. Persistent Voice Button
3. Crop Watch
4. Next 3 Days
5. Relevant Deadlines
6. Get Help
```

Do not put long scheme directories, large price tables or feeds on the default home screen.

---

## 21. Recommended MVP Architecture

```text
                         FARMER
                           │
                           ▼
                 ┌──────────────────┐
                 │ React + Vite     │
                 │ Tailwind CSS     │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ Node + Express   │
                 └────────┬─────────┘
                          │
          ┌───────────────┼────────────────┐
          │               │                │
          ▼               ▼                ▼
     ┌─────────┐     ┌──────────┐     ┌─────────┐
     │Supabase │     │WeatherAPI│     │ Gemini  │
     │         │     │          │     │         │
     └─────────┘     └──────────┘     └─────────┘
          │
          ├── PostgreSQL
          ├── Auth
          └── Storage
```

---

## 22. Project Folder Structure

Recommended repository:

```text
sheti-rakshak/
│
├── frontend/
│   ├── src/
│   ├── public/
│   └── package.json
│
├── backend/
│   ├── routes/
│   ├── services/
│   ├── middleware/
│   ├── utils/
│   ├── server.js
│   └── package.json
│
├── README.md
├── .gitignore
└── .env.example
```

Keep the first repository small and understandable.

---

## 23. Development Phases

### Phase 1 — MVP

Implement:

```text
React
Vite
Tailwind
Node
Express
Supabase
WeatherAPI
Gemini
Web Speech API
SpeechSynthesis
```

Core features:

- Marathi UI
- Home dashboard
- Weather
- Crop profile
- Basic crop problem flow
- Voice interaction
- Basic expert request
- Source/date/confidence display

### Phase 2

Add:

```text
PWA
IndexedDB
Better Marathi speech services
Expert dashboard
Government source integrations
Market integrations
Notifications
```

### Phase 3

Only when real usage justifies them:

```text
Advanced crop vision
Dedicated AI services
Notification infrastructure
Analytics
Native Android application
```

### Phase 4 — Scale

Only when necessary:

```text
TypeScript migration
Redis
Queues
Specialized services
More advanced cloud infrastructure
```

---

## 24. What NOT to Build Yet

Avoid:

```text
❌ Microservices
❌ Kubernetes
❌ Kafka
❌ Redis
❌ Docker-first architecture
❌ Separate Python AI server
❌ Vector database
❌ LangChain
❌ Complex AWS architecture
❌ Custom authentication system
❌ Custom file-storage system
❌ Custom voice infrastructure
❌ Large expert marketplace
```

These can be introduced later if actual product requirements justify them.

---

## 25. Product-to-Technology Mapping

| Brand Requirement | Technical Solution |
|---|---|
| Marathi-first | React UI + Mukta/Noto Sans Devanagari |
| Voice-first | Web Speech API + SpeechSynthesis initially |
| Weather guidance | WeatherAPI + application rules |
| Crop guidance | Photo upload + AI + expert escalation |
| Human backup | Expert request workflow |
| Source transparency | Database fields + Trust Strip |
| Confidence | Application-level confidence states |
| Weak networks | PWA + IndexedDB + cached data |
| Low-bandwidth | Compressed images + lightweight UI |
| Official schemes | Verified government sources |
| Market transparency | Source/date-backed market records |
| Simple UX | React component system |
| Brand consistency | Tailwind design tokens |
| Scalability | Modular frontend/backend structure |
| Privacy | Supabase security + explicit consent |

---

## 26. Core Engineering Rules

### Rule 1 — Data before AI

If a fact can come from a verified source, retrieve the fact from the source first.

### Rule 2 — AI explains; it should not invent

AI should operate on verified/available context whenever possible.

### Rule 3 — Every important answer has a next step

```text
What is happening?
        ↓
What does it mean?
        ↓
What should I do next?
        ↓
How confident are we?
        ↓
Who can help?
```

### Rule 4 — Uncertainty is a feature

Use:

```text
High:
"ही शक्यता जास्त आहे"

Medium:
"ही एक शक्यता आहे"

Low:
"खात्री नाही; तज्ज्ञांना विचारा"
```

### Rule 5 — Human escalation is normal

Low confidence, severe/spreading symptoms, treatment-dose questions, or an explicit request should trigger human help rather than increasingly confident guessing.

### Rule 6 — Keep the Home screen calm

Do not add features just because they are technically possible.

### Rule 7 — Keep external services replaceable

Put WeatherAPI/Gemini calls behind backend service modules so providers can be changed later.

---

## 27. Final Decision

### LOCKED MVP STACK

```text
Frontend:
React + Vite

Styling:
Tailwind CSS

Icons:
Lucide React

Backend:
Node.js + Express

Database:
Supabase PostgreSQL

Auth:
Supabase Auth

Storage:
Supabase Storage

Weather:
WeatherAPI.com

AI:
Gemini API

Voice:
Web Speech API
SpeechSynthesis

Location:
Browser Geolocation API

Offline:
PWA + IndexedDB

Frontend Hosting:
Vercel

Backend Hosting:
Render

Version Control:
Git + GitHub

Language:
JavaScript
```

### Guiding principle

> **Simple code. Verified information. Clear next step. Human help when needed.**

This stack is intentionally small enough for the MVP to be developed and understood by one developer, while leaving clear upgrade paths when ShetiRakshak gains real users and real usage data.
