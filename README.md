# Travia Egypt — Budget-First AI Travel Platform

A production-ready full-stack application for planning budget-conscious trips to Egypt.

## 🏗 Architecture

```
travia-egypt/
├── apps/
│   ├── web/                    # Next.js 14 + TypeScript + Tailwind (Port 3000)
│   ├── api-gateway/            # NestJS API Gateway (Port 3000)
│   ├── auth-service/           # NestJS Auth + JWT (Port 3001)
│   ├── trip-engine/            # NestJS Trip Orchestration (Port 3002)
│   ├── transport-service/      # Egypt Flights & Buses (Port 3003)
│   ├── hotel-service/          # Egypt Hotels (Port 3004)
│   ├── activities-service/     # Egypt Experiences (Port 3005)
│   └── ai-service/             # OpenAI + Budget Engine (Port 3006)
├── packages/
│   ├── database/               # Prisma ORM + Schema
│   └── shared/                 # Shared types, constants, utils
└── docker-compose.yml          # PostgreSQL + Redis
```

## 🚀 Quick Start

### 1. Prerequisites
- Node.js 18+
- Docker & Docker Compose
- OpenAI API key

### 2. Setup
```bash
# Clone and install
npm install

# Copy environment
cp .env.example .env
# Edit .env with your OpenAI API key

# Start databases
docker compose up -d

# Generate Prisma client and push schema
cd packages/database
npm run db:generate
npm run db:push
npm run db:seed

# Run all services
cd ../..
npm run dev
```

### 3. Access
- **Frontend**: http://localhost:3000
- **API Gateway**: http://localhost:3000/api
- **Auth Service**: http://localhost:3001/api/auth
- **Trip Engine**: http://localhost:3002/api/trips
- **Transport**: http://localhost:3003/api/transport
- **Hotels**: http://localhost:3004/api/hotels
- **Activities**: http://localhost:3005/api/activities
- **AI Service**: http://localhost:3006/api/ai

## 📱 UI Screens

1. **Onboarding** — Intro + Budget input (min $100)
2. **Destination Selection** — Cairo, Luxor, Aswan, Hurghada, Sharm El Sheikh, Alexandria + "Anywhere"
3. **Date Selection** — Departure + Return with validation
4. **Traveler Info** — Count + type (Solo/Couple/Family/Group)
5. **Preferences** — Multi-select interests (max 5)
6. **AI Generation** — Animated loading with steps
7. **Package Comparison** — Budget/Standard/Luxury plans
8. **Transport Selection** — Flights + buses with budget tracker
9. **Hotel Selection** — Tiered hotels with budget tracker
10. **Activities** — Experiences with real-time cost
11. **Trip Summary** — Full itinerary + budget breakdown
12. **AI Assistant** — Chat interface for trip planning
13. **Auth** — Login, Signup
14. **Profile** — User info + saved trips

## 🗄 Database

PostgreSQL with Prisma ORM. Tables:
- Users, Trips, TripPlans, TripStops
- Destinations (Egypt only)
- Transport, Hotels, Activities
- Bookings, Conversations, AiSessions

## 🤖 AI Logic

Budget allocation per plan type:
| Plan | Transport | Hotel | Activities |
|------|-----------|-------|------------|
| Budget | 25% | 50% | 25% |
| Standard | 30% | 45% | 25% |
| Luxury | 35% | 40% | 25% |

OpenAI GPT-4o-mini generates:
- Recommended itineraries
- Per-destination activity suggestions
- Travel tips specific to Egypt

## 🔑 API Endpoints

### Auth
- `POST /api/auth/register` — Register
- `POST /api/auth/login` — Login
- `GET /api/auth/profile` — Get profile (JWT)
- `PUT /api/auth/profile` — Update profile (JWT)

### Transport
- `GET /api/transport` — All transport
- `GET /api/transport/search?from=Cairo&to=Luxor` — Search
- `GET /api/transport/by-type?type=FLIGHT` — Filter by type

### Hotels
- `GET /api/hotels` — All hotels
- `GET /api/hotels/destination/:id` — By destination
- `GET /api/hotels/tier/:tier` — By tier

### Activities
- `GET /api/activities` — All activities
- `GET /api/activities/destination/:id` — By destination
- `GET /api/activities/top-rated` — Top rated

### Trips
- `POST /api/trips/create` — Create trip
- `POST /api/trips/:id/generate` — Generate AI plans
- `PUT /api/trips/:id/select-plan` — Select plan
- `GET /api/trips/:id` — Get trip
- `PUT /api/trips/:id/confirm` — Confirm trip

### AI
- `POST /api/ai/generate-trip` — Generate trip plan
- `POST /api/ai/chat` — AI assistant chat

## 🧪 Test Account

After seeding:
- **Email**: test@travia.egypt
- **Password**: Test1234!

## 📦 Tech Stack

**Frontend**: Next.js 14, TypeScript, Tailwind CSS, Zustand, Axios, Lucide Icons
**Backend**: NestJS, Prisma, PostgreSQL, Passport JWT, OpenAI API
**Infrastructure**: Docker Compose, Turborepo monorepo

## 🎯 Key Features

- Egypt-only destinations (Cairo, Luxor, Aswan, Hurghada, Sharm El Sheikh, Alexandria)
- Budget-first planning with real-time budget tracking
- AI-powered trip generation with OpenAI
- Three plan tiers: Budget, Standard, Luxury
- Transport comparison (flights + buses)
- Hotel selection with tier filtering
- Activity multi-select with category filters
- AI chat assistant for trip recommendations
- User authentication and profile management
- Responsive, production-ready UI
