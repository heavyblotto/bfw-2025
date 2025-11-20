# Bigfoot War Game Design

## Summary
Classic War turn-based card game mixed with fast slot-like play.

- **Platform**: Web browser (Chrome, Firefox, Safari, Edge) - no app store required  
- **Mobile-first**: Optimized responsive design for mobile devices by default with breakpoints for other display sizes  
- **URL**: bigfootwar.com (hosted on Vercel)  
- **Technology**: Next.js, React, Canvas API  
- **Monetization**: Free-to-play with ads / $3.99 one-time purchase for ad-free / Gold IAP  

### Game Rules

**Game Type:** Single player game - Player Bigfoot Warlord vs Enemy Bigfoot Warlord

#### Deck Composition
- **Deck Size:** 38 cards total (referred to as 36-card deck variant)
- **Composition:** Ranks 6–Ace (36 suited cards) + 1 Joker + 1 Signature Card
- **Suited Cards (36):** 9 ranks × 4 suits (Ace, King, Queen, Jack, 10, 9, 8, 7, 6)
- **1 Joker:** Neutral wild card, auto-win + shuffle (classic War behavior)
- **1 Signature Card:** Unique hyper-thematic card per Warlord (replaces 2nd Joker, creates distinct "boss moment")
- Decks are shuffled independently at game start
- Cards are recycled: When cards are captured, they go to the bottom of the winner's deck (not removed from play)
- Total cards in play: 76 cards (38 per player at start)

#### Card Ranks
1. **Signature Card:** Absolute Highest (Beats Ace, Joker, and all other cards). Ties only with enemy Signature Card (Immediate War).
2. **Joker:** Beats all suited cards (Ace–6). Loses to Signature Card.
3. **Ace:** Highest suited rank.
4. **King, Queen, Jack, 10, 9, 8, 7, 6:** Descending order.

#### Signature Card Rules
- **Quantity:** Exactly 1 Signature Card per Warlord.
- **Behavior:** Triggers its unique effect immediately and automatically upon reveal (before rank comparison).
- **Effect Priority:** Effect happens even if you lose the turn (unless the effect explicitly states otherwise or is negated).
- **Capture:** Goes to the bottom of the winner’s deck exactly like any other card — can be stolen and used by the opponent.
- **Visuals:** Full-bleed hero portrait, gold border, epic particle burst + unique sound when revealed.

#### Joker Rules

**Joker Behavior:**
- Joker rank: Highest possible rank (beats all other cards, wins all ties)
- Neutral card: Same behavior for all Warlords (classic War auto-win + shuffle)
- When Joker is drawn: Immediately triggers deck shuffle for that player
- Shuffle timing: Occurs immediately upon drawing the Joker (before rank comparison)
- Turn resolution: After shuffle, the Joker still wins the turn (highest rank)
- Shuffle effect: Only affects the player who drew the Joker (not both players)
- **Gameplay Impact:** Creates exciting shuffle moments, resets deck order unpredictably

**Joker Turn Flow:**
1. Player draws Joker
2. That player's deck immediately shuffles
3. Rank comparison: Joker wins (highest rank)
4. Damage dealt, cards captured normally
5. Joker goes to bottom of winner's deck after capture

#### Specials Rules

**When Specials Can Be Played:**
- Post-win only: Specials can only be played by the turn winner
- Timing: After card capture, before next turn begins
- Limit: Winner may play 0-2 specials per turn (mix of suit specials and/or Warlord Power)

**Suit-Based Specials:**
- Four specials per Warlord: Hearts, Diamonds, Clubs, Spades
- Charge mechanism: Ready when X cards of that suit are captured
- Charge threshold: Varies by Warlord and suit (typically 1-6 cards, reduced by 1 from previous 2-7 range to account for smaller capture pools with 36-card decks)
- Charge reset: Only when special is used (charges reset to 0 after activation)
- **Comeback Mechanic**: Suit charges persist through losses, allowing players to build up counter-attacks even when behind

**Warlord Special Power:**
- One unique power per Warlord
- Charge mechanism: Charges on wins AND on taking damage (pity mechanic)
- Charge threshold: Varies by Warlord (typically 3-7 wins OR 5-10 damage taken)
- Charge progress: Tracks wins and damage taken since last reset
- Charge reset: Only after use (charges reset to 0 after activation)
- **Comeback Mechanic**: Taking damage builds charge, giving losing players a path to their ultimate ability
- More powerful than suit specials; strategic climax abilities

**Card Manipulation:**
- Some specials can steal, bury, or banish cards between decks
- Cards are never removed from play entirely; they cycle between decks

*For detailed specials mechanics and status effects, see: `## Game Design and Systems` → `### Specials and Status Effects`*  
*For UX flow, see: `## Game Flows` → `### Main Game Flow`*

#### Status Effects and Special Mechanics

Specials can apply status effects (DoT, Armor, Invulnerable, Dodge, Blind, Confuse, Silence, Transform) or trigger special mechanics (turn manipulation, damage types, card effects, special effects, passive effects). These effects modify gameplay in various ways.

*For detailed mechanics of all status effects and special mechanics, see: `## Game Design and Systems` → `### Specials and Status Effects`*

#### Win Conditions

**Player Wins Game When:**
1. Enemy Warlord HP reduced to 0, OR
2. Enemy deck is empty (no cards remaining to draw)

**Player Loses Game When:**
1. Player Warlord HP reduced to 0, OR
2. Player deck is empty (no cards remaining to draw)

**Note:** Cards are never removed from play entirely. However, card manipulation mechanics (steal/bury/banish) can create deck size imbalances between players. While deck depletion is theoretically possible if one player's deck becomes significantly smaller, the primary win condition remains HP reduction. Deck depletion win condition serves as a strategic alternative when card manipulation creates large deck imbalances.

#### Progression and Rewards

**Turn Rewards** (Player wins only):
- Gold and XP earned per turn win (amounts vary by card rank and streak multipliers)
- Streak bonuses: Consecutive wins multiply rewards (3+ wins = 1.5x, 5+ wins = 2x)
- Streak resets on any turn loss

**Game Completion Rewards:**
- Bonus Gold and XP for winning games
- First-time defeat bonuses for new Enemy Warlords
- Challenge bonuses for completing objectives

**Level Progression:**
- XP-based level advancement unlocks new Enemy Warlords (1 per level)
- Gold fee required for game attempts after first 3 free attempts per Enemy Warlord
- Level advancement requires both XP threshold AND defeating current Enemy Warlord

**Warlord Unlocks:**
- **Initial Unlocks:** New players start with levels 1-5 unlocked for both Enemy and Player Warlords (Sasquatch, Skunk Ape, Wendigo, Jersey Devil, Grassman)
- **Enemy Warlords:** Levels 1-5 unlocked initially; Level 6+ unlocked sequentially by level (1 per level)
- **Player Warlords:** Levels 1-5 unlocked initially (treated as already defeated); Level 6+ unlocked after defeating corresponding Enemy Warlord
- Defeated Enemy Warlords can be replayed for free

*For detailed economy mechanics, see: `## Game Design and Systems` → `### Game Economies`*  
*For detailed progression flows, see: `## Game Flows` → `### XP, Levels, and Progress Flow`*

### Game Look & Feel
- One page with minimal UI elements
- Retro SNES-style pixel art
- Dark-mode themed
- Plays happens on table like a card game
- Primary CTA at thumb-level
- Secondary CTAs for:
  - Warlord Special (available as inline icon on main board, tappable when ready)
- Default layout shows Enemy Warlord avatar at top, Player Warlord avatar at bottom of screen
- At game start, show decks adjacent to Warlords
- Display card count for each deck
- Minimal animation
- Card faces display simple Suit and Rank along with Warlord hero image
- Cards in battle zone are larger (100x150px) for enhanced hero visibility and readability
- Cards dealt in middle of screen, player on left, enemy on right
- XP and Gold rewards and Level ups displayed when won but do not persistent in-game (no top bars with XP, Gold, Level, etc.)
- HP displayed as Health Bar per Warlord
- Warlord avatars react to outcomes
- Game Status displayed in banner area at top of page
  - Displays outcomes, describes plays, game / turn status, prompts for decisions
- Overlays for:
  - Tapping Game Menu (anytime)
  - Tapping Warlords (anytime)
  - Specials Icons (gameplay - inline on main board, tappable when ready)
  - Enemy Special Notification Overlay (gameplay - appears briefly after enemy wins and plays specials)
  - Game End Outcomes (gameplay)
  - Tapping Enemy Warlord Select (pre-game)
  - Tapping Player Warlord Select (pre-game)
  - Tapping Challenges (pre-game)
  - Tapping IAP for Gold
  - Tapping `Upgrade` CTA for 1-time purchase (pre-game/post-game)
  - Tapping AdMob CTAs (pre-game/post-game)

## Game Flows

### New Player Flow

1. No sign-up to play, user data is saved locally
2. Player optionally pays $3.99 for to save game data to cloud (portable across devices) and get automatic Gold rewards matching ad-based rewards
3. No onboarding flow due to simple and discoverable UX / UI
4. **Initial Unlocks:** New players start with the first five levels (1-5) unlocked:
   - **Enemy Warlords:** Levels 1-5 unlocked for battle (Sasquatch, Skunk Ape, Wendigo, Jersey Devil, Grassman)
   - **Player Warlords:** Levels 1-5 unlocked for play (defeat-based, but treated as already defeated for new players)
   - Players can immediately select any of these 5 Enemy Warlords or 5 Player Warlords
   - Level 6+ Warlords unlock sequentially as player progresses (Level 6 unlocks at Level 6, etc.)

### Pre-Game Flow

1. Player taps `Select Enemy Warlord` CTA (beneath Enemy Warlord avatar) - default Warlord selected (last played or new player)
2. Player taps `Select Player Warlord` CTA (above Player Warlord avatar) - default Warlord selected (last played or new player)
3. Player taps Primary CTA button to start the game.

Other pre-game options:

- Player views `XP`, `Level`, and `Gold`, taps `Gold` to purchase more Gold, taps `XP` to view level progression
- Player taps `Game Menu` (always displays top-right of screen) to view Game Options Overlay
- Player taps `Upgrade` to make 1-time purchase and upgrade to PAID account
- Player taps Enemy Warlord avatar to view Warlord details: status (locked, unlocked, defeated), Warlord stats, Special Power, Specials, game history with Player, CTA to select new Warlord
- Player taps Player Warlord avatar to view Warlord details: can purchase Battle Items (1 per level), can view Warlord stats, can view Warlord Special Power (changes per level), can view card Specials (changes per level), game history with Player, CTA to select new Warlord
- Player taps `Challenge` to view and accept challenges
- Player taps `Top Up` to view AdMob for Gold payout

### Main Game Flow

After starting the app removes pre-game CTAs and displays Decks (showing # of cards) and HP for each Warlord.

**Turn Flow:**

1. **Pre-Turn State**
   - Sound: Ambient game music (if enabled)
   - State: Previous turn complete, decks updated, charges maintained
   - Messaging: Status banner shows "Tap Play to Draw" or "Use Battle Item?"
   - Primary CTA displays "Play" button
   - **Battle Item Activation Available**: Player can tap Battle Item button to activate owned Battle Items before drawing

2. **Battle Item Activation Phase (Optional)**
   - **Player Battle Item Activation:**
     - Player can activate one owned Battle Item per turn (before card draw)
     - Battle Item button appears in Pre-Turn State (if player owns items with remaining charges for current level)
     - **Level Restriction:** Only Battle Items unlocked for the current level are available for activation
     - Tap Battle Item button → Battle Item Selection Overlay appears
     - Overlay shows all owned Battle Items with remaining charges
     - Each Battle Item shows: Icon, name, effect description
     - Player selects Battle Item to activate
     - Battle Item effect applies to upcoming draw (e.g., "+2 rank to next card", "Predict next card", "Extra draw")
     - Battle Item charge consumed (charges remaining decreases)
     - Overlay closes, effect indicator appears on status banner
     - State: Battle Item effect active for next draw
   
   - **Enemy Battle Item Activation (AI):**
     - Enemy AI evaluates game state (HP deficit, charge progress, deck size)
     - AI decides whether to activate Battle Item based on Warlord's assigned item and strategy
     - Activation probability: 5% on first play, 20% on replays (increased difficulty)
     - If activated, enemy Battle Item effect applies to upcoming draw
     - Enemy Battle Item charge consumed (charges remaining decreases)
     - Enemy Battle Item Notification appears briefly (shows item name and effect)
     - State: Enemy Battle Item effect active for next draw

3. **Card Draw Phase**
   - Player taps `Play` to start the game turn
   - Sound: Card flip sound (crisp chiptune)
   - Animation: Cards slide from decks to center battle zone (simultaneous for both)
   - Animation: Card flip reveal (180° rotate, face-up)
   - State: Cards drawn from shuffled decks, ranks compared
   - Messaging: Status banner updates to show cards drawn

3. **Resolution Phase**
   - Winner determined by card rank comparison
   - Sound: Win jingle (triumphant) or loss sound (low rumble)
   - Animation: Cards slide toward winner's deck area
   - State: Damage calculated (base + rank bonus), cards captured
   - Messaging: Status banner shows winner ("You Win!" or "Enemy Wins!")

4. **Post-Win Flow - Player Win:**
   - Sound: Win jingle, card capture sound
   - Animation: Cards slide to player deck, damage flash on enemy HP bar
   - State: Damage applied to enemy HP, cards added to player deck bottom, suit charges updated based on captured cards, Warlord charge progress updated (wins)
   - Messaging: Status banner shows "You Win! +X Damage"
   - Animation: Gold and XP rewards displayed (popup animation with numbers)
   - **Chain Check:** System checks for chain triggers (suit chains and poker-style chains)
   - **Chain Trigger:** If chain threshold reached, burst effect triggers immediately (visual explosion, sound, effect applied)
   - **Specials Icons Update:** Inline special icons on main board update to show ready status (glowing if ready, dimmed if unready)
   - Ready specials: Icons glow with pulsing animation (color matches suit)
   - Unready specials: Icons dimmed, show charge progress on tap (tooltip: "3/4 Hearts captured")
   - Player can tap ready special icons to activate (0-2 specials per turn)
   - Sound: Special activation sound (varies by type)
   - Animation: Special effects play on activation (visual effects match special type)
   - State: Special effects applied (heal, damage, buffs, etc.), charges reset if used
   - Primary CTA updates to "Next Turn" (player proceeds when ready)
   - Player taps "Next Turn" to proceed to next turn

5. **Post-Win Flow - Enemy Win:**
   - Sound: Loss sound, card capture sound
   - Animation: Cards slide to enemy deck, damage flash on player HP bar
   - State: Damage applied to player HP, cards added to enemy deck bottom, enemy suit charges updated, enemy Warlord charge progress updated (wins), player Warlord charge progress updated (damage taken adds to charge)
   - Messaging: Status banner shows "Enemy Wins! -X Damage"
   - **Enemy Chain Check:** System checks for enemy chain triggers (suit chains and poker-style chains)
   - **Enemy Chain Trigger:** If enemy chain threshold reached, enemy burst effect triggers automatically (visual notification, sound, effect applied)
   - Enemy AI evaluates ready specials and plays 0-2 highest-scoring specials
   - **Enemy Special Notification Overlay appears briefly**
   - Overlay shows what enemy played (suit specials + warlord special if used)
   - Sound: Enemy special activation sounds (thematic to special type)
   - Animation: Brief visual effects for enemy specials (matches special type)
   - State: Enemy special effects applied (damage, debuffs, etc.)
   - Overlay auto-dismisses after 2-3 seconds
   - Sound: Overlay dismiss sound (subtle)
   - Primary CTA updates to "Play" for next turn

6. **Turn Completion**
   - State: All turn effects resolved, decks updated, HP updated, charges maintained (Warlord Power charge updated if damage taken)
   - Animation: HP bars update smoothly, deck counts refresh
   - Messaging: Status banner ready for next turn
   - Return to Pre-Turn State

### Post-Game Flow

Gold Top-Up
- F2P player optionally taps CTA to earn extra Gold (Google AdMob)
- PAID player automatically earns extra Gold AND can still earn extra Gold through AdMob
- Payout varies and is displayed before player clicks-through

### XP, Levels, and Progress Flow

This section details how players earn XP, progress through levels, unlock content, and track their advancement through the game.

#### XP Earning Flow

**Turn Win XP Calculation:**
- Base XP: 7 XP per turn win (constant across all levels) - **Increased ~40% from 5 XP to compensate for shorter games with 36-card decks**
- Rank Bonus: +1 XP for Ace, +0.5 XP for King/Queen/Jack (rounded down), +0.25 XP for number cards 8-10
- Example: Win with Ace = 7 + 1 = 8 XP; Win with King = 7 + 0.5 = 7 XP; Win with 7 = 7 + 0 = 7 XP
- Streak Multiplier: Applied after base + rank bonus calculation
  - 3+ consecutive wins: 1.5x multiplier
  - 5+ consecutive wins: 2x multiplier
  - 10+ consecutive wins: 2.5x multiplier
- Maximum turn XP: ~20 XP (Ace win with 10+ streak = 8 × 2.5 = 20 XP)

**Game Win XP Bonuses:**
- Completion Bonus: +20 XP for winning the game
- First-Time Defeat Bonus: +50 XP for defeating an Enemy Warlord for the first time
- Streak Completion Bonus: If game won with active streak, multiply completion bonus by streak multiplier
- Example: Win game with 5-win streak = (20 + 50) × 2 = 140 XP bonus

**XP Display and Feedback:**
- Turn Win: Popup animation shows "+X XP" above card (fades after 2 seconds)
- Sound: Brief chiptune chime for XP gain (pitch increases with amount)
- Game Win: XP total displayed on results screen with progress bar fill animation
- Level Progress: Visual progress bar fills toward next level threshold
- No persistent XP bar in-game (keeps UI minimal)

**XP Sources Summary:**
- Turn wins: 7-20 XP per turn (with bonuses, increased ~40% for 36-card deck rebalance)
- Game completion: 20 XP base
- First-time defeats: 50 XP bonus
- Challenges: Variable (see Challenges section)
- Total per game: ~50-200 XP depending on performance (maintains similar totals despite shorter games)

#### Level Progression Flow

**XP Thresholds:**
- Level 1→2: 100 XP
- Level 2→3: 150 XP
- Level 3→4: 200 XP
- Level 4→5: 250 XP
- Level 5→10: +50 XP per level (300, 350, 400, 450, 500)
- Level 10→20: +75 XP per level (575, 650, 725, 800, 875, 950, 1025, 1100, 1175, 1250)
- Level 20→30: +100 XP per level (1350, 1450, 1550, 1650, 1750, 1850, 1950, 2050, 2150, 2250)
- Level 30→40: +125 XP per level (2375, 2500, 2625, 2750, 2875, 3000, 3125, 3250, 3375, 3500)
- Level 40→50: +150 XP per level (3650, 3800, 3950, 4100, 4250, 4400, 4550, 4700, 4850, 5000)
- Level 50→59: +200 XP per level (5200, 5400, 5600, 5800, 6000, 6200, 6400, 6600, 6800)
- Total XP to max level (59): ~68,000 XP

**Level-Up Sequence:**
1. **Trigger:** XP threshold reached (can happen mid-game or post-game)
2. **Timing:** 
   - If mid-game: Level-up occurs after current game ends
   - If post-game: Level-up occurs immediately after results screen
3. **Animation:** 
   - Screen dims slightly (50% opacity overlay)
   - Level number animates upward with particle effects
   - "LEVEL UP!" text appears with chiptune fanfare (2 seconds)
   - Progress bar resets and fills to show new level progress
4. **Notification:** 
   - "You've reached Level X!"
   - Display unlocks (new Enemy Warlord, Battle Items available)
   - Show level-up bonus Gold (see Gold Economy below)
5. **Unlocks Display:**
   - New Enemy Warlord: Avatar preview, name, level requirement
   - Battle Items: List of new items available for purchase
   - "Try New Warlord?" prompt displayed
6. **State Update:**
   - Level incremented
   - XP reset to 0 (or carry over excess XP if applicable)
   - New content unlocked
   - UI updates (Warlord selection screens refresh)

**Level-Up Rewards:**
- Bonus Gold: 50 Gold × new level (e.g., Level 5 = 250 Gold bonus)
- Unlock: 1 new Enemy Warlord (if available)
- Unlock: New Battle Items become available for purchase
- Stat Preview: Show next level's potential unlocks

**Level Display:**
- Pre-game: Level shown in Warlord selection screens (top-right corner)
- Post-game: Level shown on results screen
- Menu: Level shown in Game Menu overlay
- In-game: Level NOT displayed (keeps UI minimal)

#### Gold Economy Flow

**Gold Earning Sources:**

**Turn Win Gold:**
- Base Gold: 14 Gold per turn win (constant across all levels) - **Increased ~40% from 10 Gold to compensate for shorter games with 36-card decks**
- Rank Bonus: +2 Gold for Ace, +1 Gold for King/Queen/Jack, +0.5 Gold for number cards 8-10 (rounded down)
- Example: Win with Ace = 14 + 2 = 16 Gold; Win with King = 14 + 1 = 15 Gold
- Streak Multiplier: Applied after base + rank bonus
  - 3+ consecutive wins: 1.5x multiplier
  - 5+ consecutive wins: 2x multiplier
  - 10+ consecutive wins: 2.5x multiplier
- Maximum turn Gold: ~40 Gold (Ace win with 10+ streak = 16 × 2.5 = 40 Gold)

**Game Win Gold:**
- Completion Bonus: +50 Gold for winning the game
- First-Time Defeat Bonus: +100 Gold for defeating Enemy Warlord for the first time
- Streak Completion Bonus: Multiply completion bonus by streak multiplier
- Example: Win game with 5-win streak = (50 + 100) × 2 = 300 Gold bonus

**Level-Up Gold:**
- Bonus Gold: 50 Gold × new level
- Example: Level 5 = 250 Gold bonus

**Advertising Gold (F2P):**
- AdMob Rewarded Video: 25-100 Gold (randomized, displayed before ad)
- AdMob Interstitial: 10-50 Gold (randomized, displayed before ad)
- Daily Ad Bonus: 50 Gold (first ad of the day)
- Maximum per day: ~500 Gold from ads (soft cap)

**PAID Account Gold:**
- Automatic Gold: Matches ad-based rewards automatically (no ads required)
- Same amounts as F2P ad rewards
- Can still watch ads for additional Gold (optional)

**IAP Gold Packages:**
- Small Pack: $0.99 = 500 Gold
- Medium Pack: $2.99 = 1,750 Gold (17% bonus)
- Large Pack: $4.99 = 3,500 Gold (40% bonus)
- Mega Pack: $9.99 = 8,000 Gold (60% bonus)

**Gold Spending:**

**Game Attempt Fees:**
- First 3 attempts per Enemy Warlord: Free
- Subsequent attempts: 25 Gold per attempt (constant across all levels)
- Fee displayed before game starts (if applicable)
- "Insufficient Gold" warning if player lacks funds

**Battle Items:**
- Cost varies by item level and power
- Level 1-10 items: 100-300 Gold
- Level 11-25 items: 300-750 Gold
- Level 26-40 items: 750-1,500 Gold
- Level 41+ items: 1,500-3,000 Gold
- One-time purchase per item (unlock for that level only)
- **Level Restriction:** Battle Items are only available during the level they're unlocked. Advancing to a new level means starting without Battle Items from previous levels

**Gold Display and Notifications:**
- Pre-game: Gold shown in Warlord selection screens (top-left corner)
- Post-game: Gold total displayed on results screen
- Menu: Gold shown in Game Menu overlay
- In-game: Gold NOT displayed (keeps UI minimal)
- Low Balance Warning: If Gold < 50, show warning when attempting paid game
- Gold Gain Popup: "+X Gold" animation on turn/game win (fades after 2 seconds)
- Sound: Brief chiptune chime for Gold gain (different pitch from XP)

**Gold Economy Balance:**
- Average game: ~100-200 Gold earned (with bonuses)
- Average game cost: 0-25 Gold (first 3 attempts free)
- Net Gold per game: ~75-200 Gold (positive economy)
- Battle Items: Require 2-5 games to afford (encourages replay)

#### Warlord Unlock Flow

**Enemy Warlord Unlocks (Level-Based):**

**Unlock Trigger:**
- One new Enemy Warlord unlocked per level
- Unlock occurs when player reaches the required level
- **Initial Unlocks:** New players start with levels 1-5 unlocked (Sasquatch, Skunk Ape, Wendigo, Jersey Devil, Grassman)
- **Progressive Unlocks:** Level 6+ unlock sequentially (Level 6 unlocks at Level 6, Level 7 at Level 7, etc.)

**Unlock Sequence:**
1. **Level-Up Occurs:** Player reaches new level
2. **Unlock Notification:** "New Enemy Warlord Unlocked!" appears
3. **Warlord Preview:**
   - Avatar displayed (100x120px)
   - Name and level requirement shown
   - Brief description (1-2 sentences)
   - Stats preview (HP, Damage, Charge)
4. **Visual Feedback:**
   - Avatar glows/pulses
   - Particle effects around avatar
   - Sound: Thematic chiptune (matches Warlord theme)
5. **Access Granted:**
   - Warlord added to Enemy Warlord selection gallery
   - Warlord appears in selection screen immediately
   - "Try This Warlord?" prompt displayed

**First-Time Defeat Rewards:**
- +50 XP bonus
- +100 Gold bonus
- Unlocks corresponding Player Warlord (see below)
- "First Defeat" badge on Warlord details screen

**Player Warlord Unlocks (Defeat-Based):**

**Unlock Trigger:**
- Player Warlord unlocked after defeating corresponding Enemy Warlord
- Must be first-time defeat (replays don't unlock)
- Unlock occurs immediately after game win
- **Initial Unlocks:** New players start with levels 1-5 unlocked (Sasquatch, Skunk Ape, Wendigo, Jersey Devil, Grassman). These are treated as already defeated for new players, allowing immediate selection
- **Progressive Unlocks:** Level 6+ Player Warlords unlock after first-time defeat of corresponding Enemy Warlord

**Unlock Sequence:**
1. **Game Win:** Player defeats Enemy Warlord for first time
2. **Unlock Notification:** "New Player Warlord Unlocked!" appears
3. **Warlord Preview:**
   - Avatar displayed (100x120px)
   - Name shown
   - "You can now play as [Warlord Name]!"
   - Stats preview (HP, Damage, Charge, Specials)
4. **Visual Feedback:**
   - Avatar glows/pulses
   - Particle effects around avatar
   - Sound: Triumphant chiptune fanfare
5. **Access Granted:**
   - Warlord added to Player Warlord selection gallery
   - Warlord appears in selection screen immediately
   - "Play as [Warlord]?" prompt displayed

**Unlock Display Locations:**
- Pre-game: Unlocked Warlords shown in selection galleries
- Locked Warlords: Grayed out with "Locked" badge and level requirement
- Defeated Warlords: Show "Defeated" badge and replay option
- Menu: Warlord gallery accessible from Game Menu overlay

**Replay System:**
- Defeated Enemy Warlords: Can be replayed for free (no Gold fee)
- Replay rewards: Normal turn/game rewards (no first-time bonuses)
- Replay difficulty: Slightly increased (+10% AI difficulty, enemy stats scale)
- Replay tracking: Game history shows win/loss record vs. each Warlord

#### Streak System Flow

**Streak Tracking:**
- Streak counter: Tracks consecutive turn wins (not game wins)
- Streak resets: On any turn loss (enemy wins a turn)
- Streak persists: Across turns within the same game
- Streak display: Visual indicator on game table (subtle, top-center)

**Streak Milestones:**
- 3 consecutive wins: 1.5x multiplier activated
- 5 consecutive wins: 2x multiplier activated
- 10 consecutive wins: 2.5x multiplier activated
- 15 consecutive wins: 3x multiplier activated (rare achievement)
- 20+ consecutive wins: 3x multiplier + special visual effect

**Streak Visual Feedback:**
- Streak Counter: Small number indicator (top-center of screen, subtle)
- Milestone Notifications: "3 Win Streak!" popup (fades after 2 seconds)
- Visual Effects: Cards glow brighter with higher streaks
- Sound: Escalating chiptune arpeggio (higher pitch with longer streaks)

**Streak Bonuses:**
- XP Multiplier: Applied to turn XP (see XP Earning Flow above)
- Gold Multiplier: Applied to turn Gold (see Gold Economy Flow above)
- Game Completion: Streak multiplier applies to completion bonuses
- Visual Reward: Streak counter glows/pulses at milestones

**Streak Reset:**
- Trigger: Player loses any turn (enemy wins)
- Notification: "Streak Broken!" brief message (1 second)
- Visual: Streak counter fades out
- Sound: Brief "break" sound effect
- Reset: Streak counter returns to 0

**Streak Persistence:**
- Streak continues: Within the same game
- Streak resets: Between games (new game = fresh streak)
- Streak tracking: Shown in post-game statistics

#### Progress Visualization

**Progress Bars:**

**XP Progress Bar:**
- Location: Pre-game Warlord selection screens, post-game results screen
- Display: Shows current XP / XP needed for next level
- Visual: Pixel art progress bar (fills left to right)
- Animation: Smooth fill animation when XP gained
- Example: "1,250 / 1,350 XP to Level 21"

**Charge Progress Indicators:**
- Location: Inline special icons on main board (in-game)
- Display: Shows charge progress on tap (tooltip appears)
- Format: 
  - Suit specials: "X/Y [Suit] captured" (e.g., "3/4 Hearts captured")
  - Warlord Power: "X/Y wins OR X/Y damage" (e.g., "2/5 wins OR 4/8 damage")
- Visual: Tooltip with progress text appears on tap (unready specials)
- Ready State: Icon glows with pulsing animation when threshold reached

**Progress Indicators Summary:**
- Level: Number display (pre-game, post-game, menu)
- XP: Progress bar (pre-game, post-game)
- Gold: Number display (pre-game, post-game, menu)
- Streak: Counter (in-game, subtle)
- Charges: Progress indicators (in-game overlay)

**Level Display:**
- Format: "Level X"
- Font: Pixel font, 16-20px
- Color: Yellow/gold accent color
- Position: Top-right corner (pre-game screens)

**Unlock Previews:**
- Next Level Preview: Shows what unlocks at next level
- Format: "Level X unlocks: [Enemy Warlord Name]"
- Location: Pre-game screens, level progress display
- Visual: Small avatar preview + name

**Statistics Tracking:**
- Games Played: Total games started
- Games Won: Total games completed successfully
- Win Rate: Percentage (Games Won / Games Played)
- Total XP Earned: Lifetime XP accumulation
- Total Gold Earned: Lifetime Gold accumulation
- Highest Streak: Best consecutive turn wins
- Warlords Defeated: Count of unique Enemy Warlords defeated
- Location: Game Menu overlay, "Statistics" section

#### Post-Game Progression

**Results Screen Flow:**

1. **Game End:** Win or loss condition met
2. **Results Screen Appears:**
   - Dims game table (50% opacity overlay)
   - Results panel slides up from bottom (centered)
   - Sound: Win fanfare or loss sound

3. **Results Display:**
   - **Win/Loss Status:** Large text ("VICTORY!" or "DEFEAT")
   - **XP Gained:** Total XP earned this game (with breakdown)
     - Turn XP: X XP
     - Completion Bonus: X XP
     - First-Time Bonus: X XP (if applicable)
     - Streak Bonus: X XP (if applicable)
     - Total: X XP
   - **Gold Gained:** Total Gold earned this game (with breakdown)
     - Turn Gold: X Gold
     - Completion Bonus: X Gold
     - First-Time Bonus: X Gold (if applicable)
     - Streak Bonus: X Gold (if applicable)
     - Total: X Gold
   - **Level Progress:** Progress bar showing XP toward next level
   - **Streak Display:** Final streak count (if applicable)

4. **Progress Bar Animation:**
   - XP progress bar fills smoothly (2-3 seconds)
   - Gold number counts up (1-2 seconds)
   - Visual feedback: Particles/sparks on fill completion

5. **Level-Up Check:**
   - If XP threshold reached: Trigger level-up sequence (see Level Progression Flow)
   - If not: Show "X XP to next level" message

6. **Unlock Check:**
   - If new Warlord unlocked: Show unlock sequence (see Warlord Unlock Flow)
   - If Battle Items available: Show "New Items Available" notification

7. **Next Steps:**
   - **Primary CTA:** "Continue" or "Play Again"
   - **Secondary CTAs:** 
     - "Select Warlord" (change Warlord)
     - "View Progress" (detailed stats)
     - "Earn Gold" (watch ad, F2P only)

**Level-Up Celebration (Post-Game):**
- Occurs after results screen if level-up threshold reached
- Full-screen celebration overlay
- "LEVEL UP!" animation (2-3 seconds)
- Unlocks displayed (new Enemy Warlord, Battle Items)
- Level-up bonus Gold awarded
- Sound: Extended fanfare (3-4 seconds)

**Unlock Celebration (Post-Game):**
- Occurs after results screen if Warlord unlocked
- Overlay shows Warlord preview
- "New Warlord Unlocked!" message
- Avatar animation (glow, pulse, particles)
- Sound: Thematic chiptune (matches Warlord)
- Duration: 3-4 seconds

**Post-Game Options:**
- **Continue:** Return to pre-game screen (select Warlord, start new game)
- **Replay:** Immediately restart game with same Warlords
- **Select Warlord:** Change Player or Enemy Warlord
- **View Progress:** Detailed statistics and progress screens
- **Earn Gold:** Watch ad for Gold (F2P only)
- **Menu:** Access Game Menu overlay

#### Challenges Integration

**Challenge Progress Tracking:**
- Challenges: Optional objectives that provide bonus rewards
- Progress Display: Shown in Game Menu overlay, "Challenges" section
- Format: "Challenge: [Objective] - Progress: X/Y"
- Example: "Defeat 5 Warlords - Progress: 3/5"

**Challenge Types:**
- **Win Streaks:** "Win 10 turns in a row" - Rewards: 100 Gold, 50 XP
- **Warlord Defeats:** "Defeat 5 different Warlords" - Rewards: 200 Gold, 100 XP
- **Special Usage:** "Use 20 specials" - Rewards: 150 Gold, 75 XP
- **Gold Collection:** "Earn 1,000 Gold" - Rewards: 500 Gold, 200 XP
- **Level Milestones:** "Reach Level 10" - Rewards: 300 Gold, 150 XP

**Challenge Completion:**
- Notification: "Challenge Complete!" popup
- Rewards: Gold and XP awarded immediately
- Visual: Challenge badge animates, checkmark appears
- Sound: Achievement chiptune
- Progress: Challenge marked as complete, new challenge unlocked

**Challenge Notifications:**
- Pre-game: Show active challenges in Warlord selection screen
- Post-game: Show challenge progress updates on results screen
- Menu: Full challenge list in Game Menu overlay

**Challenge Rewards:**
- Gold: 50-500 Gold per challenge (varies by difficulty)
- XP: 25-200 XP per challenge (varies by difficulty)
- Badges: Visual badges for completed challenges
- Unlocks: Some challenges unlock special content (rare)

#### Progress Persistence

**Local Storage (F2P):**
- Progress saved: Level, XP, Gold, Unlocks, Statistics
- Storage: Browser localStorage (persists across sessions)
- Limitations: Device-specific (not portable)
- Backup: Cloud save available via PAID upgrade

**Cloud Storage (PAID):**
- Progress saved: All F2P data + cloud sync
- Storage: Server-side database (portable across devices)
- Sync: Automatic on login (if implemented)
- Backup: Redundant backups, progress recovery

**Progress Loss Prevention:**
- Auto-save: After every game completion
- Manual Save: Available in Game Menu (PAID accounts)
- Recovery: Contact support for progress recovery (PAID accounts)
- Warning: "Progress not saved" message if localStorage fails

**Cross-Device Sync (PAID):**
- Login: Account system (email/password) for PAID users
- Sync: Progress syncs automatically on login
- Conflict Resolution: Most recent progress takes precedence
- Offline Mode: Progress cached locally, syncs when online

#### Progression Pacing

**Early Game (Levels 1-10):**
- Fast progression: ~2-3 games per level
- Frequent unlocks: New Warlord every level
- Learning curve: Players learn mechanics
- Rewards: Generous Gold/XP to encourage play

**Mid Game (Levels 11-25):**
- Moderate progression: ~3-5 games per level
- Steady unlocks: New Warlord every level
- Mastery phase: Players develop strategies
- Rewards: Balanced Gold/XP economy

**Late Game (Levels 26-40):**
- Slower progression: ~5-8 games per level
- Challenging unlocks: Higher level Warlords
- Expert play: Requires skill and strategy
- Rewards: Higher Gold/XP but longer grinds

**End Game (Levels 41-59):**
- Slow progression: ~8-12 games per level
- Prestige unlocks: Rare, powerful Warlords
- Mastery required: Optimal play necessary
- Rewards: Maximum Gold/XP, achievement-focused

**Progression Balance:**
- Average game duration: ~5-10 minutes
- Average XP per game: ~50-200 XP
- Average Gold per game: ~100-200 Gold
- Time to max level: ~40-60 hours of gameplay (estimated)
- Encourages: Replayability, skill improvement, strategic play


## Game Design and Systems

### Core App Loop

The Core App Loop represents the meta-gamecycle that keeps players engaged beyond individual game sessions. It encompasses the full player journey from app launch through progression, unlocks, monetization, and re-engagement. This loop is distinct from the Core Game Loop, which handles turn-by-turn gameplay within a single session.

#### Overview

**Definition:** The Core App Loop is the repeating cycle of Pre-Game → Game → Post-Game → Pre-Game that drives player retention, progression, and monetization.

**Key Objectives:**
- Retain players through progression and unlocks
- Encourage daily engagement
- Integrate monetization naturally
- Provide clear goals and feedback
- Create collection and completion incentives

**Relationship to Core Game Loop:**
- Core Game Loop: Handles turn-by-turn mechanics within a game session
- Core App Loop: Handles the broader player journey across multiple sessions
- Core Game Loop is nested within the Core App Loop's "Game" phase

#### Primary Loop Flow

**Main Cycle:**
```
App Launch
  ↓
Pre-Game Screen
  ↓
[Daily Bonus Check] → Award if applicable
  ↓
Warlord Selection (Player + Enemy)
  ↓
Battle Item Management
  ↓
Gold Balance Check
  ↓
[Gold Fee Required?] → Yes → Payment/Ad Prompt → Continue
  ↓ No
Game Session (Core Game Loop)
  ↓
Post-Game Results
  ↓
[Level-Up?] → Yes → Level-Up Celebration → Continue
  ↓ No
[Unlocks?] → Yes → Unlock Celebration → Continue
  ↓ No
[Collection Milestone?] → Yes → Achievement Celebration → Continue
  ↓ No
Reward Summary & Next Actions
  ↓
[Player Continues?] → Yes → Return to Pre-Game
  ↓ No
App Exit / Background
```

**Secondary Loops (can enter/exit anytime):**
- Menu Navigation (Game Menu overlay)
- Warlord Selection (pre-game)
- Battle Item Shop (pre-game)
- Challenge Viewing (pre-game/post-game)
- Leaderboards (pre-game/post-game)
- Statistics (pre-game/post-game)

#### Session Entry Flow

**App Launch Sequence:**

1. **Page Load**
   - Loading screen: Pixel art logo, "Loading..." text
   - Sound: Brief loading chiptune
   - Duration: <2 seconds (optimize for fast load)

2. **Progress Loading**
   - Check localStorage for saved progress
   - Load player data:
     - Level, XP, Gold
     - Unlocked Warlords (Enemy + Player)
     - Battle Items owned
     - Statistics (games played, win rate, etc.)
     - Collection progress
   - Check for PAID account status (if applicable)
   - Load cloud sync data (PAID accounts only)

3. **First-Time vs Returning Player Detection**
   - **First-Time:** No localStorage data found
     - Initialize default state: Level 1, 0 XP, 100 Gold (starter Gold)
     - Set default Warlords: Sasquatch vs Sasquatch
     - **Initial Unlocks:** Unlock first five levels (1-5) for both Enemy and Player Warlords:
       - Enemy Warlords unlocked: Sasquatch (L1), Skunk Ape (L2), Wendigo (L3), Jersey Devil (L4), Grassman (L5)
       - Player Warlords unlocked: Same 5 Warlords (treated as already defeated for new players)
       - Levels 6+ unlock sequentially as player progresses
     - No tutorial (player learns through play)
   - **Returning:** localStorage data found
     - Load saved state
     - Calculate time since last session
     - Check for daily bonus eligibility

4. **Daily Bonus Check**
   - Check last login timestamp
   - If 24+ hours since last login: Award daily bonus
   - Daily Bonus: 100 Gold + 50 XP
   - Display: "Daily Bonus!" popup with rewards
   - Sound: Celebration chiptune
   - Update last login timestamp

5. **Notification Check**
   - Check for pending notifications:
     - New unlocks available
     - Challenge completions
     - Achievement milestones
     - Leaderboard updates
   - Display notification badges on relevant UI elements

6. **Initial State Setup**
   - Display pre-game screen
   - Show current Warlords (default or last played)
   - Show Gold balance
   - Show level and XP progress
   - Show any notification badges

**First-Time Player Experience:**

**No Tutorial Approach:**
- Player immediately sees pre-game screen
- Default setup: Sasquatch (Player) vs Sasquatch (Enemy)
- **Initial Unlocks:** Player can immediately select any of 5 unlocked Enemy Warlords or 5 unlocked Player Warlords
- Player can tap "Play" immediately
- Learning happens through:
  - Visual feedback (cards, HP bars, status messages)
  - Trial and error
  - Natural discovery of mechanics
  - Status banner messages guide decisions
  - Experimentation with different Warlord combinations (5 Enemy × 5 Player = 25 combinations available immediately)

**Progression Path:**
- **Initial State:** New players start with levels 1-5 unlocked for both Enemy and Player Warlords
- Level 1: Player can immediately select any of the 5 unlocked Enemy Warlords (Sasquatch, Skunk Ape, Wendigo, Jersey Devil, Grassman)
- Player can select any of the 5 unlocked Player Warlords
- Default setup: Sasquatch (Player) vs Sasquatch (Enemy)
- Upon first defeat: Player learns mechanics, can replay or try different Warlord combinations
- Upon first win: Player earns XP and Gold, can continue with any unlocked Warlords
- **Progressive Unlocks:** Level 6+ unlock sequentially as player reaches each level (Level 6 unlocks at Level 6, Level 7 at Level 7, etc.)

**Onboarding Hints:**
- First game: Status banner shows "Tap Play to Draw Cards"
- First win: Status banner shows "You Win! Tap to Continue"
- First special ready: Status banner shows "Special Ready! Check Overlay"
- Hints fade after 3-5 games (player has learned basics)

#### Pre-Game Phase

**Pre-Game Screen Layout:**
- Enemy Warlord avatar (top)
- Player Warlord avatar (bottom)
- Gold balance display (top-left)
- Level/XP display (top-right)
- Primary CTA: "Play" button (bottom-center)
- Secondary CTAs: Menu icon, Warlord selection buttons
- **Gauntlet Mode Toggle:** Mode selector button (top-center, visible only if unlocked)

**Pre-Game Flow:**

1. **Screen Display**
   - Show selected Warlords (default or last played)
   - Display Gold balance
   - Display level and XP progress bar
   - **Gauntlet Mode Indicator:** If Gauntlet Mode unlocked, show mode toggle button
   - **Gauntlet Status:** If active Gauntlet run exists, show "Resume Gauntlet" option

2. **Mode Selection (Gauntlet Mode Unlocked)**
   - Player taps "Mode" button (top-center)
   - Mode Selection Overlay opens
   - Options displayed:
     - "Standard Mode" (default, current mode)
     - "Gauntlet Mode" (unlocked after defeating all 59 Warlords)
   - **Gauntlet Mode Active:** Shows current wave/battle progress, best wave reached
   - **Resume Option:** If active Gauntlet run exists, "Resume Gauntlet" button prominent
   - Player selects mode
   - Overlay closes, mode indicator updates
   - **Gauntlet Mode Active:** Pre-Game screen updates to show Gauntlet-specific UI (wave counter, enemy selection disabled)

3. **Warlord Selection**
   - **Standard Mode:** Player can select both Enemy and Player Warlords
   - **Gauntlet Mode:** Enemy Warlord selection disabled (automatically assigned by wave), Player Warlord selection enabled
   
   - Player taps "Select Enemy Warlord" button (Standard Mode only)
   - Enemy Warlord Select Gallery opens
   - Shows all unlocked Enemy Warlords
   - **New Players:** Levels 1-5 unlocked immediately (Sasquatch, Skunk Ape, Wendigo, Jersey Devil, Grassman)
   - Locked Warlords: Grayed out, show level requirement (Level 6+)
   - Defeated Warlords: Show "Defeated" badge, replay option
   - **Warlord of the Day:** Special badge/indicator (e.g., "⭐ Warlord of the Day") with active modifier displayed (e.g., "Double Streak Multiplier Active")
   - Player selects Enemy Warlord
   - Gallery closes, new Enemy Warlord displayed
   
   - Player taps "Select Player Warlord" button
   - Player Warlord Select Gallery opens
   - Shows all unlocked Player Warlords
   - **New Players:** Levels 1-5 unlocked immediately (Sasquatch, Skunk Ape, Wendigo, Jersey Devil, Grassman)
   - Locked Warlords: Grayed out, show "Defeat [Enemy Warlord] to unlock" (Level 6+)
   - Player selects Player Warlord
   - Gallery closes, new Player Warlord displayed

   - Player taps "Select Player Warlord" button
   - Player Warlord Select Gallery opens
   - Shows all unlocked Player Warlords
   - **New Players:** Levels 1-5 unlocked immediately (Sasquatch, Skunk Ape, Wendigo, Jersey Devil, Grassman)
   - Locked Warlords: Grayed out, show "Defeat [Enemy Warlord] to unlock" (Level 6+)
   - Player selects Player Warlord
   - Gallery closes, new Player Warlord displayed

4. **Battle Item Management**
   - Player taps Player Warlord avatar
   - Warlord Details Overlay opens
   - Shows equipped Battle Item (if any)
   - Shows available Battle Items for purchase
   - Player can purchase and equip Battle Items
   - Cost: 100-3,000 Gold (varies by level)
   - One Battle Item per level (available only during that level)
   - **Level Restriction:** Battle Items are only available during the level they're unlocked. When advancing to a new level, player starts without Battle Items from previous levels
   - Overlay closes after selection

5. **Challenge Viewing**
   - Player taps "Challenges" button (if available)
   - Challenges Overlay opens
   - Shows active challenges and progress
   - Shows completed challenges
   - Player can view rewards
   - Overlay closes

6. **Leaderboard Viewing**
   - Player taps "Leaderboards" button (if available)
   - Leaderboards Overlay opens
   - Shows global leaderboards:
     - Highest Level
     - Most Warlords Defeated
     - Highest Win Streak
     - Total Games Won
   - Shows player's rank and position
   - Overlay closes

7. **Gold Balance Check (Standard Mode Only)**
   - **Standard Mode:** System checks if Gold fee is required
   - First 3 attempts per Enemy Warlord: Free
   - Subsequent attempts: 25 Gold fee
   - If insufficient Gold: Show warning before game starts
   - **Gauntlet Mode:** No Gold fee required (free to play)

8. **Game Fee Payment (If Required, Standard Mode Only)**
   - If Gold fee required and player has sufficient Gold:
     - Deduct Gold immediately
     - Show "-25 Gold" animation
     - Proceed to game start
   - If Gold fee required and player lacks Gold:
     - Show "Insufficient Gold" message
     - Display options:
       - "Watch Ad for Gold" (F2P)
       - "Purchase Gold" (IAP)
       - "Cancel"
     - Player selects option or cancels

9. **Game Start**
   - Player taps "Play" button
   - Pre-game CTAs fade out
   - Game table appears
   - Decks displayed
   - HP bars displayed
   - Primary CTA updates to "Play" (for card draw)
   - Transition to Core Game Loop

**Pre-Game State Persistence:**
- Warlord selections saved to localStorage
- Last played Warlords become defaults for next session
- Gold balance persists
- Progress persists

#### Post-Game Phase

**Post-Game Flow:**

1. **Game End Trigger**
   - Win condition met (HP = 0 or deck empty)
   - Loss condition met (HP = 0 or deck empty)
   - Game state frozen

2. **Results Screen Display**
   - Dim game table (50% opacity overlay)
   - Results panel slides up from bottom (centered)
   - Sound: Win fanfare (victory) or loss sound (defeat)

3. **Results Display Content**
   - **Win/Loss Status:** Large text ("VICTORY!" or "DEFEAT")
   - **XP Gained:** Total XP earned (with breakdown)
     - Turn XP: X XP
     - Completion Bonus: X XP
     - First-Time Bonus: X XP (if applicable, Standard Mode only)
     - Streak Bonus: X XP (if applicable)
     - Gauntlet Streak Bonus: X XP (if applicable, Gauntlet Mode only)
     - Wave Completion Bonus: X XP (if applicable, Gauntlet Mode only)
     - Daily Challenge Bonus: +50 XP (if Warlord of the Day defeated, Standard Mode only)
     - Total: X XP
   - **Gold Gained:** Total Gold earned (with breakdown)
     - Turn Gold: X Gold
     - Completion Bonus: X Gold
     - First-Time Bonus: X Gold (if applicable, Standard Mode only)
     - Streak Bonus: X Gold (if applicable)
     - Gauntlet Streak Bonus: X Gold (if applicable, Gauntlet Mode only)
     - Wave Completion Bonus: X Gold (if applicable, Gauntlet Mode only)
     - Daily Challenge Bonus: +100 Gold (if Warlord of the Day defeated, Standard Mode only)
     - Total: X Gold
   - **Level Progress:** Progress bar showing XP toward next level
   - **Streak Display:** Final streak count (if applicable)
   - **Gauntlet Progress:** Wave/battle progress (if Gauntlet Mode active)
   - **Daily Challenge Complete:** "⭐ Daily Challenge Complete!" message and animation (if Warlord of the Day defeated, Standard Mode only)
   - **Statistics Update:** Games played, win rate, etc.

4. **Progress Bar Animations**
   - XP progress bar fills smoothly (2-3 seconds)
   - Gold number counts up (1-2 seconds)
   - Visual feedback: Particles/sparks on fill completion
   - Sound: Escalating chiptune as progress fills

5. **Level-Up Check**
   - If XP threshold reached:
     - Trigger level-up sequence (see Level Progression Flow in XP section)
     - Level-up celebration overlay
     - Unlocks displayed
     - Level-up bonus Gold awarded
     - Continue to unlock check
   - If not:
     - Show "X XP to next level" message
     - Continue to unlock check

6. **Unlock Check**
   - Check for new Warlord unlocks (Enemy or Player)
   - If unlocked:
     - Trigger unlock celebration (see Warlord Unlock Flow)
     - Unlock overlay with Warlord preview
     - Sound: Thematic chiptune
     - Continue to collection check
   - If not:
     - Continue to collection check

7. **Collection Milestone Check**
   - Check collection progress:
     - Warlords defeated count
     - Battle Items collected count
     - Achievement milestones
   - If milestone reached:
     - Achievement celebration overlay
     - Badge awarded
     - Reward displayed (Gold, XP, or special unlock)
     - Sound: Achievement chiptune
     - Continue to monetization hooks
   - If not:
     - Continue to monetization hooks

8. **Monetization Hooks**
   - **F2P Players:**
     - "Earn Extra Gold" button (watch ad)
     - Ad reward: 25-100 Gold (randomized, displayed before ad)
     - "Upgrade to PAID" prompt displayed (if low Gold)
   - **PAID Players:**
     - Automatic Gold bonus (matches ad rewards, no ad required)
     - "Watch Ad for Extra Gold" button available (can still watch ads)
   - **All Players:**
     - "Purchase Gold" button (IAP) - always available
     - IAP packages displayed if player taps

9. **Gauntlet Mode Transition Check (Gauntlet Mode Only)**
   - **Battle Win:**
     - Check if wave complete (5 battles won)
     - If wave complete: Show "Wave Complete!" celebration overlay
     - Wave completion bonus displayed
     - Milestone check (if applicable)
     - "Continue to Next Battle" button (proceeds to next battle in wave)
     - "Change Warlord" option (allows Warlord selection before next battle)
   - **Battle Loss:**
     - Show "Gauntlet Run Ended" message
     - Display final wave reached
     - Show total rewards earned during run
     - "Restart Gauntlet" button (starts new run from Wave 1)
     - "Exit to Menu" button (returns to Pre-Game)
   - **Standard Mode:** Skip this step

10. **Next Action Prompts**
   - **Standard Mode:**
     - **Primary CTA:** "Play Again" (restart with same Warlords)
     - **Secondary CTAs:**
       - "Select Warlord" (change Warlords)
       - "View Progress" (detailed statistics)
       - "View Challenges" (challenge progress)
       - "View Leaderboards" (rankings)
       - "Share Result" (social sharing)
       - "Menu" (access game menu)
   - **Gauntlet Mode (Battle Win):**
     - **Primary CTA:** "Continue Gauntlet" (proceed to next battle)
     - **Secondary CTAs:**
       - "Change Warlord" (select different Player Warlord)
       - "Exit Gauntlet" (save progress, return to Pre-Game)
       - "View Gauntlet Stats" (current run statistics)
   - **Gauntlet Mode (Battle Loss):**
     - **Primary CTA:** "Restart Gauntlet" (start new run)
     - **Secondary CTAs:**
       - "Exit to Menu" (return to Pre-Game)
       - "View Gauntlet Leaderboard" (see rankings)

11. **Player Decision**
    - Player selects next action
    - **Standard Mode:**
      - If "Play Again": Return to Pre-Game (same Warlords)
      - If "Select Warlord": Return to Pre-Game (Warlord selection)
      - If other: Navigate to respective screen/overlay
    - **Gauntlet Mode:**
      - If "Continue Gauntlet": Proceed to next battle (enemy auto-selected)
      - If "Change Warlord": Warlord selection overlay, then continue
      - If "Restart Gauntlet": Reset Gauntlet state, start Wave 1
      - If "Exit Gauntlet": Save progress, return to Pre-Game
    - If exit: Save progress, app backgrounds/closes

**Post-Game State Updates:**
- XP accumulated
- Gold accumulated
- Level updated (if leveled up)
- Unlocks updated
- Statistics updated
- Collection progress updated
- All saved to localStorage

#### Progression Integration

**How Progression Fits into the Loop:**

**XP Accumulation:**
- XP earned during game (turn wins)
- XP bonus on game completion
- XP displayed on post-game results
- XP progress bar updates
- Level-up triggers when threshold reached

**Level Progression:**
- Level increases unlock new content
- Each level unlocks 1 new Enemy Warlord
- Level-up celebrations occur post-game
- Level displayed in pre-game screens

**Unlock Flow:**
- Enemy Warlords: Unlocked by level (automatic)
- Player Warlords: Unlocked by defeating Enemy Warlord (first-time defeat)
- Battle Items: Unlocked by level (available for purchase)
- Unlocks celebrated post-game

**Progress Visualization:**
- Progress bars: XP, charges, challenges
- Level display: Current level, next level preview
- Collection percentage: "X/59 Warlords Defeated"
- Statistics: Games played, win rate, highest streak

**Progression Carrots:**
- "X XP to next level" messaging
- "X Gold to afford [Battle Item]" messaging
- Unlock previews: "Defeat [Warlord] to unlock [Player Warlord]"
- Collection progress: "X/59 Warlords Defeated"

#### Re-engagement Hooks

**Daily Engagement Mechanics:**

**Daily Login Bonus:**
- Trigger: 24+ hours since last login
- Reward: 100 Gold + 50 XP
- Display: "Daily Bonus!" popup on app launch
- Sound: Celebration chiptune
- Visual: Gold/XP animation
- Persistence: Last login timestamp saved

**Daily Challenge Refresh:**
- New challenges available daily
- Challenge types rotate
- Progress resets for new challenges
- Notification: "New Challenges Available!" badge

**Daily Ad Bonus:**
- First ad of the day: +50 Gold bonus
- Subsequent ads: Normal rewards (25-100 Gold)
- Resets at midnight (local time)
- Notification: "Daily Ad Bonus Available!" badge

**Daily Challenge / Warlord of the Day:**
- **Rotation:** One Enemy Warlord selected as "Warlord of the Day" each day
- **Refresh:** Changes at midnight local time (player's timezone)
- **Selection:** Randomly chosen from all unlocked Enemy Warlords (weighted toward player's current level range)
- **Display:** Special badge/indicator on Warlord selection screen (e.g., "⭐ Warlord of the Day")
- **Visual:** Warlord avatar highlighted with special border/glow effect
- **Daily Modifier:** Each day's Warlord has one active modifier that provides bonus benefits:
  - **Double Streak Multiplier:** All streak multipliers are doubled (3+ wins = 3x instead of 1.5x, 5+ wins = 4x instead of 2x, 10+ wins = 5x instead of 2.5x)
  - **Free Battle Item:** Player receives one free Battle Item charge for the current level (if Battle Items are unlocked for that level)
  - **Bonus Gold:** +50% Gold earned from all turn wins and completion bonuses
  - **Bonus XP:** +50% XP earned from all turn wins and completion bonuses
  - **Reduced Entry Cost:** Battle attempt costs 50% less Gold (or free if normally free)
  - **Double First-Time Bonus:** First-time defeat bonus doubled (if not yet defeated)
  - **Charge Boost:** All suit charges and Warlord Power charges accumulate 25% faster
  - **HP Boost:** Player starts with +10 HP for the battle
- **Modifier Rotation:** Modifier changes daily (randomly selected from available modifiers)
- **Completion Bonus:** Defeating the Warlord of the Day grants additional completion bonus:
  - +100 Gold bonus (in addition to normal completion bonus)
  - +50 XP bonus (in addition to normal completion bonus)
  - "Daily Challenge Complete!" achievement notification
- **Tracking:** Defeating Warlord of the Day tracked in statistics (daily challenge completion count)
- **Notification:** "New Warlord of the Day Available!" badge appears on app launch (if new day)
- **Pre-Game Display:** Warlord selection screen shows:
  - Warlord of the Day highlighted with special indicator
  - Active modifier displayed (e.g., "⭐ Double Streak Multiplier Active")
  - Completion bonus preview (e.g., "+100 Gold, +50 XP bonus")
- **Post-Game:** If Warlord of the Day defeated, special celebration animation and "Daily Challenge Complete!" message
- **Persistence:** Daily challenge completion tracked in localStorage/cloud save
- **Replay:** Warlord of the Day can be replayed multiple times per day (modifier applies to all attempts)
- **Design Purpose:** Encourages daily engagement, provides variety through rotating Warlords and modifiers, offers bonus rewards for daily play

**Streak Encouragement:**
- Display current streak on pre-game screen
- "Continue Your Streak!" messaging
- Streak milestones highlighted
- Streak reset notifications (if broken)

**Progress Reminders:**
- "X XP to next level" on pre-game screen
- "X Gold to afford [Battle Item]" messaging
- Collection progress: "X/59 Warlords Defeated"
- Achievement progress: "X/10 Challenges Complete"

**New Content Notifications:**
- "New Warlord Unlocked!" badge
- "New Battle Items Available!" badge
- "New Challenges Available!" badge
- Badges appear on relevant UI elements

**Returning Player Experience:**
- "Welcome Back!" message displayed (first return of day)
- Show progress since last session:
  - "You've gained X XP since last session"
  - "You've earned X Gold since last session"
- Highlight new content (if any)
- Encourage continued play

#### Monetization Integration

**Ad Placement Points:**

**Post-Game Rewarded Video (F2P):**
- Trigger: After game completion (win or loss)
- Placement: "Earn Extra Gold" button on results screen
- Reward: 25-100 Gold (randomized, displayed before ad)
- Frequency: Unlimited (but daily bonus only on first)
- Player can skip ad (no penalty)

**Post-Game Interstitial (F2P):**
- Trigger: Every 3-5 games (configurable)
- Placement: After results screen, before returning to pre-game
- Reward: 10-50 Gold (randomized, displayed before ad)
- Frequency: Limited (prevents ad fatigue)
- Can be skipped after 5 seconds

**Pre-Game Rewarded Video (F2P):**
- Trigger: If player lacks Gold for game fee
- Placement: "Watch Ad for Gold" button
- Reward: 25-100 Gold (randomized)
- Frequency: As needed (when Gold insufficient)

**IAP Purchase Points:**

**Gold Purchase Prompts:**
- Post-game: "Purchase Gold" button (always available)
- Pre-game: If insufficient Gold for game fee
- Battle Item Shop: If insufficient Gold for item purchase
- Low Gold Warning: If Gold < 50, show upgrade prompt

**IAP Packages:**
- Small Pack: $0.99 = 500 Gold
- Medium Pack: $2.99 = 1,750 Gold (17% bonus)
- Large Pack: $4.99 = 3,500 Gold (40% bonus)
- Mega Pack: $9.99 = 8,000 Gold (60% bonus)

**PAID Account Upgrade:**
- One-time purchase: $3.99
- Benefits:
  - Cloud save (cross-device sync)
  - Automatic Gold rewards (matches ad rewards, no ads required)
  - Can still watch ads for extra Gold
- Prompts:
  - Pre-game: "Upgrade to PAID" button (if F2P)
  - Post-game: "Upgrade to PAID" prompt (if low Gold, F2P)
  - Menu: "Upgrade" option in Game Menu

**Gold Scarcity Moments:**
- After 3 free attempts per Enemy Warlord
- When purchasing Battle Items
- When low on Gold (<50 Gold)
- Natural scarcity encourages ad viewing or IAP

**Monetization Balance:**
- F2P players: Can progress through ads (generous ad rewards)
- PAID players: Automatic rewards, optional ads
- IAP: Always available, never forced
- No pay-to-win: All content unlockable through play

#### Notification System

**Push Notifications (Web App):**
- **Daily Login Reminder:** "Your daily bonus is ready!"
- **Streak Reminder:** "Continue your streak! Play now!"
- **Challenge Update:** "New challenges available!"
- **Achievement:** "You've unlocked [Achievement]!"
- **Leaderboard:** "You've moved up the leaderboard!"
- **Frequency:** Maximum 1-2 per day (respect user preferences)
- **Opt-in:** Player must enable notifications (browser permission)

**In-App Notifications:**
- **Badge System:** Visual badges on UI elements
  - Warlord selection: "New Warlord Unlocked!" badge
  - Challenges: "New Challenges!" badge
  - Leaderboards: "Rank Updated!" badge
  - Menu: "Achievement Unlocked!" badge
- **Popup Notifications:**
  - Level-up: "Level Up!" popup
  - Unlock: "New Warlord Unlocked!" popup
  - Achievement: "Achievement Unlocked!" popup
  - Daily bonus: "Daily Bonus!" popup
- **Status Banner:** In-game status messages
  - "You Win! +X Damage"
  - "Special Ready!"
  - "Streak: X wins!"

**Progress Reminders:**
- Pre-game screen: "X XP to next level"
- Pre-game screen: "X Gold to afford [Battle Item]"
- Collection progress: "X/59 Warlords Defeated"
- Challenge progress: "X/Y challenges complete"

**Notification Settings:**
- Game Menu: "Notifications" toggle
- Options:
  - Enable/disable push notifications
  - Enable/disable in-app badges
  - Enable/disable popup notifications
  - Customize notification types
- Saved to localStorage

#### Social Elements

**Leaderboards:**

**Global Leaderboards:**
- **Highest Level:** Top players by level (ties broken by XP)
- **Most Warlords Defeated:** Top players by unique Warlords defeated
- **Highest Win Streak:** Top players by best turn streak
- **Total Games Won:** Top players by total game wins
- **Collection Complete:** Players who've defeated all 59 Warlords
- **Gauntlet Mode Leaderboards:** (Unlocked after defeating all 59 Warlords)
  - **Highest Wave Reached:** Top players by best wave completed
  - **Longest Gauntlet Streak:** Top players by consecutive Gauntlet wins
  - **Total Gauntlet Battles Won:** Top players by lifetime Gauntlet victories
  - **Fastest Wave Completion:** Top players by fastest wave completion time

**Leaderboard Display:**
- Pre-game: "Leaderboards" button
- Post-game: "View Leaderboards" button
- Leaderboards Overlay:
  - Top 100 players displayed
  - Player's rank highlighted
  - Player's position shown (e.g., "Rank #1,234")
  - Refresh button to update rankings
  - Filter by category (Level, Defeats, Streak, Wins, Collection, Gauntlet)
  - **Gauntlet Tab:** Separate tab for Gauntlet leaderboards (visible only if unlocked)

**Leaderboard Updates:**
- Real-time: Updates after each game completion
- Caching: Leaderboards cached for performance
- Refresh: Manual refresh available
- Privacy: Player names anonymized (use display names)

**Sharing:**

**Share Results:**
- Post-game: "Share Result" button
- Share content:
  - Game result (Win/Loss)
  - Warlords used (Player vs Enemy)
  - Final score (HP remaining, turns taken)
  - Streak achieved (if applicable)
  - Level progress
- Share formats:
  - Text: "I just defeated [Warlord] as [Player Warlord] in Bigfoot War!"
  - Image: Screenshot of results screen
  - Link: bigfootwar.com/share/[game-id]

**Share Achievements:**
- Achievement unlocked: "Share" button
- Share content:
  - Achievement name and description
  - Badge image
  - Progress milestone
- Share formats:
  - Text: "I unlocked [Achievement] in Bigfoot War!"
  - Image: Achievement badge
  - Link: bigfootwar.com/achievement/[achievement-id]

**Share Collection:**
- Collection milestone: "Share" button
- Share content:
  - Collection progress (e.g., "X/59 Warlords Defeated")
  - Completion percentage
  - Favorite Warlord
- Share formats:
  - Text: "I've defeated X Warlords in Bigfoot War!"
  - Image: Collection progress screenshot
  - Link: bigfootwar.com/collection/[player-id]

**Social Platforms:**
- Native sharing API (Web Share API)
- Platforms: Twitter, Facebook, Reddit, Discord, etc.
- Fallback: Copy link to clipboard
- Analytics: Track share events

#### Collection Completion System

**Collection Tracking:**

**Warlord Collection:**
- Total: 59 Warlords (Enemy + Player)
- Progress: "X/59 Warlords Defeated"
- Display: Collection percentage (e.g., "45% Complete")
- Tracking: Defeated Warlords marked in collection
- Player Warlords: Unlocked after defeating Enemy Warlord

**Battle Item Collection:**
- Total: 59 Battle Items (one per level)
- Progress: "X/59 Battle Items Collected"
- Display: Collection percentage
- Tracking: Owned Battle Items marked in collection
- Purchase required: Battle Items must be purchased with Gold
- **Level Restriction:** Battle Items are only available during the level they're unlocked. Collection tracking shows items owned, but items from previous levels are not usable when advancing to new levels

**Collection Display:**
- Pre-game: Collection progress shown in menu
- Post-game: Collection progress updated
- Menu: "Collection" section shows:
  - Warlord gallery (defeated/undefeated)
  - Battle Item gallery (owned/unowned)
  - Completion percentage
  - Next unlock preview

**Completion Rewards:**

**Warlord Collection Milestones:**
- 10 Warlords Defeated: 500 Gold + 200 XP + Badge
- 25 Warlords Defeated: 1,000 Gold + 500 XP + Badge
- 50 Warlords Defeated: 2,500 Gold + 1,000 XP + Badge
- 59 Warlords Defeated (Complete): 5,000 Gold + 2,000 XP + "Master Collector" Badge + Special Title

**Battle Item Collection Milestones:**
- 10 Items Collected: 300 Gold + 100 XP + Badge
- 25 Items Collected: 750 Gold + 300 XP + Badge
- 50 Items Collected: 1,500 Gold + 750 XP + Badge
- 59 Items Collected (Complete): 3,000 Gold + 1,500 XP + "Item Master" Badge + Special Title

**Completionist Achievements:**
- **Master Collector:** Defeat all 59 Warlords
- **Item Master:** Collect all 59 Battle Items
- **Perfect Collection:** Defeat all Warlords + Collect all Items
- **Level Master:** Reach max level (59)
- **Streak Master:** Achieve 20+ turn streak
- **Win Master:** Win 100 games
- **Completionist:** Unlock all achievements

**Collection Percentage Display:**
- Pre-game: "Collection: X% Complete" (top of screen, subtle)
- Menu: Detailed collection breakdown
- Post-game: Collection progress updated
- Visual: Progress bar showing completion percentage

**Completion Rewards Flow:**
1. Milestone reached (e.g., 10 Warlords Defeated)
2. Achievement celebration overlay
3. Badge awarded and displayed
4. Rewards awarded (Gold, XP)
5. Notification: "Collection Milestone Reached!"
6. Share option: "Share Achievement" button
7. Continue to post-game flow

### Endless Gauntlet Mode

Endless Gauntlet Mode is an infinite challenge mode that unlocks after defeating all 59 Warlords. Players face an escalating series of battles with increasing difficulty, testing their mastery of the game's mechanics and providing a long-term endgame challenge.

#### Unlock Requirements

**Prerequisites:**
- **Master Collector Achievement:** Must have defeated all 59 Warlords (warlordCompletion = 100%)
- **Unlock Notification:** Upon completing the 59th Warlord, special celebration overlay appears:
  - "Endless Gauntlet Unlocked!" message
  - Visual: Epic particle burst, triumphant chiptune fanfare
  - Badge: "Gauntlet Master" badge awarded
  - Rewards: 1,000 Gold + 500 XP bonus

**Access:**
- New "Gauntlet Mode" button appears in Pre-Game screen (prominent placement, glowing effect)
- Button remains visible once unlocked (permanent unlock)
- Can be accessed from any Pre-Game state

#### Core Mechanics

**Progressive Difficulty:**
- **Wave System:** Battles organized into "Waves" (sets of 5 battles)
- **Wave 1:** Levels 1-5 Warlords (randomized order)
- **Wave 2:** Levels 6-10 Warlords (randomized order)
- **Wave 3:** Levels 11-15 Warlords (randomized order)
- **Pattern Continues:** Each wave cycles through 5 consecutive level ranges
- **After Wave 12 (Levels 56-59):** Cycles repeat with **Difficulty Modifiers** applied

**Difficulty Scaling:**
- **Wave 1-12:** Standard difficulty (no modifiers)
- **Wave 13+:** +10% enemy HP and damage per wave cycle
- **Wave 25+:** +20% enemy HP and damage per wave cycle
- **Wave 50+:** +30% enemy HP and damage per wave cycle
- **Maximum Scaling:** Caps at +100% (Wave 100+)
- **AI Difficulty:** Enemy AI uses optimized strategies (Replay Mode difficulty) starting Wave 13+

**Enemy Selection:**
- **Randomization:** Each wave randomly selects 5 Warlords from the level range
- **No Repeats:** Within a single wave, no Warlord appears twice
- **Full Rotation:** All 59 Warlords appear before any repeats (ensures variety)

**Player Warlord Selection:**
- **Free Choice:** Player can select any unlocked Player Warlord before each battle
- **Warlord Switching:** Can change Warlord between battles (no penalty)
- **Strategic Planning:** Allows adaptation to upcoming enemy types

**Battle Items:**
- **Full Access:** All owned Battle Items available (no level restrictions)
- **Charges Reset:** Battle Item charges reset to full after each battle
- **Strategic Use:** Encourages optimal item usage per battle

**Charms:**
- **Full Access:** All owned Charms available for equipping
- **Durability Persists:** Charm durability carries across battles within the same Gauntlet run
- **Strategic Planning:** Durability management becomes critical for long runs

#### Progression and Rewards

**Wave Completion Rewards:**
- **Per Battle Win:** Standard turn/game rewards (Gold, XP)
- **Wave Completion Bonus:** +200 Gold + 100 XP (after completing all 5 battles in a wave)
- **Milestone Bonuses:**
  - Wave 5 Complete: +500 Gold + 250 XP
  - Wave 10 Complete: +1,000 Gold + 500 XP
  - Wave 25 Complete: +2,500 Gold + 1,250 XP
  - Wave 50 Complete: +5,000 Gold + 2,500 XP
  - Wave 100 Complete: +10,000 Gold + 5,000 XP

**Streak Multipliers:**
- **Consecutive Wins:** Streak multipliers apply (same as standard gameplay)
- **Gauntlet Streak:** Separate streak counter for Gauntlet mode (persists across battles)
- **Streak Bonus:** +5% Gold/XP per consecutive win (stacks with turn streak multipliers)
- **Streak Reset:** Resets to 0 on any battle loss

**Loss Conditions:**
- **Battle Loss:** Losing any battle ends the Gauntlet run
- **Progress Saved:** Wave progress saved up to last completed wave
- **Rewards Retained:** All rewards earned up to loss point are kept
- **Restart Option:** Can immediately restart from Wave 1 or exit to Pre-Game

**Leaderboard Integration:**
- **Gauntlet Leaderboards:** Separate leaderboard category for Gauntlet mode
- **Metrics Tracked:**
  - Highest Wave Reached
  - Longest Gauntlet Streak
  - Total Gauntlet Battles Won
  - Fastest Wave Completion Time
- **Rankings:** Global leaderboard showing top Gauntlet performers

#### UI and Flow

**Pre-Game Gauntlet Selection:**
- **Mode Toggle:** "Standard Mode" / "Gauntlet Mode" toggle button (top-center of Pre-Game screen)
- **Gauntlet Indicator:** When Gauntlet Mode active, prominent "GAUNTLET MODE" banner displayed
- **Wave Display:** Shows current wave number and progress (e.g., "Wave 3 - Battle 2/5")
- **Best Run Display:** Shows personal best wave reached (e.g., "Best: Wave 12")

**Between Battles:**
- **Victory Screen:** Brief celebration, rewards displayed, "Continue" button
- **Wave Complete Screen:** Special celebration for wave completion, milestone bonuses highlighted
- **Warlord Selection:** Option to change Player Warlord before next battle
- **Battle Item Management:** Can review/equip Battle Items
- **Exit Option:** Can exit Gauntlet at any time (progress saved)

**Gauntlet Run State:**
- **State Persistence:** Gauntlet progress saved after each battle
- **Resume Capability:** Can resume interrupted Gauntlet run (from last completed battle)
- **Abandon Option:** Can abandon current run to start fresh (confirmation required)

**Visual Indicators:**
- **Wave Counter:** Prominent display showing current wave and battle number
- **Difficulty Indicator:** Visual indicator showing current difficulty scaling (e.g., "+20% Difficulty")
- **Streak Display:** Gauntlet streak counter displayed prominently
- **Progress Bar:** Visual progress bar showing wave completion percentage

#### Data Structure

```typescript
interface GauntletState {
  active: boolean; // Whether currently in a Gauntlet run
  currentWave: number; // Current wave number (1-based)
  currentBattle: number; // Current battle within wave (1-5)
  difficultyModifier: number; // Percentage increase (0-100)
  streak: number; // Consecutive wins in current run
  bestWave: number; // Personal best wave reached
  totalBattlesWon: number; // Lifetime Gauntlet battles won
  lastCompletedWave: number; // Last wave fully completed (for resume)
  enemyPool: number[]; // Remaining Warlords in current wave
}

interface GauntletRewards {
  waveCompletionBonus: number; // Gold bonus for completing wave
  milestoneBonus: number; // Gold bonus for milestone waves
  streakMultiplier: number; // Current streak multiplier
}
```

#### Achievements

**Gauntlet-Specific Achievements:**
- **Gauntlet Initiate:** Complete Wave 1 (100 Gold + 50 XP)
- **Gauntlet Veteran:** Complete Wave 10 (500 Gold + 250 XP + Badge)
- **Gauntlet Master:** Complete Wave 25 (1,000 Gold + 500 XP + Badge)
- **Gauntlet Legend:** Complete Wave 50 (2,500 Gold + 1,250 XP + Badge)
- **Gauntlet Immortal:** Complete Wave 100 (5,000 Gold + 2,500 XP + Badge + Special Title)
- **Perfect Gauntlet:** Complete Wave 10 without losing a single battle (1,000 Gold + 500 XP + Badge)
- **Gauntlet Streak Master:** Achieve 50+ consecutive wins in Gauntlet mode (2,000 Gold + 1,000 XP + Badge)

#### Balance Considerations

**Reward Scaling:**
- Rewards scale appropriately with difficulty increase
- Milestone bonuses provide meaningful progression goals
- Streak multipliers reward consistent performance

**Difficulty Curve:**
- Early waves (1-12) provide warm-up and familiarization
- Mid waves (13-50) test mastery of game mechanics
- Late waves (50+) become extreme challenges for dedicated players

**Time Investment:**
- Each battle: ~2-5 minutes (standard game length)
- Each wave: ~10-25 minutes (5 battles)
- Full run to Wave 100: ~3-4 hours (for top players)

**Replayability:**
- Random enemy selection ensures variety
- Difficulty scaling provides long-term challenge
- Leaderboard competition drives engagement
- Milestone rewards create progression goals

#### Exit Points and Re-entry

**Natural Completion:**
- Game won or lost
- Results screen displayed
- Player can continue or exit
- Progress saved automatically

**Player-Initiated Exit:**
- Menu → Exit Game
- Browser close/background
- Progress saved automatically
- Last state preserved

**Progress Saving:**
- Auto-save: After every game completion
- Manual save: Available in menu (PAID accounts)
- Saved data:
  - Level, XP, Gold
  - Unlocked Warlords
  - Battle Items owned
  - Statistics
  - Collection progress
  - Settings and preferences

**Re-entry Experience:**
- App loads saved progress
- Daily bonus check (if eligible)
- Notification check (pending notifications)
- Return to pre-game screen
- Last played Warlords restored
- Seamless continuation

**Progress Loss Prevention:**
- LocalStorage: Primary storage (F2P)
- Cloud sync: Backup storage (PAID)
- Recovery: Contact support for progress recovery (PAID)
- Warning: "Progress not saved" message if localStorage fails

#### Player Journey Variations

**First-Time Player Experience:**
- No tutorial, immediate play
- Default: Sasquatch vs Sasquatch
- Learn through play and visual feedback
- First win unlocks Level 2 (Skunk Ape)
- Progressive unlocks guide learning
- Generous early rewards encourage play

**Returning Player Experience:**
- Progress loaded from localStorage
- Daily bonus check (if eligible)
- Last played Warlords restored
- Continue from where left off
- New content highlighted (if any)

**High-Level Player Experience:**
- Slower progression (higher XP thresholds)
- Challenging Warlords (levels 40-59)
- Collection-focused gameplay
- Achievement hunting
- Leaderboard competition
- **Endless Gauntlet Mode:** Unlocks after defeating all 59 Warlords, provides infinite challenge with escalating difficulty
- Prestige unlocks

**F2P vs PAID Experience:**

**F2P Players:**
- Watch ads for Gold rewards
- LocalStorage only (device-specific)
- Can upgrade to PAID anytime
- Full game access (no paywalls)
- Slower Gold accumulation (ad-dependent)

**PAID Players:**
- Automatic Gold rewards (no ads required)
- Cloud save (cross-device sync)
- Can still watch ads for extra Gold
- Faster Gold accumulation
- Progress recovery support

**Both:**
- Same gameplay experience
- Same progression path
- Same unlocks and content
- No pay-to-win mechanics

#### Retention Mechanics Summary

**Daily Engagement:**
- Daily login bonus (100 Gold + 50 XP)
- Daily challenge refresh
- Daily ad bonus (first ad of day)
- Streak encouragement

**Progression Carrots:**
- "X XP to next level" messaging
- "X Gold to afford [Battle Item]" messaging
- Unlock previews
- Collection progress

**Collection Mechanics:**
- 59 Warlords to defeat
- 59 Battle Items to collect
- Completion rewards
- Collection percentage tracking

**Achievement System:**
- Milestone achievements
- Streak achievements
- Collection achievements
- Completionist achievements
- Badge rewards

**Social Elements:**
- Leaderboards (5 categories)
- Share results
- Share achievements
- Share collection progress

**Monetization Integration:**
- Natural ad placement
- Optional IAP
- PAID upgrade option
- No forced monetization

**Feedback Loops:**
- Positive: Rewards, unlocks, achievements
- Progress: Visual progress bars, collection tracking
- Goals: Clear objectives, unlock previews
- Recognition: Leaderboards, achievements, badges

### Game menu, settings, and options

The Game Menu provides centralized access to game features, settings, statistics, and options. It's accessible from any game state (pre-game, in-game, post-game) and serves as the hub for player customization and information.

#### Game Menu Access

**Access Points:**
- **Menu Icon:** Always visible bottom-right corner (32x32px)
- **Accessible From:** Any game state (pre-game, in-game, post-game)
- **Behavior:** Tap opens fullscreen overlay, dims background 50% opacity
- **Close:** Tap outside overlay, close button (top-right), or ESC key

**Menu State:**
- Overlay state: Does not pause gameplay (if accessed during game)
- Return behavior: Returns to previous game state when closed
- Persistence: Menu selections and settings persist across sessions

#### Menu Structure

**Main Menu Sections:**

1. **Statistics**
   - Games played (total)
   - Games won (total)
   - Win rate (percentage)
   - Highest streak (turns)
   - Total Gold earned (lifetime)
   - Total XP earned (lifetime)
   - Warlords defeated (count)
   - Collection progress (percentage)
   - Detailed breakdown: Tap to expand full statistics overlay

2. **Challenges**
   - Active challenges count badge
   - Quick preview: Shows 2-3 active challenges
   - Progress indicators: "X/Y" progress for each challenge
   - Tap to open: Full Challenges overlay
   - Badge: Red notification badge if new challenges available

3. **Leaderboards**
   - Current rank display: "Rank #X" for each category
   - Quick preview: Shows player's position in top categories
   - Categories: Highest Level, Most Defeated, Highest Streak, Total Wins, Collection Complete
   - Tap to open: Full Leaderboards overlay
   - Refresh: Manual refresh button to update rankings

4. **Collection**
   - Warlord gallery: Shows all 59 Warlords
   - Battle Item gallery: Shows all 59 Battle Items
   - Completion percentage: "X/59 Warlords Defeated", "X/59 Items Collected"
   - Filter options: All, Unlocked, Locked, Defeated
   - Tap to open: Full Collection overlay with detailed galleries

5. **Settings**
   - Sound effects toggle (on/off)
   - Background music toggle (on/off)
   - Volume slider (0-100%)
   - Notifications toggle (on/off)
   - Push notifications toggle (on/off, requires browser permission)
   - In-app badges toggle (on/off)
   - Popup notifications toggle (on/off)
   - High contrast mode toggle (on/off)
   - Challenge display preferences:
     - Show challenges in pre-game (on/off)
     - Show challenge progress in post-game (on/off)
     - Challenge completion sounds (on/off)
   - Language selection (if multi-language support)
   - Data management:
     - Clear local data (F2P)
     - Cloud sync status (PAID)
     - Manual save (PAID)
     - Export data (PAID)

6. **About**
   - Game version: "Version X.X.X"
   - Build number: "Build XXXXX"
   - Credits: Developer credits, artist credits, sound credits
   - Privacy policy: Link to privacy policy page
   - Terms of service: Link to terms of service page
   - Support: Support link
   - License: Open source licenses (if applicable)

7. **Upgrade to PAID** (F2P players only)
   - Prominent button: "Upgrade to PAID - $3.99"
   - Benefits listed:
     - Cloud save (cross-device sync)
     - Automatic Gold rewards (no ads required)
     - Can still watch ads for extra Gold
     - Ad-free experience
   - Tap to open: Purchase flow overlay
   - Not shown: For PAID account holders

#### Settings Details

**Audio Settings:**

**Sound Effects:**
- Toggle: Enable/disable all sound effects
- Default: Enabled
- Persistence: Saved to localStorage
- Scope: Card flips, specials, wins, losses, UI interactions
- Behavior: When disabled, all sound effects muted (except music if enabled)

**Background Music:**
- Toggle: Enable/disable background music
- Default: Enabled
- Persistence: Saved to localStorage
- Scope: Ambient background music during gameplay
- Behavior: When disabled, background music stops (sound effects still play if enabled)

**Volume Control:**
- Slider: 0-100% volume
- Default: 80%
- Persistence: Saved to localStorage
- Scope: Controls both sound effects and music volume
- Behavior: Real-time adjustment, immediate feedback

**Notification Settings:**

**Notifications Master Toggle:**
- Toggle: Enable/disable all notifications
- Default: Enabled
- Persistence: Saved to localStorage
- Scope: Controls all notification types
- Behavior: When disabled, all notifications disabled (overrides individual toggles)

**Push Notifications:**
- Toggle: Enable/disable browser push notifications
- Default: Disabled (requires opt-in)
- Persistence: Saved to localStorage + browser permission
- Scope: Browser push notifications (daily reminders, streak reminders, etc.)
- Behavior: Requires browser notification permission, prompts user if not granted

**In-App Badges:**
- Toggle: Enable/disable visual badges on UI elements
- Default: Enabled
- Persistence: Saved to localStorage
- Scope: Badge indicators on menu items, Warlord selection, etc.
- Behavior: When disabled, badges hidden but functionality remains

**Popup Notifications:**
- Toggle: Enable/disable popup notifications
- Default: Enabled
- Persistence: Saved to localStorage
- Scope: Level-up popups, unlock popups, achievement popups, daily bonus popups
- Behavior: When disabled, popups hidden but events still logged

**Display Settings:**

**High Contrast Mode:**
- Toggle: Enable/disable high contrast mode
- Default: Disabled
- Persistence: Saved to localStorage
- Scope: Increases contrast for accessibility (WCAG AAA compliance)
- Behavior: When enabled, uses high-contrast color scheme (4.5:1+ ratios)

**Challenge Display Preferences:**
- Show challenges in pre-game: Toggle (default: enabled)
- Show challenge progress in post-game: Toggle (default: enabled)
- Challenge completion sounds: Toggle (default: enabled)
- Persistence: Saved to localStorage

**Language Selection:**
- Dropdown: Select language (if multi-language support)
- Default: English (en-US)
- Persistence: Saved to localStorage
- Scope: UI text, game text, notifications
- Behavior: Changes language immediately, requires page refresh for full effect

**Data Management:**

**Clear Local Data (F2P):**
- Button: "Clear All Data"
- Warning: Confirmation dialog required
- Scope: Clears all localStorage and IndexedDB data
- Behavior: Resets game to first-time player state
- Irreversible: Cannot be undone

**Cloud Sync Status (PAID):**
- Display: "Synced" or "Sync Pending" or "Sync Error"
- Last sync timestamp: "Last synced: [date/time]"
- Manual sync button: "Sync Now"
- Behavior: Shows sync status, allows manual sync trigger

**Manual Save (PAID):**
- Button: "Save Progress"
- Behavior: Immediately saves progress to cloud
- Feedback: "Progress saved!" confirmation message
- Scope: All player progress, settings, statistics

**Export Data (PAID):**
- Button: "Export Data"
- Format: JSON file download
- Scope: All player progress, settings, statistics
- Behavior: Downloads JSON file with all player data

#### Menu Navigation

**Navigation Flow:**
- Main Menu → Section Selection → Sub-menu or Overlay
- Breadcrumb: Shows current location (e.g., "Menu > Settings > Audio")
- Back button: Returns to previous menu level
- Close button: Returns to game (closes entire menu)

**Menu Organization:**
- Vertical list layout (mobile-first)
- Scrollable: If content exceeds viewport height
- Section headers: Bold pixel text (18px)
- Menu items: Regular pixel text (16px)
- Icons: 24x24px pixel sprites (left-aligned)

**Quick Actions:**
- Some menu items have quick actions (e.g., toggle switches)
- Quick actions: Inline controls (toggles, sliders)
- Full details: Tap menu item to open detailed overlay

#### Settings Persistence

**Storage Method:**
- **F2P Players:** localStorage (browser-specific)
- **PAID Players:** localStorage + cloud sync (cross-device)

**Settings Saved:**
- Audio preferences (sound, music, volume)
- Notification preferences (all notification types)
- Display preferences (high contrast, challenge display)
- Language preference
- Last menu state saved (for quick return)

**Settings Sync:**
- **F2P:** Local only (device-specific)
- **PAID:** Cloud sync (cross-device, automatic on login)

**Default Settings:**
- Sound effects: Enabled
- Background music: Enabled
- Volume: 80%
- Notifications: Enabled
- Push notifications: Disabled (opt-in)
- In-app badges: Enabled
- Popup notifications: Enabled
- High contrast: Disabled
- Challenge display: All enabled
- Language: English (en-US)

**Settings Reset:**
- Option: "Reset to Defaults" button in Settings
- Warning: Confirmation dialog required
- Behavior: Resets all settings to defaults
- Scope: Settings only (does not affect game progress)

#### Menu Accessibility

**Accessibility Features:**
- Keyboard navigation: Arrow keys, Enter, ESC
- Screen reader support: ARIA labels, semantic HTML
- High contrast mode: WCAG AAA compliance option
- Touch targets: Minimum 48x48px for all interactive elements
- Text size: Scalable pixel fonts (respects browser zoom)

**Visual Feedback:**
- Hover states: Glow effect on menu items
- Active states: Highlighted current selection
- Disabled states: Grayed out, non-interactive
- Loading states: Progress indicator

#### Menu Performance

**Load Time:**
- Menu overlay: <100ms to open
- Settings load: Instant (from localStorage)
- Statistics load: <200ms (calculated on demand)
- Leaderboards load: <500ms (fetched from server if online)

**Optimization:**
- Lazy loading: Statistics and leaderboards loaded on demand
- Caching: Settings cached in memory, persisted to localStorage
- Debouncing: Settings changes debounced (save after 500ms idle)

#### Menu Customization

**Player Preferences:**
- Menu order: Fixed (cannot be customized)
- Menu visibility: All sections always visible
- Quick access: Most-used sections at top (Statistics, Challenges)

**Personalization:**
- Last accessed: Menu remembers last opened section
- Favorites: Not implemented (future enhancement)
- Customization: Not available (consistent UX)

### Core Game Loop

The core game loop consists of repeating turn cycles until a win condition is met. Each turn follows a structured sequence:

**Turn Structure:**

1. **Pre-Turn State**
   - Visual: Game table displays current state (HP bars, deck counts, avatars)
   - Sound: Ambient background music (if enabled)
   - State: Previous turn resolved, all effects applied, Battle Item effects cleared
   - Messaging: Status banner shows "Tap Play to Draw" or "Use Battle Item?"
   - UI: Primary CTA displays "Play" button
   - UI: Battle Item button displays (if player owns items with remaining charges)
   - **Battle Item Activation**: Player can tap Battle Item button to activate owned Battle Items before drawing

2. **Card Draw Phase**
   - Trigger: Player taps "Play" button
   - Sound: Card flip sound effect (crisp chiptune flip)
   - Animation: Cards animate from deck positions to center battle zone
   - Animation: Simultaneous card flip reveal (180° rotation, face-up)
   - State: Cards drawn from shuffled decks (36 cards per deck: 24 A–6 + 1 Joker + 1 Signature)
   - State: Active Battle Item effects applied (player and/or enemy, e.g., rank boost, predict, extra draw)
   - State: Card ranks compared (Ace high, Jokers trigger shuffle)
   - State: Battle Item charges consumed after draw (charges remaining decrease, both player and enemy)
   - Messaging: Status banner updates to show cards drawn and Battle Item effects (if active)
   - Messaging: Enemy Battle Item Notification appears if enemy activated item (brief display)

3. **Resolution Phase**
   - Winner determination: Highest card rank wins (ties trigger War scenario)
   - Sound: Win jingle (triumphant chiptune) or loss sound (low rumble)
   - Animation: Winning card highlighted, cards slide toward winner's deck area
   - State: Damage calculated (base damage + rank bonus/10)
   - State: Cards captured and added to winner's deck bottom
   - Messaging: Status banner shows winner and damage dealt

5. **Post-Win Overlay Phase**

   **Player Win Path:**
   - Sound: Win jingle, card capture sound
   - Animation: Cards slide to player deck, damage flash on enemy HP bar
   - State: Enemy HP reduced, player deck updated, suit charges incremented based on captured cards, Warlord charge progress incremented (wins)
   - Messaging: Status banner shows "You Win! +X Damage"
   - Animation: Gold/XP reward popups (numbers animate upward)
   - **Chain Check:** System checks player chains (suit chains and poker-style chains)
   - **Chain Trigger:** If chain threshold reached, burst effect triggers immediately (visual explosion, sound, effect applied)
   - Specials icons on main board update (ready icons glow, unready icons dimmed)
   - Player can tap ready special icons to activate (0-2 specials per turn)
   - Sound: Special activation sound (varies by type)
   - Animation: Special effects play on activation
   - Primary CTA updates to "Next Turn" (player proceeds when ready)

   **Enemy Win Path:**
   - Sound: Loss sound, card capture sound
   - Animation: Cards slide to enemy deck, damage flash on player HP bar
   - State: Player HP reduced, enemy deck updated, enemy suit charges incremented, enemy Warlord charge progress incremented (wins), player Warlord charge progress incremented (damage taken)
   - Messaging: Status banner shows "Enemy Wins! -X Damage"
   - **Enemy Chain Check:** System checks enemy chains (suit chains and poker-style chains)
   - **Enemy Chain Trigger:** If enemy chain threshold reached, enemy burst effect triggers automatically (visual notification, sound, effect applied)
   - Enemy AI evaluates and plays specials (if ready)
   - Enemy Special Notification Overlay appears briefly
   - Shows enemy specials played
   - Overlay auto-dismisses after 2-3 seconds
   - Sound: Overlay dismiss sound

6. **State Transitions**
   - HP updates: Bars animate to new values
   - Deck counts: Numbers update, visual deck stack adjusts
   - Charge progress: Suit charges updated based on captured cards, Warlord charge incremented
   - Turn counter: Incremented for streak tracking
   - Special effects: Buffs/debuffs applied and tracked

6. **Turn Completion**
   - All animations complete
   - All state changes applied
   - Game checks win/loss conditions (HP = 0 or deck empty)
   - If game continues: Return to Pre-Turn State
   - If game ends: Trigger Game End Outcomes overlay

**War Scenario Handling:**
- Ties trigger War: 2 face-down cards + 1 face-up card
- Sound: War trigger sound (dramatic chiptune)
- Animation: Additional cards dealt face-down, then reveal
- Resolution: Highest face-up card wins all cards
- Recursive: War can trigger War (max depth 5 to prevent loops)
- State: All War cards captured by winner

**Joker Handling:**
- Joker drawn: Triggers deck shuffle
- Sound: Shuffle sound (card riffle chiptune)
- Animation: Deck visual shuffle effect
- State: Deck reshuffled, Joker removed from play
- Messaging: Status banner shows "Deck Shuffled!"

### Game and App States

This section defines all game and app states, their transitions, and data structures. States are organized hierarchically: App-Level States → Game-Level States → Turn-Level States.

#### State Hierarchy

**App-Level States:** High-level application states (Pre-Game, In-Game, Post-Game, etc.)
**Game-Level States:** States within a game session (Game Initialization, Turn Cycle, War, Game End)
**Turn-Level States:** States within a single turn (Pre-Turn, Draw, Resolution, Post-Win)

#### App-Level States

**1. App Launch**
- **Description:** Initial app load, progress loading, initialization
- **Entry:** Page load, app open
- **Exit:** Progress loaded, transitions to Pre-Game
- **Key Actions:**
  - Load localStorage data
  - Check for PAID account
  - Check daily bonus eligibility
  - Load cloud sync (PAID)
  - Initialize default state (first-time players)
- **Data:** Player progress, settings, preferences

**2. Pre-Game**
- **Description:** Warlord selection, Battle Item management, game preparation
- **Entry:** App launch complete, post-game complete, menu exit
- **Exit:** Game start initiated
- **Key Actions:**
  - Display Warlord selection
  - Manage Battle Items
  - Check Gold balance
  - Process game fee payment
  - View challenges/leaderboards
- **Data:** Selected Warlords, Gold balance, level, XP, unlocked content

**3. In-Game**
- **Description:** Active game session, Core Game Loop running
- **Entry:** Pre-Game → Game start
- **Exit:** Game end (win/loss)
- **Key Actions:**
  - Execute Core Game Loop
  - Handle turn cycles
  - Process specials
  - Update game state
- **Data:** Game state (HP, decks, charges, buffs/debuffs, etc.)

**4. Post-Game**
- **Description:** Results screen, rewards, progression, unlocks
- **Entry:** Game end (win/loss)
- **Exit:** Return to Pre-Game or App Exit
- **Key Actions:**
  - Display results
  - Calculate rewards
  - Check level-up
  - Check unlocks
  - Show monetization hooks
  - Present next actions
- **Data:** Results, rewards, progression updates

**5. Menu/Overlay**
- **Description:** Overlay states (can occur from any app state)
- **Entry:** Menu button tap, overlay trigger
- **Exit:** Overlay close, return to previous state
- **Key Actions:**
  - Display menu options
  - Show overlays (Warlord Select, Battle Items, Challenges, etc.)
  - Handle settings
  - View statistics
- **Data:** Overlay-specific data, menu state

**6. Exit/Background**
- **Description:** App closed or backgrounded
- **Entry:** Browser close, app background, explicit exit
- **Exit:** App reopen, return to previous state
- **Key Actions:**
  - Save progress
  - Persist state
  - Clean up resources
- **Data:** Saved progress, last state

#### Game-Level States

**1. Game Initialization**
- **Description:** Game session setup, deck shuffling, initial state
- **Entry:** Pre-Game → Game start
- **Exit:** Initialization complete, transitions to Turn Cycle
- **Key Actions:**
  - Initialize Warlords (HP, stats, charges)
  - Shuffle decks (36 cards each: 24 A–6 + 1 Joker + 1 Signature)
  - Set initial state
  - Display game table
  - Hide pre-game UI
- **Data:** Game initialization state

**2. Turn Cycle**
- **Description:** Active turn-by-turn gameplay
- **Entry:** Game Initialization complete, previous turn complete
- **Exit:** Game end condition met, transitions to Game End
- **Key Actions:**
  - Execute turn phases (Pre-Turn → Draw → Resolution → Post-Win)
  - Process specials
  - Update game state
  - Check win/loss conditions
- **Data:** Current turn state, game state

**3. War Scenario**
- **Description:** War triggered by tie, nested within Turn Cycle
- **Entry:** Tie condition in Resolution Phase
- **Exit:** War resolved, returns to Turn Cycle
- **Key Actions:**
  - Deal War cards (2 face-down + 1 face-up)
  - Resolve War
  - Handle War recursion (max depth 5)
  - Capture War cards
- **Data:** War state (cards, depth, resolution)

**4. Game End**
- **Description:** Win/loss condition met, game session complete
- **Entry:** HP = 0 or deck empty
- **Exit:** Transitions to Post-Game
- **Key Actions:**
  - Determine winner/loser
  - Freeze game state
  - Calculate final rewards
  - Update statistics
- **Data:** Final game state, results

#### Turn-Level States

**1. Pre-Turn**
- **Description:** Ready for next turn, player can activate Battle Items or proceed to draw
- **Entry:** Previous turn complete, Post-Win complete
- **Exit:** Player taps "Play" button (after optional Battle Item activation)
- **Key Actions:**
  - Display game state
  - Update UI (HP bars, deck counts)
  - Show "Play" button
  - Show "Battle Item" button (if player owns items with remaining charges)
  - Battle Item Selection Overlay available (if Battle Item button tapped)
  - Process passive effects (if any)
- **Data:** Turn-ready state, active Battle Item effect (if any)

**2. Card Draw**
- **Description:** Cards drawn, revealed, compared (Battle Item effects applied if active)
- **Entry:** Player taps "Play" button (after optional Battle Item activation)
- **Exit:** Cards revealed, winner determined
- **Key Actions:**
  - Apply active Battle Item effects to draw (e.g., rank boost, predict, extra draw)
  - Draw cards from decks
  - Reveal cards
  - Compare ranks
  - Consume Battle Item charge after draw (charges remaining decrease)
- **Key Actions:**
  - Draw cards from decks
  - Animate card reveal
  - Compare card ranks
  - Handle Jokers (shuffle trigger)
- **Data:** Drawn cards, ranks, comparison result

**3. Resolution**
- **Description:** Winner determined, damage calculated
- **Entry:** Cards compared, winner determined
- **Exit:** Damage applied, cards captured
- **Key Actions:**
  - Determine winner
  - Calculate damage
  - Apply damage to HP
  - Capture cards
  - Update charges
- **Data:** Winner, damage, captured cards, updated HP

**4. Post-Win (Player Win)**
- **Description:** Player won turn, specials available
- **Entry:** Player wins Resolution Phase
- **Exit:** Specials played or skipped, turn complete
- **Key Actions:**
  - Display rewards (Gold/XP popups)
  - Check chain triggers (suit chains and poker-style chains)
  - Trigger chain burst effects if thresholds reached (visual explosion, sound, effect applied)
  - Update chain state (suit chain length, rank history, suit history)
  - Update specials icons on main board (ready icons glow)
  - Process specials (if played)
  - Update charges
  - Return to Pre-Turn
- **Data:** Rewards, specials state, charges

**5. Post-Win (Enemy Win)**
- **Description:** Enemy won turn, enemy specials processed
- **Entry:** Enemy wins Resolution Phase
- **Exit:** Enemy specials processed, turn complete
- **Key Actions:**
  - Display loss feedback
  - Check enemy chain triggers (suit chains and poker-style chains)
  - Trigger enemy chain burst effects if thresholds reached (visual notification, sound, effect applied)
  - Update enemy chain state (suit chain length, rank history, suit history)
  - Process enemy AI specials
  - Show Enemy Special Notification Overlay
  - Update player Warlord Power charge progress (damage taken adds to charge)
  - Return to Pre-Turn
- **Data:** Loss state, enemy specials, charges

#### State Transitions

**App-Level Transitions:**

```
App Launch
  → Pre-Game (always, after initialization)

Pre-Game
  → In-Game (game start)
  → Menu/Overlay (menu tap)
  → Exit/Background (app close)

In-Game
  → Post-Game (game end)
  → Menu/Overlay (menu tap, pause)
  → Exit/Background (app close)

Post-Game
  → Pre-Game (continue, play again)
  → Menu/Overlay (menu tap)
  → Exit/Background (app close)

Menu/Overlay
  → Previous State (overlay close)
  → Any State (navigation)

Exit/Background
  → Previous State (app reopen)
```

**Game-Level Transitions:**

```
Game Initialization
  → Turn Cycle (initialization complete)

Turn Cycle
  → War Scenario (tie condition)
  → Game End (win/loss condition)
  → Turn Cycle (turn complete, continue)

War Scenario
  → Turn Cycle (War resolved)
  → War Scenario (War recursion, if tie again)

Game End
  → Post-Game (always)
```

**Turn-Level Transitions:**

```
Pre-Turn
  → Card Draw (player taps "Play")

Card Draw
  → Resolution (cards revealed, winner determined)
  → War Scenario (tie condition)

Resolution
  → Post-Win (Player Win) (player wins)
  → Post-Win (Enemy Win) (enemy wins)

Post-Win (Player Win)
  → Pre-Turn (specials complete, turn done)

Post-Win (Enemy Win)
  → Pre-Turn (enemy specials complete, turn done)
```

#### State Data Structures

**App State Structure:**

```typescript
interface AppState {
  currentAppState: 'appLaunch' | 'preGame' | 'inGame' | 'postGame' | 'menu' | 'exit';
  previousAppState: AppState['currentAppState'] | null;
  playerProgress: PlayerProgress;
  settings: GameSettings;
  notifications: Notification[];
  dailyBonus: DailyBonusState;
}

interface PlayerProgress {
  level: number;
  xp: number;
  gold: number;
  unlockedEnemyWarlords: number[]; // Warlord IDs
  unlockedPlayerWarlords: number[]; // Warlord IDs
  ownedBattleItems: number[]; // Battle Item IDs
  statistics: Statistics;
  collection: CollectionProgress;
  lastLoginTimestamp: number;
}

interface Statistics {
  gamesPlayed: number;
  gamesWon: number;
  winRate: number; // Calculated: gamesWon / gamesPlayed
  totalXPEarned: number;
  totalGoldEarned: number;
  highestStreak: number;
  warlordsDefeated: number;
}

interface CollectionProgress {
  warlordsDefeated: number[]; // Warlord IDs
  battleItemsCollected: number[]; // Battle Item IDs
  warlordCompletion: number; // Percentage: defeated.length / 59
  itemCompletion: number; // Percentage: collected.length / 59
}

interface DailyBonusState {
  lastLoginDate: string; // YYYY-MM-DD format
  bonusClaimed: boolean;
  eligible: boolean; // 24+ hours since last login
}

interface GameSettings {
  soundEnabled: boolean;
  musicEnabled: boolean;
  notificationsEnabled: boolean;
  pushNotificationsEnabled: boolean;
  volume: number; // 0-1
}
```

**Game State Structure:**

```typescript
interface GameState {
  gameId: string; // Unique game session ID
  currentGameState: 'initialization' | 'turnCycle' | 'war' | 'gameEnd';
  playerWarlord: WarlordState;
  enemyWarlord: WarlordState;
  turnNumber: number;
  streak: number; // Consecutive turn wins
  playerChains: ChainState; // Player chain tracking
  enemyChains: ChainState; // Enemy chain tracking
  gameStartTime: number; // Timestamp
  gameEndTime: number | null; // Timestamp, null if game ongoing
}

interface WarlordState {
  warlordId: number; // From roster table
  currentHP: number;
  maxHP: number;
  baseDamage: number;
  suitCharges: SuitCharges;
  warlordCharge: ChargeState;
  buffs: Buff[];
  debuffs: Debuff[];
  deck: DeckState;
  ownedBattleItems: BattleItemState[]; // Array of owned Battle Items (player only)
  assignedBattleItem: number | null; // Battle Item ID assigned to this Warlord (from roster, enemy only)
  activeBattleItemEffect: BattleItemEffect | null; // Active effect for current turn (player or enemy)
}

interface SuitCharges {
  hearts: ChargeState;
  diamonds: ChargeState;
  clubs: ChargeState;
  spades: ChargeState;
}

interface ChargeState {
  current: number; // Current charge progress
  threshold: number; // Charge threshold (from roster table)
  ready: boolean; // Whether special is ready
  overcharge: number; // Charge beyond threshold (for bonus potency)
}

interface DeckState {
  cards: Card[]; // Array of cards in deck
  deckSize: number; // Current deck size
  capturedCards: Card[]; // Cards captured this game (for charge calculation)
  buriedCards: Card[]; // Cards marked as buried (always return to owner)
  banishedCards: Card[]; // Cards marked as banished (permanently locked)
}

interface Card {
  suit: 'hearts' | 'diamonds' | 'clubs' | 'spades' | 'joker';
  rank: number; // 2-14 (2-10, 11=Jack, 12=Queen, 13=King, 14=Ace)
  isJoker: boolean;
  owner: 'player' | 'enemy'; // Current owner
  buried: boolean; // Marked as buried
  banished: boolean; // Marked as banished
}

interface Buff {
  type: 'armor' | 'damage' | 'heal' | 'stat' | 'passive';
  amount: number;
  duration: number; // Turns remaining (-1 for permanent)
  source: string; // Special name or source
}

interface Debuff {
  type: 'dot' | 'blind' | 'confuse' | 'silence' | 'chargeModifier';
  amount: number;
  duration: number; // Turns remaining
  source: string; // Special name or source
}

interface BattleItemState {
  itemId: number; // Battle Item ID
  owned: boolean; // Whether player owns this item
  maxCharges: number; // Maximum charges per game (1-3, varies by item level/power)
  currentCharges: number; // Current charges remaining this game (recharges after game within same level)
  level: number; // Warlord level when item was unlocked (item only available during this level)
}

interface BattleItemEffect {
  type: 'rankBoost' | 'predict' | 'extraDraw' | 'swap' | 'autoWin' | 'other';
  amount: number; // Effect magnitude (e.g., +2 rank, predict accuracy %)
  duration: number; // Turns remaining (typically 1 for pre-turn activation)
  itemId: number; // Source Battle Item ID
}

interface ChainState {
  // Suit Chain Tracking
  currentSuit: 'hearts' | 'diamonds' | 'clubs' | 'spades' | null;
  suitChainLength: number; // Consecutive wins with current suit (persists across losses)
  lastWinSuit: 'hearts' | 'diamonds' | 'clubs' | 'spades' | null;
  
  // Rank Chain Tracking (for poker-style chains)
  rankHistory: number[]; // Last 6 ranks won (for Straight, Pair detection)
  suitHistory: ('hearts' | 'diamonds' | 'clubs' | 'spades')[]; // Last 6 suits won
  
  // Chain History
  chainHistory: ChainTrigger[]; // Track triggered chains this game
  challengeModifiers: ChallengeChainModifier[]; // Active challenge effects
}

interface ChainTrigger {
  type: 'burst' | 'enhanced' | 'mega' | 'fullHouse' | 'straight' | 'pair' | 'threeKind' | 'fourKind' | 'straightFlush' | 'royalFlush' | 'rainbow' | 'ultimate';
  suit?: string;
  rank?: number;
  triggered: boolean;
  turnNumber: number;
}

interface ChallengeChainModifier {
  challengeId: number;
  modifier: 'easierTrigger' | 'bonusEffect' | 'earlyUnlock';
  value: number;
}

interface ChainState {
  // Suit Chain Tracking
  currentSuit: 'hearts' | 'diamonds' | 'clubs' | 'spades' | null;
  suitChainLength: number; // Consecutive wins with current suit (persists across losses)
  lastWinSuit: 'hearts' | 'diamonds' | 'clubs' | 'spades' | null;
  
  // Rank Chain Tracking (for poker-style chains)
  rankHistory: number[]; // Last 6 ranks won (for Straight, Pair detection)
  suitHistory: ('hearts' | 'diamonds' | 'clubs' | 'spades')[]; // Last 6 suits won
  
  // Chain History
  chainHistory: ChainTrigger[]; // Track triggered chains this game
  challengeModifiers: ChallengeChainModifier[]; // Active challenge effects
}

interface ChainTrigger {
  type: 'burst' | 'enhanced' | 'mega' | 'fullHouse' | 'straight' | 'pair' | 'threeKind' | 'fourKind' | 'straightFlush' | 'royalFlush' | 'rainbow' | 'ultimate';
  suit?: string;
  rank?: number;
  triggered: boolean;
  turnNumber: number;
}

interface ChallengeChainModifier {
  challengeId: number;
  modifier: 'easierTrigger' | 'bonusEffect' | 'earlyUnlock';
  value: number;
}
```

**Turn State Structure:**

```typescript
interface TurnState {
  turnNumber: number;
  currentTurnState: 'preTurn' | 'cardDraw' | 'resolution' | 'postWinPlayer' | 'postWinEnemy';
  playerCard: Card | null;
  enemyCard: Card | null;
  winner: 'player' | 'enemy' | null;
  damage: number;
  cardsCaptured: Card[];
  warState: WarState | null;
  specialsPlayed: SpecialPlay[];
}

interface WarState {
  warDepth: number; // Current War depth (1-5 max)
  playerFaceDown: Card[]; // 2 face-down cards
  playerFaceUp: Card | null;
  enemyFaceDown: Card[]; // 2 face-down cards
  enemyFaceUp: Card | null;
  warWinner: 'player' | 'enemy' | null;
  allWarCards: Card[]; // All cards involved in War
}

interface SpecialPlay {
  type: 'suit' | 'warlord';
  suit?: 'hearts' | 'diamonds' | 'clubs' | 'spades';
  playedBy: 'player' | 'enemy';
  timestamp: number;
  effects: SpecialEffect[];
}

interface SpecialEffect {
  type: 'heal' | 'damage' | 'armor' | 'gold' | 'cardManipulation' | 'status' | 'turnManipulation';
  target: 'player' | 'enemy' | 'both';
  amount: number;
  duration?: number; // For status effects
  description: string;
}
```

**Post-Game State Structure:**

```typescript
interface PostGameState {
  gameResult: 'win' | 'loss';
  finalHP: {
    player: number;
    enemy: number;
  };
  rewards: {
    xp: RewardBreakdown;
    gold: RewardBreakdown;
  };
  levelUp: LevelUpState | null;
  unlocks: UnlockState[];
  collectionMilestones: CollectionMilestone[];
  statistics: StatisticsUpdate;
}

interface RewardBreakdown {
  turnRewards: number;
  completionBonus: number;
  firstTimeBonus: number; // If first-time defeat
  streakBonus: number; // Streak multiplier applied
  total: number;
}

interface LevelUpState {
  newLevel: number;
  bonusGold: number; // 50 × new level
  unlocks: {
    enemyWarlord: number | null; // Warlord ID
    battleItems: number[]; // Battle Item IDs
  };
}

interface UnlockState {
  type: 'enemyWarlord' | 'playerWarlord' | 'battleItem';
  warlordId?: number;
  battleItemId?: number;
  name: string;
  description: string;
}

interface CollectionMilestone {
  type: 'warlord' | 'battleItem';
  milestone: number; // 10, 25, 50, 59
  reward: {
    gold: number;
    xp: number;
    badge: string;
  };
}

interface StatisticsUpdate {
  gamesPlayed: number; // Incremented
  gamesWon: number; // Incremented if win
  winRate: number; // Recalculated
  totalXPEarned: number; // Incremented
  totalGoldEarned: number; // Incremented
  highestStreak: number; // Updated if new record
  warlordsDefeated: number; // Incremented if first-time defeat
}
```

#### State Persistence

**What Gets Saved:**

**LocalStorage (F2P):**
- Player progress (level, XP, Gold)
- Unlocked Warlords (Enemy + Player)
- Owned Battle Items
- Statistics
- Collection progress
- Settings and preferences
- Last login timestamp
- Last played Warlords (for defaults)

**Cloud Storage (PAID):**
- All LocalStorage data
- Additional: Game history, achievement progress
- Cross-device sync enabled

**What Does NOT Get Saved:**
- Active game state (game in progress)
- Turn state (resets on app close)
- Temporary overlays state
- Animation states

**When State Gets Saved:**

**Auto-Save Triggers:**
- After game completion (post-game)
- After level-up
- After unlock
- After Gold/XP changes
- After settings changes
- On app exit/background

**Manual Save:**
- Available in Game Menu (PAID accounts)
- "Save Progress" button
- Confirmation: "Progress Saved!"

**State Restoration:**

**On App Launch:**
1. Load localStorage data
2. Restore player progress
3. Restore settings
4. Restore last played Warlords
5. Check daily bonus eligibility
6. Load cloud sync (PAID)

**On Game Start:**
- Game state initialized fresh (not restored)
- Previous game state discarded
- New game session begins

**State Recovery:**
- If localStorage corrupted: Initialize default state, warn player
- If cloud sync fails: Use local data, retry sync
- If progress lost: Contact support (PAID accounts only)

#### State Machine Implementation Notes

**State Machine Pattern:**
- Use finite state machine (FSM) pattern
- States are mutually exclusive
- Transitions are well-defined
- State changes trigger side effects (animations, sounds, saves)

**State Management:**
- Zustand store (lightweight, React-friendly)
- Separate stores: AppState, GameState, TurnState
- State updates trigger UI re-renders
- State persistence handled separately

**State Validation:**
- Validate state transitions (prevent invalid transitions)
- Validate state data (ensure consistency)
- Log state changes (for debugging)
- Handle edge cases (invalid states, corrupted data)

**Performance:**
- State updates batched when possible
- React.memo used for expensive components
- Rapid state changes debounced
- State persistence optimized (not saved every frame)

**Testing:**
- Test all state transitions
- Test state persistence/restoration
- Test invalid state handling
- Test state recovery scenarios

### Decks and Cards

This section details the structure, composition, visual design, and management of decks and cards in Bigfoot War.

#### Deck Composition

**Standard Deck Structure:**
- Each Warlord uses a streamlined deck: 36 cards total
- **A–6 Cards:** 6 ranks × 4 suits = 24 cards
  - Ranks: Ace, 6, 5, 4, 3, 2
  - Suits: Hearts, Diamonds, Clubs, Spades
  - Each rank/suit combination appears exactly once
- **1 Joker:** Neutral wild card, auto-win + shuffle (classic War behavior players expect)
- **1 Signature Card:** Unique hyper-thematic card per Warlord (creates distinct "boss moment" every match)
- **Total per deck:** 36 cards (24 A–6 + 1 Joker + 1 Signature)
- **Total in play:** 72 cards (36 per player at game start)

**Card Distribution:**
- Hearts: Ace, 6, 5, 4, 3, 2 (6 cards)
- Diamonds: Ace, 6, 5, 4, 3, 2 (6 cards)
- Clubs: Ace, 6, 5, 4, 3, 2 (6 cards)
- Spades: Ace, 6, 5, 4, 3, 2 (6 cards)
- Joker: 1 card (neutral, no suit designation)
- Signature: 1 card (unique per Warlord, hyper-thematic)

**Deck Initialization:**
- At game start, each Warlord's deck is created fresh
- All 36 cards are added to deck array (24 A–6 cards + 1 Joker + 1 Signature)
- Signature card is assigned based on Warlord ID (each Warlord has unique Signature)
- Deck is shuffled using Fisher-Yates algorithm
- Shuffling is independent per player (no shared seed)
- Decks are shuffled before first draw

**Deck State Tracking:**
- Deck size: Current number of cards in deck
- Card order: Array of cards (top to bottom)
- Captured cards: Cards captured this game (for charge calculation)
- Buried cards: Cards marked as buried (always return to owner)
- Banished cards: Cards marked as banished (permanently locked)
- Total cards: Always 72 cards in play (distributed between decks)
- Signature cards: Can be captured and used by opponent (creates strategic tension and "boss moment" when drawn)

**Deck Visualization:**
- Deck indicator: Visual stack representation + count
- Position: Adjacent to Warlord avatar
- Size: 150x40px (deck stack icon + count text)
- Animation: Pulse effect when deck size < 10 cards
- Display: "Deck: X" text (16px pixel font)

#### Card Structure

**Card Data Model:**

```typescript
interface Card {
  id: string; // Unique card identifier (e.g., "hearts-ace-1", "signature-sasquatch-1")
  suit: 'hearts' | 'diamonds' | 'clubs' | 'spades' | 'joker' | 'signature';
  rank: number; // 2-14 (2-6, 14=Ace for A-6 cards; 15=Joker; varies for Signature)
  rankName: string; // "Ace", "6", "5", "4", "3", "2", "JOKER", or Signature name
  isJoker: boolean;
  isSignature: boolean; // True if this is the Warlord's Signature card
  signatureWarlordId: number | null; // Warlord ID this Signature belongs to (null if not Signature)
  signatureEffect: SignatureEffect | null; // Signature card effect (if Signature)
  owner: 'player' | 'enemy'; // Current owner
  buried: boolean; // Marked as buried (always returns to owner)
  banished: boolean; // Marked as banished (permanently locked)
  originalOwner: 'player' | 'enemy'; // Original owner (for banished cards)
}

interface SignatureEffect {
  warlordId: number;
  effectType: 'instant' | 'ongoing' | 'trigger';
  effect: string; // Effect description
  rank: number; // Signature card rank (typically 14-16)
}
```

**Card Properties:**

**Rank Values:**
- Ace = 14 (highest standard rank in A–6 set)
- 6, 5, 4, 3, 2 = face value (6, 5, 4, 3, 2)
- Joker = 15 (highest, beats all cards including Signature)
- Signature = Variable rank (determined by Signature card effect, typically 14-16 range)

**Rank Names:**
- Ace: Display as "ACE"
- Number cards: Use numeric display (6, 5, 4, 3, 2)
- Joker: Display as "JOKER"
- Signature: Display as Signature card name (e.g., "SASQUATCH'S ROAR", "YETI'S FURY") 

**Suit Properties:**
- Hearts: Red suit, healing/sustain theme
- Diamonds: Red suit, utility/Gold theme
- Clubs: Black suit, physical damage theme
- Spades: Black suit, ranged damage theme
- Joker: No suit, neutral wild card (same for all Warlords)
- Signature: No suit, hyper-thematic card (unique per Warlord, creates "boss moment")

**Card Status Flags:**
- `buried`: Card always returns to owner even if enemy wins it
- `banished`: Card permanently locked to owner's deck
- `owner`: Current deck owner (can change via steal)
- `originalOwner`: Original owner (for banished cards, never changes)

**Card Identification:**
- Each card has unique ID for tracking
- Format: `{suit}-{rank}-{instance}` (e.g., "hearts-ace-1", "joker-1")
- Used for tracking card movement, buried/banished status
- Helps with debugging and state management

#### Card Visual Design

**Card Dimensions:**

**Deck Cards:**
- Size: 80x120px
- Aspect ratio: 2:3 (standard playing card ratio)
- Used for: Deck indicators, card stacks, in-deck display

**Battle Zone Cards:**
- Size: 100x150px (25% larger than deck cards)
- Aspect ratio: 2:3 (maintains proportions)
- Used for: Cards in play, card reveals, battle zone display
- Rationale: Enhanced hero visibility and readability

**Card Face Layout:**

**Standard Cards (80x120px deck / 100x150px battle zone):**
- **Background:** Suit-colored frame (red for Hearts/Diamonds, black for Clubs/Spades)
- **Top Section:** Hero image (40x60px deck / 50x75px battle zone)
  - Position: Top-center, 8px from top edge
  - Source: Warlord hero sprite (from Warlord roster)
  - Display: Prominently featured, thematic to Warlord
- **Center Section:** Rank display
  - Font: Bold pixel font (Press Start 2P)
  - Size: 32px (deck) / 40px (battle zone)
  - Position: Center of card
  - Color: High contrast (white/black depending on suit)
  - Format: Rank name (Ace, King, Queen, Jack) or number (2-10)
- **Bottom Section:** Suit icon
  - Size: 24x24px (deck) / 30x30px (battle zone)
  - Position: Bottom-center, 8px from bottom edge
  - Display: Suit symbol (♥ ♦ ♣ ♠) + colorblind-friendly shape
  - Color: Red (Hearts/Diamonds) or Black (Clubs/Spades)
- **Border:** 2px pixel border (suit color)
- **Corners:** Rounded corners (4px radius) for modern feel

**Joker Cards:**
- **Background:** Wild swirl pattern (animated)
- **Hero Image:** Same as standard cards (Warlord hero)
- **Center:** "JOKER" text (large, bold, wild font)
- **Visual Effect:** Glowing border, pulsing animation
- **Color Scheme:** Gold accent (distinctive)

**Card Back Design:**

**Generic Design (No Warlord Avatar):**
- **Background:** Dark wood texture (#3A2A1A) matching game table
- **Pattern:** Subtle pixel art pattern (repeating geometric design)
- **Border:** 2px border (muted color)
- **Style:** Retro SNES aesthetic, matches game theme
- **Consistency:** Same design for all cards (no personalization)
- **Display:** Shown when cards are face-down (War scenarios, deck indicators)

**Card Back Specifications:**
- Size: Matches card face (80x120px deck / 100x150px battle zone)
- Visual: Distinct from card face (no confusion)
- Style: Pixel art, retro aesthetic
- Color: Dark, muted tones (doesn't distract from game)

**Suit Representation:**

**Visual Design:**
- Hearts: ♥ symbol (red)
- Diamonds: ♦ symbol (red)
- Clubs: ♣ symbol (black)
- Spades: ♠ symbol (black)
- Icons: Pixel art style, clear and readable

**Colorblind-Friendly Design:**
- Hearts: Red + Circle shape
- Diamonds: Red + Diamond shape
- Clubs: Black + Clover shape
- Spades: Black + Spade shape
- Shapes: Distinct geometric shapes in addition to color
- High contrast: Ensures visibility for colorblind players

**Rank Display:**

**Typography:**
- Font: Press Start 2P (pixel font) 
- Size: 32px (deck cards) / 40px (battle zone cards)
- Weight: Bold
- Color: High contrast (white on dark, black on light)
- Style: Uppercase for face cards (ACE, KING, QUEEN, JACK)

**Positioning:**
- Center of card (primary rank display)
- Top-left corner: Small rank indicator (16px)
- Bottom-right corner: Small rank indicator (16px)
- Format: Large center display for readability

**Hero Image Integration:**

**Hero Image Specifications:**
- Source: Warlord hero sprite (from Warlord roster)
- Size: 40x60px (deck cards) / 50x75px (battle zone cards)
- Position: Top-center of card
- Style: Pixel art, retro SNES aesthetic
- Display: Prominently featured, thematic to Warlord

**Hero Image Display:**
- All cards show the same hero image (current Warlord's hero)
- Hero image matches Player Warlord (for player cards)
- Hero image matches Enemy Warlord (for enemy cards)
- Provides visual identity and thematic connection

**Visual Effects:**

**Card States:**
- **Normal:** Standard appearance
- **Highlighted:** Winner card glows (pulsing border, 2s cycle)
- **Dimmed:** Loser card dims (50% opacity)
- **Ready:** Special-ready cards glow (if applicable)
- **Buried:** Subtle marker/border (if visible)
- **Banished:** Distinct marker/border (if visible)

**Card Animations:**
- **Flip:** 180° rotation (0.3s duration, step-wise easing)
- **Slide:** Smooth translation (0.4s duration, ease-out)
- **Glow:** Pulsing border (2s cycle, continuous)
- **Capture:** Slide to deck + fade (0.5s duration)

#### Deck Management

**Shuffling Algorithm:**

**Fisher-Yates Shuffle:**
- Algorithm: Standard unbiased shuffle
- Implementation: Swap each card with random card from remaining unshuffled portion
- Performance: O(n) time complexity
- Randomness: Cryptographically secure random (crypto.getRandomValues)
- Usage: Game initialization, Joker shuffle trigger

**Shuffle Triggers:**
- Game initialization: Both decks shuffled independently
- Joker drawn: That player's deck shuffled immediately
- Reshuffle specials: Triggered by special abilities (e.g., Demonic Flight)

**Shuffle Visual Feedback:**
- Animation: Deck visual shuffle effect
- Sound: Card riffle chiptune sound
- Duration: <1 second (quick, doesn't delay gameplay)
- Messaging: Status banner shows "Deck Shuffled!" (if Joker trigger)

**Drawing Mechanics:**

**Card Draw Process:**
1. Check deck size (must have cards to draw)
2. Remove top card from deck array
3. Update deck size counter
4. Return card object
5. If deck empty: Trigger game end (deck depletion win condition)

**Draw Timing:**
- Simultaneous: Both players draw at same time
- No delay: Instant draw (no waiting for animation)
- Animation: Cards animate from deck to battle zone (visual only)

**Card Capture:**

**Capture Process:**
1. Winner determined (card rank comparison)
2. Both cards (player + enemy) marked for capture
3. Cards added to winner's deck bottom
4. Update winner's deck size
5. Update captured cards tracking (for charge calculation)
6. Cards maintain their properties (suit, rank, status flags)

**Capture Rules:**
- Winner takes all cards from table (both cards)
- Cards go to bottom of winner's deck (not top)
- Cards maintain buried/banished status
- Buried cards: Always return to original owner (even if enemy wins)
- Banished cards: Permanently locked to owner (never leave deck)

**Card Recycling:**

**Recycling Mechanics:**
- Cards are never removed from play
- Cards cycle through decks continuously
- When deck depleted: Cards from bottom cycle to top (if any remain)
- Total cards: Always 72 cards in play (distributed between decks)
- Signature cards: Can be captured and used by opponent (creates strategic tension and "boss moment" when drawn)

**Recycling Behavior:**
- Cards captured go to bottom of deck
- Cards drawn from top of deck
- Natural cycling: Cards move through deck over time
- No card loss: All cards remain in play for entire game

**Deck Size Tracking:**

**Size Calculation:**
- Initial size: 36 cards per deck (24 A–6 + 1 Joker + 1 Signature)
- After capture: Size increases (cards added)
- After draw: Size decreases (cards removed)
- After manipulation: Size changes (steal/bury/banish)

**Size Display:**
- Deck indicator: Shows current deck size
- Format: "Deck: X" (16px pixel font)
- Update: Real-time as cards move
- Visual: Deck stack icon + count

**Deck Depletion:**

**Depletion Condition:**
- Deck size reaches 0 (no cards remaining)
- Cannot draw card (deck empty)
- Triggers game end (deck depletion win condition)

**Depletion Handling:**
- Check deck size before each draw
- If deck empty: Game ends, opponent wins
- Visual: Deck indicator shows "0" 
- Animation: Deck indicator pulses/flashes when low (<10 cards)

#### Card Manipulation

**Steal Mechanics:**

**Steal Process:**
1. Special triggers steal (e.g., Cannibal Feast)
2. Select target card(s) from enemy deck
3. Remove card(s) from enemy deck
4. Add card(s) to player deck bottom
5. Update card owner property
6. Update deck sizes

**Steal Rules:**
- Cards moved from enemy deck to player deck
- Cards can be recaptured normally (enemy can win them back)
- Cards maintain suit/rank properties
- Cards go to bottom of deck (not top)
- Steal affects deck sizes (asymmetric transfer)

**Bury Mechanics:**

**Bury Process:**
1. Special triggers bury (e.g., Avalanche)
2. Select target card(s) from enemy deck
3. Remove card(s) from enemy deck
4. Add card(s) to player deck bottom
5. Mark card(s) as buried (buried flag = true)
6. Update card owner property
7. Update deck sizes

**Bury Rules:**
- Cards moved from enemy deck to player deck
- Cards marked as buried (buried flag = true)
- Buried cards always return to player deck (even if enemy wins them)
- Bury effect persists for entire game
- Cards maintain suit/rank properties

**Bury Tracking:**
- Buried cards tracked in buriedCards array
- When enemy wins buried card: Card returns to player deck (not enemy deck)
- Visual marker: Subtle indicator on buried cards

**Banish Mechanics:**

**Banish Process:**
1. Special triggers banish (e.g., Portal Rift)
2. Select target card(s) from enemy deck
3. Remove card(s) from enemy deck
4. Add card(s) to player deck bottom
5. Mark card(s) as banished (banished flag = true)
6. Set originalOwner property (never changes)
7. Update card owner property
8. Update deck sizes

**Banish Rules:**
- Cards moved from enemy deck to player deck
- Cards marked as banished (banished flag = true)
- Banished cards permanently locked to player deck
- If banished card played and loses: Card returns to player deck, next card plays instead
- Banish effect persists for entire game
- Cards maintain suit/rank properties

**Banish Tracking:**
- Banished cards tracked in banishedCards array
- Original owner never changes (even if card moves)
- When banished card loses: Card returns to deck, next card plays
- Visual marker: Distinct indicator on banished cards

**Card Tracking:**

**Tracking Requirements:**
- Track all 72 cards in play (36 cards per deck × 2)
- Track card locations (which deck)
- Track card status (buried, banished)
- Track card ownership (current owner, original owner)
- Track card movement (for charge calculation)

**Tracking Implementation:**
- Card objects contain all tracking data
- Deck arrays contain card references
- Buried/banished arrays track special cards
- Card IDs ensure unique identification
- State updates maintain consistency

#### Card Display and Animations

**Card Flip Animation:**

**Specifications:**
- Duration: 0.3 seconds (300ms)
- Easing: Step-wise (pixel snap, no smooth interpolation)
- Rotation: 180° (face-down → face-up)
- Axis: Y-axis rotation (horizontal flip)
- Style: Pixel-perfect (no anti-aliasing)

**Flip Process:**
1. Card starts face-down (card back visible)
2. Rotation begins (Y-axis 0° → 180°)
3. Midpoint: Card edge-on (brief moment)
4. Rotation completes (face-up, card face visible)
5. Hero image and rank revealed

**Flip Timing:**
- Trigger: Card draw phase
- Simultaneous: Both cards flip at same time
- Sound: Card flip chiptune sound (crisp, brief)
- Visual: Smooth 180° rotation

**Card Slide Animation:**

**Specifications:**
- Duration: 0.4 seconds (400ms)
- Easing: Ease-out (fast start, slow end)
- Path: Straight line (deck position → battle zone)
- Style: Pixel-perfect movement

**Slide Process:**
1. Card starts at deck position
2. Card animates to battle zone position
3. Card arrives at destination
4. Card flip animation begins (if applicable)

**Slide Paths:**
- Deck → Battle Zone: Top/bottom deck → center battle zone
- Battle Zone → Deck: Center → winner's deck area
- Capture: Cards slide to winner's deck bottom

**Card Reveal:**

**Reveal Timing:**
- Cards revealed simultaneously (both players)
- No delay: Instant reveal after flip animation
- Visual: Cards appear face-up in battle zone
- Sound: Card flip sound completes

**Reveal Display:**
- Cards shown face-up in battle zone
- Hero images visible
- Ranks clearly displayed
- Suits clearly displayed
- High contrast for readability

**Card Capture Animation:**

**Specifications:**
- Duration: 0.5 seconds (500ms)
- Easing: Ease-in-out
- Path: Battle zone → winner's deck
- Style: Slide + fade

**Capture Process:**
1. Winner determined
2. Cards highlight (winner card glows)
3. Cards slide toward winner's deck
4. Cards fade slightly
5. Cards arrive at deck bottom
6. Deck size updates
7. Sound: Card capture chiptune

**Capture Visual Feedback:**
- Winner card: Glowing border (pulsing)
- Loser card: Dimmed appearance (50% opacity)
- Cards: Slide animation to deck
- Deck: Visual update (size counter changes)

**War Card Display:**

**Face-Down Cards:**
- Display: Card back visible (generic design)
- Position: Stacked 
- Count: 2 face-down cards per player
- Animation: Deal animation (cards placed face-down)

**Face-Up Cards:**
- Display: Card face visible (hero, rank, suit)
- Position: Center of War area
- Count: 1 face-up card per player
- Animation: Reveal animation (flip from face-down)

**War Card Layout:**
- Face-down: Stacked vertically or horizontally
- Face-up: Centered, prominent display
- Spacing: Adequate spacing for readability
- Size: Scales down if 6 cards need to fit (80x120px)

#### Card Rendering

**Rendering Approach:**

**Hybrid Approach:**
- **Battle Zone Cards:** Canvas-rendered (better animation performance)
- **Deck Indicators:** DOM-based (simpler, less frequent updates)
- **Card Backs:** Pre-rendered sprites (loaded as images)
- **Card Faces:** Canvas-rendered dynamically (hero image + rank + suit)

**Card Pool Management:**

- **Object Pooling**: ** Reuse card elements instead of creating/destroying
- **Implementation:** Pre-create card objects, reuse for animations
- **Pool Size:** 10-20 card objects (enough for War scenarios)
- **Benefits:** Better performance, reduced garbage collection
- **Usage:** Cards drawn from pool, returned after animation

**Card Caching:**

- **Pre-Render Card Elements**: Faster rendering, consistent appearance
- **Implementation:** Pre-render card faces to image cache
- **Cache:** Store rendered cards by suit+rank+Warlord combination
- **Benefits:** Faster display, consistent rendering
- **Usage:** Load from cache when displaying cards

**Performance:**

**Rendering Optimization:**
- **Batch Updates:** Multiple cards updated in single render cycle
- **Dirty Checking:** Only changed cards re-rendered
- **Frame Budget:** Target 60fps, frames skipped if needed
- **LOD (Level of Detail):** Simpler rendering for off-screen cards

**Animation Performance:**
- **GPU Acceleration:** Canvas rendering uses browser GPU acceleration automatically (no WebGL, no CSS transforms)
- **Reduce Simultaneous Animations:** Limit to 2-4 cards animating at once
- **Animation Pooling:** Reuse animation objects
- **Frame Skipping:** Skip frames if performance drops

**Memory Management:**
- **Card Object Limits:** Maximum 72 cards in play (fixed)
- **Image Caching:** Cache rendered card images (limit cache size)
- **Cleanup:** Remove unused card objects from pool
- **Garbage Collection:** Minimize object creation/destruction

**Visual Effects:**

**Card States Rendering:**
- **Normal:** Standard rendering
- **Highlighted:** Add glow effect using Canvas shadowBlur and gradient drawing operations
- **Dimmed:** Reduce opacity (50%)
- **Ready:** Add pulsing border (animated)
- **Buried:** Add subtle marker
- **Banished:** Add distinct marker
- **Signature:** Thematic styling matching Warlord theme (unique visual treatment)
- **Joker:** Neutral styling (same for all Warlords)

**Particle Effects:**
- **Card Capture:** Minimal particles (8x8px sparks)
- **Card Reveal:** Brief flash effect
- **Winner Card:** Glow particles
- **Performance:** Limit particles, use object pooling

**Accessibility:**

**Visual Accessibility:**
- **Colorblind Support:** Shapes in addition to colors
- **High Contrast:** 4.5:1 minimum contrast ratio
- **Text Size:** Readable at card size (32-40px)
- **Alt Text:** Screen reader support (if DOM-based)

**Animation Accessibility:**
- **Reduced Motion:** Respect prefers-reduced-motion
- **Animation Duration:** Configurable (faster/slower)
- **Visual Indicators:** Clear winner/loser indication
- **Status Messages:** Text descriptions of card actions

#### Card Rendering Implementation Details

**Canvas Rendering Pipeline:**

1. **Initialization:**
   - Create canvas element (100x150px for battle zone)
   - Set up rendering context (2D or WebGL)
   - Load card assets (hero images, suit icons, fonts)

2. **Card Rendering:**
   - Clear canvas
   - Draw background (suit-colored frame)
   - Draw hero image (top-center)
   - Draw rank text (center)
   - Draw suit icon (bottom-center)
   - Draw border
   - Apply visual effects (glow, dim, etc.)

3. **Animation:**
   - Update card position (slide)
   - Update card rotation (flip)
   - Update visual effects (glow pulse)
   - Render frame
   - Repeat until animation complete

**Card Asset Loading:**

**Pre-Loading Strategy:**
- Load hero images on game start (59 Warlords × hero sprites)
- Load suit icons (4 suits)
- Load card back image (generic design)
- Load fonts (pixel fonts)
- Cache loaded assets

**Lazy Loading:**
- Load hero images on-demand (when Warlord selected)
- Load card assets when needed
- Unload unused assets (memory management)

**Asset Formats:**
- **Hero Images:** PNG (pixel art, transparent background)
- **Suit Icons:** SVG or PNG (scalable)
- **Card Back:** PNG (pixel art)
- **Fonts:** WOFF2 or TTF (pixel fonts)

**Card Rendering Performance Targets:**

**Frame Rate:**
- Target: 60fps (16.67ms per frame)
- Minimum: 30fps (acceptable for mobile)
- Optimization: Skip frames if needed, maintain gameplay

**Render Time:**
- Card render: <5ms per card
- Animation update: <10ms per card
- Batch rendering: <16ms for all cards

**Memory Usage:**
- Card objects: ~1KB per card (72 cards = ~72KB)
- Rendered images: ~50KB per card (cached)
- Total memory: <10MB for card system

**Optimization Strategies:**

**Rendering Optimizations:**
- **Dirty Rectangles:** Only re-render changed areas
- **Sprite Batching:** Batch card renders together
- **Texture Atlases:** Combine card assets into single texture
- **Level of Detail:** Simpler rendering for small cards

**Animation Optimizations:**
- **Easing Functions:** Use efficient easing (pre-calculated)
- **Animation Pooling:** Reuse animation objects
- **Frame Skipping:** Skip frames if performance drops
- **GPU Acceleration:** Canvas rendering uses browser GPU acceleration automatically

**Memory Optimizations:**
- **Object Pooling:** Reuse card objects
- **Asset Caching:** Cache rendered images
- **Garbage Collection:** Minimize object creation
- **Memory Limits:** Set maximum cache sizes

#### Card Display

**Card Rendering: Canvas-Based**
- **Rationale:** Better performance for pixel art, smoother animations, matches tech stack (WebGL/Canvas)
- **Implementation:** HTML5 Canvas for card rendering, WebGL for advanced effects
- **Benefits:** Pixel-perfect rendering, efficient animations, good performance
- **Complexity:** More complex than DOM, requires manual rendering logic

**Card Animations: Step-Wise Easing**
- **Rationale:** Matches pixel art aesthetic, feels retro, maintains visual consistency
- **Implementation:** Discrete animation steps (no smooth interpolation)
- **Duration:** 0.3s flip, 0.4s slide, 0.5s capture
- **Benefits:** Retro feel, pixel-perfect movement, clear visual feedback

**Card Display: Dynamic Sizing**
- **Rationale:** Battle zone cards larger for visibility, deck cards smaller for space efficiency
- **Implementation:** Scale cards based on context (deck vs battle zone)
- **War Scenarios:** Scale down to 80x120px if 6 cards need to fit (reduced from 8 cards with 2 face-down per player)
- **Benefits:** Optimal visibility, efficient space usage, responsive design

**Performance: Object Pooling + Caching**
- **Rationale:** Better performance, reduced memory allocation, smoother animations
- **Implementation:** Pre-create card objects, cache rendered images
- **Pool Size:** 10-20 card objects (enough for War scenarios)
- **Benefits:** Consistent 60fps, reduced garbage collection, efficient memory usage

**Visual Effects: Subtle but Clear**
- **Rationale:** Enhances feedback without overwhelming, maintains retro aesthetic
- **Implementation:** Glow effects for winners, dimming for losers, pulsing for ready specials
- **Intensity:** Moderate (visible but not distracting)
- **Benefits:** Clear feedback, maintains visual clarity, enhances gameplay


### Bigfoot Warlords

Warlord stats:
- HP: 80-120 range (rebalanced for 36-card decks - games end faster, so HP adjusted to maintain appropriate game length)
- Damage: Base dealt per win (e.g., 2 + rank bonus/10). Suits/specials multiply (e.g., Hearts: +1). **Note:** With 36-card decks having more high ranks, base damage may need slight reduction - requires playtesting.
- Power Charge: Wins OR damage taken needed to ready Warlord Special (e.g., "Steal card" at 5 wins OR 8 damage). Suits charge on capture (e.g., 3 Spades = ready). Charges persist through losses. 3-7 wins OR 5-10 damage range 

Other Warlord properties:
- Description: text description
- Level: when Warlord can be unlocked for play as Player Warlord and as Enemy Warlord
- AI strategy: code-based, described briefly in design but not shown to players
- Special Power: different powers unlock at different levels
- Specials: what they are, how they are triggered, how they change per level
- Battle Items: 1 per level (starting at unlock level)
  - New enemies don't have Battle Items enabled
  - Replayed enemies have increasing chance of enabled items during gameplay

Bigfoot Warlords Roster
| # | Warlord | Level | HP | Damage | Charge | Special Power | Hearts Special | Diamonds Special | Clubs Special | Spades Special | H Thr | D Thr | C Thr | S Thr | Battle Item | Signature Card | AI Strategy |
|---|---------|-------|----|--------|--------|---------------|----------------|------------------|---------------|----------------|-------|-------|-------|-------|-------------|----------------|-------------|
| 1 | Sasquatch | 1 | 80 | 2 | 7 | Forest Regen (Passive: +1 HP/turn) | Heal 2 | +50 Gold | Scratch (+2 dmg) | Rock Throw (rank dmg) | 1 | 2 | 2 | 3 | Moss Cloak (+2 max HP) | Bigfoot's Call (Reveal Enemy Hand) | Balanced, prioritizes power charge |
| 2 | Skunk Ape | 2 | 80 | 2 | 7 | Stink Cloud (Enemy specials disabled 2 turns) | Armor 2 (next dmg -2) | Poison DoT (1 dmg x5) | Slime Punch (+3 dmg) | Gas Spray (rank+1) | 3 | 1 | 2 | 2 | Poison Sac (Clubs apply DoT 1x3) | Toxic Belch (Poison 3) | Diamonds focus, early poison pressure |
| 3 | Wendigo | 3 | 81 | 2 | 7 | Cannibal Feast (Steal 1 card from enemy deck) | Heal 3 (lose 1 max HP) | Fear Aura (Enemy charge +1) | Antler Gore (+4 dmg) | Ice Wind (rank dmg x1.2) | 2 | 2 | 1 | 3 | Hunger Bone (+1 heal on win) | Consume (Steal 5 HP) | Aggressive Clubs, charges power fast |
| 4 | Jersey Devil | 4 | 81 | 2 | 7 | Demonic Flight (Reshuffle deck + extra draw) | Blood Heal 2 | Hellfire (rank*1.5 dmg) | Claw Rake (+3 dmg) | Wing Blast (rank+2) | 2 | 2 | 3 | 1 | Devil Wing (Spades +1 dmg) | Sonic Screech (Stun Special) | Spades spam, evasive |
| 5 | Grassman | 5 | 81 | 2 | 7 | Earth Bind (Enemy dmg -1 for 3 turns) | Grass Regen 3 | +75 Gold | Vine Slam (+4 dmg) | Seed Shot (rank dmg) | 1 | 3 | 2 | 2 | Earth Root (Armor 1 passive) | Braided Shield (+5 Armor) | Defensive Hearts/Clubs |
| 6 | Fouke Monster | 6 | 83 | 2 | 7 | Amphibious Hide (Invulnerable 1 turn) | Slime Heal 2 | +50 Gold | Webbed Bite (+4 dmg) | Tongue Lash (rank+1) | 2 | 2 | 1 | 3 | Swamp Scale (Dodge 10% chance) | Swamp Strike (+5 Dmg) | Clubs focus, opportunistic |
| 7 | Mogollon Monster | 7 | 83 | 2 | 6 | Desert Mirage (Enemy plays random card next turn) | Heat Armor 3 | Sand Curse (DoT 1x4) | Dune Punch (+3 dmg) | Cactus Spike (rank+2) | 3 | 1 | 2 | 2 | Sand Veil (Hearts charge faster) | Mimic (Copy Enemy Special) | Spades/Diamonds control |
| 8 | Honey Island Swamp Monster | 8 | 83 | 2 | 6 | Vine Entangle (Enemy skips turn) | Vine Heal 3 | +100 Gold | Mud Crush (+4 dmg) | Thorn Dart (rank dmg) | 1 | 2 | 3 | 2 | Honey Trap (+20% Gold) | Mud Slog (Enemy Speed Down - Charge -1) | Hearts/Clubs sustain |
| 9 | Pope Lick Monster | 9 | 84 | 2 | 6 | Troll Toll (Steal next Gold reward) | Ritual Heal 2 | Lick Curse (DoT 2x3) | Horn Gore (+5 dmg) | Hoof Kick (rank+1) | 2 | 1 | 2 | 3 | Goat Horn (Charge -1) | Hypnosis (Steal 1 Charge) | Aggressive Diamonds/Clubs |
| 10 | Thunderbird | 10 | 84 | 2 | 6 | Storm Call (Deal 4 direct dmg) | Storm Regen 3 | Lightning (rank*1.2 + DoT1) | Talon Slash (+4 dmg) | Thunderbolt (rank*1.5) | 3 | 2 | 2 | 1 | Feather Amulet (Spades auto-crit 10%) | Lightning Rod (Deal 5 Direct Dmg) | Spades burst |
| 11 | Yeti | 11 | 84 | 3 | 6 | Avalanche (Deal 5 dmg + bury 1 card) | Ice Armor 4 | +125 Gold | Frost Fist (+5 dmg) | Blizzard (rank+3) | 3 | 3 | 4 | 2 | Ice Shard (Armor 2 passive) | Freeze (Freeze Enemy 1 Turn) | Defensive Spades |
| 12 | Almas | 12 | 85 | 3 | 6 | Nomad Stealth (Next loss free) | Heal 4 | +100 Gold | Cave Claw (+4 dmg) | Stone Throw (rank dmg x1.2) | 2 | 4 | 3 | 3 | Nomad Pouch (Extra Gold +25%) | Ancient Wisdom (+50 XP) | Balanced, evasive |
| 13 | Yeren | 13 | 85 | 3 | 6 | Martial Strike (Double dmg next win) | Chi Heal 3 | Mystic Palm (Heal enemy 2, steal turn) | Kung Fu Kick (+6 dmg) | Flying Knee (rank*1.3) | 3 | 3 | 2 | 4 | Bamboo Staff (Clubs +2 dmg) | Chi Punch (+5 Dmg) | Clubs burst |
| 14 | Barmanou | 14 | 85 | 3 | 6 | Mountain Grip (Steal 2 cards) | Cliff Regen 4 | +150 Gold | Rock Smash (+5 dmg) | Avalanche Toss (rank+2) | 3 | 4 | 2 | 3 | Climbing Rope (Charge on loss) | Stench (Poison 2) | Physical control |
| 15 | Chuchunya | 15 | 87 | 3 | 5 | Frost Breath (Enemy HP -1/turn 3 turns) | Fur Warmth 4 | Ice Shard Curse (DoT 2x4) | Bear Hug (+5 dmg) | Spear Throw (rank*1.4) | 4 | 2 | 3 | 3 | Tundra Pelt (+3 max HP) | Cold Snap (Freeze 1 Turn) | Diamonds debuff |
| 16 | Xueren | 16 | 87 | 3 | 5 | Chi Meditation (Full charge reset + heal 5) | Aura Heal 5 | Enlightenment (+200 Gold) | Palm Strike (+5 dmg) | Energy Blast (rank+3) | 2 | 3 | 3 | 4 | Lotus Orb (Hearts double effect) | Meditation (Heal 10) | Hearts sustain, patient |
| 17 | Migoi | 17 | 87 | 3 | 5 | Phase Shift (Dodge all dmg 1 turn) | Spirit Heal 4 | Phantom Mirage (Confuse 2 turns) | Ethereal Claw (+6 dmg) | Ghost Arrow (rank dmg ignore armor) | 3 | 2 | 4 | 3 | Spirit Totem (Invuln 1/game) | Phase (Invulnerable 1 Turn) | Evasive Diamonds |
| 18 | Kikomba | 18 | 88 | 3 | 5 | Savanna Sprint (Extra turn) | Heat Heal 4 | +175 Gold | Charge Tackle (+7 dmg) | Dust Kick (rank*1.2) | 4 | 3 | 2 | 3 | Speed Herb (Charge faster) | Lion's Roar (Enemy Damage -2) | Aggressive Clubs |
| 19 | Yowie | 19 | 88 | 3 | 5 | Outback Defense (Armor 5 next 2 turns) | Dirt Regen 5 | +150 Gold | Boomerang Punch (+6 dmg) | Dirt Bomb (rank+3) | 2 | 4 | 3 | 3 | Dirt Armor (Armor 3 passive) | Boomerang (Return Damage) | Defensive Hearts |
| 20 | Moehau | 20 | 88 | 3 | 5 | War Cry (All specials ready) | Tribal Heal 5 | Ancestor Curse (Enemy dmg -2 3 turns) | Haka Slam (+7 dmg) | Spear Volley (rank*1.5) | 3 | 3 | 2 | 4 | Tattoo Mark (Damage +1) | Haka (+2 Base Dmg Permanent) | Burst Clubs |
| 21 | Hibagon | 21 | 89 | 4 | 5 | Ninja Vanish (Reshuffle + steal 1) | Shadow Heal 4 | Shuriken (DoT 1x6) | Kunai Strike (+7 dmg) | Smoke Bomb (rank dmg + blind) | 3 | 2 | 3 | 4 | Ninja Scroll (Stealth dodge 20%) | Bonsai (Heal 5) | Spades control |
| 22 | Orang Pendek | 22 | 89 | 4 | 5 | Jungle Pounce (Triple dmg next Clubs) | Vine Heal 5 | +225 Gold | Arm Swing (+8 dmg) | Fruit Throw (rank+2) | 4 | 3 | 2 | 3 | Short Limb Boost (Clubs x1.5) | Fruit Throw (Deal 3 Dmg) | Clubs focus |
| 23 | Batutut | 23 | 89 | 4 | 4 | Trap Set (Enemy next card trapped, auto loss) | Camo Heal 5 | Trap Poison (DoT 3x3) | Wire Snare (+6 dmg) | Boomerang (rank*1.3) | 3 | 2 | 4 | 3 | Trap Kit (Chance enemy special fail) | Echolocation (Predict Next 3) | Trap Diamonds |
| 24 | Agogwe | 24 | 91 | 4 | 4 | Pack Hunt (Double wins count for charge) | Pack Regen 5 | +200 Gold | Frenzy Bite (+8 dmg) | Pack Rush (rank+4) | 4 | 3 | 2 | 3 | Pack Bond (+1 charge win) | Small Thief (Steal 50 Gold) | Fast charge Clubs |
| 25 | Maricoxi | 25 | 91 | 4 | 4 | Vine Control (Steal all table cards) | Nature Heal 6 | Emerald Blast (rank*1.6) | Root Crush (+8 dmg) | Vine Whip (rank dmg x1.4) | 2 | 4 | 3 | 3 | Vine Crown (Suits charge x2) | Blowdart (Poison 4) | Control Spades |
| 26 | Sisimito | 26 | 91 | 4 | 4 | Time Warp (Rewind last loss) | Mayan Heal 6 | Time Curse (Enemy charge reset) | Rune Punch (+9 dmg) | Temporal Bolt (rank+5) | 4 | 2 | 4 | 5 | Time Amulet (Undo 1 loss/game) | Eclipse (Blind Enemy) | Diamonds utility |
| 27 | Mapinguari | 27 | 92 | 4 | 4 | Psychic Scream (Enemy specials cooldown +3) | Backward Heal 6 | Eye Beam (5 direct dmg) | Sloth Claw (+9 dmg) | Psychic Wave (rank*1.7) | 5 | 3 | 4 | 4 | Single Eye (Predict next card 20%) | Belly Mouth (Destroy Top Deck Card) | Disruptive Diamonds |
| 28 | Mono Grande | 28 | 92 | 4 | 4 | Earthquake (Deal 6 dmg to enemy) | Primal Heal 6 | +300 Gold | Gorilla Pound (+10 dmg) | Rock Fling (rank+4) | 4 | 5 | 3 | 4 | Giant Fist (+2 base dmg) | Tremor (Shuffle Decks) | High damage Clubs |
| 29 | Ucumar | 29 | 92 | 4 | 4 | Bear Rage (Damage +2 for 5 turns) | Bear Regen 7 | +250 Gold | Paw Swipe (+9 dmg) | Honey Trap Shot (rank dmg + DoT) | 2 | 4 | 3 | 5 | Bear Claw (Clubs crit 15%) | Bear Trap (Enemy takes 5 dmg next draw) | Sustain Clubs |
| 30 | Arulataq | 30 | 93 | 4 | 4 | Shapeshift (Copy enemy special 1 time) | Aurora Heal 7 | Northern Light (Blind 3 turns) | Morph Claw (+10 dmg) | Ice Spear (rank*1.8) | 3 | 2 | 5 | 4 | Aurora Shard (Random suit boost) | Shape Shift (Copy Enemy Signature) | Adaptive Diamonds |
| 31 | Woodwose | 31 | 93 | 5 | 4 | Knightly Charge (5 direct + charge reset) | Leaf Heal 7 | +325 Gold | Sword Slash (+10 dmg) | Leaf Storm (rank+5) | 4 | 5 | 3 | 4 | Knight Shield (Armor 4) | Wild Shield (Armor 10) | Balanced knight |
| 32 | Basajaun | 32 | 95 | 5 | 4 | Forest Guard (Block all dmg 2 turns) | Moss Armor 8 | Oak Blast (DoT 2x5) | Bark Smash (+11 dmg) | Acorn Volley (rank dmg x1.5) | 3 | 4 | 4 | 5 | Guardian Oak (+5 max HP) | Flock (Heal 2/turn for 3 turns) | Heavy defense Hearts |
| 33 | Salvanel | 33 | 95 | 5 | 3 | Illusion Trick (Swap cards with enemy) | Fake Heal 7 (mirror enemy heal) | Mirage Gold (+400) | Phantom Punch (+10 dmg) | Illusion Arrow (rank + confuse) | 5 | 3 | 4 | 4 | Trick Mirror (Copy item 1/game) | Trickster (Swap Suit Charges) | Deceptive Diamonds |
| 34 | Almasti | 34 | 95 | 5 | 3 | Echo Location (Predict enemy card) | Cave Heal 8 | Sonar Curse (Enemy accuracy -20%) | Echo Claw (+11 dmg) | Bat Scream (rank*2) | 4 | 2 | 5 | 3 | Echo Crystal (Predict specials) | Echo (Repeat last win bonus) | Predictive Spades |
| 35 | Kapre | 35 | 96 | 5 | 3 | Smoke Confusion (Enemy random special) | Ash Heal 8 | Cigar Cloud (DoT 3x4) | Giant Fist (+12 dmg) | Smoke Blast (rank+6) | 5 | 3 | 4 | 4 | Cigar (Diamonds DoT +1) | Smoke Ring (Confuse) | Debuff Diamonds |
| 36 | Fear Liath | 36 | 96 | 5 | 3 | Fear Induce (Enemy charge x2) | Mist Heal 8 | Grey Terror (Direct 7 dmg) | Fog Claw (+12 dmg) | Mist Wave (rank dmg ignore armor) | 4 | 2 | 5 | 4 | Fear Cloak (Enemy AI panic 10%) | Terror (Enemy drops charge to 0) | Psychological Diamonds |
| 37 | Brenin Llwyd | 37 | 96 | 5 | 3 | Spectral Command (Control enemy special 1) | Royal Heal 9 | Crown Curse (Steal charge) | Thorn Mace (+13 dmg) | Fog Spear (rank*2.1) | 3 | 4 | 4 | 5 | Grey Crown (All suits ready faster) | Grey Fog (Enemy Blind) | Control Spades |
| 38 | Leshy | 38 | 97 | 5 | 3 | Shape Shift (Change to random Warlord power) | Bark Heal 9 | Vine Teleport (Swap positions) | Root Slam (+13 dmg) | Leaf Storm (rank+7) | 2 | 5 | 4 | 4 | Shape Twig (Random buff/turn) | Forest Trick (Swap Gold Earnings) | Unpredictable Hearts |
| 39 | Troll | 39 | 97 | 5 | 3 | Regen Troll (Heal 10 on use) | Rock Armor 10 | Stone Curse (Armor break) | Club Bash (+14 dmg) | Boulder Throw (rank*2.2) | 3 | 4 | 3 | 5 | Regen Moss (Passive heal 2/turn) | Regenerate (Heal 15) | Sustain tank Clubs |
| 40 | Wildman | 40 | 97 | 5 | 3 | Berserk Fury (Damage x2 5 turns, self dmg 1/turn) | Rage Heal 9 | Fury Gold (+500) | Berserk Punch (+15 dmg) | Wild Throw (rank+8) | 5 | 4 | 3 | 4 | Rage Totem (Damage +2 risk) | Frenzy (+10 Dmg, Self 5 Dmg) | High risk Clubs burst |
| 41 | Ancient Gigantopithecus | 41 | 99 | 5 | 3 | Prehistoric Stomp (Deal 8 dmg + bury 3 cards) | Fossil Heal 10 | Ancient Curse (DoT 4x4) | Jaw Crush (+15 dmg) | Bone Spear (rank*2.3) | 5 | 4 | 3 | 6 | Fossil Tooth (+3 dmg) | Stomp (Destroy Enemy Card) | Bury control Clubs |
| 42 | Quantum Sasquatch | 42 | 99 | 5 | 3 | Quantum Glitch (Random: win/loss flip last 3 turns) | Phase Heal 10 | Probability Warp (Random dmg 1-10) | Glitch Punch (+16 dmg) | Rift Blast (rank + random) | 6 | 4 | 5 | 5 | Quantum Core (Reroll loss 15%) | Superposition (Win & Loss Rewards) | Chaotic RNG Diamonds |
| 43 | Enkidu | 43 | 99 | 5 | 3 | Bull Wrath (Full heal + 10 dmg) | Primal Heal 12 | Wild Smite (rank*3) | Beast Fist (+16 dmg) | Judgment Bolt (rank*2.5) | 4 | 5 | 5 | 4 | Bull Ring (Passive +1 all stats) | Civilize (Remove all buffs/debuffs) | Sumerian Spades burst |
| 44 | Skinwalker | 44 | 100 | 5 | 3 | Shapeshift Copy (Copy player Warlord power) | Stolen Heal 11 | Curse Skin (Steal suit charge) | Morph Bite (+17 dmg) | Shadow Shot (rank dmg x2) | 5 | 3 | 6 | 5 | Skin Patch (Steal enemy item) | Transform (Copy Enemy Stats for Turn) | Mimic Diamonds |
| 45 | Kushtaka | 45 | 100 | 5 | 3 | Soul Steal (Steal 1 win toward charge) | Otter Heal 11 | Water Trick (Confuse + DoT) | Otter Claw (+17 dmg) | Wave Splash (rank+9) | 4 | 5 | 5 | 6 | Otter Pearl (Dodge + heal on dodge) | Lure (Steal Enemy Next Draw) | Tricky Hearts |
| 46 | Genoskwa | 46 | 100 | 5 | 3 | Stone Form (Invuln 3 turns) | Rock Heal 12 | Gem Blast (8 direct) | Granite Smash (+18 dmg) | Boulder Roll (rank*2.6) | 5 | 6 | 4 | 5 | Stone Heart (+10 max HP) | Stone Skin (Invuln 2 Turns) | Ultimate tank Clubs |
| 47 | Stick Indians | 47 | 101 | 5 | 3 | Invisible Whisper (Enemy misses next 2 cards) | Wind Heal 12 | Whisper Curse (Silence specials 3) | Stick Prod (+16 dmg) | Wind Gust (rank+10) | 6 | 4 | 5 | 5 | Invis Cloak (50% dodge) | Invisibility (Dodge 100%) | Evasion max Diamonds |
| 48 | Rugaru | 48 | 101 | 5 | 3 | Lunar Howl (All charges max + dmg +1 3 turns) | Moon Regen 13 | Werebite (Transform: +2 dmg 5 turns) | Wolf Maul (+19 dmg) | Moon Beam (rank*2.8) | 5 | 4 | 3 | 6 | Silver Fang (Anti-were +dmg) | Full Moon (Max Charges) | Moon phase Clubs |
| 49 | Batsquatch | 49 | 101 | 5 | 3 | Sonic Screech (Reset all enemy charges) | Echo Heal 13 | Bat Swarm (DoT 5x3) | Wing Slash (+18 dmg) | Sonic Wave (rank +10) | 6 | 3 | 5 | 5 | Bat Wing (Flight: Spades x2) | Sonic Boom (Stun Specials) | Disrupt sonic Spades |
| 50 | Mechanical Bigfoot | 50 | 103 | 5 | 3 | Overload (Deal 12 dmg, self 4 dmg) | Repair Heal 14 | Laser (rank*3.5) | Mech Punch (+20 dmg) | Missile (rank*3) | 5 | 4 | 6 | 5 | Cyber Chip (Auto charge 1/3) | Overclock (Double Damage) | Tech burst Diamonds |
| 51 | The Primal One | 51 | 103 | 5 | 3 | Primal Aura (All stats +1 for game) | Origin Heal 15 | Adaptive Gold (+1000) | Alpha Strike (+20 dmg) | Apex Throw (rank*3.2) | 5 | 5 | 4 | 6 | Primal Essence (All suits +1) | Evolution (+1 All Stats Permanent) | God tier balanced |
| 52 | Interdimensional Sasquatch | 52 | 104 | 5 | 3 | Portal Rift (Banish 5 enemy cards) | Void Heal 15 | Dimension Warp (Random teleport win) | Rift Claw (+21 dmg) | Portal Blast (rank +15) | 6 | 5 | 5 | 4 | Rift Key (Steal card random) | Rift (Banish 3 Cards) | Dimensional chaos Spades |
| 53 | The First Walker | 53 | 104 | 5 | 3 | Ancestral Recall (Undo last 5 turns) | Elder Heal 16 | Rune Curse (Perma DoT 1/turn) | Patriarch Fist (+22 dmg) | Origin Bolt (rank*4) | 5 | 3 | 6 | 5 | Rune Stone (Predict all cards) | Ancient Power (Full Heal) | Time master Diamonds |
| 54 | Cosmic Yeti | 54 | 104 | 5 | 3 | Nebula Explosion (15 direct dmg) | Star Heal 17 | Meteor Shower (DoT 6x4) | Cosmic Punch (+23 dmg) | Black Hole (rank*4.5 suck cards) | 6 | 4 | 5 | 5 | Cosmic Dust (Suits infinite charge) | Meteor (15 Dmg) | Space nuke Diamonds |
| 55 | Shadow Squatch | 55 | 105 | 5 | 3 | Shadow Merge (Copy all enemy buffs) | Dark Heal 18 | Abyss Fear (Enemy dmg 0 4 turns) | Shadow Tendril (+24 dmg) | Void Shot (rank dmg x3) | 5 | 2 | 6 | 5 | Shadow Veil (Invis + heal steal) | Blackout (Blind 2 Turns) | Shadow steal Diamonds |
| 56 | Golden Sasquatch | 56 | 105 | 5 | 3 | Midas Touch (Turn losses to wins x3) | Gold Heal 20 | Infinite Gold (+2000) | Golden Fist (+25 dmg) | Aurum Arrow (rank +20) | 6 | 3 | 5 | 6 | Gold Crown (Gold x3 rewards) | Jackpot (+1000 Gold) | Gold economy Diamonds |
| 57 | The Collective | 57 | 105 | 5 | 3 | Hive Swarm (Spawn 2 mini-wins) | Swarm Regen 20 | Insect Plague (DoT 10x2) | Mass Bite (+26 dmg) | Drone Strike (rank*5) | 5 | 4 | 3 | 6 | Hive Mind (Charge shared) | Swarm (DoT 2x5) | Swarm overwhelm Clubs |
| 58 | Primordial Terror | 58 | 107 | 5 | 3 | Chaos Mutate (Random extreme buff/debuff) | Terror Heal 25 | Mutation Curse (Random enemy debuff) | Tentacle Lash (+30 dmg) | Chaos Blast (rank*6) | 6 | 5 | 4 | 6 | Chaos Egg (Random power/game) | Chaos (Random Effect) | Ultimate RNG Clubs |
| 59 | The Bigfoot King | 59 | 120 | 5 | 3 | Royal Decree (Win game instantly on use) | Kingly Heal 30 | Treasury (+5000 Gold) | Imperial Smite (+50 dmg) | Crown Bolt (rank*10) | 5 | 5 | 5 | 5 | King's Scepter (All previous powers 1/use) | Decree (Win Turn + Max Charges) | Final boss omniscient, all suits max |

**Threshold Assignment Logic Recap**:
- **Base**: Lv1-10:2, 11-25:3, 26-40:4, 41+:5 (reduced by 1 from previous values for 36-card deck rebalance)
- **Primary Suit** (per AI/theme): base-1 (min 1-2 for playability)
- **Weak Suit** (opposite/least thematic): base+1 (max 6 for challenge)
- **Others**: base
- Ensures ~20-30% faster ready for focus suits, promoting Warlord picks & counterplay. Replays: +1 all thr. Overcharge: bonus potency. Streaks > raw wins.

**Notes on Balance and Progression:**
- **Stats Progression**: HP ramps from 80 to 120 for endurance challenges (rebalanced for 36-card decks - games end faster, so HP adjusted to maintain appropriate game length). Damage tiers up for punchier late-game. Charge decreases for frequent ultimates in endgame.
- **Specials**: Thematic to lore (e.g., poison for Skunk Ape, time for Sisimito). Hearts focus sustain/armor; Diamonds utility/Gold/Debuffs; Clubs raw physical burst (rank diff boosted); Spades consistent ranged (rank-based). Power scales ~level/5 for fairness.
- **Special Powers**: Powerful, charge-gated climaxes. Early: utility/sustain; Mid: control/disrupt; Late: game-warping (e.g., win condition). Charge on wins AND damage taken (pity mechanic). Resets only on use for comeback potential.
- **Battle Items**: Unlocked sequentially for player (purchase with Gold, 1 per level). Active items playable pre-turn to influence draws. **Level-Based Availability:** Battle Items are only available during the level they're unlocked. When advancing to a new level, player starts without Battle Items (unless unlocking a new one at that level). Charge system (1-3 charges per game, recharge after each game within same level) ensures Gold investment provides value during that level. Enemies also use Battle Items (assigned per Warlord roster, activated by AI pre-turn, 5% chance first play, 20% on replays). Counters themes (e.g., anti-poison vs. Skunk Ape). Helps vs. stronger foes (e.g., predict vs. RNG bosses).
- **Suit Chaining**: Passive combo system rewarding consecutive same-suit wins and poker-style patterns (Full House, Straight, Pair, Royal Flush, etc.). Chains persist across losses but reset on suit change, hidden until triggered, work for both player and enemies, can trigger multiple times per game. Unlocks progressively: Basic Burst (Level 1), Enhanced/Full House/Pair (Level 11), Mega/Three of a Kind/Straight (Level 26), Straight Flush/Four of a Kind (Level 31-36), Royal Flush (Level 41).
- **AI Strategies**: Varied for replayability—teaches counterplay (e.g., burst poison users fast, out-sustain tanks). Replays increase difficulty through stat scaling, improved AI decision-making, and increased Battle Item activation frequency (5% → 20% per turn). AI also tracks chains and triggers enemy chain bursts automatically.
- **Holistic Tuning**: Early: Learn basics (low stats, simple). Mid: Counters/items matter. Late: Power spikes require streaks/perfect play. Streaks/bonuses reward mastery. Tested mentally for ~45-60 min games, win rates ~60% with optimal play.

### Battle Items

Battle Items are active consumables that players can activate pre-turn to influence upcoming card draws. They provide agency during losing streaks when specials cannot be played (specials are post-win only).

#### Battle Item System Overview

**Purpose:**
- Provide player agency during losing streaks (when specials can't be played)
- Counter RNG variance by allowing strategic influence on draws
- Add strategic depth through pre-turn decision-making
- Create comeback opportunities when behind

**Acquisition:**
- Battle Items unlocked sequentially (1 per level)
- Purchased with Gold (100-3,000 Gold, varies by level)
- One-time purchase per item (unlock for that level only)
- **Level-Based Availability:** Battle Items are only available during the level they're unlocked. When a player advances from level 2 to level 3, they start level 3 without Battle Items (unless they unlock a new Battle Item at level 3)
- Owned items persist across games within the same level and recharge after each game
- Investment Value: Gold spent unlocks the item for use during that level; charges recharge each game within that level (encourages strategic use without fear of wasting investment)

**Activation:**
- Pre-turn only: Activated before card draw phase
- One item per turn: Player can activate one Battle Item per turn (enemy AI can also activate one per turn)
- **Level Restriction:** Battle Items can only be activated during the level they were unlocked. Items from previous levels are not available when advancing to a new level
- Recharge System: Battle Items recharge after each game within the same level (not permanently consumed)
- Charges per game: Each Battle Item has 1-3 charges per game (varies by item level/power)
- Available when losing: Can be used even when losing, providing comeback agency
- Enemy AI: Enemies evaluate and activate Battle Items pre-turn based on game state (HP, deck size, charge progress)

**Battle Item Effects:**
Battle Items influence the upcoming card draw in various ways:

- **Rank Boost:** Next card drawn gets +X rank (e.g., "+2 rank to next card")
- **Predict:** Reveals next card rank/suit before draw (e.g., "Predict next card")
- **Extra Draw:** Player draws 2 cards instead of 1 (highest rank wins)
- **Swap:** Swaps top card with a random card from deck
- **Auto Win:** Next turn automatically wins (rare, high-level items)
- **Other:** Various utility effects (e.g., "Shuffle deck", "Steal top enemy card")

**Battle Item Selection:**
- Battle Item button appears in Pre-Turn State (if player owns items with remaining charges for current level)
- Tap button → Battle Item Selection Overlay appears
- Overlay shows all owned Battle Items with remaining charges (only items for current level are shown)
- Each item displays: Icon, name, effect description, charges remaining (e.g., "2/3 charges")
- Player selects item → Item activates → Effect applies to next draw
- Charge consumed after use (charges remaining decreases, e.g., "1/3 charges")
- Items recharge to full charges after each game completes (within the same level)
- **Level Advancement:** When player advances to a new level, Battle Items from previous levels are no longer available. Player starts the new level without Battle Items unless they unlock a new one at that level

**Visual Feedback:**
- Active effect indicator on status banner (e.g., "Rank Boost Active: +2")
- Battle Item button glows when items with charges available
- Effect animation when item activates
- Charge counter updates after use (e.g., "2/3 charges" → "1/3 charges")
- Items grayed out when charges depleted (recharge after game)

**Balance:**
- Battle Items provide strategic influence but don't guarantee wins
- Rank boosts are limited (typically +1 to +3 rank)
- Predict effects may have accuracy limits (e.g., 80% accurate)
- High-level items more powerful but expensive
- Charge system (1-3 charges per game) encourages strategic use without fear of wasting investment
- Recharge after each game ensures items remain useful throughout progression
- Gold investment unlocks item permanently; charges provide ongoing value

*For UI specifications, see: `## UI and UX` → `### Battle Item Selection Overlay`*  
*For asset requirements, see: `## Content and Assets` → `### Battle Items`*

### Suit Chaining (Combo System)

The Suit Chaining system is a passive combo mechanic that rewards players (and enemies) when RNG favors them with consecutive same-suit wins or poker-style rank patterns. Chains persist across losses but reset on suit change, remain hidden until triggered, and can trigger multiple times per game.

#### Chain System Overview

**Purpose:**
- Reward favorable RNG streaks without guaranteeing wins
- Add excitement and variety to gameplay through surprise bursts
- Complement existing comeback mechanics (charge persistence)
- Provide additional strategic depth through poker-style pattern recognition
- Create memorable "wow" moments when rare chains trigger

**Core Principles:**
- **Passive System:** Chains build automatically, no player action required
- **Hidden Until Triggered:** Chain progress not visible until burst occurs (prevents gaming the system)
- **Persist Across Losses:** Chains do NOT reset on turn loss (unlike streaks)
- **Reset on Suit Change:** Suit chains reset when player wins with different suit
- **Multiple Triggers:** Chains can trigger multiple times per game (reset after trigger, can rebuild)
- **Enemy Chains:** Enemies also track chains (same mechanics, AI-triggered effects)

**Chain Types:**
- **Suit Chains:** Consecutive wins with same suit (3, 4, 5, 6+ wins)
- **Poker Chains:** Rank-based patterns (Pair, Two Pair, Three of a Kind, Four of a Kind, Straight, Straight Flush, Royal Flush)
- **Hybrid Chains:** Combination patterns (Full House, Alternating, Rainbow)

#### Basic Suit Chains (Levels 1-10)

**Basic Burst (3 consecutive wins with same suit):**
- **Hearts Burst:** Instant heal 5 HP
- **Diamonds Burst:** +50 Gold
- **Clubs Burst:** Instant 5 damage to opponent
- **Spades Burst:** +1 extra card draw next turn (draw 2 cards, highest wins)

**Chain Reset:** Resets to 0 after trigger (can rebuild and trigger again)

#### Intermediate Chains (Levels 11-25)

**Enhanced Burst (4 consecutive wins with same suit):**
- **Hearts:** Heal 8 HP
- **Diamonds:** +100 Gold
- **Clubs:** 8 damage
- **Spades:** +2 extra card draws next turn

**Full House Chain (3 of one suit + 2 of another within 5 turns):**
- Hearts-Hearts-Hearts-Clubs-Clubs: "Sustain Strike" - Heal 4 HP + 3 damage
- Diamonds-Diamonds-Diamonds-Spades-Spades: "Lucky Shot" - +75 Gold + 1 extra draw
- Clubs-Clubs-Clubs-Hearts-Hearts: "Berserker's Resolve" - 4 damage + Heal 2 HP
- Spades-Spades-Spades-Diamonds-Diamonds: "Tactical Advantage" - 1 extra draw + 50 Gold

**Pair Chain (2 wins with same rank within 3 turns):**
- Pair of Aces: "Royal Pair" - +100 Gold + Heal 3 HP
- Pair of Kings: "Noble Pair" - +50 Gold + 2 damage
- Pair of Queens/Jacks: "High Pair" - +25 Gold + 1 extra draw
- Pair of Low Cards (2-5): "Underdog Pair" - +25 Gold + 1 extra draw

**Alternating Chain (Pattern: A-B-A-B within 4 turns):**
- Hearts-Diamonds-Hearts-Diamonds: "Harmony Burst" - Heal 3 HP + 25 Gold
- Clubs-Spades-Clubs-Spades: "Combat Burst" - 4 damage + 1 extra draw

#### Advanced Chains (Levels 26-40)

**Mega Burst / Flush Chain (5 consecutive wins with same suit):**
- **Hearts:** Heal 12 HP + Armor 2 for 3 turns
- **Diamonds:** +200 Gold + Predict next card
- **Clubs:** 12 damage + Damage +1 for 2 turns
- **Spades:** +3 extra draws + Rank boost +2 next turn

**Three of a Kind Chain (3 wins with same rank within 4 turns):**
- Three Aces: "Triple Crown" - +200 Gold + Heal 5 HP + 3 damage
- Three Kings: "Triple Nobles" - +100 Gold + Heal 3 HP + 2 damage
- Three Low Cards: "Triple Threat" - 5 damage + 1 extra draw + 25 Gold

**Straight Chain (5 consecutive rank wins within 5 turns):**
- Low Straight (2-3-4-5-6): "Rising Power" - Damage +2 for 3 turns + Heal 2 HP
- High Straight (8-9-10-J-Q): "Peak Performance" - All suit charges +1, Heal 3 HP + 50 Gold
- Any Straight: Moderate bonus effects (scaled by straight type)

**Rainbow Chain (All 4 suits within 6 turns, any order):**
- "Rainbow Burst" - Heal 5 HP + 50 Gold + 3 damage + 1 extra draw

**Two Pair Chain (Two different ranks, each won twice within 6 turns):**
- High Two Pair (Aces + Kings): "Double Royal" - +200 Gold + Heal 5 HP + 5 damage
- Mixed Two Pair: Moderate combined effects based on ranks

#### Expert Chains (Levels 41+)

**Perfect Chain / Straight Flush (5 same suit + consecutive ranks within 5 turns):**
- Hearts Straight Flush: "Royal Hearts" - Heal 15 HP + Armor 3 for 5 turns
- Clubs Straight Flush: "Royal Clubs" - 15 damage + Damage +2 for 3 turns
- Diamonds Straight Flush: "Royal Diamonds" - +500 Gold + Predict next 3 cards
- Spades Straight Flush: "Royal Spades" - +5 extra draws + Rank boost +3 for 2 turns

**Royal Flush Chain (Ace-King-Queen-Jack-10 all same suit within 5 turns):**
- Ultimate effect: "ROYAL FLUSH!" - Game-changing burst:
  - **Hearts:** Full heal + Max HP +5 for game + Armor 5 for 5 turns
  - **Diamonds:** +1000 Gold + All charges max + Predict all cards for 3 turns
  - **Clubs:** 20 damage + Damage +3 for 5 turns + Ignore armor for 3 turns
  - **Spades:** +10 extra draws + All cards get +3 rank boost for 3 turns + Extra turn

**Four of a Kind Chain (4 wins with same rank within 5 turns):**
- Four Aces: "Quad Aces" - Instant win condition (enemy HP -50%) + Massive Gold bonus
- Four Kings: "Quad Kings" - Enemy HP -30% + 500 Gold + Heal 8 HP
- Four Low Cards: "Quad Underdogs" - Massive comeback (Heal 10 HP + 10 damage + 3 extra draws + 100 Gold)

**Suit Mastery (6+ consecutive wins with same suit):**
- Ultimate Burst effects (scaled up from Mega Burst)
- Each additional win beyond 6 increases effect potency

#### Challenge-Specific Chain Modifiers

When certain challenges are active, chains receive modifiers:

- **"Win 10 Hearts turns" challenge:** Hearts chains trigger more easily (2 wins instead of 3)
- **"Use 20 specials" challenge:** Chains also charge suit specials faster (+1 charge per chain trigger)
- **"Deal 100 damage" challenge:** Clubs chains deal bonus damage (+2 damage per Clubs burst)
- **"Complete a Full House chain" challenge:** Full House chains unlock early (Level 8 instead of 11)
- **"Trigger a Royal Flush" challenge:** Royal Flush chains unlock at lower level (Level 35 instead of 41)
- **"Complete a Straight" challenge:** Straight chains unlock early (Level 18 instead of 21)

#### Chain Detection Logic

**Suit Chain Tracking:**
- Track winning suit on each turn win
- If same suit as previous win: Increment suit chain counter
- If different suit: Reset suit chain counter to 1 (new suit chain starts)
- If turn loss: Suit chain persists (does NOT reset)
- Check thresholds after each win (3, 4, 5, 6+ wins)

**Rank Chain Tracking:**
- Track winning rank on each turn win
- Maintain rank history (last 6 ranks won)
- Detect patterns:
  - **Pair:** Same rank appears twice within last 3 turns
  - **Two Pair:** Two different ranks each appear twice within last 6 turns
  - **Three of a Kind:** Same rank appears three times within last 4 turns
  - **Four of a Kind:** Same rank appears four times within last 5 turns
  - **Straight:** Five consecutive ranks within last 5 turns (2-3-4-5-6 or 8-9-10-J-Q)
  - **Straight Flush:** Straight + all same suit within last 5 turns
  - **Royal Flush:** Ace-King-Queen-Jack-10 all same suit within last 5 turns

**Hybrid Chain Detection:**
- **Full House:** Track suit history (last 5 suits) - detect 3 of one + 2 of another
- **Alternating:** Track suit pattern (last 4 suits) - detect A-B-A-B pattern
- **Rainbow:** Track suit history (last 6 suits) - detect all 4 suits present

**Chain Priority:**
- Check poker chains first (higher rarity = higher priority)
- Then check suit chains
- Only one chain triggers per turn (highest priority chain wins)
- Chain resets after trigger (can rebuild and trigger again)

#### Enemy Chain System

**Enemy Chain Tracking:**
- Enemies track chains using same mechanics as player
- AI evaluates chain potential when deciding card play (low priority, doesn't override optimal play)
- Enemy chains trigger automatically when thresholds reached
- Enemy chain notifications appear briefly (similar to enemy specials)
- Enemy chains add variety and challenge to gameplay

**Enemy Chain Effects:**
- Same effects as player chains
- Visual notification: "[Enemy] [Chain Type] BURST!" message
- Brief animation and sound effect
- Effects apply immediately (damage, debuffs, etc.)

*For turn flow integration, see: `## Game Flows` → `### Main Game Flow`*  
*For visual specifications, see: `## UI and UX` → `### Chain Burst Animations`*  
*For challenge integration, see: `## Progression and Rewards` → `### Challenges`*

### Charms System

The Charms system allows players to customize and influence the "Chain" mechanic logic. Unlike Battle Items (which affect immediate turns), Charms are passive equipment that alter the rules of pattern recognition, allowing for deeper strategies and mitigating RNG frustration in the late game.

#### Core Mechanics

**Slot System:**
- **Slots:** Players start with 1 Charm Slot. Unlocks a 2nd slot at Player Level 25.
- **Equip Phase:** Charms are equipped in the "Loadout" screen before a battle (alongside Warlords).
- **Durability:** Charms are fragile artifacts. Most have **Durability** (number of triggers) or are **Consumable** (lasts 1 match).
- **Purchase:** Bought with Gold in the Shop. High-tier Charms may require specific Achievements to unlock.

**Rule Alterations:**
Charms modify the `ChainSystem` logic in three primary ways:

1.  **Memory Reach (Buffer Extension):**
    - *Standard Rule:* Poker Chains check the last 5 wins.
    - *Charm Modifier:* Extends the "lookback buffer" to 7 or 10 wins.
    - *Effect:* Allows patterns (Straight, Flush) to be formed from a larger pool of recent wins, ignoring "noise" cards in between.

2.  **Reset Protection (Chain Bridging):**
    - *Standard Rule:* Winning with a different suit resets the current Suit Chain to 1.
    - *Charm Modifier:* Prevents reset on X off-suit wins.
    - *Effect:* "Pauses" the chain count instead of resetting it. Visual feedback: "Chain Anchored!"

3.  **Wildcard Logic (Suit/Rank Bridging):**
    - *Standard Rule:* Exact matches required.
    - *Charm Modifier:* Treats specific conditions as valid matches.
    - *Effect:* e.g., Red suits (Hearts/Diamonds) count as the same suit for chains.

#### Charm Archetypes

| Charm Name | Cost | Durability | Effect | Mechanic Altered |
| :--- | :--- | :--- | :--- | :--- |
| **Fool's Gold** | 250g | 3 Triggers | A loss counts as a "Wild" suit win for your current chain (Max 3 times/game). | **Extension** (Turns loss into progress) |
| **Timekeeper's Eye** | 500g | 1 Game | Poker Chains check the last **10 wins** instead of 5 for the entire match. | **Memory** (Buffer Extension) |
| **Red Ribbon** | 400g | 1 Trigger | Hearts & Diamonds (Red) count as the same suit for chains. Breaks after 1 Chain Trigger. | **Reset Rule** (Color Bridging) |
| **Black Ribbon** | 400g | 1 Trigger | Spades & Clubs (Black) count as the same suit for chains. Breaks after 1 Chain Trigger. | **Reset Rule** (Color Bridging) |
| **Anchor Stone** | 300g | 1 Use | Prevents a Suit Chain from resetting on a suit change. | **Reset Rule** (Safety Net) |
| **Echo Shell** | 600g | 3 Uses | Your last triggered Chain "echoes", counting as the start (level 1) of your next chain immediately. | **Momentum** (Kickstarter) |

#### Data Structure

```typescript
interface Charm {
  id: string;
  name: string;
  type: 'memory_extend' | 'reset_protect' | 'suit_bridge' | 'loss_convert' | 'momentum';
  value: number; // Magnitude of effect (e.g., +5 memory, 1 protected reset)
  durability: number; // Remaining uses in current game
  cost: number;
}

interface ChainState {
  // ... existing chain state ...
  activeCharms: Charm[];
  historyBuffer: Card[]; // Extended buffer for memory charms
}
```

### Specials and Status Effects

This section details all special abilities, status effects, and special mechanics that modify gameplay. Specials are abilities that Warlords can use after winning turns, while status effects are temporary or permanent modifications to gameplay state.

#### Specials System Overview

**When Specials Can Be Played:**
- Post-win only: Specials can only be played by the turn winner
- Timing: After card capture, before next turn begins
- Limit: Winner may play 0-2 specials per turn (mix of suit specials and/or Warlord Power)

**Suit-Based Specials:**
- Four specials per Warlord: Hearts, Diamonds, Clubs, Spades
- Charge mechanism: Ready when X cards of that suit are captured
- Charge threshold: Varies by Warlord and suit (typically 1-6 cards, reduced by 1 from previous 2-7 range to account for smaller capture pools with 36-card decks)
- Charge progress: Tracks cards captured since last use
- Charge reset: Only when special is used (charges reset to 0 after activation)
- Overcharge: Charges can exceed threshold for bonus potency
- **Comeback Mechanic**: Suit charges persist through losses, allowing players to build up counter-attacks even when behind

**Warlord Special Power:**
- One unique power per Warlord
- Charge mechanism: Charges on wins AND on taking damage (pity mechanic)
- Charge threshold: Varies by Warlord (typically 3-7 wins OR 5-10 damage taken)
- Charge progress: Tracks wins and damage taken since last reset
- Charge reset: Only after use (charges reset to 0 after activation)
- **Comeback Mechanic**: Taking damage builds charge, giving losing players a path to their ultimate ability
- More powerful than suit specials; strategic climax abilities

**Specials Display:**
- Player: Inline special icons on main board show all 5 specials (4 suit icons + 1 Warlord Power icon)
- Ready specials: Icons glow with pulsing animation (color matches suit), tappable to activate
- Unready specials: Icons dimmed, show charge progress on tap (tooltip: "3/4 Hearts captured")
- Player can tap ready special icons before "Next Turn" to activate (0-2 specials per turn)
- Enemy: AI evaluates ready specials and plays highest-scoring (0-2 per turn)

*For UX flow details, see: `## Game Flows` → `### Main Game Flow`*  
*For UI specifications, see: `## UI and UX` → `### Inline Specials Icons Details`*

#### Status Effects

Status effects are temporary or permanent modifications to gameplay state applied by specials.

**DoT (Damage Over Time):**
- Deals damage at the start of each of the affected player's turns
- DoT effects stack (multiple DoT sources deal damage independently)
- DoT persists for the specified number of turns and counts down each turn
- DoT damage bypasses armor but is affected by invulnerable
- Example: "Poison DoT (1 dmg x5)" deals 1 damage at the start of each turn for 5 turns

**Armor:**
- Reduces incoming damage by the specified amount
- Types:
  - **Next damage:** Reduces the next single instance of damage, then expires
  - **Next X turns:** Reduces all damage for X turns, expires after X turns complete
  - **Passive:** Always active, reduces all incoming damage permanently
- Armor stacks additively (Armor 2 + Armor 3 = Armor 5 total reduction)
- Armor cannot reduce damage below 0
- Armor applies before invulnerable checks

**Invulnerable/Invuln:**
- Prevents all damage (including DoT) for the specified duration
- Types:
  - **1 turn:** Prevents all damage during the next turn only
  - **X turns:** Prevents all damage for X turns
  - **1/game:** Can be used once per game, prevents all damage for 1 turn
- Invulnerable does NOT prevent card capture (you can still lose cards)
- Invulnerable takes precedence over armor (if invulnerable, armor doesn't matter)
- Multiple invulnerable effects don't stack (you're either invulnerable or not)

**Dodge:**
- Chance-based damage avoidance
- Types:
  - **Percentage chance:** Each instance of damage has X% chance to be dodged (e.g., 10% dodge = 10% chance each hit)
  - **Guaranteed:** "Dodge all dmg 1 turn" = 100% dodge for 1 turn
- Dodge prevents damage but does NOT prevent card capture
- Dodge is calculated per damage instance (each hit rolls separately)
- Dodge stacks multiplicatively (10% + 10% = 19% total, not 20%)

**Blind:**
- Forces the affected player to play cards randomly
- Enemy AI selects cards randomly instead of using strategy
- Player cannot see card ranks before playing (cards revealed simultaneously)
- Blind persists for the specified number of turns
- Blind does NOT affect special selection (specials can still be chosen normally)

**Confuse:**
- Forces random special selection
- Enemy AI selects specials randomly instead of using scoring heuristic
- Player's special selection is randomized (if player is confused)
- Confuse persists for the specified number of turns
- Confuse does NOT affect card draws (cards still drawn normally)

**Silence:**
- Prevents special usage
- Cannot play suit specials or Warlord Power
- Charges continue to accumulate but specials cannot be activated
- Silence persists for the specified number of turns
- Multiple silence effects stack (longest duration applies)

**Transform:**
- Temporarily changes Warlord stats or abilities
- Modify base stats (damage, HP, etc.) for the duration
- Stack additively with other stat modifiers
- Persist for the specified number of turns
- Can be removed by certain specials (if specified)

#### Turn Manipulation

**Extra Turn:**
- Grants an additional turn immediately after the current turn completes
- Occurs before the enemy's next turn
- Player draws and plays normally during extra turn
- Enemy does not draw during extra turn
- Multiple extra turns stack (player gets multiple consecutive turns)
- Extra turn does NOT reset charges or cooldowns

**Skip Turn:**
- Forces the enemy to skip their next turn
- Enemy does not draw cards
- Enemy does not deal damage
- Enemy does not capture cards
- Player's turn proceeds normally after skip
- Skip turn does NOT prevent enemy from using specials (if they have any ready)

**Steal Turn:**
- Player takes control of enemy's next turn
- Player draws from enemy deck (temporarily)
- Player plays enemy's turn as if it were their own
- Enemy does not get a turn this cycle
- Cards captured go to player's deck
- Steal turn does NOT transfer specials or charges

#### Damage Types

**Direct Damage:**
- Damage that bypasses normal damage calculation
- Deals a fixed amount regardless of card rank
- Bypasses armor (unless specified otherwise)
- Still affected by invulnerable and dodge
- Does NOT trigger card capture (damage only, no cards involved)
- Example: "Deal 4 direct dmg" = 4 damage regardless of cards

**Ignore Armor:**
- Damage that bypasses armor reduction
- Still respects invulnerable and dodge
- Still uses normal damage calculation (base + rank bonus)
- Only bypasses armor, not other damage reduction
- Example: "rank dmg ignore armor" = normal damage calculation but armor doesn't apply

**Crit (Critical Hit):**
- Damage multiplier on successful hit
- Percentage chance to trigger (e.g., 10% crit = 10% chance)
- When triggered, multiplies damage by 2x (unless specified otherwise)
- Calculated after all other damage modifiers
- Can stack with other damage multipliers
- Example: "Clubs crit 15%" = 15% chance Clubs specials deal 2x damage

#### Card Effects

**Reshuffle:**
- Shuffles the player's deck
- Occurs immediately when triggered
- Affects all cards in deck (not cards in play or captured)
- Randomizes deck order completely
- Does NOT affect cards currently on the table
- Can be triggered multiple times per game

**Extra Draw:**
- Grants an additional card draw
- Occurs on the next turn (not immediately)
- Player draws 2 cards instead of 1 on next turn
- Both cards are played simultaneously (highest rank wins)
- If both cards are same rank, triggers War normally
- Multiple extra draws stack (draw 3+ cards if multiple effects)

**Random Card:**
- Forces random card selection
- Enemy AI selects card randomly from deck (not strategically)
- Player cannot choose which card to play (if affected)
- Random selection happens at draw time
- Does NOT affect card ranks (cards still have normal ranks)

**Predict Card:**
- Reveals upcoming card information
- Shows the next card that will be drawn (rank and suit)
- Player can see this information before drawing
- Enemy AI can use prediction in decision-making
- Prediction accuracy varies (some are 100%, others are percentage-based)
- Example: "Predict next card 20%" = 20% chance to see next card correctly

**Swap Cards:**
- Exchanges cards between players
- Swaps the cards currently on the table (in play)
- If no cards in play, swaps top cards from each deck
- Cards maintain their ranks and suits
- After swap, cards are compared normally
- Swap happens before rank comparison

**Auto Loss:**
- Forces automatic turn loss
- Enemy automatically loses the next turn regardless of card ranks
- Enemy does not draw cards
- Player wins the turn automatically
- Cards are captured normally (player gets both cards)
- Auto loss does NOT prevent enemy from using specials (if ready)

#### Special Effects

**Copy:**
- Duplicates enemy specials or buffs
- **Copy Special:** Gains one-time use of the copied special (uses your charges, not enemy's)
- **Copy Buffs:** Gains all active buffs from enemy (armor, damage boosts, etc.)
- **Copy Power:** Gains the enemy's Warlord Power for one use
- Copied effects last for one use unless specified otherwise
- Cannot copy passive effects (only active abilities)

**Reset Charges:**
- Sets charge progress to 0
- **Full Reset:** All charges (suit + Warlord) reset to 0
- **Enemy Reset:** Only enemy charges reset to 0
- **Specific Reset:** Only specified charges reset
- Charges cannot go negative (minimum is 0)
- Reset does NOT affect charges that are already ready (ready specials remain ready)

**Undo/Rewind:**
- Reverses previous game state
- **Rewind Last Loss:** Reverses the last turn you lost (restores HP, cards, charges)
- **Undo Last X Turns:** Reverses the last X turns completely
- Restores HP, card positions, charges, and buffs/debuffs
- Does NOT restore Gold or XP rewards
- Cannot undo beyond the start of the current game

**Swap Positions:**
- Exchanges game positions
- Swaps HP values (if one player has more HP, they swap)
- Swaps deck sizes (if one player has more cards, they swap)
- Does NOT swap cards themselves (cards stay in their decks)
- Does NOT swap charges or buffs
- Visual effect: Avatars swap screen positions

#### Passive Effects

**Passive Healing:**
- Automatic HP restoration each turn
- Triggers at the start of each turn (before card draw)
- Heals the specified amount
- Cannot overheal (HP cannot exceed max HP)
- Stacks additively (multiple passive heals add together)
- Example: "+1 HP/turn" = gain 1 HP at start of each turn

**Passive Armor:**
- Permanent damage reduction
- Always active (no duration)
- Reduces all incoming damage by the specified amount
- Stacks additively with active armor
- Cannot reduce damage below 0
- Example: "Armor 1 passive" = always reduce damage by 1

**Passive Stat Boosts:**
- Permanent stat modifications
- Modify base stats for the duration of the game
- Stack additively (multiple boosts add together)
- Affect damage calculation, HP, or other stats
- Cannot be removed (persist until game ends)
- Example: "Damage +1" = add 1 to base damage calculation

#### Edge Cases

**Lose Max HP:**
- Reduces maximum HP
- Reduces both current and maximum HP
- If current HP exceeds new max, current HP is reduced to new max
- Max HP cannot go below 1
- Effect is permanent for the duration of the game
- Example: "Heal 3 (lose 1 max HP)" = heal 3 HP but reduce max HP by 1

**Charge Modifiers:**
- Alters charge accumulation
- **Enemy charge +X:** Enemy needs X more charges to ready specials
- **Double wins count:** Wins count as 2x for charge purposes
- **Charge -1:** Reduces charge threshold by 1
- **Charge faster:** Reduces charge threshold by percentage
- Modifiers stack additively
- Charges cannot go negative (minimum threshold is 1)

**Gold Stealing:**
- Takes Gold rewards from enemy
- Steals the next Gold reward the enemy would receive
- Player receives the stolen Gold instead
- Enemy does NOT receive Gold for that reward
- Only affects Gold, not XP
- Example: "Steal next Gold reward" = next time enemy would get Gold, player gets it instead

**Win Condition Modifiers:**
- Alters win conditions
- **Win game instantly:** Immediately ends game in player's favor (bypasses all other conditions)
- **Turn losses to wins:** Converts the last X losses into wins (restores HP, reverses card captures)
- These effects are extremely powerful and rare
- Instant win cannot be prevented by any other effect
- Turn conversion affects game state retroactively

#### Status Effect Stacking and Priority

**Stacking Rules:**
- DoT effects stack (multiple sources deal damage independently)
- Armor stacks additively
- Passive effects stack additively
- Stat boosts stack additively
- Invulnerable does NOT stack (you're either invulnerable or not)
- Dodge stacks multiplicatively (not additively)

**Priority Order (when multiple effects apply):**
1. Invulnerable (prevents all damage)
2. Dodge (chance to avoid damage)
3. Armor (reduces damage)
4. Normal damage calculation
5. DoT (applies after turn damage)

**Duration Tracking:**
- All status effects track duration in turns
- Effects expire at the start of the affected player's turn
- "Next turn" effects expire after the next turn completes
- "X turns" effects count down each turn
- Passive effects have no duration (persist until game ends)

#### Card Manipulation Mechanics

Some specials manipulate cards between decks. These mechanics work as follows:

**Steal:**
- Cards are moved from enemy deck to your deck
- Stolen cards can be recaptured normally if the enemy wins them back during a turn
- Cards go to bottom of your deck when stolen

**Bury:**
- Cards are moved from enemy deck to your deck AND marked to always return to your deck
- Even if the enemy wins a buried card during a game turn, it still goes back to your deck (not the enemy's)
- Bury effect persists for the duration of the game
- Cards go to bottom of your deck when buried

**Banish:**
- Cards are moved from enemy deck to your deck AND permanently locked to your deck
- Banished cards will never leave your deck
- If you play a banished card and lose the turn, the banished card returns to your deck and the next card in your deck is played instead (you don't lose the banished card)
- Banish effect persists for the duration of the game
- Cards go to bottom of your deck when banished

**Note:** All card manipulation (steal/bury/banish) moves cards to the bottom of the manipulating player's deck. Cards are never removed from play entirely; they remain in one deck or the other for the duration of the game.

*For detailed card manipulation implementation, see: `### Decks and Cards` → `#### Card Manipulation`*

### Enemies and AI

**Enemy AI System Design**

To support 59 distinct Warlords with unique powers, the AI uses a **Utility-Based Scoring System** rather than simple static rules. This allows enemies to behave "intelligently" according to their defined archetype (e.g., Aggressive, Defensive, Chaos) without complex machine learning.

**AI Architecture:**
1.  **State Evaluation**: The AI analyzes the current board state (HP, Deck Size, Charges, Active Effects).
2.  **Move Generation**: Identifies all legal moves (Play Special, Play Signature, Use Battle Item).
3.  **Simulation (1-Turn Lookahead)**: Calculates the immediate *projected impact* of each move (e.g., "If I Heal, I gain X HP. If I Attack, Enemy loses Y HP").
4.  **Scoring (Utility)**: Assigns a score to each move based on the Warlord's personality weights and the urgency of the situation.
5.  **Selection**: Executes the highest-scoring move (with weighted randomness to prevent predictability).

**Utility Factors & Scoring:**

The AI calculates a `Utility Score` for each action:
`Score = (Base Impact * Archetype Weight) + Situational Bonus`

| Factor | Description | Evaluation Logic |
|---|---|---|
| **Survival (HP)** | Value of staying alive | Score increases exponentially as AI HP drops < 40%. Zero value if at Max HP. |
| **Aggression (Dmg)** | Value of hurting player | Score scales with Base Damage. Bonus if Enemy HP is low (Execute range). |
| **Economy (Res)** | Value of cards/gold/charges | Score based on resource gain. High priority if AI Deck Size < Player Deck Size. |
| **Disruption** | Value of debuffs/control | Score based on impact duration. Bonus if Player has active buffs or high charges. |
| **Efficiency** | Value of using resources | Penalty for "Overkill" (e.g., dealing 10 dmg to 2 HP enemy). Bonus for using maxed charges. |

**Simulation Logic (Lookahead):**
- **Damage**: Calculates total damage (Direct + DoT duration).
- **Healing**: Calculates effective healing (capped at Max HP).
- **Buffs/Debuffs**: Estimates "value over time" (e.g., "Armor 2 for 3 turns" = potential 6 prevented damage).
- **RNG Mitigation**: Assumes "Average Case" for random effects (e.g., "Steal 1 Card" = Value of avg card rank).
- **Signature Cards**: Treated as "Ultimate" moves with very high base scores (100+), prioritized for swinging momentum or finishing games.

**Warlord Archetypes (Weights):**
Each Warlord is assigned an archetype that modifies their scoring logic:

| Archetype | Focus | Wt: Heal | Wt: Dmg | Wt: Control | Behavior |
|---|---|---|---|---|---|
| **Berserker** | All-in Aggression | 0.5x | 2.0x | 0.5x | Ignores self-damage, prioritizes kills. |
| **Guardian** | Survival/Sustain | 2.0x | 0.8x | 1.0x | Keeps HP high, turtles with Armor. |
| **Trickster** | Disruption/Chaos | 0.8x | 0.8x | 2.0x | Prioritizes Steals, Swaps, and Debuffs. |
| **Tactician** | Efficiency/Balance | 1.2x | 1.2x | 1.2x | Balanced play, maximizes charge value. |
| **Chaos** | Randomness | 1.0x | 1.0x | 1.0x | High randomness factor (+/- 30% score). |

**Battle Item AI:**
- **Trigger:** Pre-turn phase.
- **Logic:** AI checks if `Player Advantage > Threshold` (e.g., Player HP > AI HP + 20).
- **Probability:**
  - **First Play:** 5% base chance (simulate "unprepared").
  - **Replay:** 20% base chance (simulate "learning").
- **Selection:** Picks item that best counters current deficit (e.g., Heal Item if low HP, Dmg Item if high HP).

**Difficulty Scaling:**
- **Normal Mode**: Standard weights, no Battle Items (unless scripted), small random error in scoring (-10% to +10%).
- **Replay Mode (Hard)**: Optimized weights (Tactician-leaning), Battle Items enabled (20%), minimal random error. Lookahead accounts for Player's *potential* moves (e.g., "Player has max charges, expect incoming damage").

**Implementation Note:**
The AI evaluation function runs in `< 5ms` (pure JS math). It evaluates ~5-10 possible actions per turn (Specials, Sig, Item). No complex tree search is required.

**Balance Impact**
- **Base RNG**: 50%.
- **Smart AI**: Enemies win 55-65% suboptimal play; player mastery (pick counters, streaks) flips to 60%+.
- **Feels alive**: "Skunk Ape poisons early!", "Yeti avalanches at low HP!"

This scales progression: Early Warlords simple, late-game "personalities" demand strategy.

### Game Economies

This section defines all economic systems in the game: Gold currency, XP progression, monetization models, and how these systems interact to create balanced player progression and sustainable monetization.

#### Economic Systems Overview

The game features three primary economic systems:

1. **Gold Economy**: Primary currency for game attempts and Battle Item purchases
2. **XP Economy**: Progression currency for level advancement and content unlocks
3. **Monetization Economy**: F2P ads, IAP purchases, and PAID account upgrades

These systems work together to create:
- **Progression Pacing**: Balanced advancement through 59 levels
- **Monetization Opportunities**: Natural scarcity moments that encourage optional spending
- **Player Retention**: Daily engagement hooks and long-term goals
- **Fair Play**: All content unlockable through gameplay (no pay-to-win)

#### Gold Economy

**Gold** is the primary currency used for game attempts and Battle Item purchases. Players earn Gold through gameplay, ads, and optional purchases.

##### Gold Earning Sources

**Turn Win Gold:**
- Base Gold: 10 Gold per turn win (constant across all levels)
- Rank Bonus:
  - Ace: +2 Gold
  - King/Queen/Jack: +1 Gold
  - Number cards 8-10: +0.5 Gold (rounded down)
  - Number cards 2-7: +0 Gold
- Streak Multiplier (applied after base + rank bonus):
  - 3+ consecutive wins: 1.5x multiplier
  - 5+ consecutive wins: 2x multiplier
  - 10+ consecutive wins: 2.5x multiplier
- Examples:
  - Ace win (no streak): 10 + 2 = 12 Gold
  - King win (5-win streak): (10 + 1) × 2 = 22 Gold
  - Ace win (10+ streak): (10 + 2) × 2.5 = 30 Gold (maximum turn Gold)

**Game Win Gold:**
- Completion Bonus: +50 Gold for winning the game
- First-Time Defeat Bonus: +100 Gold for defeating Enemy Warlord for the first time
- Streak Completion Bonus: Multiply completion bonus by streak multiplier
- Examples:
  - First-time win (no streak): 50 + 100 = 150 Gold
  - First-time win (5-win streak): (50 + 100) × 2 = 300 Gold
  - Repeat win (10+ streak): 50 × 2.5 = 125 Gold

**Level-Up Gold:**
- Bonus Gold: 50 Gold × new level
- Examples:
  - Level 2: 50 × 2 = 100 Gold
  - Level 5: 50 × 5 = 250 Gold
  - Level 10: 50 × 10 = 500 Gold

**Daily Login Bonus:**
- Daily Bonus: 100 Gold + 50 XP (first login of the day)
- Resets: 24 hours after last login
- Display: Notification overlay on app launch

**Advertising Gold (F2P Players):**
- AdMob Rewarded Video: 25-100 Gold (randomized, displayed before ad)
- AdMob Interstitial: 10-50 Gold (randomized, displayed before ad)
- Daily Ad Bonus: +50 Gold (first ad of the day)
- Maximum per day: ~500 Gold from ads (soft cap to prevent abuse)
- Placement:
  - Post-game: "Earn Extra Gold" button (unlimited)
  - Pre-game: "Watch Ad for Gold" button (when Gold insufficient)
  - Interstitial: Every 3-5 games (skippable after 5 seconds)

**PAID Account Gold:**
- Automatic Gold: Matches ad-based rewards automatically (no ads required)
- Same amounts as F2P ad rewards (25-100 Gold per "ad slot")
- Can still watch ads for additional Gold (optional)
- Benefits: No ad interruptions, same Gold income

**IAP Gold Packages:**
- Small Pack: $0.99 = 500 Gold (baseline rate)
- Medium Pack: $2.99 = 1,750 Gold (17% bonus vs baseline)
- Large Pack: $4.99 = 3,500 Gold (40% bonus vs baseline)
- Mega Pack: $9.99 = 8,000 Gold (60% bonus vs baseline)
- Purchase Points:
  - Post-game: "Purchase Gold" button (always available)
  - Pre-game: If insufficient Gold for game fee
  - Battle Item Shop: If insufficient Gold for item purchase
  - Low Gold Warning: If Gold < 50, show upgrade prompt

##### Gold Spending Sinks

**Game Attempt Fees:**
- First 3 attempts per Enemy Warlord: Free (no Gold cost)
- Subsequent attempts: 25 Gold per attempt (constant across all levels)
- Fee displayed before game starts (if applicable)
- "Insufficient Gold" warning if player lacks funds
- Rationale: Encourages strategic play and creates natural scarcity after initial attempts

**Battle Items:**
- Cost varies by item level and power:
  - Level 1-10 items: 100-300 Gold
  - Level 11-25 items: 300-750 Gold
  - Level 26-40 items: 750-1,500 Gold
  - Level 41+ items: 1,500-3,000 Gold
- One-time purchase per item (permanent unlock)
- Items provide strategic advantages but are not required to progress

##### Gold Economy Balance

**Earning Rates:**
- Average turn win: ~12-15 Gold (with rank bonuses)
- Average game (10-15 turns): ~120-200 Gold earned
- Average game win bonus: ~150-300 Gold (first-time) or ~50-125 Gold (repeat)
- Average level-up bonus: ~250-500 Gold (mid-levels)
- Daily login bonus: 100 Gold
- Daily ad potential: ~500 Gold (F2P) or automatic equivalent (PAID)

**Spending Rates:**
- Game attempts: 0 Gold (first 3) or 25 Gold (subsequent)
- Battle Items: 100-3,000 Gold (one-time purchases)

**Net Gold Flow:**
- Average game: ~100-200 Gold earned (with bonuses)
- Average game cost: 0-25 Gold (first 3 attempts free)
- Net Gold per game: ~75-200 Gold (positive economy)
- Battle Items: Require 2-5 games to afford (encourages replay)
- Daily play: ~300-500 Gold net (with ads/login bonus)

**Economic Pacing:**
- Early game: Generous Gold flow (many free attempts, frequent level-ups)
- Mid game: Balanced flow (some paid attempts, occasional Battle Items)
- Late game: Strategic spending (higher Battle Item costs, more paid attempts)

**Scarcity Moments:**
- After 3 free attempts per Enemy Warlord (natural paywall)
- When purchasing Battle Items (strategic spending)
- When low on Gold (<50 Gold) (upgrade/IAP prompts)

##### Gold Display and Feedback

**UI Display:**
- Pre-game: Gold shown in Warlord selection screens (top-left corner)
- Post-game: Gold total displayed on results screen
- Menu: Gold shown in Game Menu overlay
- In-game: Gold NOT displayed (keeps UI minimal)

**Notifications:**
- Low Balance Warning: If Gold < 50, show warning when attempting paid game
- Gold Gain Popup: "+X Gold" animation on turn/game win (fades after 2 seconds)
- Sound: Brief chiptune chime for Gold gain (different pitch from XP)
- Insufficient Gold: Warning overlay when attempting paid game without funds

#### XP Economy

**XP** (Experience Points) is the progression currency used to advance through levels and unlock new content. Players earn XP through turn wins, game wins, and daily bonuses.

##### XP Earning Sources

**Turn Win XP:**
- Base XP: 5 XP per turn win (constant across all levels)
- Rank Bonus:
  - Ace: +1 XP
  - King/Queen/Jack: +0.5 XP (rounded down)
  - Number cards 8-10: +0.25 XP (rounded down)
  - Number cards 2-7: +0 XP
- Streak Multiplier (applied after base + rank bonus):
  - 3+ consecutive wins: 1.5x multiplier
  - 5+ consecutive wins: 2x multiplier
  - 10+ consecutive wins: 2.5x multiplier
- Examples:
  - Ace win (no streak): 5 + 1 = 6 XP
  - King win (no streak): 5 + 0.5 = 5 XP
  - Ace win (5-win streak): (5 + 1) × 2 = 12 XP
  - Ace win (10+ streak): (5 + 1) × 2.5 = 15 XP (maximum turn XP)

**Game Win XP:**
- Completion Bonus: +20 XP for winning the game
- First-Time Defeat Bonus: +50 XP for defeating Enemy Warlord for the first time
- Streak Completion Bonus: Multiply completion bonus by streak multiplier
- Examples:
  - First-time win (no streak): 20 + 50 = 70 XP
  - First-time win (5-win streak): (20 + 50) × 2 = 140 XP
  - Repeat win (10+ streak): 20 × 2.5 = 50 XP

**Daily Login Bonus:**
- Daily Bonus: 100 Gold + 50 XP (first login of the day)
- Resets: 24 hours after last login

**Challenge Completion XP:**
- Challenge rewards vary by challenge type and difficulty
- Additional XP bonuses for completing challenge objectives

##### XP Progression System

**Level Thresholds:**
- Level 1→2: 100 XP
- Level 2→3: 150 XP
- Level 3→4: 200 XP
- Level 4→5: 250 XP
- Level 5→6: 300 XP
- Level 6→7: 350 XP
- Level 7→8: 400 XP
- Level 8→9: 450 XP
- Level 9→10: 500 XP
- Level 10→11: 550 XP
- Level 11→12: 600 XP
- Level 12→13: 650 XP
- Level 13→14: 700 XP
- Level 14→15: 750 XP
- Level 15→16: 800 XP
- Level 16→17: 850 XP
- Level 17→18: 900 XP
- Level 18→19: 950 XP
- Level 19→20: 1,000 XP
- Level 20→21: 1,100 XP
- Level 21→22: 1,200 XP
- Level 22→23: 1,300 XP
- Level 23→24: 1,400 XP
- Level 24→25: 1,500 XP
- Level 25→26: 1,600 XP
- Level 26→27: 1,700 XP
- Level 27→28: 1,800 XP
- Level 28→29: 1,900 XP
- Level 29→30: 2,000 XP
- Level 30→31: 2,100 XP
- Level 31→32: 2,200 XP
- Level 32→33: 2,300 XP
- Level 33→34: 2,400 XP
- Level 34→35: 2,500 XP
- Level 35→36: 2,600 XP
- Level 36→37: 2,700 XP
- Level 37→38: 2,800 XP
- Level 38→39: 2,900 XP
- Level 39→40: 3,000 XP
- Level 40→41: 3,200 XP
- Level 41→42: 3,400 XP
- Level 42→43: 3,600 XP
- Level 43→44: 3,800 XP
- Level 44→45: 4,000 XP
- Level 45→46: 4,200 XP
- Level 46→47: 4,400 XP
- Level 47→48: 4,600 XP
- Level 48→49: 4,800 XP
- Level 49→50: 5,000 XP
- Level 50→51: 5,500 XP
- Level 51→52: 6,000 XP
- Level 52→53: 6,200 XP
- Level 53→54: 6,400 XP
- Level 54→55: 6,500 XP
- Level 55→56: 6,600 XP
- Level 56→57: 6,700 XP
- Level 57→58: 6,750 XP
- Level 58→59: 6,800 XP
- Total XP to max level (59): ~68,000 XP

**Progression Pacing:**
- Early game (Levels 1-10): Fast progression (~100-500 XP per level)
- Mid game (Levels 11-30): Moderate progression (~600-2,000 XP per level)
- Late game (Levels 31-50): Slower progression (~2,100-5,000 XP per level)
- End game (Levels 51-59): Slowest progression (~5,500-6,800 XP per level)

**Time Estimates:**
- Average game: ~50-100 XP earned (with bonuses)
- Games per level: ~2-10 games (varies by level)
- Total games to max level: ~500-1,000 games
- Estimated playtime: ~40-60 hours to max level (assuming 3-5 minutes per game)

##### XP Display and Feedback

**UI Display:**
- Pre-game: XP progress bar shown in Warlord selection screens
- Post-game: XP progress displayed on results screen
- Menu: XP progress shown in Game Menu overlay
- In-game: XP progress bar shown (top-center, minimal)

**Notifications:**
- XP Gain Popup: "+X XP" animation on turn/game win (fades after 2 seconds)
- Sound: Brief chiptune chime for XP gain (different pitch from Gold)
- Level-Up Celebration: Full-screen animation with rewards display
- Progress Reminders: "X XP to next level" shown pre-game

#### Monetization Economy

The game uses a hybrid monetization model: Free-to-play with ads, optional IAP purchases, and a one-time PAID account upgrade.

##### F2P Model (Default)

**Features:**
- Full game access (all content unlockable through gameplay)
- Ad-supported Gold earning (AdMob Rewarded Video and Interstitial)
- Local storage (progress saved locally, no cloud sync)
- No pay-to-win mechanics

**Ad Placement:**
- Post-game Rewarded Video: 25-100 Gold (unlimited, optional)
- Post-game Interstitial: 10-50 Gold (every 3-5 games, skippable)
- Pre-game Rewarded Video: 25-100 Gold (when Gold insufficient)
- Daily Ad Bonus: +50 Gold (first ad of the day)

**Ad Frequency:**
- Rewarded videos: Player-initiated (no forced ads)
- Interstitials: Every 3-5 games (configurable, skippable after 5 seconds)
- Maximum per day: ~500 Gold from ads (soft cap)

**Limitations:**
- No cloud save (progress tied to device/browser)
- Ad interruptions (optional but encouraged)
- Slower Gold earning (requires ad viewing)

##### PAID Account Model ($3.99 One-Time Purchase)

**Features:**
- All F2P features included
- Cloud save (cross-device sync via account system)
- Automatic Gold rewards (matches ad rewards, no ads required)
- Can still watch ads for extra Gold (optional)
- Ad-free experience (no forced interruptions)

**Benefits:**
- Convenience: No ad viewing required
- Cross-device sync: Play on multiple devices
- Progress security: Cloud backup prevents data loss
- Same Gold income: Automatic rewards match ad rewards

**Upgrade Prompts:**
- Pre-game: "Upgrade to PAID" button (if F2P)
- Post-game: "Upgrade to PAID" prompt (if low Gold, F2P)
- Menu: "Upgrade" option in Game Menu
- Low Gold moments: Upgrade prompts when Gold < 50

##### IAP Model (Optional Gold Purchases)

**Gold Packages:**
- Small Pack: $0.99 = 500 Gold (baseline rate: $0.002 per Gold)
- Medium Pack: $2.99 = 1,750 Gold (17% bonus: $0.00171 per Gold)
- Large Pack: $4.99 = 3,500 Gold (40% bonus: $0.00143 per Gold)
- Mega Pack: $9.99 = 8,000 Gold (60% bonus: $0.00125 per Gold)

**Purchase Points:**
- Post-game: "Purchase Gold" button (always available)
- Pre-game: If insufficient Gold for game fee
- Battle Item Shop: If insufficient Gold for item purchase
- Low Gold Warning: If Gold < 50, show upgrade prompt

**IAP Philosophy:**
- Always optional (never forced)
- Convenience purchases (skip grinding)
- No pay-to-win (all content unlockable through play)
- Value proposition: Time savings, not power

##### Monetization Balance

**F2P Player Experience:**
- Can progress through ads (generous ad rewards)
- ~500 Gold per day from ads (with daily bonus)
- ~300-500 Gold net per day (with gameplay)
- All content unlockable through play
- No forced purchases

**PAID Player Experience:**
- Automatic Gold rewards (no ads required)
- Same Gold income as F2P (automatic matching)
- Can still watch ads for extra Gold (optional)
- Cloud save convenience
- Ad-free experience

**IAP Player Experience:**
- Optional Gold purchases for convenience
- Value increases with package size (bonus Gold)
- Never required for progression
- Time savings, not power

**Revenue Streams:**
1. PAID account upgrades ($3.99 one-time)
2. IAP Gold packages ($0.99-$9.99)
3. Ad revenue (F2P players viewing ads)

**Monetization Goals:**
- Fair play: No pay-to-win mechanics
- Player choice: Multiple monetization options
- Sustainable revenue: Balanced F2P/IAP/PAID model
- Player retention: Generous free progression

#### Economic Integration

**Gold and XP Relationship:**
- Gold: Used for game attempts and Battle Items
- XP: Used for level progression and content unlocks
- Independent systems: Gold doesn't convert to XP, XP doesn't convert to Gold
- Synergy: Both earned through gameplay, both benefit from streaks

**Progression Gates:**
- Level gates: XP required to unlock new Enemy Warlords
- Gold gates: Gold required for game attempts (after 3 free)
- Battle Item gates: Gold required for item purchases
- Defeat gates: Must defeat Enemy Warlord to advance level

**Economic Loops:**
1. **Core Loop**: Play game → Earn Gold/XP → Level up → Unlock content → Play game
2. **Monetization Loop**: Low Gold → Ad/IAP prompt → Gold earned → Continue playing
3. **Retention Loop**: Daily login → Daily bonus → Play game → Progress → Return tomorrow

**Balance:**
- Early game: Generous rewards (retention)
- Mid game: Balanced rewards (engagement)
- Late game: Slower progression (longevity)
- Scarcity moments: Natural paywalls (monetization)
- Player agency: Multiple paths to progress (fair play)

### Challenges

The Challenges system provides optional objectives that reward players with bonus Gold and XP. Challenges encourage diverse playstyles, provide additional progression goals, and create engagement hooks beyond the core game loop.

#### Challenge System Overview

**Purpose:**
- Provide additional progression goals beyond level advancement
- Encourage diverse playstyles and experimentation
- Reward player engagement and skill development
- Create daily/weekly engagement hooks
- Offer bonus rewards for completing objectives

**Design Philosophy:**
- Optional objectives (never required for progression)
- Achievable goals (reasonable difficulty, not frustrating)
- Diverse objectives (combat, progression, collection, specials)
- Clear progress tracking (visual feedback, progress bars)
- Meaningful rewards (Gold and XP bonuses)

**Challenge States:**
- **Locked:** Challenge not yet available (level/defeat requirements)
- **Active:** Challenge available and in progress
- **Completed:** Challenge finished, rewards claimed
- **Expired:** Time-limited challenge expired (daily/weekly)

#### Challenge Categories

Challenges are organized into categories based on their objective type:

**Combat Challenges:**
- Turn win streaks
- Game wins
- Damage dealt
- Cards captured
- War scenarios won

**Progression Challenges:**
- Level milestones
- XP earned
- Gold collected
- Warlords defeated
- Collection completion

**Specials Challenges:**
- Specials used
- Suit specials activated
- Warlord powers used
- Special combos achieved

**Chain Challenges:**
- Suit bursts triggered
- Poker chains completed (Full House, Straight, Pair, etc.)
- Rare chains achieved (Royal Flush, Four of a Kind)
- Chain combinations completed

**Collection Challenges:**
- Warlords defeated
- Battle Items collected
- Unique Warlords defeated
- Collection milestones

**Performance Challenges:**
- Perfect games (no losses)
- Fast victories
- High damage turns
- Efficient special usage

#### Challenge Types

**Daily Challenges:**
- Refresh: Every 24 hours (midnight local time)
- Quantity: 3 daily challenges active at once
- Difficulty: Easy to Medium
- Rewards: 50-200 Gold, 25-100 XP
- Examples:
  - "Win 5 turns in a row" - 100 Gold, 50 XP
  - "Defeat 1 Warlord" - 150 Gold, 75 XP
  - "Use 3 specials" - 75 Gold, 40 XP
  - "Earn 200 Gold" - 200 Gold, 100 XP
  - "Win 1 game" - 150 Gold, 75 XP

**Weekly Challenges:**
- Refresh: Every 7 days (Monday midnight local time)
- Quantity: 5 weekly challenges active at once
- Difficulty: Medium to Hard
- Rewards: 200-500 Gold, 100-200 XP
- Examples:
  - "Win 20 turns in a row" - 300 Gold, 150 XP
  - "Defeat 5 different Warlords" - 400 Gold, 200 XP
  - "Use 20 specials" - 250 Gold, 125 XP
  - "Earn 1,000 Gold" - 500 Gold, 250 XP
  - "Reach Level 5" - 300 Gold, 150 XP

**Achievement Challenges (One-Time):**
- Unlock: Based on player progress/level
- Quantity: Unlimited (unlock as player progresses)
- Difficulty: Easy to Hard (scales with level)
- Rewards: 100-1,000 Gold, 50-500 XP
- Examples:
  - "Win your first game" - 100 Gold, 50 XP
  - "Reach Level 10" - 500 Gold, 250 XP
  - "Defeat 10 Warlords" - 400 Gold, 200 XP
  - "Use 100 specials" - 600 Gold, 300 XP
  - "Earn 10,000 Gold" - 1,000 Gold, 500 XP
  - "Complete collection (59 Warlords)" - 2,000 Gold, 1,000 XP

**Milestone Challenges:**
- Unlock: At specific level thresholds
- Quantity: One per milestone level
- Difficulty: Medium (appropriate for milestone level)
- Rewards: 300-1,000 Gold, 150-500 XP
- Examples:
  - "Reach Level 5" - 300 Gold, 150 XP
  - "Reach Level 10" - 500 Gold, 250 XP
  - "Reach Level 20" - 700 Gold, 350 XP
  - "Reach Level 30" - 800 Gold, 400 XP
  - "Reach Level 40" - 900 Gold, 450 XP
  - "Reach Level 50" - 1,000 Gold, 500 XP
  - "Reach Level 59 (Max)" - 2,000 Gold, 1,000 XP

**Collection Challenges:**
- Unlock: Based on collection progress
- Quantity: Multiple milestones
- Difficulty: Easy to Hard (scales with collection size)
- Rewards: 200-2,000 Gold, 100-1,000 XP
- Examples:
  - "Defeat 5 Warlords" - 200 Gold, 100 XP
  - "Defeat 10 Warlords" - 400 Gold, 200 XP
  - "Defeat 25 Warlords" - 800 Gold, 400 XP
  - "Defeat 50 Warlords" - 1,500 Gold, 750 XP
  - "Defeat all 59 Warlords" - 2,000 Gold, 1,000 XP

#### Challenge Difficulty Tiers

**Easy Challenges:**
- Objective: Simple, achievable in 1-3 games
- Examples: "Win 3 turns", "Use 1 special", "Earn 100 Gold"
- Rewards: 50-100 Gold, 25-50 XP
- Target: New players, daily engagement

**Medium Challenges:**
- Objective: Moderate difficulty, achievable in 3-10 games
- Examples: "Win 10 turns in a row", "Defeat 3 Warlords", "Use 10 specials"
- Rewards: 100-300 Gold, 50-150 XP
- Target: Regular players, weekly engagement

**Hard Challenges:**
- Objective: Difficult, requires skill and persistence
- Examples: "Win 20 turns in a row", "Defeat 10 Warlords", "Earn 5,000 Gold"
- Rewards: 300-500 Gold, 150-250 XP
- Target: Dedicated players, achievement hunters

**Expert Challenges:**
- Objective: Very difficult, requires mastery and dedication
- Examples: "Win 50 turns in a row", "Defeat all 59 Warlords", "Earn 50,000 Gold"
- Rewards: 500-2,000 Gold, 250-1,000 XP
- Target: Completionist players, long-term goals

#### Challenge Refresh Mechanics

**Daily Challenge Refresh:**
- Time: Midnight local time (player's timezone)
- Process:
  1. Completed challenges: Marked as complete, rewards claimed
  2. Incomplete challenges: Expired, removed from active list
  3. New challenges: 3 new daily challenges unlocked
  4. Notification: "New Daily Challenges Available!" badge appears
- Display: Refresh timer shown in Challenges overlay (e.g., "Refreshes in 5h 23m")

**Weekly Challenge Refresh:**
- Time: Monday midnight local time (player's timezone)
- Process:
  1. Completed challenges: Marked as complete, rewards claimed
  2. Incomplete challenges: Expired, removed from active list
  3. New challenges: 5 new weekly challenges unlocked
  4. Notification: "New Weekly Challenges Available!" badge appears
- Display: Refresh timer shown in Challenges overlay (e.g., "Refreshes in 2d 14h")

**Achievement Challenge Unlock:**
- Trigger: Based on player progress (level, defeats, milestones)
- Process:
  1. Condition met: Achievement challenge unlocks
  2. Notification: "New Achievement Challenge Unlocked!" badge appears
  3. Challenge added to active list
  4. Progress tracking begins immediately
- Display: Achievement challenges shown in separate section

**Milestone Challenge Unlock:**
- Trigger: Reaching specific level thresholds
- Process:
  1. Level threshold reached: Milestone challenge unlocks
  2. Notification: "Milestone Challenge Unlocked!" popup
  3. Challenge added to active list
  4. Progress tracking begins immediately
- Display: Milestone challenges shown in separate section

#### Challenge Progress Tracking

**Progress Display:**
- Format: "Challenge: [Objective] - Progress: X/Y"
- Examples:
  - "Win 10 turns in a row - Progress: 7/10"
  - "Defeat 5 Warlords - Progress: 3/5"
  - "Use 20 specials - Progress: 12/20"
  - "Earn 1,000 Gold - Progress: 650/1,000"

**Progress Updates:**
- Real-time: Progress updates immediately when objective progress occurs
- Visual: Progress bar animates, number increments
- Sound: Subtle progress chime (can be disabled in settings)
- Notification: Brief status banner for significant progress (e.g., "Challenge Progress: 8/10!")

**Progress Persistence:**
- Saved: Progress tracked in localStorage (F2P) or cloud (PAID)
- Persists: Progress maintained across game sessions
- Reset: Daily/weekly challenges reset on refresh (completed or expired)
- Achievement: One-time challenges never reset (permanent progress)

**Progress Validation:**
- Turn wins: Counted when player wins a turn
- Game wins: Counted when player wins a game
- Warlord defeats: Counted when player defeats an Enemy Warlord for the first time
- Specials used: Counted when player activates a special (suit or Warlord)
- Gold earned: Counted from all Gold sources (turn wins, game wins, ads, etc.)
- XP earned: Counted from all XP sources (turn wins, game wins, daily bonus, etc.)

#### Challenge Completion Flow

**Completion Detection:**
- Trigger: Progress reaches objective threshold (X/Y becomes Y/Y)
- Timing: Checked after each relevant game event (turn win, game win, etc.)
- Validation: Objective requirements verified before completion

**Completion Sequence:**
1. **Detection:** System detects challenge completion
2. **Notification:** "Challenge Complete!" popup appears
3. **Visual Feedback:**
   - Challenge badge animates (glow, pulse, particles)
   - Checkmark appears on challenge
   - Progress bar fills to 100%
   - "COMPLETE" badge overlays challenge
4. **Sound:** Achievement chiptune (2-3 seconds)
5. **Rewards Display:**
   - "+X Gold" animation
   - "+Y XP" animation
   - Rewards added to player's totals
6. **State Update:**
   - Challenge marked as complete
   - Rewards claimed
   - Progress saved
   - New challenge unlocked (if applicable)

**Completion Rewards:**
- Gold: Awarded immediately to player's Gold total
- XP: Awarded immediately to player's XP total
- Badge: Visual badge for completed challenge (permanent)
- Unlock: Some challenges unlock special content (rare)

**Multiple Completions:**
- If multiple challenges complete simultaneously:
  - All completions shown in sequence (one after another)
  - Each completion gets full animation and rewards
  - Total rewards displayed at end ("Total: +X Gold, +Y XP")

#### Challenge UI/UX

**Challenges Overlay:**
- Access: Game Menu → "Challenges" button
- Layout:
  - Header: "Challenges" title, refresh timer
  - Tabs: "Daily", "Weekly", "Achievements", "Milestones"
  - Challenge List: Scrollable list of challenges
  - Progress Bars: Visual progress indicators
  - Rewards Display: Gold and XP rewards shown per challenge
- Size: Full-screen overlay (mobile-first responsive)
- Style: Retro SNES 32-bit pixel art aesthetic

**Challenge Card Design:**
- Layout:
  - Challenge icon (left)
  - Challenge name and description (center)
  - Progress bar (below description)
  - Progress text "X/Y" (right)
  - Rewards display "+X Gold, +Y XP" (bottom)
  - Status badge (complete/active/locked)
- Visual States:
  - Active: Normal colors, progress bar visible
  - Complete: Dimmed, checkmark badge, "COMPLETE" overlay
  - Locked: Grayed out, lock icon, unlock requirement shown
  - Expired: Grayed out, "EXPIRED" badge (daily/weekly only)

**Pre-Game Challenge Display:**
- Location: Warlord selection screen (toggleable in settings)
- Display: Compact challenge cards showing active challenges
- Format: Icon + progress (e.g., "Win 10 turns: 7/10")
- Interaction: Tap to open full Challenges overlay

**Post-Game Challenge Display:**
- Location: Results screen (below rewards)
- Display: Challenge progress updates
- Format: "Challenge Progress: X/Y" for each active challenge
- Interaction: Tap to open full Challenges overlay

**Challenge Notifications:**
- Badge: "New Challenges!" badge on Game Menu button
- Popup: "New Daily/Weekly Challenges Available!" popup on app launch
- Status Banner: Brief progress updates during gameplay
- Sound: Achievement chiptune on completion

**Challenge Settings:**
- Toggle: Enable/disable challenge notifications
- Display: Show/hide challenges in pre-game screen
- Sound: Enable/disable challenge completion sounds
- Saved: Preferences saved to localStorage

#### Challenge Integration

**Game Flow Integration:**
- Pre-game: Active challenges displayed
- In-game: Progress tracked silently (no UI interruption)
- Post-game: Progress updates shown on results screen
- Menu: Full challenge list accessible anytime

**Progression Integration:**
- Challenges provide bonus Gold and XP (supplements core progression)
- Milestone challenges align with level progression
- Collection challenges align with Warlord unlocks
- Achievement challenges provide long-term goals

**Monetization Integration:**
- Challenges encourage daily engagement (ad viewing opportunities)
- Challenge rewards supplement Gold income (reduces IAP pressure)
- Completionist challenges provide long-term goals (retention)
- No pay-to-win: Challenges unlockable through gameplay only

**Social Integration:**
- Challenge completion tracked in statistics
- Challenge badges visible in player profile
- Leaderboards: Challenge completion counts displayed
- Sharing: Challenge completion shareable

#### Challenge Examples

**Daily Challenge Examples:**
1. "Win Streak" - Win 5 turns in a row (100 Gold, 50 XP)
2. "Warlord Hunter" - Defeat 1 Warlord (150 Gold, 75 XP)
3. "Specialist" - Use 3 specials (75 Gold, 40 XP)
4. "Gold Rush" - Earn 200 Gold (200 Gold, 100 XP)
5. "Victory" - Win 1 game (150 Gold, 75 XP)
6. "Card Collector" - Capture 20 cards (100 Gold, 50 XP)
7. "Damage Dealer" - Deal 50 damage (125 Gold, 60 XP)

**Weekly Challenge Examples:**
1. "Streak Master" - Win 20 turns in a row (300 Gold, 150 XP)
2. "Warlord Slayer" - Defeat 5 different Warlords (400 Gold, 200 XP)
3. "Special Expert" - Use 20 specials (250 Gold, 125 XP)
4. "Gold Collector" - Earn 1,000 Gold (500 Gold, 250 XP)
5. "Level Up" - Reach Level 5 (300 Gold, 150 XP)
6. "War Veteran" - Win 10 War scenarios (350 Gold, 175 XP)
7. "Perfect Game" - Win a game without losing a turn (400 Gold, 200 XP)

**Chain Challenge Examples:**
1. "Chain Master" - Trigger 3 Suit Bursts (200 Gold, 100 XP)
2. "Full House" - Complete a Full House Chain (400 Gold, 200 XP)
3. "Straight Shooter" - Complete a Straight Chain (300 Gold, 150 XP)
4. "Pair Master" - Trigger 2 Pair Chains (250 Gold, 125 XP)
5. "Rainbow Warrior" - Complete a Rainbow Chain (500 Gold, 250 XP)
6. "Royal Flush" - Trigger a Royal Flush (1,000 Gold, 500 XP) - Expert challenge
7. "Straight Flush" - Complete a Straight Flush (800 Gold, 400 XP) - Expert challenge
8. "Four of a Kind" - Trigger Four of a Kind (600 Gold, 300 XP)
9. "Hearts Specialist" - Trigger 5 Hearts Bursts (300 Gold, 150 XP)
10. "Chain Combo" - Trigger 10 total chains (1,500 Gold, 750 XP) - Expert challenge

**Achievement Challenge Examples:**
1. "First Victory" - Win your first game (100 Gold, 50 XP)
2. "Level 10" - Reach Level 10 (500 Gold, 250 XP)
3. "Warlord Master" - Defeat 10 Warlords (400 Gold, 200 XP)
4. "Special Master" - Use 100 specials (600 Gold, 300 XP)
5. "Gold Millionaire" - Earn 10,000 Gold (1,000 Gold, 500 XP)

**Chain Challenge Examples:**
1. "Chain Master" - Trigger 3 Suit Bursts (200 Gold, 100 XP)
2. "Full House" - Complete a Full House Chain (400 Gold, 200 XP)
3. "Straight Shooter" - Complete a Straight Chain (300 Gold, 150 XP)
4. "Pair Master" - Trigger 2 Pair Chains (250 Gold, 125 XP)
5. "Rainbow Warrior" - Complete a Rainbow Chain (500 Gold, 250 XP)
6. "Royal Flush" - Trigger a Royal Flush (1,000 Gold, 500 XP) - Expert challenge
7. "Straight Flush" - Complete a Straight Flush (800 Gold, 400 XP) - Expert challenge
8. "Four of a Kind" - Trigger Four of a Kind (600 Gold, 300 XP)
9. "Hearts Specialist" - Trigger 5 Hearts Bursts (300 Gold, 150 XP)
10. "Chain Combo" - Trigger 10 total chains (1,500 Gold, 750 XP) - Expert challenge
6. "Collection Complete" - Defeat all 59 Warlords (2,000 Gold, 1,000 XP)
7. "Streak Legend" - Win 100 turns in a row (1,500 Gold, 750 XP)

**Milestone Challenge Examples:**
1. "Level 5 Milestone" - Reach Level 5 (300 Gold, 150 XP)
2. "Level 10 Milestone" - Reach Level 10 (500 Gold, 250 XP)
3. "Level 20 Milestone" - Reach Level 20 (700 Gold, 350 XP)
4. "Level 30 Milestone" - Reach Level 30 (800 Gold, 400 XP)
5. "Level 40 Milestone" - Reach Level 40 (900 Gold, 450 XP)
6. "Level 50 Milestone" - Reach Level 50 (1,000 Gold, 500 XP)
7. "Max Level" - Reach Level 59 (2,000 Gold, 1,000 XP)

#### Challenge Balance

**Reward Balance:**
- Daily challenges: 50-200 Gold, 25-100 XP (supplemental income)
- Weekly challenges: 200-500 Gold, 100-200 XP (moderate bonus)
- Achievement challenges: 100-2,000 Gold, 50-1,000 XP (scaled by difficulty)
- Milestone challenges: 300-2,000 Gold, 150-1,000 XP (level-appropriate)

**Difficulty Balance:**
- Easy: Achievable in 1-3 games (daily engagement)
- Medium: Achievable in 3-10 games (weekly engagement)
- Hard: Requires skill and persistence (achievement hunters)
- Expert: Long-term goals (completionist players)

**Frequency Balance:**
- Daily: 3 challenges per day (manageable, not overwhelming)
- Weekly: 5 challenges per week (variety, multiple objectives)
- Achievement: Unlock as player progresses (natural progression)
- Milestone: One per level threshold (clear progression markers)

**Engagement Balance:**
- Optional: Never required for progression (player choice)
- Achievable: Reasonable difficulty (not frustrating)
- Rewarding: Meaningful Gold/XP bonuses (worth pursuing)
- Diverse: Multiple challenge types (cater to different playstyles)

### Updates, Fixes, and Expansions

### Admin Mode

### Testing and QA

## Visual Design

### Game Table

The Game Table is the persistent game screen that serves as the foundation for all gameplay. It maintains visual consistency across pre-game, in-game, and post-game states, with Warlord avatars and core UI elements persisting throughout.

#### Layout Structure

**Base Dimensions:**
- Mobile-first: 375x767px (portrait orientation)
- Safe area: ~375w x 700h (notch-aware)
- Responsive scaling: Proportional up to 800px max width (centered)

**Vertical Stack Layout:**
- **Top Section (20% height):** Enemy Warlord area
  - Enemy Warlord avatar (100x120px)
  - Enemy HP bar (200x20px)
  - Enemy deck indicator (150x40px)
- **Middle Section (30% height):** Battle zone
  - Card play area (centered)
  - Enemy card slot (right side)
  - Player card slot (left side)
- **Bottom Section (40% height):** Player Warlord area + CTAs
  - Player Warlord avatar (100x120px)
  - Player HP bar (200x20px)
  - Player deck indicator (150x40px)
  - Primary CTA button (300x60px, thumb-level)
  - Game Menu icon (32x32px, bottom-right)

**Status Banner:**
- Position: Top-full width (375x77px)
- Content: Game status messages, turn outcomes, prompts
- Style: Semi-transparent wood background (#3A2A1A), pixel text (20px)
- Behavior: Marquee scroll for long messages

#### Visual Style

**Background:**
- Base color: Dark forest green (#1A2A1A to #4A5A3A gradient)
- Texture: Subtle pixel dithering pattern
- Depth: Layered visual hierarchy (background → cards → avatars → UI)

**Card Rendering:**
- Deck cards: 80x120px (canvas-rendered)
- Battle zone cards: 100x150px (enhanced visibility)
- Style: Pixel-perfect rendering, no anti-aliasing
- Animation: Smooth flip transitions (180° rotate), slide animations

**Warlord Avatars:**
- Size: 100x120px (base), scales to 120x144px on larger screens
- Style: Pixel sprite art (15-20 colors per sprite)
- Emotes: Swappable head sprites (defeated, joyful, neutral)
- Interaction: Glow effect on tap (triggers overlay)

**HP Bars:**
- Size: 200x20px
- Style: Segmented pixel bar or pixel hearts (5-10 segments)
- Colors: Red (damage), green (healing), yellow (low HP warning)
- Animation: Smooth fill/deplete transitions

**Deck Indicators:**
- Size: 150x40px
- Style: Pixel stack icon + count text (16px)
- Behavior: Pulse animation when deck < 10 cards
- Position: Adjacent to Warlord avatars

#### Responsive Behavior

**Mobile (375-480px):**
- Base layout maintained
- All elements scale proportionally
- Touch targets: Minimum 48x48px

**Tablet (481-768px):**
- Icons +20% size
- Padding +10px
- Avatars: 120x144px
- Battle zone cards: 120x180px

**Desktop (769px+):**
- Max width: 800px (centered)
- Icons +25% size
- Padding +50%
- Subtle glow effects enabled
- No layout shifts (proportional scaling only)

### Pre-game

The Pre-game screen displays before each game starts, allowing players to select Warlords, manage Battle Items, and review challenges before beginning gameplay.

#### Layout

**Screen Composition:**
- Enemy Warlord avatar (top-center, 100x120px)
- Player Warlord avatar (bottom-center, 100x120px)
- Gold balance display (top-left corner)
- Level/XP progress bar (top-right corner)
- Primary CTA: "Play" button (bottom-center, 300x60px)
- Secondary CTAs:
  - "Select Enemy Warlord" button (below Enemy avatar)
  - "Select Player Warlord" button (above Player avatar)
  - Game Menu icon (bottom-right, 32x32px)
  - "Challenges" button (top-center)

**Visual Elements:**
- Background: Same Game Table background (dark forest)
- Warlord avatars: Default or last-played Warlords displayed
- Deck indicators: Show deck counts (36 cards each)
- HP bars: Hidden or shown at full (100%)
- Status banner: Shows "Select Warlords and Tap Play" or last game result

#### Warlord Selection Interface

**Enemy Warlord Selection:**
- Button: "Select Enemy Warlord" (below Enemy avatar)
- Tap action: Opens Enemy Warlord Select Gallery overlay
- Visual feedback: Button glow on hover/tap

**Player Warlord Selection:**
- Button: "Select Player Warlord" (above Player avatar)
- Tap action: Opens Player Warlord Select Gallery overlay
- Visual feedback: Button glow on hover/tap

**Default Selection:**
- First-time: Sasquatch vs Sasquatch (but player can immediately select any of 5 unlocked Enemy/Player Warlords)
- Returning: Last-played Warlord combination
- Persistence: Saved to localStorage

**Initial Unlocks for New Players:**
- Levels 1-5 unlocked for both Enemy and Player Warlords (Sasquatch, Skunk Ape, Wendigo, Jersey Devil, Grassman)
- New players can immediately select any of these 5 Enemy Warlords or 5 Player Warlords
- Level 6+ unlock sequentially as player progresses

#### Battle Item Management

**Pre-Game Access:**
- Tap Player Warlord avatar → Opens Player Warlord Details overlay
- Shows owned Battle Items (if any)
- Shows available Battle Items for purchase
- Purchase interface (one-time purchase, item added to inventory)

**In-Game Access:**
- Battle Item button appears in Pre-Turn State (if player owns items with remaining charges)
- Tap Battle Item button → Battle Item Selection Overlay appears
- Shows all owned Battle Items with remaining charges
- Each item displays: Icon, name, effect description, charges remaining (e.g., "2/3 charges")
- Player selects item to activate before card draw
- Charge consumed on activation (charges remaining decreases)
- Items recharge to full charges after each game completes

**Display:**
- Battle Item button (Pre-Turn State, if items available)
- Battle Item icon in inventory (if owned)
- Gold cost displayed for purchasable items

#### Challenge Display

**Location:** Top-center area (below status banner)
**Format:** Compact challenge cards
**Content:** Active challenges with progress (e.g., "Win 10 turns: 7/10")
**Interaction:** Tap to open full Challenges overlay

#### Gold and XP Display

**Gold Balance:**
- Position: Top-left corner
- Format: Gold icon + number (e.g., "💰 1,250")
- Style: Pixel text (18px), yellow accent color
- Update: Real-time when Gold changes

**Level/XP Progress:**
- Position: Top-right corner
- Format: "Level X" + progress bar
- Style: Pixel text (16px), progress bar (100x8px)
- Update: Real-time when XP changes

#### Primary CTA

**"Play" Button:**
- Size: 300x60px (thumb-friendly)
- Position: Bottom-center
- Style: Bold pixel text (24px), yellow glow pulse animation
- State: Enabled (if Warlords selected), disabled (if selection incomplete)
- Tap action: Starts game, transitions to Game Play screen

### Game Play

The Game Play screen is the active gameplay state where turns are played, cards are drawn, and battles are resolved.

#### Layout During Turn

**Card Draw Phase:**
- Both cards drawn simultaneously
- Cards appear in battle zone (100x150px each)
- Enemy card: Right side (x+120 offset)
- Player card: Left side (x-120 offset)
- Animation: Card flip (180° rotate, 300ms duration)

**Rank Comparison Phase:**
- Cards remain visible in battle zone
- Status banner updates: "Player Wins!" or "Enemy Wins!" or "War!"
- Visual highlight: Winner's card glows briefly

**Damage Phase:**
- HP bars animate (deplete for loser)
- Damage flash effect on HP bar
- Status banner shows damage amount: "-X Damage"

**Card Capture Phase:**
- Cards slide to winner's deck
- Animation: Slide path to deck indicator (400ms duration)
- Deck count updates (increments by 2)
- Sound: Card capture chiptune

#### War Scenario Display

**War Trigger:**
- Status banner: "WAR!" (large pixel text)
- Both players place 2 cards face-down + 1 face-up
- Total: 6 cards in battle zone

**Card Layout:**
- Face-down cards: Stacked (2 cards each, slightly offset)
- Face-up cards: Prominently displayed (top of stacks)
- Size: Scales down to 80x120px to fit (or stacks vertically)
- Animation: Sequential reveal (face-down → face-up)

**War Resolution:**
- Highest face-up card wins
- All 6 cards slide to winner's deck
- Status banner: "War Won!" or "War Lost!"

#### Inline Specials Icons

**Location:** Main game board (inline, always visible)
**Layout:** Horizontal row of 5 icons (4 suit icons + 1 Warlord Power icon)
**Position:** Below Player Warlord avatar, above Primary CTA (thumb-accessible area)
**Size:** Each icon 48x48px (touch-friendly, matches suit/Warlord theme)

**Visual Design:**
- Suit icons: Hearts (red), Diamonds (blue), Clubs (green), Spades (purple)
- Warlord Power icon: Unique icon matching Warlord theme
- Ready specials: Icons glow with pulsing animation (color matches suit/Warlord)
- Unready specials: Icons dimmed (50% opacity), no glow
- Charge progress: Tooltip appears on tap showing "X/Y [Suit] captured" or "X/Y wins OR X/Y damage"
- Spacing: 8px between icons (centered horizontally)

#### Enemy Special Notification

**Trigger:** After enemy wins a turn and plays specials
**Layout:** Compact banner (300x150px, center-top)
**Content:** Shows enemy specials played (suit icons + Warlord special if used)
**Behavior:** Auto-dismisses after 2-3 seconds
**Style:** Pixel text, semi-transparent background

#### Turn State Indicators

**Status Banner Messages:**
- "Draw Cards" (pre-turn)
- "Player Wins! -X Damage" (player win)
- "Enemy Wins! -X Damage" (enemy win)
- "WAR!" (tie scenario)
- "Special Ready!" (when specials available)

**Visual Feedback:**
- Card animations (flip, slide, capture)
- HP bar animations (deplete, flash)
- Deck count updates (real-time)
- Avatar emotes (swap based on outcome)

### Post-game

The Post-game screen displays after a game concludes (win or loss), showing results, rewards, and progression updates.

#### Results Screen Layout

**Screen Composition:**
- Game result banner (top-center): "Victory!" or "Defeat!"
- Rewards display (center):
  - Gold earned: "+X Gold" animation
  - XP earned: "+Y XP" animation
  - Streak bonus (if applicable): "Streak: X wins!"
- Warlord avatars: Final state (defeated/joyful emotes)
- HP bars: Final HP values displayed
- Statistics (expandable):
  - Turns played
  - Cards captured
  - Specials used
  - Damage dealt/taken

#### Reward Animations

**Gold Gain:**
- "+X Gold" text appears (center)
- Animation: Fade in + slide up (500ms)
- Sound: Chiptune chime (different pitch from XP)
- Duration: Fades after 2 seconds

**XP Gain:**
- "+Y XP" text appears (below Gold)
- Animation: Fade in + slide up (500ms)
- Sound: Chiptune chime (different pitch from Gold)
- Duration: Fades after 2 seconds

**Streak Display:**
- "Streak: X wins!" banner (if streak active)
- Animation: Pulse glow effect
- Multiplier shown: "1.5x" or "2x" or "2.5x"

#### Level-Up Celebration

**Trigger:** If level-up threshold reached
**Sequence:**
1. Screen dims (50% opacity overlay)
2. Level number animates upward with particle effects
3. "LEVEL UP!" text appears (large pixel text, 48px)
4. Chiptune fanfare (2-3 seconds)
5. Unlocks displayed (new Enemy Warlord, Battle Items)
6. Level-up bonus Gold shown: "+X Gold"

**Visual Design:**
- Full-screen celebration overlay
- Particle effects: Pixel sparks (8x8px)
- Color scheme: Gold/yellow accents
- Duration: 3-4 seconds total

#### Unlock Celebrations

**Warlord Unlock:**
- Overlay shows Warlord preview
- "New Warlord Unlocked!" message
- Avatar animation: Glow, pulse, particles
- Sound: Thematic chiptune (matches Warlord)
- Duration: 3-4 seconds

**Battle Item Unlock:**
- Item icon displayed
- "New Battle Item Available!" message
- Brief animation: Item icon pulse
- Duration: 2 seconds

#### Post-Game Options

**Action Buttons:**
- "Continue" (primary): Return to pre-game screen
- "Replay" (secondary): Restart game with same Warlords
- "Select Warlord" (secondary): Change Warlords
- "View Progress" (tertiary): Detailed statistics
- "Earn Gold" (tertiary, F2P): Watch ad for Gold
- "Menu" (tertiary): Access Game Menu overlay

**Button Layout:**
- Primary CTA: Bottom-center (300x60px)
- Secondary CTAs: Horizontal row above primary (200x48px each)
- Tertiary CTAs: Smaller buttons, bottom-left/right

#### Challenge Progress Updates

**Display:** Below rewards section
**Format:** "Challenge Progress: X/Y" for each active challenge
**Visual:** Progress bars update, numbers increment
**Interaction:** Tap to open full Challenges overlay

### Game Menu

The Game Menu overlay provides access to settings, statistics, challenges, leaderboards, and other game features.

#### Overlay Layout

**Access:** Tap Game Menu icon (bottom-right, 32x32px)
**Layout:** Fullscreen modal (375x767px base)
**Style:** Dark semi-transparent backdrop (50% opacity)
**Content:** Centered modal (max 320px width)

#### Menu Sections

**Header:**
- "Game Menu" title (pixel text, 24px)
- Close button (top-right, 32x32px)

**Menu Items (Vertical List):**
1. **Statistics** (icon + text)
   - Games played
   - Win rate
   - Highest streak
   - Total Gold earned
   - Total XP earned
   - Warlords defeated
   - Collection progress

2. **Challenges** (icon + text)
   - Active challenges count badge
   - Tap to open Challenges overlay

3. **Leaderboards** (icon + text)
   - Current rank display
   - Tap to open Leaderboards overlay

4. **Collection** (icon + text)
   - Warlord gallery
   - Battle Item gallery
   - Completion percentage

5. **Settings** (icon + text)
   - Sound toggle
   - Music toggle
   - Notifications toggle
   - High contrast mode
   - Challenge display preferences

6. **About** (icon + text)
   - Game version
   - Credits
   - Privacy policy link
   - Terms of service link

7. **Upgrade to PAID** (if F2P, icon + text)
   - Prominent button
   - Benefits listed
   - Tap to open purchase flow

#### Visual Design

**Menu Items:**
- Size: 280x48px each
- Style: Pixel art buttons with hover glow
- Spacing: 16px between items
- Icons: 24x24px pixel sprites
- Text: Pixel font (16px)

**Badges:**
- Notification badges on relevant items
- Style: Red circle with count (16x16px)
- Animation: Pulse when new content available

**Scrollable:**
- If content exceeds viewport, vertical scroll enabled
- Scrollbar: Pixel art style, minimal

### Enemy Warlord Select Gallery

The Enemy Warlord Select Gallery allows players to choose which Enemy Warlord to face in the next game.

**Initial Unlocks:** New players start with levels 1-5 unlocked (Sasquatch, Skunk Ape, Wendigo, Jersey Devil, Grassman). Level 6+ unlock sequentially as player progresses.

#### Overlay Layout

**Access:** Tap "Select Enemy Warlord" button (pre-game screen)
**Layout:** Fullscreen modal (375x767px base)
**Style:** Dark semi-transparent backdrop (50% opacity)
**Content:** Centered gallery grid

#### Gallery Grid

**Layout:**
- Grid: 3 columns × 2 rows (mobile), 4 columns × 2 rows (tablet+)
- Warlord cards: 100x120px each (matches avatar size)
- Spacing: 16px between cards
- Scrollable: Vertical scroll if more than 6 Warlords

**Warlord Card Design:**
- Avatar: 100x120px pixel sprite
- Name: Below avatar (pixel text, 14px)
- Level requirement: Below name (pixel text, 12px)
- Status badges:
  - "Locked" (grayed out, lock icon)
  - "Defeated" (checkmark badge)
  - "New" (glow effect for newly unlocked)

#### Filtering and Sorting

**Filters:**
- "All" (default)
- "Unlocked"
- "Defeated"
- "New"

**Sort Options:**
- By level (default)
- By name (alphabetical)
- By defeat status

#### Selection

**Tap Action:**
- Tap Warlord card → Selects Warlord
- Overlay closes
- Pre-game screen updates with selected Enemy Warlord
- Visual feedback: Selected card glows briefly

**Locked Warlords:**
- Grayed out appearance
- Lock icon overlay
- Level requirement displayed: "Level X Required"
- Tap action: Shows "Locked" message (no selection)

### Player Warlord Select Gallery

The Player Warlord Select Gallery allows players to choose which Player Warlord to use in the next game.

**Initial Unlocks:** New players start with levels 1-5 unlocked (Sasquatch, Skunk Ape, Wendigo, Jersey Devil, Grassman). These are treated as already defeated for new players. Level 6+ unlock after defeating corresponding Enemy Warlord.

#### Overlay Layout

**Access:** Tap "Select Player Warlord" button (pre-game screen)
**Layout:** Fullscreen modal (375x767px base)
**Style:** Dark semi-transparent backdrop (50% opacity)
**Content:** Centered gallery grid

#### Gallery Grid

**Layout:**
- Grid: 3 columns × 2 rows (mobile), 4 columns × 2 rows (tablet+)
- Warlord cards: 100x120px each (matches avatar size)
- Spacing: 16px between cards
- Scrollable: Vertical scroll if more than 6 Warlords

**Warlord Card Design:**
- Avatar: 100x120px pixel sprite
- Name: Below avatar (pixel text, 14px)
- Unlock requirement: Below name (pixel text, 12px)
- Status badges:
  - "Locked" (grayed out, lock icon + "Defeat [Enemy Warlord] to unlock")
  - "Available" (normal appearance)

#### Filtering and Sorting

**Filters:**
- "All" (default)
- "Unlocked"
- "Locked"

**Sort Options:**
- By unlock order (default)
- By name (alphabetical)

#### Selection

**Tap Action:**
- Tap Warlord card → Selects Warlord
- Overlay closes
- Pre-game screen updates with selected Player Warlord
- Visual feedback: Selected card glows briefly

**Locked Warlords:**
- Grayed out appearance
- Lock icon overlay
- Unlock requirement displayed: "Defeat [Enemy Warlord] to unlock"
- Tap action: Shows "Locked" message (no selection)

### Enemy Warlord Details

The Enemy Warlord Details overlay displays comprehensive information about the selected Enemy Warlord.

#### Overlay Layout

**Access:** Tap Enemy Warlord avatar (anytime)
**Layout:** Fullscreen modal (375x767px base)
**Style:** Dark semi-transparent backdrop (50% opacity)
**Content:** Centered details panel (max 320px width)

#### Details Content

**Header:**
- Warlord avatar (large, 150x180px)
- Warlord name (pixel text, 24px)
- Level requirement (pixel text, 16px)

**Statistics:**
- HP: "HP: X" with visual bar
- Base Damage: "Damage: X"
- Charge Requirements: "Charges: X wins"

**Special Abilities:**
- Suit Specials: List of 4 suit specials with descriptions
- Warlord Power: Description of unique Warlord ability
- Charge mechanics: How charges accumulate

**Battle Items (if applicable):**
- Shows Battle Items available for this Warlord level
- Purchase options (if player has Gold)

**Status:**
- "Defeated" badge (if defeated)
- "New" badge (if newly unlocked)
- "Locked" badge (if not yet unlocked)

#### Visual Design

**Layout:**
- Vertical scrollable content
- Sections separated by dividers (pixel art lines)
- Icons: 24x24px pixel sprites
- Text: Pixel font (14-16px)

**Close Button:**
- Top-right corner (32x32px)
- Tap to close overlay

### Player Warlord Details

The Player Warlord Details overlay displays comprehensive information about the selected Player Warlord, including Battle Item management.

#### Overlay Layout

**Access:** Tap Player Warlord avatar (anytime)
**Layout:** Fullscreen modal (375x767px base)
**Style:** Dark semi-transparent backdrop (50% opacity)
**Content:** Centered details panel (max 320px width)

#### Details Content

**Header:**
- Warlord avatar (large, 150x180px)
- Warlord name (pixel text, 24px)
- Unlock status (if applicable)

**Statistics:**
- HP: "HP: X" with visual bar
- Base Damage: "Damage: X"
- Charge Requirements: "Charges: X wins"

**Special Abilities:**
- Suit Specials: List of 4 suit specials with descriptions
- Warlord Power: Description of unique Warlord ability
- Charge mechanics: How charges accumulate

**Battle Item Management:**
- Owned Items: Displayed prominently (if any)
- Available Items: List of purchasable Battle Items
- Purchase Interface:
  - Item icon
  - Item name and description
  - Gold cost
  - "Purchase" button (if Gold sufficient)
  - Status: "Owned" badge (if purchased)
  - Status: "Used" badge (if consumed)

**Unlock Status:**
- "Locked" badge (if not yet unlocked)
- Unlock requirement: "Defeat [Enemy Warlord] to unlock"

#### Visual Design

**Layout:**
- Vertical scrollable content
- Sections separated by dividers (pixel art lines)
- Icons: 24x24px pixel sprites
- Text: Pixel font (14-16px)

**Battle Item Cards:**
- Size: 120x80px each
- Style: Pixel art cards
- Layout: Grid (2 columns)
- Spacing: 16px between items

**Close Button:**
- Top-right corner (32x32px)
- Tap to close overlay

The game uses a **retro SNES 32-bit pixel art aesthetic** matching the Warlord prompts: Vibrant yet limited palettes (15-20 colors per sprite, drawing from SNES Mode 7 vibes—earthy greens/browns for forests, glowing accents for powers).

**Pixel perfection**: No anti-aliasing; `image-rendering: pixelated` in CSS for crisp scaling. High contrast (4.5:1 min) for readability on mobiles; dithering for shading/transitions to evoke nostalgia without modern gloss.

| Guideline | Details | Rationale |
|-----------|---------|-----------|
| **Color Palette** | Base: Dark forests (#1A2A1A to #4A5A3A), accents: Warlord-specific (e.g., Yeti icy blues #A0C0E0). UI: Muted grays (#404040-#808080) + neon pops for CTAs (#FFAA00). Limit 256 colors total. | Fits pixel constraints; thematic cryptid mystery; scales to larger screens without washout.
 |
| **Typography** | Pixel fonts (Press Start 2P at 12-24px base). Uppercase for status; bold ranks on cards. | Legible at 375px; retro punch without overwhelming small screens. |
| **Spacing & Scale** | Base unit: 8px grid. Touch targets: 48x48px min. Whitespace: 16-32px margins. | Mobile thumb-friendly; consistent hierarchy. |
| **Animations** | Subtle: 4-8 frame cycles (e.g., avatar emote swaps, card flip 180° rotate). Easing: Step-wise for pixel snap. | 60fps perf; enhances feedback without distraction. |
| **Breakpoints** | 375x767 base. `@media (min-width: 481px)`: +20% icon sizes, +10px padding. `@media (min-width: 769px)`: Max 800px centered, subtle glows. No layout shifts—scale proportionally. | Progressive enhancement; portrait lock preserves flow. |
| **Accessibility** | Alt text on sprites; colorblind suits (shape diffs); high-contrast mode toggle. | Inclusive casual play. |


## Content and Assets

This section documents all visual and audio assets required for Bigfoot War, including specifications, formats, organization, and production guidelines. All assets follow the retro SNES 32-bit pixel art aesthetic with limited color palettes and pixel-perfect rendering.

### Overview

**Asset Philosophy:**
- Retro SNES 32-bit pixel art aesthetic
- Limited color palettes (15-20 colors per sprite, 256 colors total)
- Pixel-perfect rendering (no anti-aliasing)
- High contrast for mobile readability (4.5:1 minimum)
- Minimal file sizes for web/mobile performance

**Total Asset Counts:**
- Warlord Assets: ~500-600 individual sprites (avatars, heroes, emotes, icons)
- Card Assets: ~80-100 base assets (frames, ranks, suits, backs)
- Battle Item Assets: 59 item icons
- UI Assets: ~50-100 icons, buttons, overlays
- Sound Assets: ~80-100 sound files
- Total Images: ~700-900 individual assets (before optimization/sprites)
- Total Audio: ~80-100 sound files (<1MB total bundle)

**File Size Targets:**
- Individual sprites: <10KB each (optimized PNG)
- Sound effects: <50KB each (OGG/MP3, 128kbps mono)
- Background music: <200KB (compressed loop)
- Total asset bundle: <5MB (optimized, compressed)

### Bigfoot Warlords

The game features 59 unique Bigfoot Warlords, each requiring multiple asset types for avatars, hero images, emotes, special icons, and sounds.

#### Warlord Avatar Assets

**Base Portrait:**
- Size: 100x120px pixel sprite
- Format: PNG-8 or PNG-24 with transparency
- Style: Retro SNES 32-bit pixel art
- Color palette: 15-20 colors per sprite
- Usage: Pre-game screen, in-game display, Warlord selection galleries
- Total: 59 base portraits (one per Warlord)

**Avatar Specifications:**
- Bit depth: 8-bit (256 colors max)
- Dithering: Enabled for smooth gradients
- Anti-aliasing: Disabled (pixel-perfect)
- Export: PNG with alpha channel
- Naming: `warlord-{id}-{name}-avatar.png` (e.g., `warlord-01-sasquatch-avatar.png`)

#### Warlord Hero Images

**Hero Image:**
- Size: 200x240px full-body pixel sprite
- Format: PNG-8 or PNG-24 with transparency
- Style: Full-body character sprite (more detailed than avatar)
- Usage:
  - Card overlays: 40x60px (deck cards) / 50x75px (battle zone cards)
  - Details overlay: Full 200x240px display
  - Warlord galleries: Thumbnail views
- Total: 59 hero images (one per Warlord)

**Hero Image Specifications:**
- Aspect ratio: 5:6 (200x240px)
- Color palette: 15-20 colors per sprite
- Export: PNG with alpha channel
- Naming: `warlord-{id}-{name}-hero.png`

#### Warlord Emote System

**Emote Variants:**
The game uses a modular emote system where head sprites are swapped to show different emotional states.

**Emote Types:**
1. **Neutral** (default): Standard expression
2. **Joyful/Victory**: Win state, celebration
3. **Defeated/Loss**: Loss state, dejected
4. **Smug/Confident**: Special ready, confident
5. **Angry/Aggressive**: Low HP, aggressive

**Modular Approach:**
- Base body sprite: Shared across emotes
- Swappable head sprites: Different expressions per emote
- Efficiency: Reduces asset count from 295 (59 × 5) to ~118 (59 bodies + 59 heads × 5 variants)

**Emote Specifications:**
- Head sprite size: Variable (matches avatar proportions)
- Format: PNG with transparency
- Export: Separate head sprites for modular swapping
- Naming: `warlord-{id}-{name}-emote-{type}.png` (e.g., `warlord-01-sasquatch-emote-joyful.png`)

**Emote Animation:**
- Frame count: 1-2 frames per emote (subtle animation)
- Duration: 2-3 seconds per emote cycle
- Trigger: Based on game state (win, loss, special ready, low HP)

#### Warlord Special Visual Effects

**Special Activation Icons:**
- Size: 24x24px pixel icons
- Format: PNG with transparency
- Types:
  - Suit icons: Hearts ♥, Diamonds ♦, Clubs ♣, Spades ♠ (4 shared icons)
  - Warlord Power icons: Unique per Warlord (59 unique icons)
- Total: 4 suit icons + 59 power icons = 63 special icons

**Icon Specifications:**
- Style: Pixel art matching game aesthetic
- Color: Suit colors (red for Hearts/Diamonds, black for Clubs/Spades)
- Glow effects: Pulsing glow for ready specials
- Naming: `icon-suit-{suit}.png` (e.g., `icon-suit-hearts.png`) and `warlord-{id}-{name}-power-icon.png`

#### Warlord Color Palettes

**Per-Warlord Color Schemes:**
Each Warlord has a unique color palette (15-20 colors) that defines their visual identity.

**Palette Structure:**
- Base colors: Primary character colors (skin, fur, clothing)
- Accent colors: Power effects, glows, special highlights
- Background colors: Subtle background elements

**Example Palettes:**
- **Yeti:** Icy blues (#A0C0E0), white (#FFFFFF), dark blue (#2A4A6A)
- **Skunk Ape:** Greens (#4A6A4A), browns (#6A4A2A), dark green (#2A4A2A)
- **Sasquatch:** Browns (#5A4A3A), dark brown (#3A2A1A), forest green (#2A4A2A)

**Palette Documentation:**
- Each Warlord's palette documented in asset reference
- Color values in hex format (#RRGGBB)
- Accessibility: High contrast ratios (4.5:1+)

#### Warlord Sound Assets

**Per-Warlord Sounds:**
Each Warlord has thematic sound effects for special activations.

**Sound Types:**
- Special activation sounds: Thematic to Warlord (e.g., Yeti = ice crackle, Skunk Ape = poison hiss)
- Power activation sounds: Unique per Warlord Power
- Emote sounds: Victory cry, defeat groan

**Sound Specifications:**
- Format: OGG Vorbis (primary), MP3 (fallback)
- Bitrate: 128kbps mono
- Sample rate: 44.1kHz
- Bit depth: 8-12 bits (for retro feel)
- File size: <50KB per sound
- Duration: 1-3 seconds per sound

**Total Sounds:**
- Special sounds: ~59-118 files (1-2 per Warlord)
- Power sounds: 59 files (one per Warlord Power)
- Emote sounds: 59 files

**Naming:** `sound-warlord-{id}-{name}-{type}.ogg` (e.g., `sound-warlord-01-sasquatch-special.ogg`)

### Cards and Decks

Cards are the primary gameplay element, requiring base frames, rank displays, suit icons, card backs, jokers, and hero image overlays.

#### Card Base Assets

**Card Frame Template:**
- Size: 80x120px (deck cards) / 100x150px (battle zone cards)
- Format: Canvas-rendered or sprite template
- Style: Retro pixel art card frame
- Suit-specific colors:
  - Hearts: Red frame (#CC0000)
  - Diamonds: Red frame (#CC0000)
  - Clubs: Black frame (#000000)
  - Spades: Black frame (#000000)

**Card Frame Structure:**
- Background: Suit-colored frame
- Border: 2-3px pixel border
- Center area: Rank display area
- Top area: Hero image overlay area
- Bottom area: Suit icon area

**Rendering:**
- Cards are canvas-rendered using programmatic generation
- Single template generates all card variants dynamically

#### Card Rank Assets

**Rank Display:**
- Ranks: Ace, King, Queen, Jack, 10, 9, 8, 7, 6, 5, 4, 3, 2
- Size: 32px bold (deck cards) / 40px bold (battle zone cards)
- Format: Pixel font rendering using Press Start 2P font
- Style: Bold pixel font
- Color: High contrast (white/black) for readability

#### Card Suit Icons

**Suit Symbols:**
- Hearts: ♥ (red)
- Diamonds: ♦ (red)
- Clubs: ♣ (black)
- Spades: ♠ (black)

**Suit Icon Specifications:**
- Size: Variable (scales with card size)
- Format: PNG sprite icons
- Style: Pixel art matching game aesthetic
- Colors:
  - Hearts/Diamonds: Red (#CC0000)
  - Clubs/Spades: Black (#000000)

**Accessibility:**
- Shape differences: Each suit has distinct shape for colorblind support
- Hearts: Rounded top, pointed bottom
- Diamonds: Diamond shape
- Clubs: Three-leaf clover shape
- Spades: Pointed top, rounded bottom

**Total:** 4 suit icon sprites

#### Card Back Design

**Card Back:**
- Design: Generic retro pixel art pattern (no Warlord avatar)
- Size: 80x120px / 100x150px
- Format: Single sprite
- Style: Retro card back pattern (e.g., geometric pattern, Bigfoot-themed design)
- Color: Dark background with subtle pattern

**Card Back Specifications:**
- Pattern: Subtle, non-distracting design
- Colors: Dark tones matching game aesthetic
- Export: PNG sprite
- Naming: `card-back.png`

**Usage:** All cards use same back design (no Warlord-specific backs).

#### Joker Cards

**Joker Design:**
- Visual: Wild swirl pattern (distinctive, eye-catching)
- Size: 80x120px / 100x150px
- Format: Unique sprite
- Style: Retro pixel art with wild/swirl pattern
- Color: Vibrant colors (e.g., purple, gold, or multicolor)

**Joker Specifications:**
- Pattern: Swirl/wild pattern (distinctive from regular cards)
- Export: PNG sprite
- Naming: `card-joker.png`

**Total:** 1 Joker sprite

#### Hero Image Overlays

**Hero Sprites on Cards:**
- Size: 40x60px (deck cards) / 50x75px (battle zone cards)
- Source: Extracted/cropped from Warlord hero images (200x240px)
- Format: PNG with transparency
- Position: Top-center of card
- Style: Pixel art character sprite overlay

**Hero Overlay Specifications:**
- Extraction: Crop/resize from full hero image (200x240px)
- Aspect ratio: Maintained (2:3 ratio)
- Export: Programmatic extraction from hero images
- Naming: Reuse hero images with scaling (no separate overlay files)

**Total:** 59 hero overlays (one per Warlord, reused from hero images)

#### Card Animation Assets

**Card Flip Animation:**
- Type: 180° rotation animation
- Duration: 300ms
- Easing: Step-wise for pixel snap
- Frames: Smooth rotation animation

**Card Slide Animation:**
- Type: Slide path animation (to deck position)
- Duration: 400ms
- Path: Curved path from battle zone to deck indicator
- Easing: Ease-out

**Card Capture Animation:**
- Type: Slide + fade animation
- Duration: 400ms
- Effect: Cards slide to winner's deck, fade slightly

**Animation:**
- Card animations are canvas-rendered using programmatic animation
- Smooth rotation and slide animations generated dynamically

### Battle Items

The game features 59 unique Battle Items, each requiring icon assets and visual effects.

#### Battle Item Icons

**Item Icons:**
- Size: 24x24px (menu/UI) / 120x80px (details overlay)
- Format: PNG with transparency
- Style: Pixel art matching game aesthetic
- Total: 59 item icons (one per Battle Item)

**Icon Specifications:**
- Bit depth: 8-bit (256 colors max)
- Color palette: 10-15 colors per icon
- Style: Retro SNES pixel art
- Export: PNG-8 with alpha channel
- Naming: `item-{id}-{name}.png` (e.g., `item-01-moss-cloak.png`)

**Icon Design Guidelines:**
- Clear, recognizable design
- Distinctive silhouette
- Thematic to item effect (e.g., Moss Cloak = green cloak icon)
- High contrast for small size (24x24px)

#### Battle Item Card Assets

**Item Cards:**
- Size: 120x80px
- Layout: Icon + name + description text
- Format: Canvas-rendered using programmatic generation
- Style: Pixel art card matching game aesthetic

**Card Structure:**
- Icon: 24x24px (left side)
- Name: Pixel text (14px)
- Description: Pixel text (12px, wrapped)
- Cost: Gold amount displayed when purchasable
- Status badges: Locked, owned, equipped indicators

#### Battle Item Visual Effects

**Item Activation Effects:**
- Equipped indicator: Glow effect or badge
- Status indicators: Locked (grayed), available (normal), owned (checkmark), equipped (glow)
- Visual feedback: Brief animation on equip/unequip

**Effect Specifications:**
- Glow: Subtle pulsing glow (2s cycle)
- Badges: 16x16px status badges
- Animation: Fade in/out on state change

### UI Elements

UI elements include menu icons, status badges, button templates, overlay components, HP bars, and deck indicators.

#### Menu Icons

**Menu Icon Set:**
- Game Menu icon: 32x32px (hamburger or gear)
- Statistics icon: 24x24px
- Challenges icon: 24x24px
- Leaderboards icon: 24x24px
- Collection icon: 24x24px
- Settings icon: 24x24px
- About icon: 24x24px
- Close button: 32x32px
- Back button: 32x32px

**Icon Specifications:**
- Format: PNG with transparency
- Style: Pixel art matching game aesthetic
- Color: Muted grays (#404040-#808080) with neon accents (#FFAA00)
- Naming: `icon-{name}.png` (e.g., `icon-menu.png`)

**Total:** ~10-15 menu icons

#### Status Badges

**Status Badge Set:**
- Locked badge: 16x16px (lock icon, grayed)
- Defeated badge: 16x16px (checkmark, green)
- New badge: 16x16px (glow effect, yellow)
- Complete badge: 16x16px (checkmark, gold)
- Notification badge: 16x16px (red circle with count)

**Badge Specifications:**
- Format: PNG with transparency
- Style: Simple pixel art icons
- Colors: Status-appropriate (gray, green, yellow, gold, red)
- Naming: `badge-{status}.png`

**Total:** ~5-10 status badges

#### Button Templates

**Button Assets:**
- Primary CTA template: 300x60px
- Secondary CTA template: 200x48px
- Tertiary CTA template: Smaller variants
- Button states: Normal, hover, active, disabled

**Button Specifications:**
- Format: Canvas-rendered using programmatic generation
- Style: Pixel art buttons with pixel borders
- Colors: Yellow glow (#FFAA00) for primary, muted for secondary
- States: Visual variants for each state (normal, hover, active, disabled)
- Glow effect: Pulsing yellow glow for primary CTA
- Text overlay: Dynamic text rendered on button template

**Total:** 1 button template with multiple states

#### Overlay Components

**Overlay Assets:**
- Overlay backdrop: Semi-transparent dark pattern
- Modal frame: Border/frame design
- Scrollbar: Pixel art scrollbar (16x16px thumb)
- Progress bars: Challenge/XP progress indicators

**Overlay Specifications:**
- Backdrop: 50% opacity dark overlay (CSS or sprite)
- Modal frame: Pixel art border (8-16px border)
- Scrollbar: Minimal pixel art design
- Progress bars: Segmented pixel bars

**Total:** ~5-10 overlay components

#### HP Bar Assets

**HP Bar Components:**
- HP bar frame: 200x20px
- HP bar fill: Red (damage) / Green (healing) / Yellow (low HP)
- Format: Canvas-rendered segmented pixel bar
- Style: Pixel art segmented bar design
- Animation: Smooth fill/deplete transitions
- Colors: Red (#CC0000), green (#00CC00), yellow (#FFAA00)
- Rendering: Programmatic fill based on HP percentage

**Total:** 1 HP bar template

#### Deck Indicator Assets

**Deck Indicator Components:**
- Deck stack icon: Pixel art card stack visualization
- Card count text: Pixel font rendering
- Pulse animation: Low deck warning (<10 cards)

**Deck Indicator Specifications:**
- Size: 150x40px
- Format: Canvas-rendered using programmatic generation
- Style: Pixel art stack + count text
- Animation: Pulse effect when deck < 10 cards
- Rendering: Programmatic stack visualization + count

**Total:** 1 deck indicator template

### Particle Effects and Animations

Particle effects and animations provide visual feedback for game events, specials, and player actions.

#### Win/Loss Effects

**Win Effects:**
- Pixel bursts: 8x8px sparks (multiple particles)
- Victory particles: Explosion pattern
- Gold gain popup: "+X Gold" text animation
- XP gain popup: "+Y XP" text animation

**Loss Effects:**
- Damage flash: Red flash overlay
- HP deplete animation: Smooth bar deplete

**Effect Specifications:**
- Format: Canvas-rendered particles
- Style: Minimal pixel bursts
- Colors: Gold/yellow (win), red (loss)
- Duration: 500ms-2s per effect

**Total:** ~5-10 effect types

#### Damage Effects

**Damage Visuals:**
- HP flash: Damage flash overlay (red tint)
- Damage number popup: "-X Damage" text animation
- Critical hit effect: Enhanced flash/particles

**Effect Specifications:**
- Format: Canvas-rendered
- Style: Pixel text + flash overlay
- Animation: Fade in/out, slide up
- Duration: 1-2 seconds

**Total:** ~3-5 damage effect types

#### Special Activation Effects

**Special Effects:**
- Heal glow: Green glow effect (Hearts specials)
- Damage flash: Red flash effect (Clubs/Spades specials)
- Armor effect: Shield visual (defensive specials)
- DoT effect: Poison/curse visual (debuff specials)
- Status effect indicators: Icons for buffs/debuffs

**Effect Specifications:**
- Format: Canvas-rendered
- Style: Thematic to special type
- Duration: 1-3 seconds per effect
- Colors: Thematic (green heal, red damage, etc.)

**Total:** ~10-15 special effect types

#### Streak Effects

**Streak Visuals:**
- Streak counter popup: "+1" icon animation
- Streak multiplier display: "1.5x", "2x", "2.5x" text
- Streak glow: Pulsing border effect

**Effect Specifications:**
- Format: Canvas-rendered
- Style: Pixel text + glow effect
- Animation: Pulse, fade in/out
- Duration: 2-3 seconds

**Total:** ~3-5 streak effect types

### Backgrounds and Environments

Background assets provide the visual foundation for the game table and overlays.

#### Game Table Background

**Background Pattern:**
- Base: Dark forest green gradient (#1A2A1A to #4A5A3A)
- Texture: Dithering pattern overlay
- Format: CSS linear gradient
- Size: Responsive (375x767px base, scales proportionally)
- Colors: Dark forest greens
- Style: Retro pixel art aesthetic

#### Status Banner Background

**Banner Background:**
- Color: Semi-transparent wood (#3A2A1A)
- Format: CSS background-color with opacity
- Size: 375x77px
- Opacity: 80-90% transparency
- Style: Wood texture pattern overlay

#### Overlay Backgrounds

**Overlay Backdrops:**
- Dim overlay: 50% opacity dark overlay (black, rgba(0,0,0,0.5))
- Modal backgrounds: Dark semi-transparent patterns
- Format: CSS rgba() overlay
- Color: Black with 50% opacity
- Style: Simple dark overlay

### Typography

Typography assets include pixel fonts for UI text, card ranks, and status messages.

#### Pixel Fonts

**Primary Font:**
- Font: Press Start 2P (Google Fonts)
- Sizes: 12px, 14px, 16px, 18px, 20px, 24px, 32px, 40px, 48px
- Weights: Regular, Bold
- Usage: UI text, card ranks, status messages, button labels

**Font Specifications:**
- Format: WOFF2 (primary), WOFF (fallback), TTF (fallback)
- Loading: Preload critical fonts
- Fallback: System pixel fonts (monospace)
- Subsetting: Include only required characters

**Font Loading Strategy:**
- Preload: Critical fonts (Press Start 2P) on page load
- Fallback: System monospace fonts during load
- Font-display: swap (show fallback immediately, swap when loaded)

**Total:** 1-2 font families

### Color Palettes

Color palettes define the visual identity of the game and ensure consistency across assets.

#### Base Color Palette

**Forest Backgrounds:**
- Dark green: #1A2A1A
- Medium green: #4A5A3A
- Light green: #6A8A6A (accents)
- Gradients: Smooth transitions between greens

**UI Colors:**
- Muted grays: #404040 to #808080
- Neon CTA: #FFAA00 (yellow)
- Status colors:
  - Success: #00CC00 (green)
  - Warning: #FFAA00 (yellow)
  - Error: #CC0000 (red)
  - Info: #0088CC (blue)

#### Suit Colors

**Card Suit Colors:**
- Hearts: Red (#CC0000)
- Diamonds: Red (#CC0000)
- Clubs: Black (#000000)
- Spades: Black (#000000)

**Accessibility:**
- Shape differences: Each suit has distinct shape
- High contrast: 4.5:1+ contrast ratios
- Colorblind support: Shape-based differentiation

#### Warlord-Specific Palettes

**Per-Warlord Color Schemes:**
Each of the 59 Warlords has a unique color palette (15-20 colors) documented in the asset reference.

**Palette Structure:**
- Base colors: Primary character colors
- Accent colors: Power effects, glows
- Background colors: Subtle background elements

**Documentation:**
- Each Warlord's palette documented with hex values
- Color accessibility checked (4.5:1+ contrast)
- High contrast mode variants documented

### Sound Assets

Sound assets provide audio feedback for gameplay events, specials, and UI interactions. See the Sound Design section for detailed specifications.

#### Core Sound Effects

**Gameplay Sounds:**
- Card flip: <50KB, crisp chiptune flip sound
- Card capture: <50KB, card slide sound
- Win sound: <50KB, triumphant jingle
- Loss sound: <50KB, defeat sound
- War trigger: <50KB, dramatic sound

**Total:** ~5-10 core gameplay sounds

#### Special Sounds

**Special Activation Sounds:**
- Suit specials: 4 sounds (one per suit)
- Warlord Powers: 59 sounds (one per Warlord)
- Total: ~60-70 special sounds

#### UI Sounds

**Interface Sounds:**
- Button tap: <50KB, subtle click
- Menu open/close: <50KB, whoosh sound
- Overlay whoosh: <50KB, transition sound
- Notification chime: <50KB, brief chime

**Total:** ~5-10 UI sounds

#### Background Music

**Ambient Music:**
- Background loop: <200KB, compressed OGG/MP3
- Format: 128kbps mono
- Duration: 2-3 minute loop
- Style: Retro chiptune, ambient

**Total:** 1-2 background music loops

**Cross-Reference:** See Sound Design section for detailed sound specifications, optimization strategies, and implementation guidelines.

### Asset Organization

Assets are organized in a structured file system for efficient loading, management, and development workflow.

#### File Structure

```
/assets
  /warlords
    /avatars (59 files: warlord-{id}-{name}-avatar.png)
    /heroes (59 files: warlord-{id}-{name}-hero.png)
    /emotes (295 files: warlord-{id}-{name}-emote-{type}.png)
    /power-icons (59 files: warlord-{id}-{name}-power-icon.png)
    /sounds (59-118 files: sound-warlord-{id}-{name}-{type}.ogg)
  /cards
    /frames (4 suit variants + 1 back + 2 jokers = 7 files)
    /suits (4 icons: icon-suit-{suit}.png)
    /ranks (font-based rendering)
  /battle-items
    /icons (59 files: item-{id}-{name}.png)
  /ui
    /icons (10-15 files: icon-{name}.png)
    /badges (5-10 files: badge-{status}.png)
    /buttons (canvas-rendered templates)
    /overlays (canvas-rendered components)
  /effects
    /particles (canvas-rendered)
    /animations (canvas-rendered)
  /backgrounds
    /patterns (CSS gradients)
  /fonts
    /pixel-fonts (1-2 WOFF2 files)
  /sounds
    /sfx (80-100 files: sound-{category}-{name}.ogg)
    /music (1-2 loops: music-background.ogg)
```

#### Naming Conventions

**Warlord Assets:**
- Format: `warlord-{id}-{name}-{type}.png`
- Example: `warlord-01-sasquatch-avatar.png`
- ID: Zero-padded 2-digit number (01-59)
- Name: Lowercase, hyphenated (sasquatch, skunk-ape)

**Card Assets:**
- Format: Programmatic generation (no sprite files)
- Back: `card-back.png`
- Joker: `card-joker.png`

**Battle Item Assets:**
- Format: `item-{id}-{name}.png`
- Example: `item-01-moss-cloak.png`
- ID: Zero-padded 2-digit number (01-59)
- Name: Lowercase, hyphenated

**UI Assets:**
- Format: `icon-{name}.png` or `badge-{status}.png`
- Example: `icon-menu.png`, `badge-locked.png`

**Sound Assets:**
- Format: `sound-{category}-{name}.ogg`
- Example: `sound-gameplay-card-flip.ogg`, `sound-warlord-01-sasquatch-special.ogg`

#### Asset Formats

**Images:**
- Format: PNG-8 or PNG-24 with transparency
- Bit depth: 8-bit (256 colors max)
- Compression: Lossless PNG compression
- Optimization: PNG optimization applied

**Sounds:**
- Primary: OGG Vorbis (.ogg)
- Fallback: MP3 (.mp3)
- Bitrate: 128kbps mono
- Sample rate: 44.1kHz
- Bit depth: 8-12 bits (for retro feel)

**Fonts:**
- Primary: WOFF2 (.woff2)
- Fallback: WOFF (.woff), TTF (.ttf)
- Subsetting: Include only required characters

#### Asset Compression

**Image Optimization:**
- PNG optimization: Reduce file size without quality loss
- Sprite sheets: Combine multiple sprites into single sheets
- Target: <10KB per sprite (optimized)

**Sound Optimization:**
- OGG compression: 128kbps mono
- Bitcrushing: 8-12 bits for retro feel
- Duration: Keep sounds short (1-3 seconds)
- Target: <50KB per sound effect, <200KB for music

**Total Bundle Size:**
- Target: <5MB total (optimized, compressed)
- Loading: Lazy load non-critical assets
- Preload: Critical assets (core gameplay sounds, fonts)

### Asset Production Pipeline

Asset production follows a structured pipeline from creation to implementation.

#### Creation Tools

**Pixel Art:**
- Aseprite: Professional pixel art editor
- Piskel: Free online pixel art editor
- Photoshop: Advanced editing with pixel art plugins

**Sound:**
- Bfxr: Free chiptune sound generator
- ChipTone: Free chiptune sound generator
- Audacity: Audio editing and compression

**Animation:**
- Aseprite: Frame-based animation
- After Effects: Advanced animation

**Compression:**
- ImageOptim: PNG optimization
- TinyPNG: Online PNG compression
- Audacity: Sound compression and bitcrushing

#### Export Settings

**Images:**
- Bit depth: 8-bit (256 colors max)
- Format: PNG-8 or PNG-24 (with transparency)
- Dithering: Enabled for smooth gradients
- Anti-aliasing: Disabled (pixel-perfect)
- Compression: Lossless PNG compression

**Sounds:**
- Format: OGG Vorbis (primary), MP3 (fallback)
- Bitrate: 128kbps mono
- Sample rate: 44.1kHz
- Bit depth: 8-12 bits (for retro feel)
- Duration: 1-3 seconds per sound

#### Quality Assurance

**Image Checks:**
- Pixel-perfect rendering (no anti-aliasing)
- Color palette compliance (15-20 colors per sprite)
- Transparency handling (alpha channel)
- Size accuracy (exact pixel dimensions)
- File size (<10KB per sprite)

**Sound Checks:**
- File size (<50KB per sound effect)
- Playback compatibility (test in browsers)
- Volume normalization (consistent levels)
- Mobile performance (test on devices)

**Asset Validation:**
- Naming convention compliance
- File format correctness
- Size and dimension accuracy
- Color palette compliance
- Performance impact assessment

### Asset Totals and Inventory

Complete inventory of all assets required for the game.

#### Asset Count Summary

**Warlord Assets:**
- Base avatars: 59
- Hero images: 59
- Emote variants: 295 (59 bodies + 295 head sprites)
- Special icons: 63 (4 suit icons + 59 power icons)
- Sounds: 59-118

**Card Assets:**
- Card frames: 7 (4 suits + 1 back + 2 jokers)
- Suit icons: 4
- Rank displays: Font-based rendering
- Hero overlays: 59 (reused from hero images)

**Battle Item Assets:**
- Item icons: 59

**UI Assets:**
- Menu icons: ~10-15
- Status badges: ~5-10
- Button templates: ~5-10 (or 1 template with states)
- Overlay components: ~5-10
- HP bar: 1 template (or ~10 heart sprites)
- Deck indicator: 1 template

**Effect Assets:**
- Particle effects: ~10-20 types (canvas-rendered)
- Animation sequences: ~5-10 (canvas-rendered)

**Sound Assets:**
- Core SFX: ~10-15
- Special sounds: ~60-70
- UI sounds: ~5-10
- Background music: 1-2 loops
- Total: ~80-100 sound files

**Font Assets:**
- Pixel fonts: 1-2 font families

#### File Size Estimates

**Image Assets:**
- Individual sprites: <10KB each (optimized)
- Total images: ~700-900 individual assets
- Estimated total: ~5-7MB (before optimization)
- Optimized total: ~2-3MB (after compression)

**Sound Assets:**
- Individual sounds: <50KB each
- Background music: <200KB per loop
- Total sounds: ~80-100 files
- Estimated total: ~3-4MB (before optimization)
- Optimized total: ~1-2MB (after compression)

**Font Assets:**
- Font files: ~50-100KB each
- Total fonts: 1-2 files
- Estimated total: ~100-200KB

**Total Asset Bundle:**
- Estimated: ~8-11MB (before optimization)
- Optimized: ~3-5MB (after compression)
- Target: <5MB total bundle

#### Loading Priorities

**Critical (Preload):**
- Core gameplay sounds (card flip, win, loss)
- Primary font (Press Start 2P)
- Default Warlord assets (Sasquatch)
- Card frame templates
- UI icons (menu, buttons)

**High Priority (Load Early):**
- All Warlord avatars
- Card suit icons
- Battle Item icons
- UI badges and overlays

**Medium Priority (Lazy Load):**
- Warlord hero images
- Warlord emote variants
- Special sound effects
- Particle effects

**Low Priority (Load on Demand):**
- Warlord-specific sounds
- Background music
- Advanced particle effects
- Unlocked content assets

#### Optimization Targets

**Performance Goals:**
- Initial load: <2MB (critical assets only)
- Full load: <5MB (all assets)
- Load time: <3 seconds on 3G connection
- Frame rate: 60fps during gameplay
- Memory usage: <50MB on mobile devices

**Optimization Strategies:**
- Sprite sheets: Combine related sprites
- Lazy loading: Load assets on demand
- Compression: Optimize all assets
- Caching: Cache assets in browser
- CDN: Use CDN for asset delivery



## Sound Design

Bigfoot War uses a minimalist sound design with short, evocative chiptune cues (1-3 second loops) that evoke cryptid mystery and card battle excitement. Sound design includes subtle howls for Warlord specials, crisp "flip" sounds for draws, and triumphant jingles for streaks.

### Sound Assets

#### Core Sound Effects

**Card Draw Sounds:**
- `card-flip.ogg`: Crisp chiptune card flip sound (plays on card draw)
- `card-shuffle.ogg`: Card riffle shuffle sound (plays on Joker draw or reshuffle)
- `card-capture.ogg`: Brief capture sound (plays when cards are captured)

**Gameplay Sounds:**
- `win.ogg`: Triumphant jingle (plays on turn win)
- `loss.ogg`: Low rumble sound (plays on turn loss)
- `war-trigger.ogg`: Dramatic chiptune (plays when War scenario triggers)
- `war-resolve.ogg`: Resolution sound (plays when War resolves)

**Damage Sounds:**
- `damage-hit.ogg`: Impact sound (plays on damage dealt)
- `damage-critical.ogg`: Enhanced impact sound (plays on critical hits)
- `heal.ogg`: Positive chime (plays on healing)

**UI Sounds:**
- `button-click.ogg`: Subtle click sound (plays on button interactions)
- `overlay-open.ogg`: Subtle whoosh sound (plays on overlay open)
- `overlay-close.ogg`: Subtle whoosh sound (plays on overlay close)
- `notification.ogg`: Brief notification chime (plays on notifications)

**Special Activation Sounds:**
- `special-hearts.ogg`: Thematic sound for Hearts specials (healing/sustain theme)
- `special-diamonds.ogg`: Thematic sound for Diamonds specials (utility/Gold theme)
- `special-clubs.ogg`: Thematic sound for Clubs specials (physical damage theme)
- `special-spades.ogg`: Thematic sound for Spades specials (ranged damage theme)
- `special-warlord.ogg`: Powerful climax sound (plays on Warlord Power activation)

**Streak Sounds:**
- `streak-3.ogg`: Milestone sound (plays at 3-win streak)
- `streak-5.ogg`: Enhanced milestone sound (plays at 5-win streak)
- `streak-10.ogg`: Triumphant milestone sound (plays at 10-win streak)
- `streak-break.ogg`: Brief "break" sound (plays when streak breaks)

**Game End Sounds:**
- `victory.ogg`: Extended fanfare (plays on game win)
- `defeat.ogg`: Defeat sound (plays on game loss)
- `level-up.ogg`: Extended fanfare (plays on level up)
- `unlock.ogg`: Thematic chiptune (plays on Warlord unlock)

**Warlord-Specific Sounds:**
- Each Warlord may have 1-2 unique sounds for their special abilities
- Total: ~59 Warlord-specific sounds (one per Warlord)
- Examples: Skunk Ape poison sound, Yeti avalanche sound, Quantum Sasquatch glitch sound

**Background Music:**
- `bgm-main.ogg`: Main game loop (ambient, subtle, loops continuously)
- `bgm-menu.ogg`: Menu music (subtle background)

**Total Sound Assets:**
- Core effects: ~15 sounds
- Special sounds: ~60-70 sounds (4 suits + Warlord Powers + Warlord-specific)
- UI sounds: ~5-10 sounds
- Background music: 1-2 loops
- **Total: ~80-100 sound files**

#### Sound Event Mapping

**Card Draw Phase:**
- `card-flip.ogg` (both players draw simultaneously)

**Joker Draw:**
- `card-shuffle.ogg` (immediate shuffle)
- `card-flip.ogg` (card reveal)

**Turn Resolution:**
- `win.ogg` OR `loss.ogg` (based on outcome)
- `card-capture.ogg` (cards captured)

**War Scenario:**
- `war-trigger.ogg` (War initiated)
- `card-flip.ogg` (face-down cards placed)
- `card-flip.ogg` (face-up cards revealed)
- `war-resolve.ogg` (War resolved)
- `win.ogg` OR `loss.ogg` (outcome)

**Damage Dealt:**
- `damage-hit.ogg` (normal damage)
- `damage-critical.ogg` (critical hits only)

**Healing:**
- `heal.ogg` (any healing effect)

**Special Activation:**
- `special-[suit].ogg` (suit specials)
- `special-warlord.ogg` (Warlord Power)
- Warlord-specific sounds (if applicable)

**Streak Milestones:**
- `streak-3.ogg` (3-win streak)
- `streak-5.ogg` (5-win streak)
- `streak-10.ogg` (10-win streak)
- `streak-break.ogg` (streak broken)

**UI Interactions:**
- `button-click.ogg` (button taps)
- `overlay-open.ogg` (overlay opens)
- `overlay-close.ogg` (overlay closes)
- `notification.ogg` (notifications)

**Game End:**
- `victory.ogg` OR `defeat.ogg` (game outcome)
- `level-up.ogg` (if level up occurs)
- `unlock.ogg` (if Warlord unlocked)

**Background Music:**
- `bgm-main.ogg` (plays continuously during gameplay, loops)
- `bgm-menu.ogg` (plays in menu screens)

#### Sound Mixing and Volume Levels

**Volume Hierarchy:**
- Background music: 30% volume (subtle, non-intrusive)
- Core gameplay sounds: 70% volume (card flips, wins, losses)
- UI sounds: 50% volume (subtle feedback)
- Special sounds: 80% volume (emphasize special moments)
- Warlord Power sounds: 90% volume (climax moments)

**Simultaneous Sound Limits:**
- Maximum 2-4 sounds playing simultaneously
- Background music always plays (doesn't count toward limit)
- Priority: Special sounds > Gameplay sounds > UI sounds
- Older sounds fade out when new sounds play (if at limit)

**Dynamic Effects:**
- Streak sounds: Pitch increases with streak length (via Web Audio API)
- Warlord variety: Pitch varies by Warlord theme (deeper for massive Warlords)
- Damage sounds: Volume scales with damage amount (subtle)

### Optimization Strategies
The game maintains a lightweight audio bundle (under 1MB) for mobile responsiveness:
- **File Efficiency**: Sounds use compressed formats (OGG or MP3, 128kbps mono) with <50KB per sound. Bit depth reduced to 8-12 bits for retro feel, mimicking SNES limitations.
- **Lazy Loading & Preloading**: Sounds load on-demand (specials load when unlocked). Core effects (draw/win/loss) preload during splash screen for instant playback.
- **Performance Tuning**: Simultaneous sounds limited to 2-4 layers. Web Audio API handles dynamic effects (pitch-shifting for streaks) without extra files. Mute enabled by default (stored in localStorage) to respect user preferences and battery.
- **Minimal Layers**: One core synth (square waves for chiptune) per cue. Arpeggios (rapid note sequences) provide energy without complexity. Reverb/echo used only when thematic (faint echo for "misty" Warlords like Fear Liath).
- **Accessibility**: Volume sliders included in Game Menu. Sounds do not autoplay. Audio initialization requires user interaction (iOS compliance).

### Implementation in Next.js
The game uses Web Audio API for audio control. Howler.js provides cross-browser compatibility.

**Audio Context Setup:**
- Audio context initialized in main component (`pages/index.tsx`) on first user tap (Primary CTA) to comply with browser policies
- Core sounds preloaded: draw, win, loss
- Additional sounds loaded on-demand (specials, streaks)

**Sound Integration:**
- Sounds tied to gameplay events: `playSound('special')` on special activation
- Pitch varies for Warlord variety (deeper for massive Warlords like Mono Grande)
- Streaks layer rising arpeggio dynamically via OscillatorNode
- Howler.js API: `const sound = new Howl({ src: ['/sounds/win.ogg'] }); sound.play();`
- Handles mobile quirks (iOS unlocking)

**Retro Effects:**
- Chiptune SFX generated with Bfxr or ChipTone (bitcrushed jumps for wins, low rumbles for losses)
- Specials apply filters: Web Audio's BiquadFilterNode for lo-fi distortion
- Thematic effects match pixel art (e.g., "glitchy" for Quantum Sasquatch via random pitch shifts)

**User Controls & Persistence:**
- Mute toggle in Options overlay, saved to localStorage
- Volume sliders for Music and SFX (separate controls)
- PAID users sync preferences via Prisma
- Settings persist across sessions

#### Accessibility

**Sound Controls:**
- Mute toggle: Available in Game Menu → Settings
- Volume sliders: Separate controls for Music and SFX
- Default: Mute enabled (respects user preferences and battery)
- Auto-save: Preferences saved to localStorage immediately

**Audio Initialization:**
- Audio context initialized on first user interaction (Primary CTA tap)
- Complies with browser autoplay policies (iOS, Chrome, etc.)
- Graceful degradation: Game plays without sound if audio fails

**Visual Alternatives:**
- All sound events have visual feedback (animations, particles)
- Game is fully playable without sound
- No critical information conveyed only through sound

**Mobile Considerations:**
- Sounds do not autoplay (requires user interaction)
- Respects device silent mode (iOS)
- Battery-efficient: Minimal simultaneous sounds
- Network-efficient: Lazy loading of non-critical sounds

## UI and UX

### Main Game Table Layout (375x767 Base)

**Persistent vertical stack** for portrait: Enemy top (oppression), battle center (focus), Player bottom (control). Total safe area ~375w x 700h (notch-aware). Use Flexbox (`flex-direction: column; justify-content: space-between; align-items: center`).

**ASCII Mockup** (proportional to 375x767; scale up evenly):
```
+-----------------------------+  <- Banner (37.5w x 77h | 10%)
|  GAME STATUS: Draw! (24px)  |
+-----------------------------+
|        ENEMY DECK: 36       |  <- Enemy Section (30% h)
|         [HP BAR 100%]       |
|       [AVATAR 100x120px]    |
|                             |
|  [ENEMY CARD SLOT L/R]      |  <- Battle Zone (30% h)
|     [PLAYER CARD SLOT L/R]  |
|                             |
|        PLAYER DECK: 36      |  <- Player Section (30% h)
|         [HP BAR 100%]       |
|       [AVATAR 100x120px]    |
|                             |
|        [MENU ICON]          |  <- Bottom Bar (10% h)
|     [PRIMARY CTA 300x60px]  |  <- Thumb-center
+-----------------------------+
```

- **Proportions**: Top 20% Enemy, Middle 30% Battle, Bottom 40% Player+CTA (thumb bias).
- **Zoning**: 80% gameplay visible; overlays dim background 50% opacity.
- **Battle Zone Cards**: 100x150px for enhanced hero visibility. In War scenarios (6 cards), cards scale down to 80x120px or stack to fit within battle zone.
- **Larger Screens**: Icons +25% size, padding +50%; avatars 120x144px at 769px—no reflow. Battle zone cards scale proportionally.

### UI Elements

| Element | Size (375px Base) | Position | Style/Behavior |
|---------|-------------------|----------|---------------|
| **Game Status Banner** | 375x77px | Top-full | Pixel text (20px), marquee scroll if long. Bg: Semi-transparent wood (#3A2A1A). |
| **Warlord Avatar** | 100x120px | Enemy: Top-center; Player: Bottom-center | Pixel sprite; swap emotes (defeated/joyful). Glow on tap (overlay trigger). |
| **HP Bar** | 200x20px | Below avatar | 5-10 pixel hearts or segmented bar (red/green). Animate fill/deplete.  |
| **Deck Indicator** | 150x40px | Avatar sides | Pixel stack + count (16px). Pulse low (<10 cards). |
| **Battle Zone Cards** | 100x150px each | Center: Enemy right (x+120), Player left | Face-up reveal (flip anim). Hero image overlay (50x75px) prominently displayed on rank/suit. Larger size enhances hero visibility and card readability. |
| **Primary CTA (Play/Draw)** | 300x60px | Bottom-center | Bold pixel text (24px), yellow glow pulse. ≥48px touch. |
| **Battle Item Button** | 120x40px | Bottom-left (Pre-Turn only) | Shows if player owns items with remaining charges. Icon + "Item" text. Taps → Battle Item Selection Overlay. |
| **Game Menu Icon** | 32x32px | Bottom-right | Hamburger or gear; taps → full overlay. |
| **Specials Icons** | 5 icons × 48x48px each | Below Player avatar, above Primary CTA | Inline on main board. 4 suit icons (Hearts/Diamonds/Clubs/Spades) + 1 Warlord Power icon. Ready specials: Glow with pulsing animation (color matches suit). Unready specials: Dimmed (50% opacity). Tap ready icon to activate. Tap unready icon shows tooltip with charge progress. Sound: Activation sound on tap. |
| **Enemy Special Notification Overlay** | Compact banner (300x150px) | Center-top | Brief notification showing enemy specials played. Auto-dismisses after 2-3 seconds. Pixel text, semi-transparent background. Sound: Brief notification chime. |
| **Enemy Battle Item Notification** | Compact banner (300x100px) | Center-top | Brief notification showing enemy Battle Item activated (item name + effect). Auto-dismisses after 1-2 seconds. Pixel text, semi-transparent background. Sound: Brief activation chime. |
| **Chain Burst Animation** | Fullscreen effect | Overlay on game table | Explosive visual reveal when chain triggers. Suit/rank icons explode with particles, screen flash, status banner message. Duration: 0.5-1.0 seconds. Sound: Escalating chiptune burst (varies by chain type). |
| **Enemy Chain Notification** | Compact banner (300x100px) | Center-top | Brief notification showing enemy chain triggered (chain type). Auto-dismisses after 1-2 seconds. Pixel text, semi-transparent background. Sound: Brief enemy burst chime. |
| **Overlays** | Fullscreen modal | Centered content | Backdrop blur; e.g., Warlord Select: 3x2 grid thumbs. |

### Inline Specials Icons Details

The Specials Icons are always visible on the main game board, providing immediate visual feedback about special availability without interrupting gameplay flow.

**Visual Design:**
- Pixel art icons matching retro SNES aesthetic
- 5 icons total: 4 suit icons (Hearts, Diamonds, Clubs, Spades) + 1 Warlord Power icon
- Each icon: 48x48px (touch-friendly, matches suit/Warlord theme)
- Position: Below Player Warlord avatar, above Primary CTA (thumb-accessible area)
- Horizontal row layout, centered, 8px spacing between icons

**Ready Specials Display:**
- Icon glows with pulsing animation (color matches suit: red Hearts, blue Diamonds, green Clubs, purple Spades)
- Pulsing animation: 2s cycle, subtle glow effect
- Icon appears at full opacity (100%)
- Visual feedback: Brief flash on activation

**Unready Specials Display:**
- Icon dimmed (50% opacity)
- No glow effect
- Tap icon → Tooltip appears showing charge progress:
  - Suit specials: "X/Y [Suit] captured" (e.g., "3/4 Hearts captured")
  - Warlord Power: "X/Y wins OR X/Y damage" (e.g., "2/5 wins OR 4/8 damage")
- Tooltip auto-dismisses after 2 seconds or on tap elsewhere

**Interaction Patterns:**
- Tap ready special icon → Activates special immediately
- Can activate multiple ready specials (0-2 per turn limit)
- Tap unready special icon → Shows tooltip with charge progress
- No modal overlay interruption - seamless gameplay flow
- Primary CTA updates to "Next Turn" after player wins (player proceeds when ready)

**Sound Cues:**
- Special activation: Thematic sound matching special type (heal, damage, utility)
- Tooltip appear: Subtle chime (when tapping unready special)

**Animation:**
- Ready special glow: Pulsing animation (2s cycle, color matches suit)
- Special activation: Brief visual effect matching special type
- Icon update: Smooth transition when charge threshold reached (dimmed → glowing)

**State Management:**
- Icons update in real-time as charges accumulate
- Charge progress tracked per special (suit charges + Warlord charge)
- Special effects applied immediately on tap
- Charges reset after use (ready → unready transition)

**Accessibility:**
- Touch targets minimum 48x48px (meets accessibility guidelines)
- High contrast icons (ready: glowing, unready: dimmed)
- Clear visual distinction between ready/unready states
- Tooltip provides descriptive text for charge progress

### Chain Burst Animations

Chain bursts trigger with explosive visual effects when chain thresholds are reached. The system is hidden until triggered, creating surprise "wow" moments.

**Visual Design:**
- **Hidden System:** No visible indicator during chain building (prevents gaming the system)
- **Explosive Reveal:** When chain triggers, suit/rank icons explode/flare with color-matched particles
- **Screen Flash:** Brief screen flash (color matches suit or chain type)
- **Status Banner:** "[Chain Type] BURST!" message (e.g., "HEARTS BURST!", "ROYAL FLUSH!", "FULL HOUSE!")
- **Sound:** Escalating chiptune burst sound (varies by chain type and rarity)
- **Visual Intensity:** Scales with chain rarity (Royal Flush = most spectacular)

**Animation Details by Chain Type:**

**Basic Burst (3 same suit):**
- Simple suit icon flash + particles
- Brief screen tint (color matches suit)
- Status banner: "[SUIT] BURST!"
- Sound: Standard burst chime

**Enhanced Burst (4 same suit):**
- Larger flash + more particles
- Stronger screen tint
- Status banner: "ENHANCED [SUIT] BURST!"
- Sound: Enhanced burst chime

**Mega Burst/Flush (5 same suit):**
- Screen-wide flash + particle explosion
- Full screen color wash
- Status banner: "MEGA [SUIT] BURST!"
- Sound: Powerful burst fanfare

**Full House Chain:**
- Two suit icons combine visually
- Dual-color particle effects
- Status banner: "FULL HOUSE!"
- Sound: Harmony burst sound

**Pair Chain:**
- Rank icon multiplies (2 icons appear)
- Rank-matched particle effects
- Status banner: "PAIR OF [RANK]S!"
- Sound: Pair chime

**Three of a Kind Chain:**
- Rank icon triples (3 icons appear)
- Stronger rank-matched effects
- Status banner: "THREE OF A KIND!"
- Sound: Triple chime

**Four of a Kind Chain:**
- Rank icon quadruples (4 icons appear)
- Massive rank-matched explosion
- Status banner: "FOUR OF A KIND!"
- Sound: Quad fanfare

**Straight Chain:**
- Sequential rank icons light up (5 icons in sequence)
- Progressive animation (ranks light up one by one)
- Status banner: "STRAIGHT!"
- Sound: Rising arpeggio

**Straight Flush Chain:**
- Sequential rank icons + suit match animation
- Ultimate particle effects (suit color + sequence)
- Status banner: "STRAIGHT FLUSH!"
- Sound: Ultimate fanfare

**Royal Flush Chain:**
- Crown animation + ultimate particle effects
- Full screen spectacle (most dramatic)
- Status banner: "ROYAL FLUSH!!!"
- Sound: Royal fanfare (longest, most impressive)
- Visual: Crown icon appears above suit icons

**Rainbow Chain:**
- Rainbow particle effects (all 4 suit colors)
- Color cycle animation
- Status banner: "RAINBOW BURST!"
- Sound: Rainbow chime

**Enemy Chain Notifications:**
- Compact banner (300x100px, center-top)
- Brief notification showing enemy chain type
- Auto-dismisses after 1-2 seconds
- Pixel text, semi-transparent background
- Sound: Brief enemy burst chime

**Animation Timing:**
- Burst animation: 0.5-1.0 seconds (varies by chain type)
- Status banner: Appears immediately, fades after 2-3 seconds
- Particle effects: Continue for 1-2 seconds after trigger
- Sound: Matches animation duration

**Accessibility:**
- Visual effects have sound equivalents
- Status banner provides clear text description
- Effects don't block gameplay (non-blocking animations)
- Can be disabled in settings (for motion sensitivity)

## Technical Design

Bigfoot War is built as a lightweight, mobile-first web app using Next.js for server-side rendering and React for interactive components. The core game runs in the browser with minimal server dependencies, leveraging local storage for anonymous play and cloud integration for paid users. Canvas API handles card animations and pixel art rendering for a retro SNES feel. Deployment on Vercel ensures fast global delivery, with Prisma managing any backend data needs. The design prioritizes performance on low-end mobiles (e.g., 60fps draws) and zero-friction entry—no initial auth or installs.

### Architecture Overview

**Technology Stack:**
- **Frontend Framework**: Next.js 14+ (App Router) with React 18+
- **Styling**: Tailwind CSS for responsive, utility-first styling
- **State Management**: Zustand for game state (selector-based subscriptions prevent unnecessary re-renders, critical for 60fps mobile performance)
- **Rendering**: Canvas API for card animations
- **Backend**: Vercel Serverless Functions (API routes)
- **Database**: Vercel Postgres via Prisma ORM (PAID users only)
- **Authentication**: Clerk (PAID users only)
- **Payments**: Stripe Checkout and Payment Intents
- **Ads**: Google AdMob Web SDK
- **Analytics**: Vercel Analytics + PostHog

**Architecture Principles:**
- **Local-First**: Game fully playable offline with local storage
- **Progressive Enhancement**: Cloud features available via PAID upgrade
- **Mobile-First**: Optimized for portrait mobile devices
- **Performance**: Target 60fps, <1MB initial bundle, <3s load time
- **Zero-Friction**: No mandatory login, no app install required

### Architecture
- **Frontend**: Next.js 14+ (App Router) with React 18+. One persistent Game Table component (`/pages/index.tsx`) handles pre/main/post-game via conditional rendering and overlays. Custom modal components (no external library) for overlays. UI: Tailwind CSS for responsive, portrait-locked layouts (media queries enforce vertical stack).
- **Rendering**: Raw Canvas API (no Konva.js, no WebGL) for card draws/flips, avatar reactions, and minimal animations (card slide-ins, health bar fills). Canvas API chosen for minimal bundle size and full control. Pixel art scales via CSS (`image-rendering: pixelated`).
- **Backend**: Vercel serverless functions (API routes) for cloud sync, payments, and ads. No always-on server. Prisma Client for DB interactions in functions.
- **State Management**: Zustand for in-game state (decks, HP, specials). Zustand provides optimal performance for frequent state updates (every turn) and avoids unnecessary re-renders critical for 60fps mobile gameplay. Sync to cloud post-upgrade via API calls.

### Data Storage
- **Local Storage (Default/Anonymous)**: `localStorage` stores preferences (sound, last Warlord). IndexedDB (via `idb-keyval`) stores game data (XP, Gold, unlocks as JSON blobs). Anonymized UUID generated on load (`crypto.randomUUID()`) keys data and tracks analytics. Saves auto on events (win/loss); warns on quota limits.
- **Cloud Storage (Paid Upgrade)**: Vercel Postgres via Prisma ORM stores synced data. Schema:
  ```
  model User {
    id      String @id @default(uuid())
    email   String @unique
    data    Json   // Serialized progress (XP, unlocks, galleries)
    adFree  Boolean @default(true)
  }
  ```
  Migration: On $3.99 purchase, API route migrates local JSON to DB, linking via UUID/email. Bidirectional sync: Pull on load if logged in; push on changes.
- **Assets**: Static pixel art (sprites, emotes) hosted in Next.js public folder (`/public/assets/`). Critical assets (default Warlords) preloaded for offline feel; variants lazy-loaded.

### Authentication and Payments
- **Auth**: No mandatory login. Clerk provides email-based cloud save (magic links post-purchase). Clerk's Next.js SDK checks session on load; if present, fetches/syncs data.
- **Payments**: Stripe handles $3.99 one-time (ad-free + cloud) and Gold IAP. API route creates Checkout session (`/api/checkout`); webhook handles fulfillment (sets adFree, migrates data). Guest payments supported; email captured for receipts/refunds.
- **Ads**: Google AdMob web SDK provides interstitials/rewarded videos (post-game CTAs). Impressions tracked via anonymized events; auto-Gold for paid users.

### Analytics
- **Tracking**: Vercel Analytics tracks basics (sessions, devices). PostHog tracks events (wins, upgrades) tied to local UUID. No PII pre-purchase; emails hashed post-upgrade for cohorts.
- **Events**: Events fire on key flows: `game_start`, `upgrade_prompt_viewed`, `win_streak_5`.

### Performance and Optimization
- **Mobile-First**: Portrait lock via manifest/CSS; breakpoints (320-480px base, up to 769px+). Thumb-optimized CTAs (bottom-center, ≥48px targets).
- **Optimizations**: Code-splitting via Next.js; lazy components for overlays. Canvas offscreen rendering for smooth animations. Bundle size <1MB (pixel art compresses well). Lighthouse target: 90+ mobile score.
- **Offline**: Service worker via Next-PWA caches assets/game logic for brief disconnects; local data ensures playability.
- **Security**: No sensitive local data; HTTPS enforced. API rate-limited for sync to prevent abuse.

### State Management

**Game State Architecture:**
- **Global State**: Zustand store (lightweight, ~1KB bundle, optimal for frequent updates)
- **Rationale**: Zustand's selector-based subscriptions prevent unnecessary re-renders, critical for 60fps mobile performance. Context API would require careful provider splitting to avoid cascading re-renders on every turn update.
- **State Structure**: Hierarchical (App → Game → Turn levels)
- **State Updates**: Immutable updates (prevents bugs, enables time-travel debugging)
- **State Persistence**: Auto-save to localStorage on key events (turn end, game end)

**State Store Structure:**
```typescript
interface GameState {
  // App-level
  appState: 'pre-game' | 'in-game' | 'post-game';
  playerProgress: {
    level: number;
    xp: number;
    gold: number;
    unlockedWarlords: string[];
  };
  
  // Game-level
  gameState: {
    playerWarlord: Warlord;
    enemyWarlord: Warlord;
    playerHP: number;
    enemyHP: number;
    playerDeck: Card[];
    enemyDeck: Card[];
    streak: number;
  };
  
  // Turn-level
  turnState: {
    phase: 'pre-turn' | 'draw' | 'resolution' | 'post-win';
    playerCard: Card | null;
    enemyCard: Card | null;
    winner: 'player' | 'enemy' | null;
  };
}
```

**State Updates:**
- Batched updates for performance (React 18 automatic batching)
- Debounced saves to localStorage (prevents excessive writes)
- Optimistic updates for instant feedback

**State Recovery:**
- Auto-save checkpoints at turn boundaries
- Recovery from corrupted state (fallback to last known good state)
- State validation on load (ensure consistency)

### API Design

**API Routes Structure:**
```
/api/checkout          - Stripe checkout session creation
/api/webhook           - Stripe webhook handler (payment fulfillment)
/api/sync              - Cloud sync (PAID users only)
/api/analytics         - Analytics event tracking
```

**API Endpoints:**

**POST /api/checkout**
- Creates Stripe Checkout session for $3.99 upgrade or Gold IAP
- Returns checkout URL for redirect
- Handles guest payments (no auth required)

**POST /api/webhook**
- Handles Stripe webhook events
- Processes payment fulfillment
- Migrates local data to cloud (on upgrade)
- Updates user account status

**POST /api/sync** (PAID only)
- Syncs player progress to cloud
- Requires authentication (Clerk session)
- Bidirectional sync (pull on load, push on changes)

**POST /api/analytics**
- Tracks game events (wins, losses, upgrades)
- Anonymized tracking (UUID-based, no PII)
- Rate-limited to prevent abuse

**Error Handling:**
- Graceful degradation: API failures don't break gameplay
- Retry logic: Automatic retries for transient failures
- User feedback: Clear error messages for user-facing failures
- Logging: Server-side logging for debugging

### Performance Optimization

**Bundle Optimization:**
- Code splitting: Route-based and component-based splitting
- Tree shaking: Remove unused code
- Asset optimization: Compressed images, lazy-loaded assets
- Target bundle size: <1MB initial load, <5MB total

**Rendering Optimization:**
- Canvas offscreen rendering for smooth animations
- RequestAnimationFrame for 60fps animations
- Debounced re-renders (prevent excessive updates)
- Memoization: React.memo for expensive components

**Network Optimization:**
- CDN: Vercel Edge Network for global asset delivery
- Lazy loading: Load assets on-demand (Warlords, sounds)
- Preloading: Critical assets preloaded (default Warlords, core sounds)
- Compression: Gzip/Brotli compression for all assets

**Mobile Optimization:**
- Portrait lock: CSS and manifest enforce portrait orientation
- Touch optimization: ≥48px touch targets, thumb-optimized CTAs
- Battery efficiency: Minimal background processing, efficient animations
- Memory management: Unload unused assets, prevent memory leaks

**Performance Targets:**
- Initial load: <2 seconds (3G connection)
- Time to Interactive: <3 seconds
- Frame rate: 60fps during gameplay
- Lighthouse score: 90+ mobile score
- Memory usage: <50MB on mobile devices

### Error Handling

**Client-Side Error Handling:**
- Try-catch blocks around critical operations
- Error boundaries: React Error Boundaries for component errors
- Graceful degradation: Game continues with reduced features on errors
- User feedback: Clear error messages (no technical jargon)

**Server-Side Error Handling:**
- API error responses: Standardized error format
- Logging: Comprehensive server-side logging
- Monitoring: Error tracking
- Recovery: Automatic retries for transient failures

**Data Validation:**
- Input validation: Validate all user inputs
- State validation: Validate game state on load
- Type safety: TypeScript for compile-time type checking
- Runtime checks: Validate critical data structures

**Edge Cases:**
- Network failures: Offline mode with local storage
- Storage quota: Handle localStorage quota exceeded
- Browser compatibility: Feature detection and polyfills
- Payment failures: Clear error messages, retry options

### Testing Strategy

**Unit Testing:**
- Framework: Jest + React Testing Library
- Coverage: Core game logic (rules, calculations, state management)
- Target: 80%+ code coverage for game logic
- Examples: Card rank comparison, damage calculation, charge tracking

**Integration Testing:**
- Framework: Jest + React Testing Library
- Scope: Component interactions, state updates
- Examples: Turn flow, special activation, deck manipulation

**End-to-End Testing:**
- Framework: Cypress
- Scope: Complete user flows (pre-game → game → post-game)
- Examples: Warlord selection, game playthrough, upgrade flow
- Mobile testing: Chrome DevTools mobile emulation + real device tests

**Performance Testing:**
- Lighthouse CI: Automated performance audits
- Load testing: Simulate concurrent users (serverless functions)
- Memory profiling: Identify memory leaks
- Frame rate monitoring: Ensure 60fps during gameplay

**Manual Testing:**
- Device testing: Test on real iOS/Android devices
- Browser testing: Chrome, Safari, Firefox, Edge
- Payment testing: Stripe test mode, AdMob test ads
- Accessibility testing: Screen readers, keyboard navigation

### Deployment and Testing

**CI/CD Pipeline:**
- **Hosting**: Vercel provides CI/CD—auto-deploys from GitHub
- **Domain**: bigfootwar.com (custom domain configured)
- **Branch Strategy**: 
  - `main` branch → Production deployment
  - `develop` branch → Preview deployment
  - Feature branches → Preview deployments (PR-based)

**Deployment Process:**
1. Push to GitHub triggers Vercel build
2. Automated tests run (Jest, Cypress)
3. Build succeeds → Deploy to preview/production
4. Health checks verify deployment
5. Rollback available if issues detected

**Environment Management:**
- **Production**: Production database, Stripe live mode, AdMob live
- **Preview**: Preview database, Stripe test mode, AdMob test ads
- **Local**: Local development with mock services

**Monitoring and Observability:**
- **Error Tracking**: Sentry for error monitoring
- **Analytics**: Vercel Analytics + PostHog for user analytics
- **Performance**: Vercel Analytics for Core Web Vitals
- **Logging**: Structured logging for debugging

**Scalability:**
- **Serverless**: Auto-scales to handle traffic spikes
- **Database**: Vercel Postgres scales automatically
- **CDN**: Vercel Edge Network for global asset delivery
- **Target**: Support 1k+ DAU initially, scale to 10k+ DAU
- **Monitoring**: DB usage monitored, alerts for capacity limits
- **Redis**: Vercel KV for session caching (implemented from launch)

**Backup and Recovery:**
- **Database Backups**: Automatic daily backups (Vercel Postgres)
- **Data Recovery**: Point-in-time recovery available
- **Disaster Recovery**: Multi-region redundancy (Vercel infrastructure)