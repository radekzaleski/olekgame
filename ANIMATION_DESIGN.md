# Animacje i Visual Effects - Specyfikacja v1.0

## 1. Filozofia

- **Styl**: Pixel art z płynnymi przejściami
- **FPS**: 60fps z delta-time
- **Priorytety**:
  1. Gracz (bo to postać gracza)
  2. UI feedback (hit effects, particles)
  3. Wrogowie
  4. Bossowie
  5. Tło i atmosphere

---

## 2. Animacje Gracza

### 2.1 Idle (stan bezczynności)
- **Opis**: Delikatne "oddychanie" - skalowanie Y między 0.98 a 1.0
- **Czas**: 800ms na cykl
- **Easing**: sin wave

### 2.2 Bieg (Left/Right)
- **Opis**: 
  - Nogi naprzemiennie do przodu/do tyłu (rotation)
  - Ręce wahają się przeciwnie do nóg
  - Lekkie podskakiwanie Y (2px)
- **Czas**: 200ms na krok
- **Easing**: ease-in-out

### 2.3 Skok
- **Opis**:
  - W fazie wznoszenia: nogi do tyłu, ręce w górę
  - W fazie opadania: nogi w dół, ręce w górę
- **Czas**: Zależny od fizyki

### 2.4 Lądowanie
- **Opis**: 
  - Squish effect: Y scale do 0.85 na 50ms
  - Powrót do 1.0 przez 100ms
  - Particle kurzu (3-5 szarych kropek)
- **Czas**: 150ms total

### 2.5 Atak (miecz)
- **Obecne**: Prosta linia
- **Nowe**:
  - Broń zatacza pełny łuk 270° (nie 144°)
  - Ruch z easing: szybki start, wolniejszy koniec
  - Trail effect (5-6 poświat)
  - Particle przy trafieniu (8-12 iskier)

### 2.6 Strzała z łuku
- **Obecne**: Strzała z trailem
- **Nowe**:
  - Animacja naciągu łuku (ręka do tyłu)
  - Release: ręka szybko do przodu
  - Więcej particles przy wystrzale (10)

### 2.7 Tarcza (block)
- **Obecne**: Statyczny okrąg
- **Nowe**:
  - Pulsująca poświata (alpha 0.3-0.6)
  - Block effect: niebieskie linie od środka
  - Screen shake przy blocku

---

## 3. Animacje Wrogów

### 3.1 Chód
- **Opis**: 
  - Przechylanie w stronę ruchu (max 5°)
  - "Stępa" - nogi w miejscu, ciało idzie
- **Czas**: 300ms na krok
- **Easing**: step function

### 3.2 Atak
- **Obecne**: Broń statyczna
- **Nowe**:
  - Windup: broń do tyłu (100ms)
  - Strike: broń do przodu (80ms)
  - Recovery: powrót (150ms)
  - Różne animacje dla różnych broni

### 3.3 otrzymanie obrażeń
- **Obecne**: Nic
- **Nowe**:
  - Flash koloru: biały → normalny (100ms)
  - Cofnięcie: x -= direction * 8px
  - Krzyk text (opcjonalnie)
  - 3-5 particles obrażeń

### 3.4 Śmierć
- **Obecne**: Znika
- **Nowe**:
  - Upadek na ziemię (rotation 90°)
  - Zanik alpha 1.0 → 0.0 (500ms)
  - Blood particles (czerwone, 10-15)
  - Optional: ragdoll (proste rozłożenie)

### 3.5 Elite
- **Obecne**: Żółta poświata
- **Nowe**:
  - Pulsująca poświata (0.5s period)
  - Większy rozmiar (1.1x)
  - Particle aura wokół

---

## 4. Animacje Bossów

### 4.1 Ruch
- **Opis**: 
  - Większe przechylanie (8°)
  - Wolniejszy, cięższy krok
  - Screen shake przy kontakcie

### 4.2 Ataki specjalne (per boss)

