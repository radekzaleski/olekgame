# Tabela balansu i contentu (dla dewelopera)

Zrodla: `index.html` (aktywny prototyp runtime) + `GAME_DESIGN.md` (opis designu).

## 1) Swiaty (flow runu)

| Kolejnosc | worldId | Nazwa | Fale | Kolor UI | enemyPalette |
|---|---|---|---|---|---|
| 1 | fire | Popielna Kuznia | 1-2 | #ef4444 | 1 |
| 2 | blade | Zelazne Pogranicze | 3-4 | #9ca3af | 0 |
| 3 | storm | Sztormowe Iglice | 5-6 | #38bdf8 | 2 |
| 4 | mutation | Mutageniczne Mokradla | 7-8 | #22c55e | 0 |
| 5 | gold | Zlote Katakumby | 9-10 | #fbbf24 | 1 |

## 2) Potwory (enemy generation)

### 2.1 Rozmiary i skalowanie

| Size | Nazwa | W/H | HP mul | Speed mul |
|---|---|---|---|---|
| small | maly | 24x26 | 0.85 | 1.18 |
| medium | sredni | 30x34 | 1.05 | 1.00 |
| large | duzy | 38x44 | 1.35 | 0.84 |

### 2.2 Palette (wizual)

| Palette idx | Skin | Body | Eye | Detail | Label |
|---|---|---|---|---|---|
| 0 | #22c55e | #15803d | #f8fafc | #14532d | Blogosz |
| 1 | #f97316 | #c2410c | #fff7ed | #7c2d12 | Ogniarz |
| 2 | #a78bfa | #6d28d9 | #f5f3ff | #4c1d95 | Mrozek |

### 2.3 Typy potworow

| base | Przykladowe tytuly | Przykladowe kill msg |
|---|---|---|
| zombie | zombie, chodak, trup, rozkladajacy sie | pokonany!, zgnily!, rozpadowy!, nie zyje! |
| wojownik | wojownik, zbrojny, zolnierz, obronca | pokonany!, zlamany!, nie mial szans!, powalony! |
| zlodziej | zlodziej, szuler, zabojca, assasyn | zlapany!, unicszony!, za wolny!, wyeliminowany! |
| barbarzynca | barbarzynca, bestia, szalownik, dzikusz | poskromiony!, dziczy!, ugladzony!, zmiazdzony! |

### 2.4 Klasy i bronie enemy

| Kategoria | Wartosci |
|---|---|
| enemyWeapons | sztylet, wlocznia, mlot |
| enemyClasses | Zwiadowca, Straznik, Szlachcic, Najemnik, Kaplan, Mnich |

### 2.5 Formula i progi spawnu

| Parametr | Wartosc / formula |
|---|---|
| Bazowe HP enemy | `(14 + wave * 2.5) * hpMul` |
| Bazowa predkosc enemy | `(0.72 + wave * 0.08) * speedMul` (cap `1.85`) |
| Elite unlock | od `wave >= 6` |
| Elite chance | `min(0.08 + wave*0.015, 0.28)` |
| Elite HP multiplier | `1.45x` |
| Armor chance | `min(0.2 + wave*0.04, 0.72)` |
| Helmet chance | `min(0.1 + wave*0.05, 0.8)` |
| Weapon chance | `min(0.25 + wave*0.06, 0.9)` |

## 3) Bossowie

### 3.1 Bossowie runu (world bosses)

| worldId | Boss | HP | Speed | Contact dmg | Mini HP (0.6x) |
|---|---|---:|---:|---:|---:|
| fire | Krol Zaru | 180 | 0.85 | 2 | 108 |
| blade | General Ostrzy | 230 | 0.95 | 2 | 138 |
| storm | Wladca Burzy | 290 | 1.00 | 3 | 174 |
| mutation | Hydra Genow | 360 | 0.90 | 3 | 216 |
| gold | Poborca Cieni | 460 | 1.05 | 3 | 276 |

### 3.2 Ataki bossow (skrot tuningowy)

| Boss | Atak | Kluczowe parametry |
|---|---|---|
| Krol Zaru | Fala Ognia | telegraph 850ms, width 180, dmg 2, cd 5000ms |
| Krol Zaru | Deszcz Meteorytow | telegraph 1100ms, hits 3, dmg/hit 1, cd 8500ms |
| Krol Zaru | Plonacy Szarz | telegraph 500ms, dash 260, dmg 2, cd 7000ms |
| General Ostrzy | Wir Kling | telegraph 650ms, radius 90, dmg 2, dur 1800ms, cd 6000ms |
| General Ostrzy | Rykoszet | telegraph 1600ms, reflectMul 1.25, cd 9000ms |
| General Ostrzy | Doskok Egzekutora | telegraph 400ms, dash 220, dmg 2, slow 600ms, cd 5500ms |
| Wladca Burzy | Znaczniki Pioruna | telegraph 1200ms, markers 2+, dmg 2, cd 6500ms |
| Wladca Burzy | Lancuch Blyskawic | telegraph 800ms, jumps 3, jumpRng 180, dmg 1, cd 7500ms |
| Wladca Burzy | Skok Burzowy | telegraph 450ms, shockwaveRng 120, dmg 2, cd 8000ms |
| Hydra Genow | Plucie Mutagenem | telegraph 900ms, pools 2+, poolDur 7000ms, cd 6000ms |
| Hydra Genow | Losowa Adaptacja | telegraph 500ms, rotationTime 20000ms, cd 20000ms |
| Hydra Genow | Rozszczepienie | telegraph 700ms, summons 2, summonHp 42, dur 12000ms, cd 12000ms |
| Poborca Cieni | Podatek Krwi | telegraph 700ms, steal 12% (8-60), bonus thresh 40, cd 6800ms |
| Poborca Cieni | Dluznicy | telegraph 800ms, summons 3+, summonHp 34, summonDmg 1, cd 9500ms |
| Poborca Cieni | Pieczec Chciwosci | telegraph 900ms, dmgByCoins [0->1,150->2,300->3], cd 8200ms |

