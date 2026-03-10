# VISUAL DESIGN - Iteracja 2

Dokumentacja warstwy wizualnej dla dewelopera. Specyfikacja assetów, parametrów i zachowań.

---

## 1. HIT FEEDBACK SYSTEM (I2-H5)

### 1.1 Freeze Frame
| Parametr | Wartość | Uwagi |
|----------|---------|-------|
| Duration | 2-3 frames (~50ms @ 60fps) | Tylko przy dmg ≥ 8 |
| Trigger | Elite enemies, Boss attacks | Nie przy zwykłych ciosach |
| Implementation | `state.freezeFrame = 3` | W `step()` sprawdzać przed update |

```javascript
// W step() - na początku
if (state.freezeFrame > 0) {
  state.freezeFrame--;
  return; // pomija update this frame
}
```

### 1.2 Directional Trails (Slash Lines)
| Parametr | Wartość |
|----------|---------|
| Length | 20-60px (skalowane od dmg) |
| Width | 2-4px |
| Color | Kolor ataku gracza (fire=red, blade=silver, storm=blue) |
| Duration | 8-12 frames |
| Easing | Fast out, slow end (alpha 1.0 → 0.0) |

**Render**: `ctx.moveTo(startX, startY); ctx.lineTo(endX, endY);` z gradientem alpha.