**Fire Boss (Krol Zaru)**:
- Fala ognia: Czerwone particles lecące w stronę gracza
- Deszcz meteorytów: Orange circles spadające z góry
- Plonący szarż: Red trail, screen shake

**Blade Boss (General Ostrzy)**:
- Wir kling: Rotacja bossa 360°, blade trail
- Rykoszet: Strzała odbija się do tyłu
- Doskok: Dust trail, impact effect

**Storm Boss (Wladca Burzy)**:
- Znaczniki pioruna: Yellow markers, potem strike
- Łańcuch błyskawic: Linie między celami
- Skok burzowy: Teleport effect + shockwave

### 4.3 Zmiana fazy
- **Opis**:
  - Flash ekranu
  - Boss zmienia kolor (darker/different hue)
  - particles eksplozji

---

## 5. Effects System

### 5.1 Particles System (istniejący - rozszerzyć)

**Istniejące typy**:
- `isText` - floating text (XP, coins)
- `isRing` - rozszerzające się koło
- `isShield` - trójkąty tarczy
- `isStar` - gwiazdki

**Nowe typy do dodania**:
- `isDust` - szare kropki przy lądowaniu
- `isBlood` - czerwone kropki przy obrażeniach
- `isFire` - pomarańczowe/czerwone cząstki
- `isSwordTrail` - ślady miecza
- `isExplosion` - eksplozja z gradientem
- `isLightning` - linie błyskawic
- `isPoof` - dym/zniknięcie

### 5.2 Screen Effects
- **Damage flash**: Red overlay (istnieje)
- **Block**: Blue flash
- **Heavy hit**: Screen shake (x/y offset)
- **Boss spawn**: Zoom in + flash

### 5.3 UI Animations
- **HP change**: Smooth interpolation
- **Coins**: Pop animation (+X text)
- **XP bar**: Fill animation
- **Toast notifications**: Slide in/out

---

## 6. Środowisko (Tło)

### 6.1 Niebo
- Gradient (istnieje)
- Dodaj: przelatujące ptaki (2px, białe)
- Dodaj: zmieniające się chmury (rozszerzyć obecne)

### 6.2 Efekty pogodowe per świat
- **Fire**: Red particles (żar), occasional flare
- **Storm**: Lightning flashes (co 5-10s), rain lines
- **Blade**: Metal dust particles
- **Mutation**: Green floating spores

---

## 7. Audio-Visual Sync

- **Atak**: Sound + visual flash
- **Trafienie**: Sound + hit particles + screen shake
- **Śmierć wroga**: Sound + death particles + XP popup
- **Boss attack**: Longer telegraph + distinct sound

---

## 8. Technical Implementation

### 8.1 Animation Controller
```javascript
// Nowy system animacji
const animations = {
  player: {
    idle: { frames: 1, speed: 1, loop: true },
    run: { frames: 4, speed: 8, loop: true },
    jump: { frames: 2, speed: 1, loop: false },
    attack: { frames: 6, speed: 12, loop: false }
  }
};
```

### 8.2 Sprite Sheet Format
- Każda animacja: osobny wiersz
- Frame duration: stały lub zmienny per klatka
- Direction: mirror dla left/right

### 8.3 Performance
- Object pooling dla particles
- Max 100 particles
- Usuwanie off-screen entities
- Delta-time based animations

---

## 9. Priority Implementacji

### Faza 1 - Must Have (MVP)
1. ✅ Gracz: Idle breathing
2. ✅ Gracz: Run animation (wahadło)
3. ✅ Gracz: Landing dust
4. ✅ Gracz: Lepszy attack trail
5. ✅ Wrogowie: Hit flash + knockback
6. ✅ Wrogowie: Death animation
7. ✅ Particles: Dust, blood types

### Faza 2 - Should Have
1. Boss: Phase change effects
2. Boss: Ataki specjalne (particles)
3. Environment: Weather particles
4. UI: Smooth HP transitions

### Faza 3 - Nice to Have
1. Sprite sheets (zamiast rect)
2. Screen shake
3. Więcej szczegółów wrogów
4. Pełne sprite'y bossów