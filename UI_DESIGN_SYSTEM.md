# UI Design System - Mutacje Mocy

Dokument jest zrodlem prawdy dla warstwy UI. Kazdy nowy ekran, panel i komponent musi byc zgodny z tym plikiem.

## 1. Kontekst gry i cele UI

- Typ gry: arena action roguelite, run oparty o fale, mini-boss i final boss.
- Platforma docelowa: mobile-first (touch), ale layout musi dzialac tez na desktopie.
- Cel UI: natychmiastowa czytelnosc walki, szybkie decyzje i zero przeszkadzania gameplayowi.
- Priorytet: czytelnosc zagrozen > estetyka dekoracyjna.

## 2. Zasady nadrzedne

1. Czytelnosc w ruchu
   - UI musi byc zrozumiale podczas walki i ruchu postaci.
   - Informacje krytyczne (HP, cooldown, telegraph) sa zawsze widoczne i kontrastowe.

2. Spojnosc semantyczna
   - Kolor + ksztalt + ikona oznaczaja ten sam typ informacji w calym projekcie.
   - Nie wolno opierac znaczenia tylko na kolorze.

3. Mobile ergonomia
   - Wszystkie interaktywne elementy dotykowe maja minimum 44x44 px.
   - Najwazniejsze akcje sa w zasiegu kciuka.

4. Niski koszt poznawczy
   - Jeden panel = jedna decyzja glowna.
   - Maksymalnie 2 poziomy hierarchii informacji na ekranie.

## 3. Design tokens

### 3.1 Kolory bazowe

- `--bg1`: `#0f172a` (glowne tlo)
- `--bg2`: `#1e293b` (drugie tlo i panele)
- `--panel`: `rgba(15, 23, 42, 0.75)`
- `--ink`: `#e2e8f0` (tekst glowny)
- `--good`: `#22c55e` (stan pozytywny)
- `--warn`: `#f59e0b` (ostrzezenie)
- `--fire`: `#ef4444`
- `--blade`: `#a3a3a3`
- `--storm`: `#38bdf8`
- `--money`: `#facc15`

### 3.2 Rzadkosci i economy

- Common: `#94a3b8`
- Rare: `#38bdf8`
- Epic: `#a855f7`
- Legendary: `#fbbf24`

### 3.3 Semantyka telegraphow

- Square = AoE
- Triangle = Dash/Charge
- Circle = Projectile/Ranged
- Hexagon = Special/Summon/Phase

## 4. Typografia

- Font bazowy: `"Trebuchet MS", "Segoe UI", sans-serif`.
- Rozmiary:
  - H1: 28 px
  - H2: 22 px
  - Body: 14 px
  - Label/button: 13 px
  - Meta/pill: 11 px
  - XP micro text: 10 px
- Interlinia tekstu dluzszego: 1.45.
- Uzywaj pogrubienia tylko dla danych krytycznych (waluta, cooldown, hp, decyzje).

## 5. Siatka, odstepy, promienie

- Jednostka bazowa spacingu: 4 px.
- Standardowe odstepy: 6, 8, 10, 12, 16, 18 px.
- Radius system:
  - Chip/pill: 999 px
  - Przyciski male: 10 px
  - Karty/panele: 12-18 px
  - Arena: 16 px
- Border: 1 px, kolor `rgba(255,255,255,0.12-0.2)`.

## 6. Komponenty i wymiary referencyjne

### 6.1 Aplikacja i layout

- `#app`: grid `auto 1fr auto`, gap 6 px, safe-area insets.
- Brak scrolla pionowego i poziomego podczas walki.

### 6.2 HUD

- Panel HUD:
  - Radius 12 px
  - Padding 8 px
  - 2 kolumny, gap 6 px
  - Tlo z blur (panel translucent)
- XP bar:
  - Wysokosc 8 px
  - Radius 4 px
  - Animacja width 200 ms ease

### 6.3 Arena

- Obszar gry ma byc centralny i zawsze widoczny.
- `arenaWrap`:
  - Radius 16 px
  - Overflow hidden
  - Czytelny gradient tla bez konkurencji z postaciami.

### 6.4 Kontrolki

- Sekcja `.controls`:
  - 2 kolumny (pad + actions)
  - Min-height 180 px
  - Gap 8 px
- Przycisk globalnie:
  - Min-height 44 px
  - Radius 10 px
  - Padding 10x8 px
  - Font 13 px, bold
- Stany:
  - Active: delikatne przesuniecie `translateY(1px)`
  - Disabled/locked: `opacity ~0.45`

### 6.5 Overlays i modale

- Overlay przyciemnia tlo (`rgba(2,6,23,0.72-0.92)`), zatrzymuje tlo i focus gracza.
- Karta modala (`frontCard`):
  - max width 560 px
  - Radius 18 px
  - Padding 18 px
  - Delikatna animacja wejscia (ok. 240 ms)

### 6.6 Toast

- Pozycja: top-center.
- Styl: pill, lekko transparentny panel, border 1 px.
- Czas wejscia: 180 ms.
- Maksymalnie 1 aktywny toast naraz.

## 7. Motion i timing

- Hover/press feedback: 150 ms.
- Open panel/modal: 200-240 ms.
- Toast appear/fade: 180 ms.
- Damage flash: ok. 80 ms.
- Freeze frame przy ciezkim hicie: 2-3 klatki.
- Zasada: animacja ma informowac, nie dekorowac.

## 8. Dos and Donts

### DO

