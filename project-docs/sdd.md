# System Design Document (As-Built Implementation)

> **Living Document**: This SDD documents the **actual implementation** of Bigfoot War as it is built. It is updated incrementally during development to reflect what was actually implemented, which may differ from the design intent documented in the GDD.

## How to Use This Document

**For Development:**
- Reference GDD Technical Design section for design intent and architecture decisions
- Update this SDD as you implement features to document actual implementation
- Use code examples, file paths, and actual configurations (not just descriptions)

**For AI-Assisted Development:**
- **Prompt Engineering**: Feed AI specific excerpts from GDD/SDD (e.g., "Implement the Main Game Flow using Next.js, based on this GDD section: [paste]").
- **Iteration**: Use AI for prototypes, then validate against SDD for consistency.
- **Version Control**: Commit AI-generated code with comments referencing SDD sections to maintain auditability.
- **Limitations**: AI excels at patterns/best practices but may hallucinate; always cross-check with your docs and test.

---

## 1. Introduction and Scope

### Purpose
This document provides **as-built documentation** of the Bigfoot War system, documenting what was actually implemented rather than design intent. It serves as:
- Implementation reference for developers
- Onboarding guide for new team members
- Technical documentation for maintenance and debugging
- Record of implementation decisions and trade-offs

### Scope
This SDD covers:
- **Frontend/Backend**: Actual code structure, components, API implementations
- **Data Models**: Actual schemas, TypeScript interfaces, Prisma models
- **Deployment**: Actual configuration files, CI/CD setup, environment variables
- **Integration**: Actual implementation of external services (Stripe, AdMob, Clerk)
- **Testing**: Actual test structure, coverage, and automation

**Out of Scope:**
- Gameplay rules and mechanics (see GDD)
- Game design decisions (see GDD)
- Asset creation process (see GDD Content and Assets section)

### Relationship to GDD

**GDD Technical Design** (lines 8000-8528) describes:
- **Design Intent**: "We plan to use Zustand for state management"
- **Architecture Decisions**: "Why we chose Canvas API over WebGL"
- **Performance Targets**: "Target 60fps, <1MB initial bundle"

**This SDD** documents:
- **Actual Implementation**: "Zustand store implemented in `stores/gameStore.ts` with structure: [code]"
- **Code Structure**: "Canvas rendering implemented in `components/game/CardRenderer.tsx`"
- **Real Configuration**: "Performance achieved: [actual metrics]"

**When Implementation Differs from Design:**
- Document the difference in this SDD
- Note why the change was made
- Reference the GDD section for comparison

