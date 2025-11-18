# Bigfoot War Game Design

## Summary
Classic War turn-based card game mixed with fast slot-like play.

- **Platform**: Web browser (Chrome, Firefox, Safari, Edge) - no app store required  
- **Mobile-first**: Optimized responsive design for mobile devices by default with breakpoints for other display sizes  
- **URL**: bigfootwar.com (hosted on Vercel)  
- **Technology**: Next.js, React, WebGL/Canvas  
- **Monetization**: Free-to-play with ads / $3.99 one-time purchase for ad-free / Gold IAP  

### Game Rules
- Single player game
- Player Bigfoot Warlord vs Enemy Bigfoot Warlord
- Player and Enemy each use a shuffled deck of 52 cards + 2 Jokers
- Simultaneous card draw, highest card rank wins the turn
- Winning Warlord deals damage based on card and rank
- Ties result in War scenario
- Jokers = deck shuffle
- Each Warlord can play a Special Power
- Each Warlord can play suit-based Specials
- Winner takes all cards from the table, go to bottom of deck
- Player wins the game by reducing Enemy Warlord HP to 0 or by capturing all of the Enemy's cards
- Player loses the game by getting HP reduced to 0 or by having cards captured by the Enemy
- Player wins XP, Gold with winning turns and game, bonuses for streaks and Challenges, 
- Player unlocks 1 new Warlord Enemy per level, player pays a Gold fee per game until the Enemy Warlord is defeated, then player progresses to next level (still has XP threshold requirements)
- Players can replay any unlocked, defeated Warlords for free
- Players unlock Player Warlords after they defeat an Enemy Warlord (e.g. play against and defeat Yeti to play as the Yeti)

### Game Look & Feel
- One page with minimal UI elements
- Retro SNES-style pixel art
- Dark-mode themed
- Plays happens on table like a card game
- Primary CTA at thumb-level
- Secondary CTAs for:
  - card Specials (displayed as Hearts, Diamonds, Clubs, Spades Icon on playing field above Primary CTA)
  - Warlord Special (`Special` button available after tapping avatar to display Warlord Overlay)
- Default layout shows Enemy Warlord avatar at top, Player Warlord avatar at bottom of screen
- At game start, show decks adjacent to Warlords
- Display card count for each deck
- Minimal animation
- Card faces display simple Suit and Rank along with Warlord hero image
- Cards dealt in middle of screen, player on left, enemy on right
- XP and Gold rewards and Level ups displayed when won but do not persistent in-game (no top bars with XP, Gold, Level, etc.)
- HP displayed as Health Bar per Warlord
- Warlord avatars react to outcomes
- Game Status displayed in banner area at top of page
  - Displays outcomes, describes plays, game / turn status, prompts for decisions
- Overlays for:
  - Tapping Game Menu (anytime)
  - Tapping Warlords (anytime)
  - Tapping Suit Icons (gameplay)
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

### Pre-Game Flow

1. Player taps `Select Enemy Warlord` CTA (beneath Enemy Warlord avatar) - default Warlord selected (last played or new player)
2. Player taps `Select Player Warlord` CTA (above Player Warlord avatar) - default Warlord selected (last played or new player)
3. Player taps Primary CTA button to start the game.

Other pre-game options:

- Player views `XP`, `Level`, and `Gold`, taps `Gold` to purchase more Gold, taps `XP` to view level progression
- Player taps `Game Menu` (always displays top-right of screen) to view Game Options Overlay
- Player taps `Upgrade` to make 1-time purchase and upgrade to PAID account
- Player taps Enemy Warlord avatar to view Warlord details: status (locked, unlocked, defeated), Warlord stats, Special Power, Specials, equipped Battle Items, game history with Player, CTA to select new Warlord
- Player taps Player Warlord avatar to view Warlord details: can purchase and equip 1 Battle Item per level, can view Warlord stats, can view Warlord Special Power (changes per level), can view card Specials (changes per level), game history with Player, CTA to select new Warlord
- Player taps `Challenge` to view and accept challenges
- Player taps `Top Up` to view AdMob for Gold payout

### Main Game Flow

