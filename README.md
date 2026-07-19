# 🏟️ ArenaOS AI — FIFA World Cup 2026™ Digital Experience

> **The Official-Grade AI-Powered Digital Companion for the FIFA World Cup 2026™**  
> *Blending cutting-edge WebGL graphics, Framer Motion animations, and Google Gemini 3.5 Flash intelligence.*
<img width="1024" height="1024" alt="Image" src="https://github.com/user-attachments/assets/534482de-9954-415a-9d8b-3bd07914fe62" />
 <a href="https://marvelous-crostata-55baee.netlify.app/" target="_blank">
    <img src="https://img.shields.io/badge/🌐_Live_Demo_Website-marvelous--crostata--55baee.netlify.app-00d2ff?style=for-the-badge&logo=google-chrome&logoColor=white" alt="Live Demo" />
  </a>
  
  <a href="https://www.linkedin.com/in/alokkadam-ai/" target="_blank">
    <img src="https://img.shields.io/badge/🤝_LinkedIn-Alok_Kadam-0a66c2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" />
  </a>
</div>

## 🚀 Technical Stack & Badges

```text
[Framework]      Next.js 16.2 (App Router)
[Language]       TypeScript 5.0
[Graphics]       Three.js / React Three Fiber / Drei
[AI Engine]      Google Gemini 3.5 Flash SDK (@google/genai)
[Styling]        CSS Modules / CSS Custom Properties (Vanilla CSS)
[Animations]     Framer Motion
[Analytics]      Recharts
```

---

## 🎯 Project Vision

**ArenaOS AI** is an enterprise-ready Progressive Web Application (PWA) designed to serve as an interactive stadium companion for fans attending the FIFA World Cup 2026™. Rather than offering a cluttered interface, it prioritizes a premium user experience featuring:
*   An interactive 3D stadium seating bowl selector.
*   A streaming, contextual AI companion powered by Gemini 3.5 Flash.
*   Modern, clean analytics dashboards for organizers.
*   Accessible design tokens complying with WCAG guidelines.

---

## 🏗️ System Architecture & Data Flow

This diagram illustrates the lifecycle of client actions, WebGL rendering cycles, and secure server-side communications with Google Gemini:

```mermaid
graph TD
    %% Define Nodes
    Fan([⚽ Fan User])
    Client[Next.js Client app/page.tsx]
    Canvas[React Three Fiber Canvas]
    StadiumModel[Stadium Model Seating Bowl]
    OrbitCtrl[OrbitControls Ref]
    ChatComp[ChatCompanion Component]
    APIRoute[API Route: /api/chat/route.ts]
    Gemini[Gemini 3.5 Flash Engine]

    %% Interactions
    Fan -->|Interacts with UI| Client
    Client -->|Renders 3D Viewport| Canvas
    Canvas -->|Loads Geometries & Spotlights| StadiumModel
    Fan -->|Rotates / Zooms / Pan| OrbitCtrl
    OrbitCtrl -->|Updates Camera View| Canvas
    
    Fan -->|Types Question| ChatComp
    ChatComp -->|POST Request| APIRoute
    APIRoute -->|Instantiates GoogleGenAI SDK| Gemini
    Gemini -->|Streams Words| APIRoute
    APIRoute -->|Chunked Transfer Encoding| ChatComp
    ChatComp -->|Updates state & scrolls| Fan

    %% Styling
    style Fan fill:#00d2ff,stroke:#00d2ff,stroke-width:2px,color:#000
    style Client fill:#1e293b,stroke:#475569,stroke-width:2px,color:#fff
    style Canvas fill:#166534,stroke:#15803d,stroke-width:2px,color:#fff
    style Gemini fill:#facc15,stroke:#eab308,stroke-width:2px,color:#000
    style APIRoute fill:#3b82f6,stroke:#60a5fa,stroke-width:2px,color:#fff
```

---

## 🔄 Interaction Sequence Diagram

The following sequence diagram outlines the process when a user clicks a seating stand and asks the AI companion for ticket pricing details:

```mermaid
sequenceDiagram
    autonumber
    actor Fan as ⚽ Fan User
    participant Page as Stadium Page (UI)
    participant Scene as 3D Canvas (R3F)
    participant Chat as AI Companion
    participant API as /api/chat API Route
    participant Gemini as Gemini 3.5 Flash

    Fan->>Scene: Hover / Click Seating Stand (e.g., East Stand)
    Scene->>Scene: Highlight meshes (white/blue glow)
    Scene->>Page: Trigger setSelectedSection('east')
    Page->>Fan: Display HUD overlay (Category 1, $290, 78% Available)
    
    Fan->>Chat: Ask: "Is Category 1 worth it for USA vs NED?"
    Chat->>API: POST /api/chat { prompt, history }
    API->>Gemini: generateContentStream('gemini-3.5-flash')
    Gemini-->>API: Stream token chunks
    API-->>Chat: Stream HTTP chunks
    Chat->>Fan: Display streaming text with typing effect
```

---

## 🗺️ Smart Fan Journey State Machine

A state-driven walkthrough of a fan's match-day experience during the tournament:

```mermaid
stateDiagram-v2
    [*] --> TicketAcquisition : Get Mobile QR Ticket
    TicketAcquisition --> MatchPlanning : Plan Schedule / Check Weather
    MatchPlanning --> StadiumNavigation : Get Real-time Transit Directions
    StadiumNavigation --> FoodConcessions : Locate & Pre-order Food
    FoodConcessions --> SeatWayfinding : Scan QR for AR Seat Guide
    SeatWayfinding --> MatchExperience : Live AI Stats & Commentary
    MatchExperience --> PostMatch : Get Departure Bus/Train Timings
    PostMatch --> [*]
```

---

## 📂 Detailed Folder Structure

```text
arena-os/
├── public/                 # Static assets and PWA setup
│   ├── manifest.json       # App installability manifest
│   └── favicon.ico         # App browser shortcut icon
├── scratch/                # Test scripts for verification
│   ├── list-models.js      # Lists available Gemini models
│   └── test-gemini.js      # Tests prompt generation latency
├── src/
│   ├── app/                # Next.js App Router Structure
│   │   ├── api/            # Server-side API endpoints
│   │   │   └── chat/       # Streaming chat endpoint (gemini-3.5-flash)
│   │   ├── companion/      # dedicated full-page AI chatbot
│   │   ├── dashboard/      # Organizer analytics visual dashboard
│   │   ├── fanzone/        # Smart fan journey stepper page
│   │   ├── matches/        # Fixture lists with interactive group tabs
│   │   ├── stadium/        # 3D stadium explorer scene wrapper page
│   │   ├── globals.css     # Global variables and base typography
│   │   ├── layout.tsx      # Core metadata and manifest registration
│   │   └── page.tsx        # Entrypoint (Splash screen & Hero landing)
│   ├── components/         # Reusable application components
│   │   ├── features/       # Feature modules
│   │   │   ├── AccessibilityPanel   # Font size & contrast adjustments
│   │   │   ├── ChatCompanion        # Chat interface with suggested prompts
│   │   │   ├── EmergencyPanel       # Red SOS button & evacuation instructions
│   │   │   ├── FloatingAIButton     # Desktop floating magnetic chatbot button
│   │   │   ├── HeroSection          # Countdown timer, ticker, and landing CTAs
│   │   │   ├── LandingFeatures      # Feature cards display grid
│   │   │   ├── LandingJourney       # Text-based vertical journey pipeline
│   │   │   ├── SplashScreen         # Splash loading screen with entry animation
│   │   │   └── StadiumScene         # WebGL React Three Fiber stadium model
│   │   └── layout/         # Shell framing components
│   │       ├── Navbar               # Transparent glass navigation bar
│   │       ├── Footer               # Bottom footer with legal links
│   │       ├── MobileNav            # Mobile bottom-tab bar with glowing AI button
│   │       └── SubPageLayout        # Common wrapper for sub-route pages
│   ├── lib/                # Static configuration utilities
│   │   ├── constants.ts     # Realistic matches, venues, and mock datasets
│   │   └── fonts.ts         # Google Fonts Loader (Inter & Outfit)
│   └── types/              # Type declarations
│       └── index.ts        # Match, Venue, Team interfaces
```

