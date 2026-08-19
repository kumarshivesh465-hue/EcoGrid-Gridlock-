# EcoGrid — Smart Urban Mobility Platform

**EcoGrid** is a next-generation urban mobility platform that combines AI-powered multimodal journey planning with real-time gridlock prevention using OS-level deadlock detection algorithms. Built for sustainable, intelligent city transportation.

---

## 🎯 Overview

EcoGrid transforms urban mobility by treating city traffic as a **Resource Allocation Graph (RAG)** — applying operating system concepts like **Banker's Algorithm** and **DFS-based cycle detection** to prevent gridlock before it happens. The platform provides:

- **Multimodal Journey Planner** — Compare driving, metro, and carpooling with AI-powered insights
- **Gridlock Engine Dashboard** — Real-time deadlock detection & prevention simulation
- **Emergency Response Hub** — Priority routing for emergency vehicles
- **3D City Visualization** — Interactive Spline-powered urban environment

---

## ✨ Key Features

### 🗺️ Smart Journey Planner (`/planner`)
- **Multimodal routing**: Driving, Metro, Carpooling with live comparison
- **AI-powered insights**: Google Gemini generates contextual reroute recommendations
- **Priority modes**: Fastest, Cheapest, Greenest, Balanced
- **Carbon tracking**: CO₂ emissions & eco-points per route
- **Google Maps integration**: Live path visualization with deadlock hazard zones

### 🎮 Gridlock Engine Dashboard (`/dashboard`)
- **Real-time Resource Allocation Graph** — Intersections as resources, vehicles as processes
- **DFS Cycle Detection** — Identifies circular wait deadlocks in traffic flow
- **Banker's Safe State Simulator** — Pre-validates resource allocation before granting
- **Interactive simulation**: Trigger/break deadlocks, add traffic load, reset state
- **Firebase real-time sync** — Multi-client reactive state with local fallback

### 🚨 Emergency Response Hub (`/emergency`)
- Priority corridor routing for ambulances/fire trucks
- Live incident mapping with severity classification
- Traffic signal preemption simulation

### 🏠 Landing Page (`/`)
- 3D Spline cityscape with interactive traffic flow
- Live city intelligence ticker
- Gridlock theory explainer (OS deadlock ↔ traffic deadlock)
- Before/After interactive simulation
- AI Mobility Assistant widget

---

## 🧠 Core Algorithms

| Algorithm | Purpose | Implementation |
|-----------|---------|----------------|
| **DFS Cycle Detection** | Detect circular wait in intersection graph | `src/lib/cycleDetection.ts` |
| **Banker's Algorithm** | Safe-state validation before resource allocation | `src/lib/bankersAlgorithm.ts` |
| **Gemini AI Rerouting** | Context-aware multimodal recommendations | `src/lib/gemini.ts` + `/api/gemini/reroute` |

---

## 🛠️ Tech Stack

| Category | Technologies |
|----------|--------------|
| **Framework** | Next.js 15 (App Router), React 19, TypeScript |
| **Styling** | Tailwind CSS, Framer Motion, clsx + tailwind-merge |
| **3D/Viz** | Spline (@splinetool/react-spline), Custom Canvas visualizers |
| **AI** | Google Generative AI (Gemini 1.5 Flash), @google/genai |
| **Backend** | Firebase (Firestore real-time), Next.js API Routes |
| **Maps** | Google Maps JavaScript API |
| **Auth** | Firebase Auth (Email/Password, Google OAuth) |
| **Deployment** | Vercel / GitHub Pages (`gh-pages` branch) |
| **Quality** | ESLint 9, TypeScript strict mode |

---

## 📁 Project Structure

