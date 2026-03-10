# Mutacje Mocy - boss and loot balance draft v0.2

This doc adds concrete numeric balance for:
- 5 world bosses (3 attacks each, with phase behavior)
- world drop tables
- world mutation tables

Values are tuned to current prototype pacing in `index.html`:
- run length: 10 waves + mini boss + final boss
- baseline enemy hp formula: `(14 + wave * 2.5) * sizeMul`
- player melee baseline: `8 + wave` (up to `22 + wave` for tri power)
- heart progression from XP: `+1 max heart every 50 XP`

## Global assumptions

- World order in one run:
  1) Popielna Kuznia (waves 1-2)
  2) Zelazne Pogranicze (waves 3-4)
  3) Sztormowe Iglice (waves 5-6)
  4) Mutageniczne Mokradla (waves 7-8)
  5) Zlote Katakumby (waves 9-10)
- Mini boss appears after world 3 (wave >= 5, current behavior).
- Final boss appears after world 5 (wave >= 10, current behavior).
- Rarity baseline for world content drops:
  - common 65%
  - rare 27%
  - epic 8%

## 1) Boss design with concrete numbers

### World 1 - Krol Zaru (Popielna Kuznia)

- HP: 180
- Contact damage: 2 hearts
- Base move speed: 0.85

Attacks:
- Fala Ognia
  - Telegraph: 850 ms
  - Width: 180 px cone
  - Damage: 2 hearts
  - Cooldown: 5.0 s
- Deszcz Meteorytow
  - Telegraph: 1100 ms markers
  - Hits: 3 impacts
  - Damage per hit: 1 heart
  - Cooldown: 8.5 s
- Plonacy Szarz
  - Telegraph: 500 ms
  - Dash distance: 260 px
  - Damage: 2 hearts
  - Cooldown: 7.0 s

Phases:
- Phase 1 (100-70% HP): uses one attack at a time
- Phase 2 (70-35% HP): cooldown multiplier 0.85
- Phase 3 (35-0% HP): add 2 lava cracks on arena, tick damage 1 heart every 1.2 s inside crack

### World 2 - General Ostrzy (Zelazne Pogranicze)

- HP: 230
- Contact damage: 2 hearts
- Base move speed: 0.95

Attacks:
- Wir Kling
  - Telegraph: 650 ms
  - Radius: 90 px
  - Damage: 2 hearts
  - Duration: 1.8 s
  - Cooldown: 6.0 s
- Rykoszet
  - Reflect window: 1.6 s
  - Reflected projectile multiplier: 1.25x
  - Cooldown: 9.0 s
- Doskok Egzekutora
  - Telegraph: 400 ms
  - Dash distance: 220 px
  - Damage: 2 hearts + 0.6 s slow
  - Cooldown: 5.5 s

Phases:
- Phase 1 (100-60% HP): no trap support
- Phase 2 (60-25% HP): blade traps every 10 s, active 2.2 s
- Phase 3 (25-0% HP): passive bleed if player in melee range >1.2 s, 1 heart per 2.5 s

### World 3 - Wladca Burzy (Sztormowe Iglice)

- HP: 290
- Contact damage: 3 hearts
- Base move speed: 1.0

Attacks:
- Znaczniki Pioruna
  - Markers: 2 (phase 1), 3 (phase 2+)
  - Telegraph: 1200 ms
  - Damage: 2 hearts
  - Cooldown: 6.5 s
- Lancuch Blyskawic
  - Jump count: up to 3 targets
  - Jump range: 180 px
  - Damage: 1 heart per jump
  - Cooldown: 7.5 s
- Skok Burzowy
  - Telegraph: 450 ms
  - Teleport + shockwave radius 120 px
  - Damage: 2 hearts + pushback
  - Cooldown: 8.0 s

Phases:
- Phase 1 (100-65% HP): teleport chance 30%
- Phase 2 (65-30% HP): cooldown multiplier 0.82
- Phase 3 (30-0% HP): marker telegraph reduced to 850 ms

### World 4 - Hydra Genow (Mutageniczne Mokradla)

- HP: 360
- Contact damage: 3 hearts
- Base move speed: 0.9

Attacks:
- Plucie Mutagenem
  - Pools created: 2 (phase 1), 3 (phase 2+)
  - Pool life: 7 s
  - Effect in pool: random buff/debuff
  - Cooldown: 6.0 s
- Losowa Adaptacja
  - Rotates active element: fire/blade/storm
  - Rotation time: 20 s (phase 1), 14 s (phase 2), 10 s (phase 3)
- Rozszczepienie
  - Summons: 2 mini hydras
  - Mini hydra hp: 42
  - Duration: 12 s or until killed
  - Cooldown: 12 s

Phases:
- Phase 1 (100-70% HP): one active element
- Phase 2 (70-40% HP): gains 15% damage reduction during adaptation animation
- Phase 3 (40-0% HP): summon cooldown multiplier 0.75