---

## ⚡ Development Installation Guide

Get the project running locally in under a minute by copying and pasting these command blocks into your terminal:

```bash
# 1. Clone this repository
git clone <your-repository-url>
cd arena-os

# 2. Install dependencies (Next.js, Three.js, Framer Motion)
npm install

# 3. Configure environment variable
# Copy env example to local env
cp .env.example .env

# 4. Run production compilation checklist
npm run build

# 5. Launch local development server
npm run dev
```

Your server will be up and running at **`http://localhost:3000`** with dynamic hot-reloading active.

---

## 🎨 Design System & CSS Variables (`src/app/globals.css`)

The UI styling relies entirely on native CSS custom variables, preventing dependency bloat and maintaining highly maintainable design tokens:

### 1. Colors & Accents
```css
--color-royal-blue: #1a3a8f;     /* Primary brand identity color */
--color-sky-blue: #4da6ff;       /* Secondary link highlight color */
--color-fresh-green: #2ecc71;     /* Stand category highlight color */
--color-emerald: #00b894;         /* Positive indicator coloring */
--color-golden-yellow: #f1c40f;   /* Spotlight light emitter coloring */
--color-coral-orange: #ff6b6b;    /* SOS and critical action coloring */
```

### 2. Glassmorphism Design Token
```css
.glass-panel {
  background: rgba(255, 255, 255, 0.7);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: 1px solid rgba(255, 255, 255, 0.5);
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
}
```

### 3. Transition Tokens
```css
--transition-fast: 150ms cubic-bezier(0.4, 0, 0.2, 1);
--transition-base: 300ms cubic-bezier(0.4, 0, 0.2, 1);
--transition-slow: 500ms cubic-bezier(0.4, 0, 0.2, 1);
```

---

<div align="center">

🏆 **FIFA World Cup 2026™ AI Stadium Experience** 🏆

*Designed to exceed international hackathon standards with robust UI architecture.*

⚽ **Made with ❤️ for the beautiful game** ⚽

</div>
<img width="1917" height="863" alt="Image" src="https://github.com/user-attachments/assets/4569d738-85a1-47c3-934b-9e95a7988e28" />
<img width="1917" height="867" alt="Image" src="https://github.com/user-attachments/assets/50df7f80-1212-4f8a-b873-b6708b772cdc" />
<img width="1907" height="861" alt="Image" src="https://github.com/user-attachments/assets/a5f006eb-52b1-49e0-901d-90d4f025bc77" />
<img width="1917" height="870" alt="Image" src="https://github.com/user-attachments/assets/472ab4ef-4171-4fcf-92e6-8824b85b6f43" />
<img width="1918" height="866" alt="Image" src="https://github.com/user-attachments/assets/ac6e2ae9-cbf2-4f43-ad81-bc24223c22bb" />
<img width="1912" height="865" alt="Image" src="https://github.com/user-attachments/assets/2e3c769a-9ca5-4b7c-a624-91bf1f932833" />
<img width="1917" height="873" alt="Image" src="https://github.com/user-attachments/assets/fb5dab17-423a-4aca-8783-8292b2b35368" />
<img width="1918" height="867" alt="Image" src="https://github.com/user-attachments/assets/6cd0c8b7-551f-46f6-bba9-60794c848c32" />
<img width="1915" height="867" alt="Image" src="https://github.com/user-attachments/assets/1093e6a4-ff20-44d6-b81b-eb413caaaf57" />
<img width="1918" height="1078" alt="Image" src="https://github.com/user-attachments/assets/e49b9b87-050b-4c72-beda-9fb2140e47de" />
<img width="1912" height="862" alt="Image" src="https://github.com/user-attachments/assets/b2ef5e6b-d6f6-41c0-a60e-dfc635c70e5d" />