### 1.3 Impact Decals (Winietki)
| Parametr | Wartość |
|----------|---------|
| Type | Radial gradient na środku ekranu |
| Color | Różowy/czerwony (#ff6b6b → transparent) |
| Radius | 150px → 300px (rozszerza się) |
| Duration | 15 frames |
| Trigger | Boss melee hit, elite hit |

```javascript
// Render decal
const gradient = ctx.createRadialGradient(w/2, h/2, 0, w/2, h/2, 150 + frame * 10);
gradient.addColorStop(0, `rgba(255, 107, 107, ${0.3 - frame * 0.02})`);
gradient.addColorStop(1, 'transparent');
ctx.fillStyle = gradient;
ctx.fillRect(0, 0, w, h);
```

---

## 2. TELEGRAPH SHAPE LANGUAGE (I2-H6)

### 2.1 Shape Key
| Kształt | Znaczenie | Kolor base |
|---------|-----------|------------|
| Square (kwadrat) | AoE (area of effect) | #ef4444 (red) |
| Triangle (trójkąt) | Dash/Charge kierunkowy | #fbbf24 (yellow) |
| Circle (koło) | Ranged/Projectile | #38bdf8 (blue) |
| Hexagon (sześciokąt) | Special (summon/phase) | #a855f7 (purple) |

### 2.2 Telegraph Parameters
| Parametr | Wartość |
|----------|---------|
| Fill opacity | 0.15 → 0.35 (pulsujące) |
| Outline width | 2px |
| Outline opacity | 0.5 → 0.9 (pulsujące) |
| Pulse frequency | 8Hz (133ms per cycle) |
| Warning time | `boss.attacks[i].telegraph` ms (z GAME_DESIGN.md) |

### 2.3 Pulsowanie (pseudocode)
```javascript
const pulsePhase = (performance.now() / 133) % 1; // 133ms = 8Hz
const fillAlpha = 0.15 + pulsePhase * 0.2;
const outlineAlpha = 0.5 + pulsePhase * 0.4;

// Render shapes zgodnie z typem ataku
switch(attackShape) {
  case 'square': renderAoE(x, y, w, h, fillAlpha, outlineAlpha); break;
  case 'triangle': renderDash(dir, x, y, w, h, fillAlpha, outlineAlpha); break;
  case 'circle': renderRadius(x, y, radius, fillAlpha, outlineAlpha); break;
  case 'hexagon': renderHex(x, y, size, fillAlpha, outlineAlpha); break;
}
```

### 2.4 Mapowanie ataków bossów (z GAME_DESIGN.md)
| Boss | Attack | Shape | Telegraph (ms) |
|------|--------|-------|----------------|
| Krol Zaru | Fala Ognia | Triangle | 850 |
| Krol Zaru | Deszcz Meteorytow | Circle (markers) | 1100 |
| Krol Zaru | Plonacy Szarz | Triangle | 500 |
| General Ostrzy | Wir Kling | Circle | 650 |
| General Ostrzy | Rykoszet | Square (reflect zone) | 1600 |
| General Ostrzy | Doskok Egzekutora | Triangle | 400 |
| Wladca Burzy | Znaczniki Pioruna | Circle | 1200 |
| Wladca Burzy | Lancuch Blyskawic | Hexagon (chain) | 800 |
| Wladca Burzy | Skok Burzowy | Triangle | 450 |
| Hydra Genow | Plucie Mutagenem | Circle (pools) | 900 |
| Hydra Genow | Losowa Adaptacja | Hexagon | 500 |
| Hydra Genow | Rozszczepienie | Hexagon | 700 |
| Poborca Cieni | Podatek Krwi | Square | 700 |
| Poborca Cieni | Dluznicy | Hexagon (summons) | 800 |
| Poborca Cieni | Pieczec Chciwosci | Square | 900 |

---

## 3. PARALLAX BACKGROUNDS (I2-N1)

### 3.1 Layer Configuration
| Layer | Parallax Factor | Speed | Element Size |
|-------|-----------------|-------|--------------|
| Far (0.2x) | 0.2 | 0.1 px/frame | Duże (300-500px) |
| Mid (0.5x) | 0.5 | 0.25 px/frame | Średnie (100-200px) |
| Fore (0.8x) | 0.8 | 0.4 px/frame | Małe (30-80px) |

### 3.2 Per-World Assets

**Fire World (Popielna Kuznia)**
```
Far:  [color=#2d1111] ciemne niebo wulkaniczne, pomarańczowa poświata
       shapes: rozległe góry, chmury dymu
Mid:  [color=#4a1f1f] skalne szczyty, słupy dymu
       shapes: pionowe formacje, języki lawy w tle
Fore: [color=#5a2a2a] dymiące szczeliny, iskry
       shapes: małe elementy, particle iskier
```

**Blade World (Zelazne Pogranicze)**
```
Far:  [color=#1a1a1a] stalowe niebo, kratownice
Mid:  [color=#2d2d2d] metalowe konstrukcje, mosty
Fore: [color=#3d3d3d] metalowe szczątki, iskry spawalnicze
```

**Storm World (Sztormowe Iglice)**
```
Far:  [color=#0a1a2a] burzowe chmury, błyskawice
Mid:  [color=#112233] iglice, skały wystające z chmur
Fore: [color=#1a3040] krople deszczu, mgiełka
```

**Mutation World (Mutageniczne Mokradla)**
```
Far:  [color=#0a1a0a] zielonkawa mgła, wielkie grzyby
Mid:  [color=#112211] trujące rośliny, bąble
Fore: [color=#1a2a1a] pęcherzyki, unoszące się geny
```

**Gold World (Zlote Katakumby)**
```
Far:  [color=#1a1608] złote sklepienia, starożytne ruiny
Mid:  [color=#2d2611] kolumny, posągi
Fore: [color=#3d3520] złote drobiny, promienie światła
```

### 3.3 Implementation
```javascript
const parallaxLayers = [
  { factor: 0.2, elements: [] }, // far
  { factor: 0.5, elements: [] }, // mid
  { factor: 0.8, elements: [] }  // fore
];

function renderBackground() {
  const offset = state.player.x * state.cameraX;
  
  parallaxLayers.forEach((layer, idx) => {
    layer.elements.forEach(el => {
      const x = el.baseX - offset * layer.factor;
      ctx.fillStyle = el.color;
      ctx.fillRect(x, el.y, el.w, el.h);
    });
  });
}
```

---

## 4. ENEMY ROLE SILHOUETTES (I2-N2)

### 4.1 Shape Definitions
| Role | Body Shape | Weapon Position | Key Feature |
|------|------------|-----------------|-------------|
| Charger | Pochylony do przodu (15°), szerokie ramiona | Broń przy ciele | Masywna sylwetka |
| Ranged | Wyprostowany, jedna ręka wyciągnięta | Broń przedłużona | Smukły profil |
| Buffer | Normalny, ręce uniesione | Brak lub amulet | Elementy nad głową |
| Summoner | Otoczony mgłą/aurą | Ręce w geście | Dodatkowe elementy (rogi, skrzydła) |

### 4.2 Visual Cues Per Role
```javascript
const ROLE_VISUALS = {
  charger: {
    bodyAngle: 0.26, // ~15 stopni
    shoulderWidth: 1.3,
    weaponClose: true,
    aura: null,
    extraElements: []
  },
  ranged: {
    bodyAngle: 0,
    shoulderWidth: 0.9,
    weaponClose: false,
    weaponReach: 1.4,
    aura: null,
    extraElements: []
  },
  buffer: {
    bodyAngle: 0,
    shoulderWidth: 1.0,
    weaponClose: false,
    handHeight: 1.3, // ręce w górze
    aura: { type: 'glow', color: ROLE_COLORS.buffer },
    extraElements: ['totem', 'charm', 'floating_orb']
  },
  summoner: {
    bodyAngle: 0,
    shoulderWidth: 1.1,
    aura: { type: 'mist', color: ROLE_COLORS.summoner },
    extraElements: ['horns', 'wings', 'shadow_clone']
  }
};
```

### 4.3 Render Priority
1. Aura/mist (jeśli istnieje) - render za postacią
2. Extra elements (rogi, skrzydła)
3. Body z kątem
4. Weapon
5. Aura glow (jeśli buffer) - render na wierzchu z alpha

---

## 5. WORLD AMBIENT FX (I2-N3)

### 5.1 Per-World Effects
| World | Primary FX | Secondary FX | Particles |
|-------|------------|--------------|-----------|
| Fire | iskry (20-30/s), pomarańczowa mgiełka | dym z podłogi (5/s) | #f97316, #ef4444 |
| Blade | metaliczny pył (15/s) | iskry spawalnicze (3/s) | #9ca3af, #d1d5db |
| Storm | krople deszczu (40/s) | błyskawice w tle (co 5s) | #38bdf8, #0ea5e9 |
| Mutation | bąbelny (10/s), zielona mgiełka | geny/DNA (2/s) | #22c55e, #86efac |
| Gold | złote drobiny (25/s) | promienie światła (co 8s) | #fbbf24, #fcd34d |

### 5.2 Particle System Parameters
```javascript
const AMBIENT_FX = {
  fire: {
    sparks: {
      spawnRate: 25, // per second
      x: 'random_arena',
      y: 'ground',
      vy: -2 to -4,
      vx: -0.5 to 0.5,
      life: 60-90 frames,
      color: ['#f97316', '#ef4444'],
      size: 1-3px,
      fadeOut: true
    },
    haze: {
      spawnRate: 5,
      x: 'random_arena', 
      y: 'ground to mid',
      vy: -0.2,
      life: 180 frames,
      color: '#f9731640', // 25% alpha
      size: 40-80px,
      blur: true
    }
  },
  // ... similar for other worlds
};
```

### 5.3 Lightning (Storm World only)
| Parametr | Wartość |
|----------|---------|
| Interval | 5000ms ± 2000ms random |
| Duration | 80-150ms |
| Branches | 2-4 |
| Color | #38bdf8 → #0ea5e9 |
| Position | Górna 30% ekranu |
| Audio | S1: thunder crack (opcjonalnie) |

```javascript
function renderLightning() {
  // Branch algorithm (fractal)
  const startX = random(0, w);
  const startY = 0;
  let x = startX, y = startY;
  
  ctx.strokeStyle = '#38bdf8';
  ctx.lineWidth = 2;
  ctx.beginPath();
  ctx.moveTo(x, y);
  
  while (y < h * 0.3) {
    x += random(-20, 20);
    y += random(10, 25);
    ctx.lineTo(x, y);
    // chance to branch
    if (random() < 0.3) {
      // draw branch
    }
  }
  ctx.stroke();
}
```

---

## 6. BOSS ARENA MECHANICS (I2-H4)

### 6.1 Lava Cracks (Fire Boss Phase 3)
| Parametr | Wartość |
|----------|---------|
| Count | 2 cracks |
| Shape | Kręta linia (bezier curves) |
| Color base | #7f1d1d |
| Color glow | #ef4444 |
| Glow pulse | 0.5-1.0 alpha, 1Hz |
| Tick indicator | #fb923c center line |
| Damage tick | Co 1200ms |

```javascript
const lavaCracks = [
  { points: [{x: 100, y: ground}, {x: 200, y: ground-20}, ...] },
  { points: [...] }
];

function renderLavaCracks() {
  lavaCracks.forEach(crack => {
    // Base crack
    ctx.strokeStyle = '#7f1d1d';
    ctx.lineWidth = 8;
    ctx.strokePolyline(crack.points);
    
    // Glow
    const pulse = 0.5 + Math.sin(performance.now() / 500) * 0.5;
    ctx.strokeStyle = `rgba(239, 68, 68, ${pulse})`;
    ctx.lineWidth = 4;
    ctx.strokePolyline(crack.points);
    
    // Center tick indicator
    ctx.fillStyle = '#fb923c';
    crack.points.forEach(p => ctx.fillRect(p.x - 2, p.y - 2, 4, 4));
  });
}
```

### 6.2 Blade Traps (Blade Boss Phase 2)
| Parametr | Wartość |
|----------|---------|
| Shape | Diament (rotated square) |
| Size | 40x40px |
| Color inactive | #4b556340 (20% gray) |
| Color active | #ef4444 |
| Active duration | 2200ms |
| Interval | 10000ms |
| Animation | Scale 0 → 1, then flash on activate |

### 6.3 Storm Pylons (Storm Boss)
| Parametr | Wartość |
|----------|---------|
| Shape | Column/cylinder |
| Height | 100-150px |
| Color | #38bdf8 with white top |
| Particles | Spikes rising (10/s each) |
| Activation | Glow intensifies on boss attack |

### 6.4 Mutagen Pools (Mutation Boss)
| Parametr | Wartość |
|----------|---------|
| Shape | Amorphous blob (circle + distortion) |
| Size | 60-80px diameter |
| Color | #22c55e → #86efac gradient |
| Animation | Bubbles rising (5/s per pool) |
| Effect inside | Random buff/debuff icon overlay |

---

## 7. WAVE MUTATOR UI (I2-M1)

### 7.1 HUD Display
```
┌─────────────────────────────────────┐
│ MUTATOR: LOW GRAVITY                │
│ ↑ Skok +40%  |  Spadek -30%        │
└─────────────────────────────────────┘
```

| Parametr | Wartość |
|----------|---------|
| Position | Pod przyciskiem mutacji |
| Background | #0f172a z 2px border |
| Text color | #a855f7 (epic purple) |
| Icon size | 16x16px per effect |
| Display duration | 3 seconds on wave start |

### 7.2 Mutator Icons
| Mutator | Icon | Color |
|---------|------|-------|
| Low Gravity | ↑ arrow | #38bdf8 |
| Toxic Ground | ☣ symbol | #22c55e |
| Fast Projectiles | →→ arrow | #f59e0b |
| Extra Enemies | ⚔ crossed | #ef4444 |
| Healing x0.5 | ♡ broken | #ec4899 |
| Coin Bonus | $ gold | #fbbf24 |

---

## 8. CHEST VARIANTS (I2-M4)

### 8.1 Visual Differences
| Type | Color | Particles | Size |
|------|-------|-----------|------|
| Standard | #854d0e (gold) | Standard sparkle | 24x24 |
| Cursed | #7f1d1d (dark red) | Red mist, skull | 28x28 |
| Safe (heal) | #22c55e (green) | Hearts rising | 24x24 |

### 8.2 Animation States
1. **Idle**: Gentle pulse (scale 1.0 → 1.05)
2. **Approach**: Glow intensifies within 80px
3. **Open**: Flash + particles burst
4. **Loot reveal**: Item floats up with rarity glow

```javascript
const CHEST_STATES = {
  idle: { scalePulse: [1.0, 1.05], period: 1500 },
  approach: { glowRadius: [20, 60], glowColor: rarityColor },
  open: { flashFrames: 6, particleBurst: 15 },
  reveal: { floatY: -30, duration: 800 }
};
```

---

## 9. COLOR PALETTE REFERENCE

### 9.1 UI Colors
| Purpose | Hex | Usage |
|---------|-----|-------|
| Background 1 | #0f172a | Main bg |
| Background 2 | #1e293b | Panels |
| Text primary | #e2e8f0 | Main text |
| Text secondary | #94a3b8 | Labels |

### 9.2 Rarity Colors
| Rarity | Hex | Border |
|--------|-----|--------|
| Common | #94a3b8 | gray |
| Rare | #38bdf8 | blue |
| Epic | #a855f7 | purple |
| Legendary | #fbbf24 | gold |

### 9.3 Element Colors
| Element | Hex | Usage |
|---------|-----|-------|
| Fire | #ef4444 | Attacks, fire particles |
| Blade | #9ca3af | Blade attacks, metal |
| Storm | #38bdf8 | Ranged, electricity |
| Mutation | #22c55e | Bio effects |
| Gold | #fbbf24 | Coins, rewards |

---

## 10. ANIMATION TIMINGS

### 10.1 Common Transitions
| Animation | Duration | Easing |
|-----------|----------|--------|
| Button hover | 150ms | ease-out |
| Panel open | 200ms | ease-out |
| Toast appear | 180ms | ease-in-out |
| Damage flash | 80ms | instant |
| Hit react | 150ms | ease-out |

### 10.2 Particle Lifetimes
| Type | Min | Max |
|------|-----|-----|
| Blood | 20 | 35 frames |
| Fire | 14 | 26 frames |
| Dust | 20 | 30 frames |
| Impact | 12 | 18 frames |
| Ambient | 60 | 180 frames |

---

## 11. IMPLEMENTATION CHECKLIST

- [ ] I2-H5: Freeze frame system
- [ ] I2-H5: Directional slash trails
- [ ] I2-H5: Impact decals
- [ ] I2-H6: Telegraph shapes (4 types)
- [ ] I2-H6: Telegraph pulse animation
- [ ] I2-N1: Parallax background layers (3 worlds)
- [ ] I2-N1: World-specific assets
- [ ] I2-N2: Role silhouette differentiation
- [ ] I2-N3: Ambient FX particles (all worlds)
- [ ] I2-N3: Lightning system (storm world)
- [ ] I2-H4: Boss arena mechanics visual
- [ ] I2-M1: Wave mutator HUD display
- [ ] I2-M4: Chest variants visual