### World 5 - Poborca Cieni (Zlote Katakumby)

- HP: 460
- Contact damage: 3 hearts
- Base move speed: 1.05

Attacks:
- Podatek Krwi
  - On hit: steals 12% current coins (min 8, max 60)
  - Bonus damage from steal: +1 heart if steal >= 40 coins
  - Cooldown: 6.8 s
- Dluznicy
  - Summons: 3 adds (phase 1-2), 5 adds (phase 3)
  - Add hp: 34
  - Add contact damage: 1 heart
  - Cooldown: 9.5 s
- Pieczec Chciwosci
  - Scales with player coins:
    - 0-149 coins: 1 heart
    - 150-299 coins: 2 hearts
    - 300+ coins: 3 hearts
  - Telegraph: 900 ms
  - Cooldown: 8.2 s

Phases:
- Phase 1 (100-75% HP): debt stacks disabled
- Phase 2 (75-35% HP): debt stack on hit, +5% damage taken per stack (max 4), stack duration 10 s
- Phase 3 (35-0% HP): add cooldown multiplier 0.7, tax steal cap increased to 80

## 2) World drop tables

All world enemies can drop one world material with the rarity split below.

### Popielna Kuznia
- Common (65%): Zarowy Odlamek x1-2
- Rare (27%): Rdzen Lawy x1
- Epic (8%): Serce Eruptora x1

### Zelazne Pogranicze
- Common (65%): Stalowy Nit x1-2
- Rare (27%): Ostrze Weterana x1
- Epic (8%): Pieczec Kuzni x1

### Sztormowe Iglice
- Common (65%): Iskra Chmur x1-2
- Rare (27%): Kondensator Burzy x1
- Epic (8%): Korona Piorunow x1

### Mutageniczne Mokradla
- Common (65%): Sluz Mutagenu x1-2
- Rare (27%): Niestabilny Genom x1
- Epic (8%): Matryca Chimery x1

### Zlote Katakumby
- Common (65%): Pradawna Moneta x1-3
- Rare (27%): Kontrakt Cieni x1
- Epic (8%): Relikwia Skarbca x1

## 3) World mutation tables (numeric odds)

Mutation draft currently offers 3 cards. Proposed odds by world are below.

### Global rarity odds per offered card
- Worlds 1-2: common 72%, rare 24%, epic 4%
- World 3: common 64%, rare 30%, epic 6%
- World 4: common 56%, rare 34%, epic 10%
- World 5: common 48%, rare 38%, epic 14%

### World 1 (fire focus)
- Plomien Krytyczny (common)
  - +12% chance to apply burn for 3 s
  - Burn tick: 1 damage every 0.5 s
- Skora Bazaltowa (rare)
  - -20% fire damage taken
- Afterburn (epic)
  - On enemy death: 60 px explosion, 14 damage

### World 2 (blade focus)
- Mistrz Kontry (common)
  - Perfect timing window: 220 ms
  - On success: next hit +40% damage
- Tnaca Aura (rare)
  - Aura radius 55 px
  - Tick damage: 3 every 0.6 s
- Pancerz Segmentowy (epic)
  - On hit taken: 35% damage reduction for 1.8 s
  - Internal cooldown: 10 s

### World 3 (storm focus)
- Lancuch Uderzen (common)
  - Melee and arrow can chain to 1 extra target
  - Chain damage multiplier: 0.7x
- Nadprzewodnik (rare)
  - Bow XP cost reduced by 20%
  - Shield drain interval improved from 120 ms to 150 ms
- Faraday Dash (epic)
  - Dash grants 30 shield for 1.0 s
  - Internal cooldown: 6 s

### World 4 (mutation focus)
- Losowy Booster (common)
  - Every new wave: random +10% bonus to dmg, speed, or xp gain for that wave
- Regeneracja Tkanek (rare)
  - On 5-kill streak: heal 1 heart
  - Internal cooldown: 12 s
- Adaptacja (epic)
  - Gain 45% resistance to last received damage type for 3 s

### World 5 (risk/reward focus)
- Hazardzista (common)
  - +18% coin gain
  - +10% enemy damage taken
- Odsetki (rare)
  - At wave end: gain coins equal to 8% of current coins (cap 45)
- Zlota Tarcza (epic)
  - 15% of gained coins converted to temporary shield
  - Shield cap: 120
  - Shield decay: 8 per second out of combat

## 4) Integration note for prototype

To keep compatibility with current code:
- keep existing `MUTATION_RARITIES` for now in code,
- apply world-based rarity odds only during wave mutation drafts,
- keep existing boss slots and map world bosses to run milestones:
  - world boss 1/2/4 can be optional challenge bosses,
  - world boss 3 = mini boss slot,
  - world boss 5 = final boss slot.