```
ecogrid/
├── src/
│   ├── app/
│   │   ├── page.tsx              # Landing page
│   │   ├── planner/page.tsx      # Multimodal journey planner
│   │   ├── dashboard/page.tsx    # Gridlock engine dashboard
│   │   ├── emergency/page.tsx    # Emergency response hub
│   │   ├── api/gemini/reroute/   # Gemini AI reroute endpoint
│   │   └── layout.tsx            # Root layout + providers
│   ├── components/
│   │   ├── hero/                 # 3D Spline hero section
│   │   ├── landing/              # Landing page sections
│   │   ├── planner/              # Planner UI components
│   │   ├── dashboard/            # Dashboard widgets & visualizers
│   │   ├── emergency/            # Emergency dashboard
│   │   ├── layout/               # Navbar, Footer
│   │   └── auth/                 # Auth modal & provider
│   ├── lib/
│   │   ├── cycleDetection.ts     # DFS deadlock detection
│   │   ├── bankersAlgorithm.ts   # Banker's safe state check
│   │   ├── gemini.ts             # Client-side Gemini integration
│   │   ├── firebase.ts           # Firebase config & auth
│   │   └── mockData.ts           # Intersection graph & route data
│   └── types/index.ts            # TypeScript interfaces
├── public/                       # Static assets
├── next.config.ts                # Next.js configuration
└── package.json
```

---

## 🚀 Getting Started

### Prerequisites
- Node.js 18+
- npm / pnpm / yarn
- Firebase project (for real-time sync)
- Google Cloud project (Maps API + Gemini API)

### Installation

```bash
# Clone the repository
git clone https://github.com/kumarshivesh465-hue/EcoGrid-Gridlock-.git
cd EcoGrid-Gridlock-

# Install dependencies
npm install

# Copy environment template
cp .env.example .env.local
```

### Environment Variables

```env
# Firebase
NEXT_PUBLIC_FIREBASE_API_KEY=
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=
NEXT_PUBLIC_FIREBASE_PROJECT_ID=
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=
NEXT_PUBLIC_FIREBASE_APP_ID=

# Google Maps
NEXT_PUBLIC_GOOGLE_MAPS_API_KEY=

# Gemini AI
GEMINI_API_KEY=
NEXT_PUBLIC_GEMINI_API_KEY=
```

### Development

```bash
# Start dev server
npm run dev

# Run linting
npm run lint

# Type checking
npx tsc --noEmit
```

Open [http://localhost:3000](http://localhost:3000) to view the app.

---

## 📦 Deployment

### Vercel (Recommended)
```bash
# Connect repo to Vercel, add env vars, deploy
vercel
```

### GitHub Pages
```bash
# Build & deploy to gh-pages branch
npm run deploy
```

---

## 🔬 How It Works

### Traffic as a Resource Allocation Graph
Each intersection is a **resource** with capacity. Each vehicle route is a **process** requesting resources. When vehicles form a circular wait (A→B, B→C, C→A), a **deadlock** = **gridlock**.

### Deadlock Prevention Pipeline
```
1. Monitor intersection loads in real-time (Firestore / local state)
2. Run DFS cycle detection on Resource Allocation Graph
3. If cycle found → Banker's Algorithm validates safe sequences
4. If unsafe → AI suggests preemption (reroute, signal priority)
5. Apply resolution → Update graph → Sync to all clients
```

---

## 🤝 Contributing

1. Fork the repository
2. Create feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m 'Add amazing feature'`
4. Push branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.

---

## 🙏 Acknowledgments

- **Next.js Team** — For the incredible App Router
- **Google AI** — Gemini for multimodal intelligence
- **Spline** — For accessible 3D web experiences
- **Firebase** — Real-time sync made simple
- **Operating Systems Concepts** — Silberschatz, Galvin, Gagne (inspiration for deadlock modeling)

---

## 📞 Contact

**Shivesh Kumar** — [@kumarshivesh465](https://github.com/kumarshivesh465-hue)

Project Link: [https://github.com/kumarshivesh465-hue/EcoGrid-Gridlock-](https://github.com/kumarshivesh465-hue/EcoGrid-Gridlock-)

---

> **EcoGrid** — Where OS theory meets urban mobility. 🌿🚦