### 3.3 Fazy bossow (co sie zmienia)

| Boss | Faza 1 | Faza 2 | Faza 3 |
|---|---|---|---|
| Krol Zaru | hp>=70%, cdMul 1.0 | hp>=35%, cdMul 0.85, lavaCracks | hp<35%, lava tick 1/1200ms |
| General Ostrzy | hp>=60%, bez trapow | hp>=25%, trapInt 10000ms | hp<25%, bleed 1/2500ms |
| Wladca Burzy | hp>=65%, teleport 0.3 | hp>=30%, cdMul 0.82 | hp<30%, telegraphReduced 850ms |
| Hydra Genow | hp>=70%, baseline | hp>=40%, dmgReduct 0.15 | hp<40%, summonCdMul 0.75 |
| Poborca Cieni | hp>=75%, debt off | hp>=35%, debt +5%/hit (max4, 10s) | hp<35%, summonCdMul 0.7, maxSteal 80 |

### 3.4 Bossowie debug/manual (poza run loop)

| kind | Name | HP | Reward unlock |
|---|---|---:|---|
| fire | Ognik | 120 | fire |
| blade | Mistrz Szabli | 140 | blade |
| storm | Burzak | 150 | storm |

## 4) Bronie i moce gracza

| Kategoria | Elementy |
|---|---|
| Aktywne moce | basic, fire, blade, storm |
| Synergie mocy | fire_blade (Ognista Szabla), fire_storm (Plomienna Burza), blade_storm (Wir Szabli), tri (Legenda 3 Mocy) |
| Skill: bow | koszt `15 XP` |
| Skill: shield | koszt `1 XP` co tick |
| Shield drain interval | `120ms` (base) |

## 5) Dropy swiatow

| worldId | Common | Rare | Epic |
|---|---|---|---|
| fire | Zarowy Odlamek x1-2 | Rdzen Lawy x1 | Serce Eruptora x1 |
| blade | Stalowy Nit x1-2 | Ostrze Weterana x1 | Pieczec Kuzni x1 |
| storm | Iskra Chmur x1-2 | Kondensator Burzy x1 | Korona Piorunow x1 |
| mutation | Sluz Mutagenu x1-2 | Niestabilny Genom x1 | Matryca Chimery x1 |
| gold | Pradawna Moneta x1-3 | Kontrakt Cieni x1 | Relikwia Skarbca x1 |

## 6) Mutacje i rarity

### 6.1 World rarity odds (draft kart mutacji)

| Swiat (kolejnosc) | Common | Rare | Epic |
|---|---:|---:|---:|
| 1 (fire) | 72 | 24 | 4 |
| 2 (blade) | 72 | 24 | 4 |
| 3 (storm) | 64 | 30 | 6 |
| 4 (mutation) | 56 | 34 | 10 |
| 5 (gold) | 48 | 38 | 14 |

### 6.2 World mutations (po 3/swiat)

| worldId | common | rare | epic |
|---|---|---|---|
| fire | Plomien Krytyczny | Skora Bazaltowa | Afterburn |
| blade | Mistrz Kontry | Tnaca Aura | Pancerz Segmentowy |
| storm | Lancuch Uderzen | Nadprzewodnik | Faraday Dash |
| mutation | Losowy Booster | Regeneracja Tkanek | Adaptacja |
| gold | Hazardzista | Odsetki | Zlota Tarcza |

### 6.3 Global mutation db i synergie

| Typ | Ilosc | Notatka |
|---|---:|---|
| MUTATIONS_DB | 12 | fallback pool gdy brak kandydatow worldowych |
| SYNERGIES | 6 | odpalane gdy gracz ma komplet tagow |
| MUTATION_TAGS | 6 | fire, blade, storm, defense, mobility, attack |
| MUTATION_RARITIES (global) | common/rare/epic = 60/30/10 | obecnie nadal istnieje jako baseline |

## 7) Inne zmienne kluczowe (balans runu)

| Kategoria | Zmienna | Wartosc |
|---|---|---|
| Run | liczba fal | 10 |
| Run | mini boss trigger | wave >= 5 |
| Run | final boss trigger | wave >= 10 |
| Fale | enemyWave.every | 3500ms |
| Fale | start enemiesInWave | 2 |
| Skrzynki | chestSpawn.every | 12000ms |
| XP/HP | xpToNextHeart | 50 |
| XP/HP | bazowe serca | 3 |
| Reward | essence gain | `floor(wave*6 + kills*2 + (victory?80:20))` |
| Player | speed | 2.7 |
| Player | jump | -10.5 |
| Physics | gravity | 0.5 |

## 8) Gdzie to edytowac (szybka mapa pliku)

| Obszar | Szukaj w kodzie |
|---|---|
| Swiaty | `const WORLDS` |
| Dropy | `const WORLD_DROPS` |
| Mutacje per swiat | `const WORLD_MUTATIONS` |
| Szanse rarity per swiat | `const WORLD_RARITY_ODDS` |
| Bossowie runu | `const WORLD_BOSSES` |
| Potwory (archetypy i bronie) | `enemySizes`, `enemyTypes`, `enemyWeapons`, `enemyClasses` |
| Globalne mutacje/synergie | `MUTATIONS_DB`, `SYNERGIES` |
| Spawn i scaling enemy | `function spawnEnemy()` |
| Run economy / reward | `function endRun()` |