- Utrzymuj staly jezyk kolorow elementow (`fire`, `blade`, `storm`, economy).
- Uzywaj shape language telegraphow dla wszystkich nowych atakow i hazardow.
- Pokazuj cooldown i blokade akcji jednoznacznie (ikona + przygaszenie + liczba).
- Projektuj pod jedna reke: najczestsze akcje przy dolnej krawedzi ekranu.
- Testuj UI na malym ekranie (min 360x640) i na desktopie.

### DONT

- Nie dodawaj nowego znaczenia dla istniejacego koloru semantycznego.
- Nie tworz paneli, ktore zaslaniaja postac podczas walki.
- Nie opieraj ostrzezen tylko na kolorze bez ksztaltu/ikony.
- Nie schodz ponizej 44 px dla klikalnych elementow.
- Nie uzywaj dlugich blokow tekstu w trakcie aktywnej walki.

## 9. Dostepnosc i czytelnosc

- Kontrast tekstu do tla: min WCAG AA (4.5:1 dla tekstu zwyklego).
- Krytyczne sygnaly zagrozenia musza miec:
  - kolor,
  - ksztalt,
  - puls lub animacje,
  - opcjonalnie dzwiek.
- Informacje o stanie gracza (HP, xp, waluta) stale widoczne i nieanimowane agresywnie.

## 10. Responsywnosc

- Mobile (default): 2 sekcje kontrolne obok siebie.
- Przy bardzo waskim ekranie mozliwy fallback do ukladania pionowego, ale:
  - arena musi pozostac dominant visual,
  - przyciski akcji nadal min 44 px,
  - brak horyzontalnego scrolla.

## 11. Checklist PR dla UI

Kazdy PR ruszajacy UI powinien potwierdzac:

- [ ] zgodnosc z kolorami semantycznymi i shape language
- [ ] touch target min 44x44 px
- [ ] czytelnosc HUD na 360x640
- [ ] brak zaslaniania krytycznych elementow walki
- [ ] animacje zgodne z timingami systemu
- [ ] stany disabled/active/error sa widoczne i spojne

## 12. Starter kit do wdrozen (copy/paste)

### 12.1 CSS custom properties

```css
:root {
  --bg1: #0f172a;
  --bg2: #1e293b;
  --panel: rgba(15, 23, 42, 0.75);
  --ink: #e2e8f0;
  --muted: #94a3b8;

  --good: #22c55e;
  --warn: #f59e0b;
  --danger: #ef4444;

  --fire: #ef4444;
  --blade: #a3a3a3;
  --storm: #38bdf8;
  --money: #facc15;

  --rarity-common: #94a3b8;
  --rarity-rare: #38bdf8;
  --rarity-epic: #a855f7;
  --rarity-legendary: #fbbf24;

  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;

  --radius-sm: 10px;
  --radius-md: 12px;
  --radius-lg: 16px;
  --radius-xl: 18px;
  --radius-pill: 999px;

  --border-soft: 1px solid rgba(255, 255, 255, 0.12);
  --border-strong: 1px solid rgba(255, 255, 255, 0.2);

  --dur-fast: 150ms;
  --dur-mid: 200ms;
  --dur-overlay: 240ms;
  --ease-default: ease-out;
}
```

### 12.2 Przycisk bazowy + warianty

```css
.btn {
  min-height: 44px;
  border: 0;
  border-radius: var(--radius-sm);
  padding: 10px 8px;
  font-size: 13px;
  font-weight: 700;
  color: #fff;
  background: linear-gradient(180deg, #334155, #1e293b);
  box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.15);
  transition: transform var(--dur-fast) var(--ease-default), opacity var(--dur-fast) var(--ease-default);
}

.btn:active { transform: translateY(1px); }
.btn[disabled], .btn.is-locked { opacity: 0.45; pointer-events: none; }

.btn--fire { background: linear-gradient(180deg, #ef4444, #b91c1c); }
.btn--blade { background: linear-gradient(180deg, #9ca3af, #4b5563); }
.btn--storm { background: linear-gradient(180deg, #38bdf8, #0369a1); }
.btn--boss { background: linear-gradient(180deg, #f59e0b, #b45309); }
.btn--mut { background: linear-gradient(180deg, #22c55e, #166534); }
```

### 12.3 Panel HUD

```css
.hud {
  background: var(--panel);
  border: var(--border-soft);
  border-radius: var(--radius-md);
  padding: var(--space-2);
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 6px;
  font-size: 14px;
  backdrop-filter: blur(3px);
}

.hud__line { display: flex; justify-content: space-between; gap: 8px; }
.hud__money { color: var(--money); font-weight: 700; }
.hud__xp { color: var(--rarity-epic); font-weight: 700; }
.hud__hp { color: #fca5a5; }
```

### 12.4 Modal/overlay

```css
.overlay {
  position: fixed;
  inset: 0;
  z-index: 50;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: var(--space-4);
  background: rgba(2, 6, 23, 0.92);
  backdrop-filter: blur(8px);
}

.modal {
  width: min(560px, 100%);
  border-radius: var(--radius-xl);
  border: var(--border-strong);
  background: rgba(15, 23, 42, 0.9);
  padding: 18px;
  box-shadow: 0 18px 40px rgba(0, 0, 0, 0.35);
  animation: modalIn var(--dur-overlay) var(--ease-default);
}
```

### 12.5 Snippet JS - mapa telegraph shape

```js
const TELEGRAPH_SHAPE = {
  aoe: 'square',
  dash: 'triangle',
  projectile: 'circle',
  special: 'hexagon'
};

const TELEGRAPH_COLOR = {
  square: '#ef4444',
  triangle: '#fbbf24',
  circle: '#38bdf8',
  hexagon: '#a855f7'
};
```
