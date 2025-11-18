# System Design Document

Best practices here include:
- **Prompt Engineering**: Feed AI specific excerpts from GDD/SDD (e.g., "Implement the Main Game Flow using Next.js, based on this GDD section: [paste]").
- **Iteration**: Use AI for prototypes, then validate against SDD for consistency.
- **Version Control**: Commit AI-generated code with comments referencing SDD sections to maintain auditability.
- **Limitations**: AI excels at patterns/best practices but may hallucinate; always cross-check with your docs and test.

1. **Introduction and Scope**
   - Purpose: "As-built documentation of the Bigfoot War system, referencing GDD for design intent."
   - Scope: What the SDD covers (e.g., frontend/backend, but not gameplay rules).
   - References: Link to GDD, todo.md, external docs (e.g., Next.js API).
   - **Improvement**: Add a glossary (e.g., define "Warlord Special" technically) and version history (e.g., "v1.0 - Initial build").

2. **System Overview**
   - High-level architecture: Monolithic Next.js app with client-side game logic, serverless APIs for sync/payments.
   - Key components: Game Table (persistent UI), Overlays, State Management (e.g., Zustand for game state).
   - **New**: Include a diagram (e.g., block diagram of frontend-backend flow, using tools like Draw.io).

3. **Constraints and Assumptions**
   - Technical: Browser compatibility (Chrome, etc.), mobile-first (breakpoints), no installs.
   - Non-functional: Performance targets (60fps), budget (free Vercel tier).
   - **New**: Risks/mitigations (e.g., "LocalStorage limits: Mitigate with IndexedDB fallback").

4. **Building Blocks / Components**
   - Detailed breakdown: Pages/Routes (e.g., `/` for Game Table), React components (e.g., WarlordAvatar, CardRenderer via Canvas).
   - Assets: Pixel art sprites, audio files (formats, loading strategy).
   - Patterns/Best Practices: e.g., Hooks for state, pixelated CSS for retro look.
   - **Improvement**: Add code structure (e.g., folder layout: `/components`, `/lib/game-rules.js`).

5. **Runtime View / Processes**
   - Flows: Sequence diagrams for Main Game Flow, Pre-Game, Post-Game (e.g., turn resolution with specials).
   - Game Loop: Draw → Resolve → Specials → Next.
   - Inputs/Outputs: e.g., User tap → API call → State update.
   - **New**: State machines (e.g., for game phases: idle, drawing, resolving).

6. **Data Models and Storage**
   - Schemas: JSON structures for Warlords (from roster table), Decks, Suits charges.
   - Persistence: LocalStorage/IndexedDB for anonymous, Prisma for paid cloud sync.
   - **New**: Data flows (e.g., how XP/Gold updates propagate).

7. **APIs and Integrations**
   - Internal: Next.js API routes (e.g., `/api/sync` for cloud save).
   - External: Stripe for IAP, AdMob for ads, Clerk for auth.
   - **Improvement**: Specs (e.g., endpoints, request/response schemas, auth tokens).

8. **Deployment and Environments**
   - Setup: Vercel hosting, domains (bigfootwar.com).
   - Environments: Dev (local), Staging (Vercel preview), Prod.
   - CI/CD: GitHub actions for auto-deploys.
   - **New**: Monitoring (Vercel Analytics, error tracking with Sentry).

9. **Error Handling and Logging**
   - Types: Network errors (e.g., offline play), Game errors (e.g., invalid state).
   - Strategies: Graceful fallbacks (e.g., retry on sync fail), user-friendly messages.
   - **Improvement**: Logging levels (console in dev, cloud in prod).

10. **Testing and QA**
    - Types: Unit (Jest for rules logic), E2E (Cypress for flows), Manual (mobile emulators).
    - Coverage: Key paths (e.g., win/loss, specials), edge cases (low cards, ties).
    - **New**: Automation scripts, QA checklists tied to GDD flows.

11. **Design Decisions and Best Practices**
    - Rationale: e.g., "Chose Canvas for animations over CSS for pixel precision."
    - Tools/Processes: Next.js for SSR, Tailwind for UI, Howler.js for audio.
    - **New**: Trade-offs (e.g., "Local-first for speed, but risks data loss—mitigated by paid cloud").

12. **Quality Scenarios and Future Work**
    - Scenarios: e.g., "High-load: 100 concurrent games—Vercel scales auto."
    - **New**: Security (e.g., no PII pre-purchase), Accessibility (alt text, high contrast toggle), Scalability (e.g., API rate limits).