After starting the app removes pre-game CTAs and displays Decks (showing # of cards), HP for each Warlord, and Hearts, Diamonds, Clubs, Spades icons.

1. Player taps `Play` to start the game turn.
2. App reveals Player and Enemy cards face up on the playing field.
- Player optionally taps Hearts, Diamonds, Clubs, Spades icons to display Special info, power up status
- Player optionally taps Warlord avatar to display Warlord info, power up status
3. On Player win,
- Game indicates Winner
- Damage is dealt to Enemy
- Gold and XP rewards are displayed
- Hearts, Diamonds, Clubs, Spades Icons indicate power up status based on captured cards
- If Hearts, Diamonds, Clubs, Spades are powered up, indicate Ready Status with icon
4. The Player or Enemy optionally plays any Specials (Cards or Warlord Special Powers if available)
- Player optionally taps Hearts, Diamonds, Clubs, Spades icons to display Special info, power up status, and if Ready status, CTA to play the Special
- Player optionally taps Warlord avatar to display Warlord info, power up status, and if Ready, CTA to play the Special Power
5. On Player loss,
- Game indicates Winner
- Damage is dealt to the Player
6. Player taps Primary CTA to start next turn.

### Post-Game Flow

Gold Top-Up
- F2P player optionally taps CTA to earn extra Gold (Google AdMob)
- PAID player automatically earns extra Gold AND can still earn extra Gold through AdMob
- Payout varies and is displayed before player clicks-through

### XP, Levels, and Progress Flow


## Game Design and Systems

### Core App Loop


### Game menu, settings, and options


### Core Game Loop


### Game and App States


### Decks and Cards


### Bigfoot Warlords


Warlord stats:
- HP: 20-50 range
- Damage: Base dealt per win (e.g., 2 + rank bonus/10). Suits/specials multiply (e.g., Hearts: +1).
- Power Charge: Wins needed to ready Warlord Special (e.g., "Steal card" at 5). Suits charge on capture (e.g., 3 Spades = ready). Resets on loss. 3-7 wins range 

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
| # | Warlord | Level | HP | Damage | Charge | Special Power | Hearts Special | Diamonds Special | Clubs Special | Spades Special | H Thr | D Thr | C Thr | S Thr | Battle Item | AI Strategy |
|---|---------|-------|----|--------|--------|---------------|----------------|------------------|---------------|----------------|-------|-------|-------|-------|-------------|-------------|
| 1 | Sasquatch | 1 | 20 | 2 | 7 | Forest Regen (Passive: +1 HP/turn) | Heal 2 | +50 Gold | Scratch (+2 dmg) | Rock Throw (rank dmg) | 2 | 3 | 3 | 4 | Moss Cloak (+2 max HP) | Balanced, prioritizes power charge |
| 2 | Skunk Ape | 2 | 20 | 2 | 7 | Stink Cloud (Enemy specials disabled 2 turns) | Armor 2 (next dmg -2) | Poison DoT (1 dmg x5) | Slime Punch (+3 dmg) | Gas Spray (rank+1) | 4 | 2 | 3 | 3 | Poison Sac (Clubs apply DoT 1x3) | Diamonds focus, early poison pressure |
| 3 | Wendigo | 3 | 21 | 2 | 7 | Cannibal Feast (Steal 1 card from enemy deck) | Heal 3 (lose 1 max HP) | Fear Aura (Enemy charge +1) | Antler Gore (+4 dmg) | Ice Wind (rank dmg x1.2) | 3 | 3 | 2 | 4 | Hunger Bone (+1 heal on win) | Aggressive Clubs, charges power fast |
| 4 | Jersey Devil | 4 | 21 | 2 | 7 | Demonic Flight (Reshuffle deck + extra draw) | Blood Heal 2 | Hellfire (rank*1.5 dmg) | Claw Rake (+3 dmg) | Wing Blast (rank+2) | 3 | 3 | 4 | 2 | Devil Wing (Spades +1 dmg) | Spades spam, evasive |
| 5 | Grassman | 5 | 21 | 2 | 7 | Earth Bind (Enemy dmg -1 for 3 turns) | Grass Regen 3 | +75 Gold | Vine Slam (+4 dmg) | Seed Shot (rank dmg) | 2 | 4 | 3 | 3 | Earth Root (Armor 1 passive) | Defensive Hearts/Clubs |
| 6 | Fouke Monster | 6 | 22 | 2 | 7 | Amphibious Hide (Invulnerable 1 turn) | Slime Heal 2 | +50 Gold | Webbed Bite (+4 dmg) | Tongue Lash (rank+1) | 3 | 3 | 2 | 4 | Swamp Scale (Dodge 10% chance) | Clubs focus, opportunistic |
| 7 | Mogollon Monster | 7 | 22 | 2 | 6 | Desert Mirage (Enemy plays random card next turn) | Heat Armor 3 | Sand Curse (DoT 1x4) | Dune Punch (+3 dmg) | Cactus Spike (rank+2) | 4 | 2 | 3 | 3 | Sand Veil (Hearts charge faster) | Spades/Diamonds control |
| 8 | Honey Island Swamp Monster | 8 | 22 | 2 | 6 | Vine Entangle (Enemy skips turn) | Vine Heal 3 | +100 Gold | Mud Crush (+4 dmg) | Thorn Dart (rank dmg) | 2 | 3 | 4 | 3 | Honey Trap (+20% Gold) | Hearts/Clubs sustain |
| 9 | Pope Lick Monster | 9 | 23 | 2 | 6 | Troll Toll (Steal next Gold reward) | Ritual Heal 2 | Lick Curse (DoT 2x3) | Horn Gore (+5 dmg) | Hoof Kick (rank+1) | 3 | 2 | 3 | 4 | Goat Horn (Charge -1) | Aggressive Diamonds/Clubs |
| 10 | Thunderbird | 10 | 23 | 2 | 6 | Storm Call (Deal 4 direct dmg) | Storm Regen 3 | Lightning (rank*1.2 + DoT1) | Talon Slash (+4 dmg) | Thunderbolt (rank*1.5) | 4 | 3 | 3 | 2 | Feather Amulet (Spades auto-crit 10%) | Spades burst |
| 11 | Yeti | 11 | 23 | 3 | 6 | Avalanche (Deal 5 dmg + bury 1 card) | Ice Armor 4 | +125 Gold | Frost Fist (+5 dmg) | Blizzard (rank+3) | 4 | 4 | 5 | 3 | Ice Shard (Armor 2 passive) | Defensive Spades |
| 12 | Almas | 12 | 24 | 3 | 6 | Nomad Stealth (Next loss free) | Heal 4 | +100 Gold | Cave Claw (+4 dmg) | Stone Throw (rank dmg x1.2) | 3 | 5 | 4 | 4 | Nomad Pouch (Extra Gold +25%) | Balanced, evasive |
| 13 | Yeren | 13 | 24 | 3 | 6 | Martial Strike (Double dmg next win) | Chi Heal 3 | Mystic Palm (Heal enemy 2, steal turn) | Kung Fu Kick (+6 dmg) | Flying Knee (rank*1.3) | 4 | 4 | 3 | 5 | Bamboo Staff (Clubs +2 dmg) | Clubs burst |
| 14 | Barmanou | 14 | 24 | 3 | 6 | Mountain Grip (Steal 2 cards) | Cliff Regen 4 | +150 Gold | Rock Smash (+5 dmg) | Avalanche Toss (rank+2) | 4 | 5 | 3 | 4 | Climbing Rope (Charge on loss) | Physical control |
| 15 | Chuchunya | 15 | 25 | 3 | 5 | Frost Breath (Enemy HP -1/turn 3 turns) | Fur Warmth 4 | Ice Shard Curse (DoT 2x4) | Bear Hug (+5 dmg) | Spear Throw (rank*1.4) | 5 | 3 | 4 | 4 | Tundra Pelt (+3 max HP) | Diamonds debuff |
| 16 | Xueren | 16 | 25 | 3 | 5 | Chi Meditation (Full charge reset + heal 5) | Aura Heal 5 | Enlightenment (+200 Gold) | Palm Strike (+5 dmg) | Energy Blast (rank+3) | 3 | 4 | 4 | 5 | Lotus Orb (Hearts double effect) | Hearts sustain, patient |
| 17 | Migoi | 17 | 25 | 3 | 5 | Phase Shift (Dodge all dmg 1 turn) | Spirit Heal 4 | Phantom Mirage (Confuse 2 turns) | Ethereal Claw (+6 dmg) | Ghost Arrow (rank dmg ignore armor) | 4 | 3 | 5 | 4 | Spirit Totem (Invuln 1/game) | Evasive Diamonds |
| 18 | Kikomba | 18 | 26 | 3 | 5 | Savanna Sprint (Extra turn) | Heat Heal 4 | +175 Gold | Charge Tackle (+7 dmg) | Dust Kick (rank*1.2) | 5 | 4 | 3 | 4 | Speed Herb (Charge faster) | Aggressive Clubs |
| 19 | Yowie | 19 | 26 | 3 | 5 | Outback Defense (Armor 5 next 2 turns) | Dirt Regen 5 | +150 Gold | Boomerang Punch (+6 dmg) | Dirt Bomb (rank+3) | 3 | 5 | 4 | 4 | Dirt Armor (Armor 3 passive) | Defensive Hearts |
| 20 | Moehau | 20 | 26 | 3 | 5 | War Cry (All specials ready) | Tribal Heal 5 | Ancestor Curse (Enemy dmg -2 3 turns) | Haka Slam (+7 dmg) | Spear Volley (rank*1.5) | 4 | 4 | 3 | 5 | Tattoo Mark (Damage +1) | Burst Clubs |
| 21 | Hibagon | 21 | 27 | 4 | 5 | Ninja Vanish (Reshuffle + steal 1) | Shadow Heal 4 | Shuriken (DoT 1x6) | Kunai Strike (+7 dmg) | Smoke Bomb (rank dmg + blind) | 4 | 3 | 4 | 5 | Ninja Scroll (Stealth dodge 20%) | Spades control |
| 22 | Orang Pendek | 22 | 27 | 4 | 5 | Jungle Pounce (Triple dmg next Clubs) | Vine Heal 5 | +225 Gold | Arm Swing (+8 dmg) | Fruit Throw (rank+2) | 5 | 4 | 3 | 4 | Short Limb Boost (Clubs x1.5) | Clubs focus |
| 23 | Batutut | 23 | 27 | 4 | 4 | Trap Set (Enemy next card trapped, auto loss) | Camo Heal 5 | Trap Poison (DoT 3x3) | Wire Snare (+6 dmg) | Boomerang (rank*1.3) | 4 | 3 | 5 | 4 | Trap Kit (Chance enemy special fail) | Trap Diamonds |
| 24 | Agogwe | 24 | 28 | 4 | 4 | Pack Hunt (Double wins count for charge) | Pack Regen 5 | +200 Gold | Frenzy Bite (+8 dmg) | Pack Rush (rank+4) | 5 | 4 | 3 | 4 | Pack Bond (+1 charge win) | Fast charge Clubs |
| 25 | Maricoxi | 25 | 28 | 4 | 4 | Vine Control (Steal all table cards) | Nature Heal 6 | Emerald Blast (rank*1.6) | Root Crush (+8 dmg) | Vine Whip (rank dmg x1.4) | 3 | 5 | 4 | 4 | Vine Crown (Suits charge x2) | Control Spades |
| 26 | Sisimito | 26 | 28 | 4 | 4 | Time Warp (Rewind last loss) | Mayan Heal 6 | Time Curse (Enemy charge reset) | Rune Punch (+9 dmg) | Temporal Bolt (rank+5) | 5 | 3 | 5 | 6 | Time Amulet (Undo 1 loss/game) | Diamonds utility |
| 27 | Mapinguari | 27 | 29 | 4 | 4 | Psychic Scream (Enemy specials cooldown +3) | Backward Heal 6 | Eye Beam (5 direct dmg) | Sloth Claw (+9 dmg) | Psychic Wave (rank*1.7) | 6 | 4 | 5 | 5 | Single Eye (Predict next card 20%) | Disruptive Diamonds |
| 28 | Mono Grande | 28 | 29 | 4 | 4 | Earthquake (Deal 6 dmg to enemy) | Primal Heal 6 | +300 Gold | Gorilla Pound (+10 dmg) | Rock Fling (rank+4) | 5 | 6 | 4 | 5 | Giant Fist (+2 base dmg) | High damage Clubs |
| 29 | Ucumar | 29 | 29 | 4 | 4 | Bear Rage (Damage +2 for 5 turns) | Bear Regen 7 | +250 Gold | Paw Swipe (+9 dmg) | Honey Trap Shot (rank dmg + DoT) | 3 | 5 | 4 | 6 | Bear Claw (Clubs crit 15%) | Sustain Clubs |
| 30 | Arulataq | 30 | 30 | 4 | 4 | Shapeshift (Copy enemy special 1 time) | Aurora Heal 7 | Northern Light (Blind 3 turns) | Morph Claw (+10 dmg) | Ice Spear (rank*1.8) | 4 | 3 | 6 | 5 | Aurora Shard (Random suit boost) | Adaptive Diamonds |
| 31 | Woodwose | 31 | 30 | 5 | 4 | Knightly Charge (5 direct + charge reset) | Leaf Heal 7 | +325 Gold | Sword Slash (+10 dmg) | Leaf Storm (rank+5) | 5 | 6 | 4 | 5 | Knight Shield (Armor 4) | Balanced knight |
| 32 | Basajaun | 32 | 31 | 5 | 4 | Forest Guard (Block all dmg 2 turns) | Moss Armor 8 | Oak Blast (DoT 2x5) | Bark Smash (+11 dmg) | Acorn Volley (rank dmg x1.5) | 4 | 5 | 5 | 6 | Guardian Oak (+5 max HP) | Heavy defense Hearts |
| 33 | Salvanel | 33 | 31 | 5 | 3 | Illusion Trick (Swap cards with enemy) | Fake Heal 7 (mirror enemy heal) | Mirage Gold (+400) | Phantom Punch (+10 dmg) | Illusion Arrow (rank + confuse) | 6 | 4 | 5 | 5 | Trick Mirror (Copy item 1/game) | Deceptive Diamonds |
| 34 | Almasti | 34 | 31 | 5 | 3 | Echo Location (Predict enemy card) | Cave Heal 8 | Sonar Curse (Enemy accuracy -20%) | Echo Claw (+11 dmg) | Bat Scream (rank*2) | 5 | 3 | 6 | 4 | Echo Crystal (Predict specials) | Predictive Spades |
| 35 | Kapre | 35 | 32 | 5 | 3 | Smoke Confusion (Enemy random special) | Ash Heal 8 | Cigar Cloud (DoT 3x4) | Giant Fist (+12 dmg) | Smoke Blast (rank+6) | 6 | 4 | 5 | 5 | Cigar (Diamonds DoT +1) | Debuff Diamonds |
| 36 | Fear Liath | 36 | 32 | 5 | 3 | Fear Induce (Enemy charge x2) | Mist Heal 8 | Grey Terror (Direct 7 dmg) | Fog Claw (+12 dmg) | Mist Wave (rank dmg ignore armor) | 5 | 3 | 6 | 5 | Fear Cloak (Enemy AI panic 10%) | Psychological Diamonds |
| 37 | Brenin Llwyd | 37 | 32 | 5 | 3 | Spectral Command (Control enemy special 1) | Royal Heal 9 | Crown Curse (Steal charge) | Thorn Mace (+13 dmg) | Fog Spear (rank*2.1) | 4 | 5 | 5 | 6 | Grey Crown (All suits ready faster) | Control Spades |
| 38 | Leshy | 38 | 33 | 5 | 3 | Shape Shift (Change to random Warlord power) | Bark Heal 9 | Vine Teleport (Swap positions) | Root Slam (+13 dmg) | Leaf Storm (rank+7) | 3 | 6 | 5 | 5 | Shape Twig (Random buff/turn) | Unpredictable Hearts |
| 39 | Troll | 39 | 33 | 5 | 3 | Regen Troll (Heal 10 on use) | Rock Armor 10 | Stone Curse (Armor break) | Club Bash (+14 dmg) | Boulder Throw (rank*2.2) | 4 | 5 | 4 | 6 | Regen Moss (Passive heal 2/turn) | Sustain tank Clubs |
| 40 | Wildman | 40 | 33 | 5 | 3 | Berserk Fury (Damage x2 5 turns, self dmg 1/turn) | Rage Heal 9 | Fury Gold (+500) | Berserk Punch (+15 dmg) | Wild Throw (rank+8) | 6 | 5 | 4 | 5 | Rage Totem (Damage +2 risk) | High risk Clubs burst |
| 41 | Ancient Gigantopithecus | 41 | 34 | 5 | 3 | Prehistoric Stomp (Deal 8 dmg + bury 3 cards) | Fossil Heal 10 | Ancient Curse (DoT 4x4) | Jaw Crush (+15 dmg) | Bone Spear (rank*2.3) | 6 | 5 | 4 | 7 | Fossil Tooth (+3 dmg) | Bury control Clubs |
| 42 | Quantum Sasquatch | 42 | 34 | 5 | 3 | Quantum Glitch (Random: win/loss flip last 3 turns) | Phase Heal 10 | Probability Warp (Random dmg 1-10) | Glitch Punch (+16 dmg) | Rift Blast (rank + random) | 7 | 5 | 6 | 6 | Quantum Core (Reroll loss 15%) | Chaotic RNG Diamonds |
| 43 | Enkidu | 43 | 34 | 5 | 3 | Bull Wrath (Full heal + 10 dmg) | Primal Heal 12 | Wild Smite (rank*3) | Beast Fist (+16 dmg) | Judgment Bolt (rank*2.5) | 5 | 6 | 6 | 5 | Bull Ring (Passive +1 all stats) | Sumerian Spades burst |
| 44 | Skinwalker | 44 | 35 | 5 | 3 | Shapeshift Copy (Copy player Warlord power) | Stolen Heal 11 | Curse Skin (Steal suit charge) | Morph Bite (+17 dmg) | Shadow Shot (rank dmg x2) | 6 | 4 | 7 | 6 | Skin Patch (Steal enemy item) | Mimic Diamonds |
| 45 | Kushtaka | 45 | 35 | 5 | 3 | Soul Steal (Steal 1 win toward charge) | Otter Heal 11 | Water Trick (Confuse + DoT) | Otter Claw (+17 dmg) | Wave Splash (rank+9) | 5 | 6 | 6 | 7 | Otter Pearl (Dodge + heal on dodge) | Tricky Hearts |
| 46 | Genoskwa | 46 | 35 | 5 | 3 | Stone Form (Invuln 3 turns) | Rock Heal 12 | Gem Blast (8 direct) | Granite Smash (+18 dmg) | Boulder Roll (rank*2.6) | 6 | 7 | 5 | 6 | Stone Heart (+10 max HP) | Ultimate tank Clubs |
| 47 | Stick Indians | 47 | 36 | 5 | 3 | Invisible Whisper (Enemy misses next 2 cards) | Wind Heal 12 | Whisper Curse (Silence specials 3) | Stick Prod (+16 dmg) | Wind Gust (rank+10) | 7 | 5 | 6 | 6 | Invis Cloak (50% dodge) | Evasion max Diamonds |
| 48 | Rugaru | 48 | 36 | 5 | 3 | Lunar Howl (All charges max + dmg +1 3 turns) | Moon Regen 13 | Werebite (Transform: +2 dmg 5 turns) | Wolf Maul (+19 dmg) | Moon Beam (rank*2.8) | 6 | 5 | 4 | 7 | Silver Fang (Anti-were +dmg) | Moon phase Clubs |
| 49 | Batsquatch | 49 | 36 | 5 | 3 | Sonic Screech (Reset all enemy charges) | Echo Heal 13 | Bat Swarm (DoT 5x3) | Wing Slash (+18 dmg) | Sonic Wave (rank +10) | 7 | 4 | 6 | 6 | Bat Wing (Flight: Spades x2) | Disrupt sonic Spades |
| 50 | Mechanical Bigfoot | 50 | 37 | 5 | 3 | Overload (Deal 12 dmg, self 4 dmg) | Repair Heal 14 | Laser (rank*3.5) | Mech Punch (+20 dmg) | Missile (rank*3) | 6 | 5 | 7 | 6 | Cyber Chip (Auto charge 1/3) | Tech burst Diamonds |
| 51 | The Primal One | 51 | 37 | 5 | 3 | Primal Aura (All stats +1 for game) | Origin Heal 15 | Adaptive Gold (+1000) | Alpha Strike (+20 dmg) | Apex Throw (rank*3.2) | 6 | 6 | 5 | 7 | Primal Essence (All suits +1) | God tier balanced |
| 52 | Interdimensional Sasquatch | 52 | 38 | 5 | 3 | Portal Rift (Banish 5 enemy cards) | Void Heal 15 | Dimension Warp (Random teleport win) | Rift Claw (+21 dmg) | Portal Blast (rank +15) | 7 | 6 | 6 | 5 | Rift Key (Steal card random) | Dimensional chaos Spades |
| 53 | The First Walker | 53 | 38 | 5 | 3 | Ancestral Recall (Undo last 5 turns) | Elder Heal 16 | Rune Curse (Perma DoT 1/turn) | Patriarch Fist (+22 dmg) | Origin Bolt (rank*4) | 6 | 4 | 7 | 6 | Rune Stone (Predict all cards) | Time master Diamonds |
| 54 | Cosmic Yeti | 54 | 38 | 5 | 3 | Nebula Explosion (15 direct dmg) | Star Heal 17 | Meteor Shower (DoT 6x4) | Cosmic Punch (+23 dmg) | Black Hole (rank*4.5 suck cards) | 7 | 5 | 6 | 6 | Cosmic Dust (Suits infinite charge) | Space nuke Diamonds |
| 55 | Shadow Squatch | 55 | 39 | 5 | 3 | Shadow Merge (Copy all enemy buffs) | Dark Heal 18 | Abyss Fear (Enemy dmg 0 4 turns) | Shadow Tendril (+24 dmg) | Void Shot (rank dmg x3) | 6 | 3 | 7 | 6 | Shadow Veil (Invis + heal steal) | Shadow steal Diamonds |
| 56 | Golden Sasquatch | 56 | 39 | 5 | 3 | Midas Touch (Turn losses to wins x3) | Gold Heal 20 | Infinite Gold (+2000) | Golden Fist (+25 dmg) | Aurum Arrow (rank +20) | 7 | 4 | 6 | 7 | Gold Crown (Gold x3 rewards) | Gold economy Diamonds |
| 57 | The Collective | 57 | 39 | 5 | 3 | Hive Swarm (Spawn 2 mini-wins) | Swarm Regen 20 | Insect Plague (DoT 10x2) | Mass Bite (+26 dmg) | Drone Strike (rank*5) | 6 | 5 | 4 | 7 | Hive Mind (Charge shared) | Swarm overwhelm Clubs |
| 58 | Primordial Terror | 58 | 40 | 5 | 3 | Chaos Mutate (Random extreme buff/debuff) | Terror Heal 25 | Mutation Curse (Random enemy debuff) | Tentacle Lash (+30 dmg) | Chaos Blast (rank*6) | 7 | 6 | 5 | 7 | Chaos Egg (Random power/game) | Ultimate RNG Clubs |
| 59 | The Bigfoot King | 59 | 50 | 5 | 3 | Royal Decree (Win game instantly on use) | Kingly Heal 30 | Treasury (+5000 Gold) | Imperial Smite (+50 dmg) | Crown Bolt (rank*10) | 6 | 6 | 6 | 6 | King's Scepter (All previous powers 1/use) | Final boss omniscient, all suits max |

**Threshold Assignment Logic Recap**:
- **Base**: Lv1-10:3, 11-25:4, 26-40:5, 41+:6
- **Primary Suit** (per AI/theme): base-1 (min 2-3 for playability)
- **Weak Suit** (opposite/least thematic): base+1 (max 7 for challenge)
- **Others**: base
- Ensures ~20-30% faster ready for focus suits, promoting Warlord picks & counterplay. Replays: +1 all thr. Overcharge: bonus potency. Streaks > raw wins.

**Notes on Balance and Progression:**
- **Stats Progression**: HP ramps from 20 to 50 for endurance challenges. Damage tiers up for punchier late-game. Charge decreases for frequent ultimates in endgame.
- **Specials**: Thematic to lore (e.g., poison for Skunk Ape, time for Sisimito). Hearts focus sustain/armor; Diamonds utility/Gold/Debuffs; Clubs raw physical burst (rank diff boosted); Spades consistent ranged (rank-based). Power scales ~level/5 for fairness.
- **Special Powers**: Powerful, charge-gated climaxes. Early: utility/sustain; Mid: control/disrupt; Late: game-warping (e.g., win condition). Resets on loss/use for tension.
- **Battle Items**: Unlocked sequentially for player (equip 1/level). Counters themes (e.g., anti-poison vs. Skunk Ape). Helps vs. stronger foes (e.g., predict vs. RNG bosses).
- **AI Strategies**: Varied for replayability—teaches counterplay (e.g., burst poison users fast, out-sustain tanks). Replays add Battle Item chance, escalating difficulty.
- **Holistic Tuning**: Early: Learn basics (low stats, simple). Mid: Counters/items matter. Late: Power spikes require streaks/perfect play. Streaks/bonuses reward mastery. Tested mentally for ~45-60 min games, win rates ~60% with optimal play.

### Enemies and AI

**Enemy AI System Design**

Bigfoot War's core is symmetric RNG draws from full 52-card decks (shuffled independently per player/enemy), yielding ~50% base win probability per turn. Specials (suit-based and Warlord Power) are the only decisions, triggered post-win by capturing cards (count-based charges, reset on loss). Ties trigger "War" (standard: 3 face-down + 1 face-up; highest wins all; auto-simultaneous for both sides—no AI choice).

**Lightweight Rule-Based AI (No Search/ML)**
- **Why minimal?** Hyper-casual mobile/browser perf (60fps, <1MB bundle). Draws are unpredictable (shuffles), so minimax/MCTS branching explodes (52! states)—too slow even shallow. Rule-based is O(1), thematic (per-Warlord "personality"), and replayable with light rand. Matches Hearthstone solo AI critiques: rules > complex for fun balance.
- **None/random**: Boring, unthematic (enemies ignore powers).
- **Advanced (RL/MCTS)**: Overkill, high latency/battery drain.

**Decision Points**
- **Post-Resolution (Win Only)**: Evaluate ready specials (≤5 options: 4 suits + Warlord). Play 0-2 highest-scoring.
- **Pre-Turn**: None (simultaneous draws).
- **War**: Auto-resolve sub-turns (recursive, cap depth 5 to prevent loops).
- **Replays**: +10% rand deviation; 20% chance equip Battle Item (per GDD).

**Scoring Heuristic (JS Pseudocode)**
```js
function aiScore(special, gameState, warlordWeights) {
  let score = 0;
  const { myHP, maxHP, enemyHP, streakWins, charges } = gameState;

  // Base value (thematic potency)
  if (special.type === 'heal' || 'armor') score += special.amount * 1.5;
  if (special.type === 'dmg') score += special.amount * warlordWeights.dmg;
  if (special.type === 'control/debuff/gold') score += special.value * warlordWeights.control;
  if (special === 'warlordPower') score += 10 + (charges.needed - charges.current); // High prio

  // State multipliers
  if (myHP / maxHP < 0.4) score *= 2.5;  // Urgency: low HP → sustain
  if (enemyHP / enemyMaxHP < 0.4) score *= 2.0;  // Burst low foe
  if (streakWins >= 3) score *= 1.2;  // Snowball
  if (charges.current >= charges.threshold * 1.5) score *= 1.1;  // Overcharge bonus

  return score * warlordWeights[special.primarySuit || 'balanced'];
}
```
- **Select**: Sort ready specials descending score. Play top if >5 (threshold); else hold. Rand tiebreak 10%.
- **Multi-Play**: If top2 >4, chain (e.g., heal then dmg).

**Warlord-Specific Weights** (Ties to Roster Table Strategies)
| Strategy Example | Heal/Armor Wt | Dmg Wt | Control/Gold Wt | Power Charge Bias |
|------------------|---------------|--------|-----------------|-------------------|
| Balanced (Sasquatch) | 1.0 | 1.0 | 1.0 | Prioritize if >80% |
| Diamonds Focus (Skunk Ape) | 0.8 | 0.8 | 1.8 | Debuff always |
| Aggressive Clubs | 0.6 | 2.0 | 0.8 | Burst <50% enemy HP |
| Defensive Hearts | 2.0 | 0.7 | 1.0 | Heal prio |
| Spades Burst | 0.9 | 1.5 | 1.0 | Hold for Warlord |
| ... (per table) | ... | ... | ... | ... |

- **Tune**: Playtest/sim 1000 games/Warlord → target 45-55% player win (skill gap via streaks/specials). Replays: weights *1.1.
- **Edge Cases**: Low cards (<5): Desperate heal. Jokers: AI picks weak suit.

**Implementation (Next.js/React)**
- Zustand store: `aiDecisions: { weights, evaluate() }`
- Per-Warlord JSON config (static, 1KB).
- Total: ~200 LOC, <0.1ms/turn.

**Balance Impact**
- Base RNG: 50%.
- Smart AI: Enemies win 55-65% suboptimal play; player mastery (pick counters, streaks) flips to 60%+.
- Feels alive: "Skunk Ape poisons early!", "Yeti avalanches at low HP!"

This scales progression: Early Warlords simple, late-game "personalities" demand strategy.

### Game Economies

### XP, Levels, Rewards, and Progression

### Advertising

### IAP

### PAID accounts

### Challenges

### Updates, Fixes, and Expansions

### Admin Mode

### Testing and QA

## Visual Design

### Game Table

There is one Game Table that serves as the persistent game screen. Enemy and Player Warlord avatars persist on the game table. Overlays and conditional UI elements extend the Game Table.

### Pre-game

### Game Play

### Post-game

### Game Menu

### Enemy Warlord Select Gallery

### Player Warlord Select Gallery

### Enemy Warlord Details

### Player Warlord Details

## Visual Design

Embrace a **retro SNES 32-bit pixel art aesthetic** to match the Warlord prompts: Vibrant yet limited palettes (15-20 colors per sprite, drawing from SNES Mode 7 vibes—earthy greens/browns for forests, glowing accents for powers). 

Prioritize **pixel perfection**: No anti-aliasing; use `image-rendering: pixelated` in CSS for crisp scaling. High contrast (4.5:1 min) for readability on mobiles; dithering for shading/transitions to evoke nostalgia without modern gloss.

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

- **Cards**: 80x120px canvas-rendered. Bg frame (suit color), center rank (32px bold pixel), top hero sprite (40x60px from Warlord prompts). Jokers: Wild swirl.
- **Warlord Assets**: Per GDD prompts—base portrait 100x120px; emotes swap head (e.g., smug eyes). Hero image: Full-body 200x240px for details overlay.
- **Particles/Effects**: Minimal pixel bursts (e.g., 8x8 sparks on win). Use Canvas for HP flashes, streak counters (pop-up +1 icons).
- **CTAs and Messaging**: Simple, well-known patterns using fonts and CSS styling to compose obvious buttons and other affordances that are in accord with the style guidelines


### Bigfoot Warlords

Avatars, emotes, hero image, sounds for each Warlord.

### Cards and Decks

### Battle Items

### UX Elements

## Sound Design
Bigfoot War's retro SNES-inspired pixel art and hyper-casual gameplay call for a minimalist sound design that enhances immersion without overwhelming the simple UI or taxing web/mobile performance. Focus on short, evocative chiptune cues (e.g., 1-3 second loops) that evoke cryptid mystery and card battle excitement—think subtle howls for Warlord specials, crisp "flip" for draws, and triumphant jingles for streaks. This aligns with trends in indie retro games like Sea of Stars, where audio blends nostalgia with modern subtlety to avoid clutter.

### Sound Assets

### Optimization Strategies
To keep the game lightweight (under 1MB audio bundle) and responsive on mobiles:
- **File Efficiency**: Use compressed formats like OGG or MP3 (128kbps mono) for short clips—aim for <50KB per sound. Tools like Audacity can batch-compress; avoid WAV for web. For retro feel, apply bitcrushing (reduce bit depth to 8-12 bits) to mimic SNES limitations without heavy files.
- **Lazy Loading & Preloading**: Load sounds on-demand (e.g., specials only when unlocked) to reduce initial load times. Preload core effects (e.g., draw/win/loss) during Splash for instant playback.
- **Performance Tuning**: Limit simultaneous sounds to 2-4 layers (e.g., no dense orchestras). Use Web Audio API for dynamic effects like pitch-shifting (e.g., higher pitch on streaks) without extra files. On mobiles, test for latency—enable mute by default (store in localStorage) to respect user prefs and battery.
- **Minimal Layers**: Embrace simplicity: One core synth (e.g., square waves for chiptune) per cue. Use arpeggios (rapid note sequences) for energy without complexity, as in classic retro games. Avoid reverb/echo unless thematic (e.g., faint echo for "misty" Warlords like Fear Liath).
- **Accessibility & Testing**: Include volume sliders in Game Menu; ensure sounds don't autoplay. Test on emulators (Chrome DevTools) for Android/iOS quirks—e.g., iOS requires user interaction for audio init.

### Implementation in Next.js
Leverage native Web Audio API for control (no heavy libs needed for minimalism), or Howler.js for cross-browser ease. Here's a step-by-step guide tailored to your one-page Game Table:

1. **Setup Audio Context**: In your main component (`pages/index.tsx`), init Web Audio on first user tap (e.g., Primary CTA) to comply with browser policies.
   ```tsx
   import { useEffect, useRef } from 'react';

   const GameTable = () => {
     const audioCtx = useRef<AudioContext | null>(null);
     const sounds = useRef<{ [key: string]: AudioBuffer }>({});

     useEffect(() => {
       audioCtx.current = new (window.AudioContext || (window as any).webkitAudioContext)();
       // Preload core sounds
       loadSound('/sounds/draw.mp3', 'draw');
       loadSound('/sounds/win.ogg', 'win');
       // Add more for specials, streaks
     }, []);

     const loadSound = async (url: string, name: string) => {
       const response = await fetch(url);
       const arrayBuffer = await response.arrayBuffer();
       const audioBuffer = await audioCtx.current!.decodeAudioData(arrayBuffer);
       sounds.current[name] = audioBuffer;
     };

     const playSound = (name: string, volume = 0.5) => {
       if (!audioCtx.current || !sounds.current[name]) return;
       const source = audioCtx.current.createBufferSource();
       source.buffer = sounds.current[name];
       const gainNode = audioCtx.current.createGain();
       gainNode.gain.value = volume;
       source.connect(gainNode).connect(audioCtx.current.destination);
       source.start(0);
     };

     // Example: On draw tap
     const handlePlay = () => {
       playSound('draw');
       // Game logic...
     };

     return <button onClick={handlePlay}>Play</button>;
   };
   ```
   This uses async decoding for MP3/OGG; store in Vercel public folder or Blob for assets.

2. **Integrate with Gameplay**: Tie sounds to events—e.g., `playSound('special')` on suit icon tap; vary pitch for Warlord variety (e.g., deeper for massive ones like Mono Grande). For streaks, layer a rising arpeggio dynamically via OscillatorNode.
   - Use Howler.js for simpler API if Web Audio feels low-level: `npm i howler`, then `const sound = new Howl({ src: ['/sounds/win.ogg'] }); sound.play();`. It handles mobile quirks like iOS unlocking.

3. **Retro Effects**: Use free tools like Bfxr or ChipTone for generating chiptune SFX (e.g., bitcrushed jumps for wins, low rumbles for losses). For specials, apply filters: Web Audio's BiquadFilterNode for lo-fi distortion. Match pixel art—e.g., "glitchy" for Quantum Sasquatch via random pitch shifts.

4. **User Controls & Persistence**: Mute toggle in Options overlay, saved to localStorage. For paid users, sync prefs via Prisma.

## UI and UX

### Main Game Table Layout (375x767 Base)

**Persistent vertical stack** for portrait: Enemy top (oppression), battle center (focus), Player bottom (control). Total safe area ~375w x 700h (notch-aware). Use Flexbox (`flex-direction: column; justify-content: space-between; align-items: center`).

**ASCII Mockup** (proportional to 375x767; scale up evenly):
```
+-----------------------------+  <- Banner (37.5w x 77h | 10%)
|  GAME STATUS: Draw! (24px)  |
+-----------------------------+
|        ENEMY DECK: 52       |  <- Enemy Section (30% h)
|         [HP BAR 100%]       |
|       [AVATAR 100x120px]    |
|                             |
|  [ENEMY CARD SLOT L/R]      |  <- Battle Zone (30% h)
|     [PLAYER CARD SLOT L/R]  |
|                             |
|        PLAYER DECK: 52      |  <- Player Section (30% h)
|         [HP BAR 100%]       |
|       [AVATAR 100x120px]    |
|                             |
| ♥ ♦ ♣ ♠  [MENU ICON]        |  <- Bottom Bar (10% h)
|     [PRIMARY CTA 300x60px]  |  <- Thumb-center
+-----------------------------+
```

- **Proportions**: Top 20% Enemy, Middle 30% Battle, Bottom 40% Player+CTA (thumb bias).
- **Zoning**: 80% gameplay visible; overlays dim background 50% opacity.
- **Larger Screens**: Icons +25% size, padding +50%; e.g., avatars 120x144px at 769px—no reflow.

### UI Elements

| Element | Size (375px Base) | Position | Style/Behavior |
|---------|-------------------|----------|---------------|
| **Game Status Banner** | 375x77px | Top-full | Pixel text (20px), marquee scroll if long. Bg: Semi-transparent wood (#3A2A1A). |
| **Warlord Avatar** | 100x120px | Enemy: Top-center; Player: Bottom-center | Pixel sprite; swap emotes (defeated/joyful). Glow on tap (overlay trigger). |
| **HP Bar** | 200x20px | Below avatar | 5-10 pixel hearts or segmented bar (red/green). Animate fill/deplete.  |
| **Deck Indicator** | 150x40px | Avatar sides | Pixel stack + count (16px). Pulse low (<10 cards). |
| **Battle Zone Cards** | 80x120px each | Center: Enemy right (x+100), Player left | Face-up reveal (flip anim). Hero image overlay on rank/suit. |
| **Suit Icons (♥♦♣♠)** | 40x40px | Bottom bar, left-aligned | Glow when ready; tap → power-up overlay. |
| **Primary CTA (Play/Draw)** | 300x60px | Bottom-center | Bold pixel text (24px), yellow glow pulse. ≥48px touch. |
| **Game Menu Icon** | 32x32px | Bottom-right | Hamburger or gear; taps → full overlay. |
| **Overlays** | Fullscreen modal | Centered content | Backdrop blur; e.g., Warlord Select: 3x2 grid thumbs. |

## Technical Design
Bigfoot War is built as a lightweight, mobile-first web app using Next.js for server-side rendering and React for interactive components. 

The core game runs in the browser with minimal server dependencies, leveraging local storage for anonymous play and optional cloud integration for paid users. 

WebGL/Canvas handles card animations and pixel art rendering for a retro SNES feel. 

Deployment on Vercel ensures fast global delivery, with Prisma managing any backend data needs. 

The design prioritizes performance on low-end mobiles (e.g., 60fps draws) and zero-friction entry—no initial auth or installs.

### Architecture
- **Frontend**: Next.js (App Router) with React hooks for state management (e.g., `useState` for game table, `useEffect` for local saves). One persistent Game Table component (`/pages/index.tsx`) handles pre/main/post-game via conditional rendering and overlays (e.g., Modals from Headless UI or custom). UI: Tailwind CSS for responsive, portrait-locked layouts (media queries enforce vertical stack).
- **Rendering**: Canvas/WebGL via Konva.js or raw Canvas API for card draws/flips, avatar reactions, and minimal animations (e.g., card slide-ins, health bar fills). Pixel art scales via CSS (e.g., `image-rendering: pixelated`).
- **Backend**: Minimal—Vercel serverless functions (API routes) for cloud sync, payments, and ads. No always-on server; Prisma Client for DB interactions in functions.
- **State Management**: Local-first with Zustand or Context API for in-game state (decks, HP, specials). Sync to cloud post-upgrade via API calls.

### Data Storage
- **Local Storage (Default/Anonymous)**: Use `localStorage` for preferences (e.g., sound, last Warlord) and IndexedDB (via `idb-keyval`) for game data (e.g., XP, Gold, unlocks as JSON blobs). Anonymized UUID generated on load (`crypto.randomUUID()`) keys data and tracks analytics. Saves auto on events (e.g., win/loss); warn on quota limits.
- **Cloud Storage (Paid Upgrade)**: Vercel Postgres via Prisma ORM for synced data. Minimal schema:
  ```
  model User {
    id      String @id @default(uuid())
    email   String @unique
    data    Json   // Serialized progress (XP, unlocks, galleries)
    adFree  Boolean @default(true)
  }
  ```
  Migration: On $3.99 purchase, API route migrates local JSON to DB, linking via UUID/email. Bidirectional sync: Pull on load if logged in; push on changes.
- **Assets**: Static pixel art (sprites, emotes) hosted on Vercel Blob or public folder. Preload critical (e.g., default Warlords) for offline feel; lazy-load variants.

### Authentication and Payments
- **Auth**: No mandatory login—Clerk for optional email-based cloud save (magic links post-purchase). Integrate via Clerk's Next.js SDK: Check session on load; if present, fetch/sync data.
- **Payments**: Stripe for $3.99 one-time (ad-free + cloud) and Gold IAP. API route creates Checkout session (`/api/checkout`); webhook handles fulfillment (e.g., set adFree, migrate data). Guest payments supported; email captured for receipts/refunds.
- **Ads**: Google AdMob web SDK for interstitials/rewarded videos (post-game CTAs). Track impressions via anonymized events; auto-Gold for paid users.

### Analytics
- **Tracking**: Vercel Analytics for basics (sessions, devices); PostHog for events (e.g., wins, upgrades) tied to local UUID. No PII pre-purchase; hash emails post-upgrade for cohorts.
- **Events**: Fire on key flows (e.g., `game_start`, `upgrade_prompt_viewed`, `win_streak_5`).

### Performance and Optimization
- **Mobile-First**: Portrait lock via manifest/CSS; breakpoints (320-480px base, up to 769px+). Thumb-optimized CTAs (bottom-center, ≥48px targets).
- **Optimizations**: Code-splitting via Next.js; lazy components for overlays. Canvas offscreen rendering for smooth anims. Bundle size <1MB (pixel art compresses well). Lighthouse target: 90+ mobile score.
- **Offline**: Service worker (via Next-PWA) caches assets/game logic for brief disconnects; local data ensures playability.
- **Security**: No sensitive local data; HTTPS enforced. Rate-limit API for sync to prevent abuse.

### Deployment and Testing
- **Hosting**: Vercel for CI/CD—auto-deploys from GitHub. Domains: bigfootwar.com.
- **Testing**: Jest for units (rules logic); Cypress for E2E flows (pre-game selects, turns). Emulate mobiles (Chrome DevTools); real-device tests for AdMob/Stripe.
- **Scalability**: Serverless scales to 1k+ DAU; monitor DB usage (free tier suffices initially). Future: Add Redis (Vercel KV) for session caching if needed.