### References
- **GDD**: `project-docs/gdd.md` - Game Design Document (design intent)
- **Technical Design**: `project-docs/gdd.md` lines 8000-8528 - Technical architecture and decisions
- **External Docs**: 
  - [Next.js Documentation](https://nextjs.org/docs)
  - [Vercel Documentation](https://vercel.com/docs)
  - [Zustand Documentation](https://github.com/pmndrs/zustand)
  - [Prisma Documentation](https://www.prisma.io/docs)

### Version History
- **v0.1** - Initial SDD structure (pre-implementation)
- _[Add version entries as implementation progresses]_

### Glossary
- **Warlord Special**: Unique ability per Warlord, implemented as `WarlordPower` component with charge tracking
- **Suit Special**: Ability triggered by capturing X cards of a suit, implemented in `specialSystem.ts`
- **Signature Card**: Unique card per Warlord with special effect, implemented in `cardSystem.ts`
- **Battle Item**: Consumable item purchased with Gold, implemented in `battleItemSystem.ts`
- _[Add technical definitions as implementation progresses]_

---

## 2. System Overview

### High-Level Architecture

**Architecture Type**: Monolithic Next.js application with client-side game logic and serverless API routes

**Key Characteristics:**
- Single-page application (SPA) with Next.js App Router
- Client-side game logic (no server-side game state)
- Serverless API routes for cloud sync, payments, leaderboards
- Local-first design (fully playable offline)

### Architecture Diagram

```
┌─────────────────────────────────────────────────────────┐
│                    Client Browser                       │
│  ┌──────────────────────────────────────────────────┐  │
│  │         Next.js App (React + Canvas)              │  │
│  │  ┌──────────────┐  ┌──────────────┐             │  │
│  │  │ Game Table   │  │   Overlays   │             │  │
│  │  │ Component    │  │  (Modals)    │             │  │
│  │  └──────────────┘  └──────────────┘             │  │
│  │  ┌──────────────────────────────────────────┐   │  │
│  │  │      Zustand Store (Game State)          │   │  │
│  │  └──────────────────────────────────────────┘   │  │
│  │  ┌──────────────────────────────────────────┐   │  │
│  │  │   IndexedDB (Game Data)                  │   │  │
│  │  │   localStorage (Preferences)              │   │  │
│  │  └──────────────────────────────────────────┘   │  │
│  └──────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
                          ↕ HTTP/HTTPS
┌─────────────────────────────────────────────────────────┐
│              Vercel Serverless Functions                 │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐            │
│  │ /api/    │  │ /api/    │  │ /api/    │            │
│  │ sync     │  │ checkout │  │ leader-  │            │
│  │          │  │          │  │ boards  │            │
│  └──────────┘  └──────────┘  └──────────┘            │
└─────────────────────────────────────────────────────────┘
                          ↕
┌─────────────────────────────────────────────────────────┐
│              External Services                          │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐            │
│  │ Stripe   │  │ AdMob    │  │ Clerk    │            │
│  │ (Pay)    │  │ (Ads)    │  │ (Auth)   │            │
│  └──────────┘  └──────────┘  └──────────┘            │
└─────────────────────────────────────────────────────────┘
                          ↕
┌─────────────────────────────────────────────────────────┐
│              Vercel Infrastructure                     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐            │
│  │ Postgres │  │ KV       │  │ Edge     │            │
│  │ (DB)     │  │ (Redis)   │  │ (CDN)    │            │
│  └──────────┘  └──────────┘  └──────────┘            │
└─────────────────────────────────────────────────────────┘
```

**TODO**: Create detailed architecture diagram using Draw.io or similar tool

### Key Components

**Frontend Components:**
- **GameTable**: Persistent component handling pre-game/in-game/post-game states
- **Overlays**: Custom modal system (no external library)
- **State Management**: Zustand store for game state
- **Canvas Renderer**: Card animations and pixel art rendering

**Backend Components:**
- **API Routes**: Next.js serverless functions
- **Database**: Vercel Postgres (Prisma ORM)
- **Cache**: Vercel KV (Redis) for sessions, rate limiting, leaderboards

**External Integrations:**
- **Stripe**: Payment processing
- **AdMob**: Ad serving
- **Clerk**: Authentication (paid users only)

---

## 3. Constraints and Assumptions

### Technical Constraints

**Browser Compatibility:**
- **Target Browsers**: Chrome, Firefox, Safari, Edge (latest 2 versions)
- **Mobile-First**: Optimized for portrait mobile devices (320-480px base)
- **No Install Required**: Progressive Web App (PWA) capabilities, but no app store requirement
- **Feature Detection**: Graceful degradation for unsupported features (e.g., haptics)

**Platform Constraints:**
- **No Native Apps**: Web-only, no iOS/Android native apps
- **Serverless**: No always-on server, all backend via Vercel Functions
- **Storage Limits**: 
  - IndexedDB: ~50% disk space (minimum 10MB)
  - localStorage: 5-10MB per origin
  - Mitigation: Quota checking and user warnings

### Non-Functional Requirements

**Performance Targets** (from GDD Technical Design):
- **Bundle Size**: <1MB initial bundle (gzipped), <5MB total
- **Load Time**: <3s Time to Interactive (3G connection)
- **Frame Rate**: Target 60fps (minimum 30fps on low-end devices)
- **Memory**: <50MB on mobile devices
- **Lighthouse Score**: 90+ mobile performance score

**Budget Constraints:**
- **Hosting**: Vercel free tier initially, scale to paid as needed
- **Database**: Vercel Postgres (paid tier for production)
- **CDN**: Vercel Edge Network (included)
- **External Services**: Stripe, AdMob, Clerk (pay-as-you-go)

### Assumptions

**User Behavior:**
- Users have modern browsers with JavaScript enabled
- Users accept cookies/localStorage (required for game data)
- Users have internet connection for initial load (offline play after)
- Users understand card game mechanics (no tutorial required)

**Technical Assumptions:**
- Vercel infrastructure is reliable (99.9% uptime)
- External services (Stripe, AdMob, Clerk) are available
- Browser APIs (Canvas, IndexedDB, Vibration) are supported
- Mobile devices can handle 60fps Canvas rendering

### Risks and Mitigations

**Risk**: LocalStorage quota exceeded
- **Mitigation**: Use IndexedDB for game data, localStorage only for preferences
- **Fallback**: Warn user, offer cloud sync upgrade

**Risk**: Browser doesn't support required APIs
- **Mitigation**: Feature detection, graceful degradation
- **Fallback**: Show compatibility message, suggest different browser

**Risk**: Network failure during critical operations
- **Mitigation**: Offline-first design, local state persistence
- **Fallback**: Queue API calls, retry when online

**Risk**: Performance issues on low-end devices
- **Mitigation**: Frame skipping, adaptive quality, object pooling
- **Fallback**: Reduce to 30fps target, disable particle effects

**Risk**: Data loss (browser data cleared)
- **Mitigation**: Cloud sync for paid users, clear warnings for free users
- **Fallback**: Encourage cloud sync upgrade

---

## 4. Code Structure

### Project Structure

```
bfw-2025/
├── app/                          # Next.js App Router
│   ├── page.tsx                 # Main game page (GameTable component)
│   ├── share/
│   │   └── [id]/
│   │       └── page.tsx          # Share link page (SSR)
│   ├── api/                      # API routes
│   │   ├── checkout/
│   │   │   └── route.ts         # Stripe checkout session
│   │   ├── webhook/
│   │   │   └── route.ts         # Stripe webhook handler
│   │   ├── sync/
│   │   │   └── route.ts         # Cloud sync (PAID only)
│   │   ├── analytics/
│   │   │   └── route.ts         # Analytics event tracking
│   │   ├── leaderboards/
│   │   │   ├── route.ts         # GET leaderboards
│   │   │   └── update/
│   │   │       └── route.ts     # POST leaderboard update
│   │   └── share/
│   │       ├── [id]/
│   │       │   └── route.ts     # GET share content
│   │       └── create/
│   │           └── route.ts     # POST create share link
│   └── layout.tsx                # Root layout
├── components/                    # React components
│   ├── game/
│   │   ├── GameTable.tsx        # Main game component
│   │   ├── CardRenderer.tsx     # Canvas card rendering
│   │   ├── DeckDisplay.tsx      # Deck count display
│   │   └── HPBar.tsx            # Health bar component
│   ├── ui/
│   │   ├── WarlordAvatar.tsx    # Warlord avatar display
│   │   ├── Overlay.tsx           # Base overlay component
│   │   ├── Modal.tsx             # Modal wrapper
│   │   └── Button.tsx            # Button component
│   └── overlays/
│       ├── PreGameOverlay.tsx    # Pre-game selection
│       ├── PostGameOverlay.tsx   # Post-game results
│       ├── MenuOverlay.tsx       # Game menu
│       └── LeaderboardOverlay.tsx # Leaderboard display
├── stores/                       # Zustand stores
│   ├── gameStore.ts             # Main game state
│   ├── uiStore.ts                # UI state (overlays, modals)
│   └── progressStore.ts          # Player progress (XP, Gold, unlocks)
├── lib/                          # Utility libraries
│   ├── game-rules.ts             # Game logic (card comparison, War)
│   ├── card-utils.ts             # Card utilities (shuffle, deal)
│   ├── special-system.ts         # Special activation system
│   ├── chain-detection.ts        # Chain detection (poker, suit)
│   ├── storage.ts                # IndexedDB/localStorage utilities
│   └── api-client.ts             # API client utilities
├── types/                        # TypeScript types
│   ├── game.ts                   # Game state types
│   ├── card.ts                    # Card types
│   ├── warlord.ts                 # Warlord types
│   └── api.ts                     # API request/response types
├── hooks/                        # React hooks
│   ├── useGameState.ts           # Game state hook
│   ├── useCanvas.ts              # Canvas rendering hook
│   └── useStorage.ts             # Storage hook
├── public/                       # Static assets
│   └── assets/
│       ├── sprites/              # Pixel art sprites
│       ├── sounds/               # Audio files
│       └── images/               # Other images
├── prisma/                       # Prisma schema and migrations
│   ├── schema.prisma             # Database schema
│   └── migrations/               # Migration files
├── tests/                        # Test files
│   ├── unit/                     # Unit tests
│   ├── integration/              # Integration tests
│   └── e2e/                      # End-to-end tests
├── .env.local                    # Local environment variables
├── .env.example                  # Environment variable template
├── next.config.js                # Next.js configuration
├── tailwind.config.js            # Tailwind CSS configuration
├── tsconfig.json                 # TypeScript configuration
└── package.json                  # Dependencies and scripts
```

**TODO**: Update with actual file structure as implementation progresses

### Component Hierarchy

```
App (layout.tsx)
└── GameTable (page.tsx)
    ├── WarlordAvatar (enemy)
    ├── WarlordAvatar (player)
    ├── DeckDisplay (enemy)
    ├── DeckDisplay (player)
    ├── HPBar (enemy)
    ├── HPBar (player)
    ├── CardRenderer (Canvas)
    └── Overlay System
        ├── PreGameOverlay
        ├── PostGameOverlay
        ├── MenuOverlay
        ├── LeaderboardOverlay
        └── [Other Overlays]
```

**TODO**: Create detailed component tree diagram

### Key Files and Their Purpose

**Core Game Files:**
- `app/page.tsx`: Main game page, renders GameTable component
- `components/game/GameTable.tsx`: Persistent component handling game states
- `components/game/CardRenderer.tsx`: Canvas-based card rendering
- `stores/gameStore.ts`: Zustand store for game state management
- `lib/game-rules.ts`: Core game logic (card comparison, War resolution)

**API Files:**
- `app/api/sync/route.ts`: Cloud sync endpoint (PAID users)
- `app/api/leaderboards/route.ts`: Leaderboard data endpoint
- `app/api/checkout/route.ts`: Stripe checkout session creation

**Storage Files:**
- `lib/storage.ts`: IndexedDB/localStorage abstraction
- `prisma/schema.prisma`: Database schema definition

**TODO**: Document actual file purposes as implementation progresses

---

## 5. Building Blocks / Components

### Pages and Routes

**Main Route: `/`**
- **Component**: `app/page.tsx` → `GameTable` component
- **Purpose**: Single-page application, handles all game states
- **State Management**: Uses Zustand store (`gameStore`)
- **Rendering**: Conditional rendering based on `appState` ('pre-game' | 'in-game' | 'post-game')

**Share Route: `/share/[id]`**
- **Component**: `app/share/[id]/page.tsx`
- **Purpose**: Server-side rendered share link page
- **Data Fetching**: Calls `/api/share/[id]` on server
- **SEO**: Optimized for social sharing (Open Graph tags)

**TODO**: Document actual route implementations

### React Components

**Game Components:**

**GameTable** (`components/game/GameTable.tsx`)
- **Purpose**: Main game container, handles state transitions
- **Props**: None (uses Zustand store)
- **State**: Manages appState, gameState, turnState via Zustand
- **Children**: Renders overlays conditionally based on state

**CardRenderer** (`components/game/CardRenderer.tsx`)
- **Purpose**: Canvas-based card rendering and animations
- **Props**: `cards: Card[]`, `position: {x, y}`, `flipped: boolean`
- **Implementation**: Uses Canvas API, offscreen rendering for performance
- **Animations**: Card flip, slide-in, health bar fill

**WarlordAvatar** (`components/ui/WarlordAvatar.tsx`)
- **Purpose**: Displays Warlord avatar with reactions
- **Props**: `warlord: Warlord`, `reaction?: 'win' | 'lose' | 'neutral'`
- **Implementation**: Pixel art sprite rendering

**TODO**: Document actual component implementations with code examples

### Overlay System

**Base Overlay** (`components/ui/Overlay.tsx`)
- **Purpose**: Base component for all overlays
- **Features**: Backdrop, close button, animation
- **Usage**: All overlays extend this component

**Overlay Types:**
- `PreGameOverlay`: Warlord selection, Battle Item management
- `PostGameOverlay`: Results, rewards, next actions
- `MenuOverlay`: Settings, statistics, challenges
- `LeaderboardOverlay`: Global leaderboards display

**TODO**: Document actual overlay implementations

### State Management

**Zustand Stores:**

**gameStore** (`stores/gameStore.ts`)
- **Purpose**: Main game state (decks, HP, turn state)
- **Structure**: See Data Models section
- **Persistence**: Auto-saves to IndexedDB on state changes
- **Selectors**: Fine-grained selectors to prevent unnecessary re-renders

**progressStore** (`stores/progressStore.ts`)
- **Purpose**: Player progress (XP, Gold, unlocks, level)
- **Persistence**: IndexedDB for local, cloud sync for paid users
- **Updates**: On game completion, level-up, unlock

**uiStore** (`stores/uiStore.ts`)
- **Purpose**: UI state (overlay visibility, modal state)
- **Persistence**: localStorage (preferences only)

**TODO**: Document actual store implementations with TypeScript interfaces

### Assets

**Pixel Art Sprites:**
- **Format**: PNG (lossless), WebP (compressed, 80% quality)
- **Loading**: Lazy-loaded on Warlord selection
- **Caching**: Browser cache, Service Worker cache
- **Location**: `public/assets/sprites/`

**Audio Files:**
- **Format**: MP3 (fallback), OGG (preferred)
- **Loading**: Lazy-loaded, preloaded for critical sounds
- **Library**: Howler.js for audio management
- **Location**: `public/assets/sounds/`

**TODO**: Document actual asset loading strategy and formats

### Patterns and Best Practices

**Component Patterns:**
- Functional components with hooks
- Custom hooks for reusable logic (`useGameState`, `useCanvas`)
- Compound components for complex UI (Overlay system)

**State Management Patterns:**
- Zustand selectors for performance optimization
- Immutable updates using `immer` middleware
- Optimistic updates for instant feedback

**Rendering Patterns:**
- Canvas API for card animations (not CSS animations)
- CSS `image-rendering: pixelated` for pixel art
- RequestAnimationFrame for 60fps animations

**TODO**: Document actual patterns used in implementation

---

## 6. Runtime View / Processes

### Main Game Flow

**Sequence Diagram:**

```
User → GameTable → gameStore → CardRenderer → API (if needed)
  ↓        ↓           ↓            ↓              ↓
Tap    State      Update      Render        Sync/Leaderboard
```

**TODO**: Create detailed sequence diagrams for:
- Pre-Game → Game Start flow
- Turn resolution flow (Draw → Resolve → Specials)
- Post-Game → Pre-Game flow
- Cloud sync flow
- Leaderboard update flow

### Game Loop

**Turn Cycle:**
1. **Pre-Turn**: Player can activate Battle Items
2. **Draw**: Cards drawn, revealed
3. **Resolution**: Rank comparison, winner determined
4. **War** (if tie): Recursive War resolution (max depth 5)
5. **Post-Win**: Specials activated, rewards calculated
6. **Next Turn**: Return to Pre-Turn or Game End

**State Machine:**

```
pre-game → in-game (initialization)
  ↓
in-game → turn-cycle
  ↓
turn-cycle → war-scenario (if tie)
  ↓
war-scenario → turn-cycle (after resolution)
  ↓
turn-cycle → game-end (HP = 0 or deck empty)
  ↓
game-end → post-game
  ↓
post-game → pre-game (continue)
```

**TODO**: Document actual state machine implementation with code

### Input/Output Flows

**User Input → State Update:**
- Tap "Play" button → `gameStore.startGame()`
- Tap card → `gameStore.playCard()`
- Tap special → `gameStore.activateSpecial()`

**State Update → Rendering:**
- Zustand store update → Component re-render (via selector)
- Canvas state update → `CardRenderer` redraw

**API Calls:**
- Game completion → `/api/leaderboards/update` (async, non-blocking)
- Paid user sync → `/api/sync` (on state change)
- Analytics → `/api/analytics` (debounced)

**TODO**: Document actual input/output flows with code examples

---

## 7. Data Models and Storage

### TypeScript Interfaces

**Game State** (`types/game.ts`):
```typescript
interface GameState {
  appState: 'pre-game' | 'in-game' | 'post-game';
  playerProgress: {
    level: number;
    xp: number;
    gold: number;
    unlockedWarlords: string[];
  };
  gameState: {
    playerWarlord: Warlord;
    enemyWarlord: Warlord;
    playerHP: number;
    enemyHP: number;
    playerDeck: Card[];
    enemyDeck: Card[];
    streak: number;
  };
  turnState: {
    phase: 'pre-turn' | 'draw' | 'resolution' | 'post-win';
    playerCard: Card | null;
    enemyCard: Card | null;
    winner: 'player' | 'enemy' | null;
  };
}
```

**TODO**: Document actual TypeScript interfaces from implementation

### Card Data Structure

**Card Type** (`types/card.ts`):
```typescript
interface Card {
  id: string;
  rank: '6' | '7' | '8' | '9' | '10' | 'J' | 'Q' | 'K' | 'A' | 'Joker' | 'Signature';
  suit: 'hearts' | 'diamonds' | 'clubs' | 'spades' | null;
  warlordId?: string; // For Signature cards
}
```

**TODO**: Document actual card structure from implementation

### Warlord Data Structure

**Warlord Type** (`types/warlord.ts`):
```typescript
interface Warlord {
  id: string;
  name: string;
  level: number;
  hp: number;
  specialPower: SpecialPower;
  suitSpecials: {
    hearts: SuitSpecial;
    diamonds: SuitSpecial;
    clubs: SuitSpecial;
    spades: SuitSpecial;
  };
}
```

**TODO**: Document actual Warlord structure from implementation

### Database Schema (Prisma)

**User Model** (`prisma/schema.prisma`):
```prisma
model User {
  id          String   @id @default(uuid())
  email       String   @unique
  data        Json     // Serialized progress (XP, unlocks, galleries)
  adFree      Boolean  @default(true)
  version     Int      @default(1) // For conflict resolution
  lastModified DateTime @default(now())
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
}
```

**TODO**: Document actual Prisma schema from implementation

### Storage Implementation

**IndexedDB Structure:**
- **Object Store**: `game_data`
  - Key: `user_uuid`
  - Value: Serialized game state (JSON)
- **Object Store**: `user_metadata`
  - Key: `user_uuid`
  - Value: UUID, preferences

**localStorage Keys:**
- `bfw_sound_enabled`: boolean
- `bfw_haptic_enabled`: boolean
- `bfw_last_warlord`: string (Warlord ID)
- `bfw_ad_frequency`: number (interstitial counter)

**TODO**: Document actual storage implementation with code examples

### Data Flow

**XP/Gold Update Flow:**
1. Game completion → `progressStore.addXP(gained)`
2. Store update → IndexedDB save (debounced)
3. If paid user → `/api/sync` call (async)
4. Server validation → Database update
5. Conflict resolution → Merge if needed

**TODO**: Document actual data flow implementations

---

## 8. APIs and Integrations

### Internal API Routes

**POST /api/checkout**
- **Purpose**: Create Stripe Checkout session
- **Request**: `{ productId: string, userId?: string }`
- **Response**: `{ url: string }`
- **Implementation**: `app/api/checkout/route.ts`

**POST /api/webhook**
- **Purpose**: Handle Stripe webhook events
- **Request**: Stripe webhook payload
- **Response**: `{ success: boolean }`
- **Implementation**: `app/api/webhook/route.ts`
- **Security**: Webhook signature verification

**POST /api/sync** (PAID only)
- **Purpose**: Cloud sync player progress
- **Request**: `{ data: GameState, version: number, lastModified: Date }`
- **Response**: `{ success: boolean, conflict?: ConflictData }`
- **Implementation**: `app/api/sync/route.ts`
- **Authentication**: Clerk session required
- **Validation**: Checksum validation, anomaly detection

**GET /api/leaderboards**
- **Purpose**: Fetch leaderboard data
- **Query Params**: `category`, `limit`, `offset`
- **Response**: `{ entries: LeaderboardEntry[], playerRank: number }`
- **Implementation**: `app/api/leaderboards/route.ts`
- **Caching**: Vercel KV (5 minute TTL)

**POST /api/leaderboards/update**
- **Purpose**: Update player ranking
- **Request**: `{ category: string, score: number, playerId: string }`
- **Response**: `{ rank: number }`
- **Implementation**: `app/api/leaderboards/update/route.ts`
- **Storage**: Vercel KV (sorted sets)

**GET /api/share/[id]**
- **Purpose**: Fetch share link content
- **Response**: `{ type: 'game' | 'achievement', data: ShareData }`
- **Implementation**: `app/api/share/[id]/route.ts`
- **TTL**: 30 days

**POST /api/analytics**
- **Purpose**: Track game events
- **Request**: `{ event: string, properties: object, userId: string }`
- **Response**: `{ success: boolean }`
- **Implementation**: `app/api/analytics/route.ts`
- **Rate Limiting**: 100 requests per 15 minutes per UUID

**TODO**: Document actual API implementations with request/response schemas

### External Integrations

**Stripe Integration:**
- **Purpose**: Payment processing ($3.99 upgrade, Gold IAP)
- **SDK**: `@stripe/stripe-js`
- **Configuration**: Environment variables (`STRIPE_SECRET_KEY`, `STRIPE_PUBLISHABLE_KEY`)
- **Webhooks**: Signature verification, idempotency handling

**AdMob Integration:**
- **Purpose**: Ad serving (interstitials, rewarded videos)
- **SDK**: `admob-plus-web`
- **Configuration**: Environment variables (`ADMOB_APP_ID`, `ADMOB_AD_UNIT_ID`)
- **Placement**: Post-game interstitials, user-initiated rewarded videos

**Clerk Integration:**
- **Purpose**: Authentication (paid users only)
- **SDK**: `@clerk/nextjs`
- **Configuration**: Environment variables (`NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY`, `CLERK_SECRET_KEY`)
- **Flow**: Magic links, session management

**Vercel KV (Redis):**
- **Purpose**: Caching, rate limiting, leaderboards
- **SDK**: `@vercel/kv`
- **Use Cases**: Session caching, rate limiting, leaderboard caching
- **Configuration**: Environment variables (`KV_REST_API_URL`, `KV_REST_API_TOKEN`)

**TODO**: Document actual integration implementations with code examples

---

## 9. Deployment and Environments

### Environment Setup

**Local Development:**
- **Node Version**: 18.x or higher
- **Package Manager**: npm or yarn
- **Database**: Local Postgres (via Docker) or Vercel Postgres (remote)
- **Environment Variables**: `.env.local` file
- **Commands**: `npm run dev` (development server)

**Staging:**
- **Hosting**: Vercel Preview deployments
- **Database**: Vercel Postgres (preview database)
- **Environment**: Stripe test mode, AdMob test ads
- **Deployment**: Automatic on PR creation

**Production:**
- **Hosting**: Vercel Production
- **Domain**: bigfootwar.com
- **Database**: Vercel Postgres (production database)
- **Environment**: Stripe live mode, AdMob live ads
- **Deployment**: Automatic on `main` branch push

**TODO**: Document actual environment setup with commands and configuration

### CI/CD Pipeline

**GitHub Actions Workflow:**
1. Push to GitHub → Trigger Vercel build
2. Run tests (Jest, Cypress)
3. Build Next.js application
4. Deploy to preview/production
5. Health checks verify deployment

**Branch Strategy:**
- `main` → Production deployment
- `develop` → Preview deployment
- Feature branches → Preview deployments (PR-based)

**TODO**: Document actual CI/CD configuration

### Environment Variables

**Required Variables:**
- `DATABASE_URL`: Postgres connection string
- `KV_REST_API_URL`: Vercel KV API URL
- `KV_REST_API_TOKEN`: Vercel KV API token
- `STRIPE_SECRET_KEY`: Stripe secret key
- `NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY`: Stripe publishable key
- `CLERK_SECRET_KEY`: Clerk secret key
- `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY`: Clerk publishable key
- `ADMOB_APP_ID`: AdMob app ID
- `ADMOB_AD_UNIT_ID`: AdMob ad unit ID

**TODO**: Document actual environment variables from `.env.example`

### Monitoring and Observability

**Error Tracking:**
- **Tool**: Sentry
- **Configuration**: Error boundaries, API error logging
- **Alerts**: Email/Slack on critical errors

**Analytics:**
- **Tool**: Vercel Analytics + PostHog
- **Metrics**: Page views, API calls, performance
- **Events**: Game events, user actions

**Performance Monitoring:**
- **Tool**: Vercel Analytics (Core Web Vitals)
- **Metrics**: FCP, LCP, TTI, FID
- **Alerts**: Performance degradation alerts

**TODO**: Document actual monitoring setup

---

## 10. Error Handling and Logging

### Error Types

**Network Errors:**
- **Offline**: Game continues with local state, API calls queued
- **API Failure**: Retry logic, graceful degradation
- **Timeout**: User-friendly error message, retry option

**Game Errors:**
- **Invalid State**: State validation, recovery to last known good state
- **Corrupted Data**: Data validation on load, fallback to defaults
- **Storage Quota**: User warning, offer cloud sync upgrade

**Payment Errors:**
- **Stripe Failure**: Clear error message, retry option
- **Webhook Failure**: Logging, manual recovery process

**TODO**: Document actual error handling implementations

### Error Handling Strategies

**Client-Side:**
- **React Error Boundaries**: Catch component errors
- **Try-Catch Blocks**: Critical operations wrapped
- **Graceful Degradation**: Game continues with reduced features
- **User Feedback**: Clear, non-technical error messages

**Server-Side:**
- **API Error Responses**: Standardized format `{ error: string, code: string }`
- **Logging**: Comprehensive server-side logging
- **Retry Logic**: Automatic retries for transient failures
- **Monitoring**: Error tracking via Sentry

**TODO**: Document actual error handling code

### Logging

**Development:**
- **Console Logging**: Detailed logs for debugging
- **Log Levels**: `debug`, `info`, `warn`, `error`
- **Format**: Structured JSON logs

**Production:**
- **Cloud Logging**: Vercel logs, Sentry
- **Log Levels**: `info`, `warn`, `error` (no debug)
- **Format**: Structured JSON logs
- **Retention**: 30 days

**TODO**: Document actual logging implementation

---

## 11. Testing and QA

### Unit Testing

**Framework**: Jest + React Testing Library
**Coverage Target**: 80%+ for game logic
**Test Files**: `tests/unit/`

**Test Areas:**
- Game rules (card comparison, War resolution)
- State management (Zustand stores)
- Utility functions (card shuffling, special activation)
- Calculations (XP/Gold rewards, damage)

**TODO**: Document actual test structure and examples

### Integration Testing

**Framework**: Jest + React Testing Library
**Test Files**: `tests/integration/`

**Test Areas:**
- Component interactions
- State updates
- API integration (mocked)
- Storage operations

**TODO**: Document actual integration tests

### End-to-End Testing

**Framework**: Cypress
**Test Files**: `tests/e2e/`

**Test Scenarios:**
- Complete game flow (pre-game → game → post-game)
- Warlord selection
- Battle Item purchase
- Upgrade flow
- Leaderboard viewing

**Mobile Testing**: Chrome DevTools mobile emulation + real device tests

**TODO**: Document actual E2E test scenarios

### Performance Testing

**Tools**: Lighthouse CI, Chrome DevTools
**Metrics**: Bundle size, load time, frame rate, memory usage
**Automation**: Lighthouse CI in CI/CD pipeline

**TODO**: Document actual performance test results

### Manual Testing

**Device Testing**: Real iOS/Android devices
**Browser Testing**: Chrome, Safari, Firefox, Edge
**Payment Testing**: Stripe test mode, AdMob test ads
**Accessibility Testing**: Screen readers, keyboard navigation

**TODO**: Document QA checklists

---

## 12. Design Decisions and Best Practices

### Key Design Decisions

**Canvas API over CSS Animations:**
- **Rationale**: Pixel-perfect control, better performance for card animations
- **Trade-off**: More complex code, but necessary for retro aesthetic
- **Implementation**: `CardRenderer` component uses Canvas API

**Zustand over Redux Toolkit:**
- **Rationale**: Smaller bundle size (~3KB vs ~40KB), better performance for frequent updates
- **Trade-off**: Less ecosystem, but sufficient for this use case
- **Implementation**: `stores/gameStore.ts` uses Zustand

**Local-First Architecture:**
- **Rationale**: Zero-friction entry, offline play, fast performance
- **Trade-off**: Data loss risk, mitigated by cloud sync for paid users
- **Implementation**: IndexedDB for local data, cloud sync optional

**Serverless API Routes:**
- **Rationale**: No server maintenance, auto-scaling, cost-effective
- **Trade-off**: Cold starts, mitigated by Vercel Edge Network
- **Implementation**: Next.js API routes, Vercel Functions

**TODO**: Document actual design decisions and trade-offs from implementation

### Code Patterns

**Component Patterns:**
- Functional components with hooks
- Compound components for complex UI
- Custom hooks for reusable logic

**State Management Patterns:**
- Zustand selectors for performance
- Immutable updates with `immer`
- Optimistic updates for instant feedback

**Rendering Patterns:**
- Canvas API for animations
- CSS `image-rendering: pixelated` for pixel art
- RequestAnimationFrame for 60fps

**TODO**: Document actual code patterns with examples

### Best Practices

**Performance:**
- Code splitting by route
- Lazy loading for assets
- Object pooling for frequent allocations
- Frame skipping for low-end devices

**Security:**
- No PII in local storage (anonymous UUID only)
- API rate limiting
- Webhook signature verification
- Input validation on server

**Accessibility:**
- Semantic HTML
- ARIA labels
- Keyboard navigation
- Screen reader support

**TODO**: Document actual best practices followed

---

## 13. Quality Scenarios and Future Work

### Quality Scenarios

**High Load:**
- **Scenario**: 100 concurrent games
- **Expected**: Vercel auto-scales serverless functions
- **Monitoring**: API response times, error rates
- **Mitigation**: Rate limiting, caching

**Low-End Device:**
- **Scenario**: Moto G4 (2016 Android)
- **Expected**: 30fps minimum, reduced particle effects
- **Monitoring**: Frame rate tracking
- **Mitigation**: Adaptive quality, frame skipping

**Network Failure:**
- **Scenario**: User goes offline mid-game
- **Expected**: Game continues, API calls queued
- **Monitoring**: Offline detection, sync queue
- **Mitigation**: Local-first design, retry logic

**TODO**: Document actual quality scenarios and results

### Security Considerations

**Data Privacy:**
- No PII stored locally (anonymous UUID only)
- Email only collected for paid users (via Clerk)
- GDPR/CCPA compliance (privacy policy)

**API Security:**
- Rate limiting per UUID/IP
- Webhook signature verification
- Input validation and sanitization
- HTTPS enforced

**TODO**: Document actual security measures

### Accessibility

**Features:**
- Semantic HTML structure
- ARIA labels for screen readers
- Keyboard navigation support
- High contrast mode toggle
- Alt text for images

**TODO**: Document actual accessibility implementation

### Scalability

**Current Capacity:**
- Target: 1k+ DAU initially
- Scale to: 10k+ DAU
- Infrastructure: Vercel auto-scaling

**Scaling Triggers:**
- Database usage monitoring
- API response time alerts
- Error rate thresholds

**TODO**: Document actual scalability planning

### Future Work

**Planned Enhancements:**
- [ ] Server-side ad reward verification
- [ ] Enhanced conflict resolution UI
- [ ] More detailed analytics
- [ ] Performance optimizations based on real-world data

**TODO**: Update as implementation progresses

---

## Appendix: Implementation Checklist

Use this checklist to track implementation progress:

- [ ] Code structure established
- [ ] Core components implemented
- [ ] State management (Zustand) set up
- [ ] Canvas rendering implemented
- [ ] API routes implemented
- [ ] Database schema created
- [ ] Storage (IndexedDB/localStorage) implemented
- [ ] External integrations (Stripe, AdMob, Clerk) configured
- [ ] Testing framework set up
- [ ] CI/CD pipeline configured
- [ ] Monitoring and logging configured
- [ ] Documentation updated

**Update this checklist as implementation progresses**
