# Mutacje Mocy

Prototyp mobilnej gry arena-action z runami opartymi o fale, mutacje i walki z bossami.

## Dokumentacja projektu

- `GAME_DESIGN.md` - zasady runu, bossowie, dropy, mutacje i balans liczb.
- `VISUAL_DESIGN.md` - specyfikacja efektow wizualnych, telegraphow i warstwy artystycznej.
- `ANIMATION_DESIGN.md` - zalozenia i backlog animacji.
- `AUDIO_DESIGN.md` - zalozenia i backlog audio.
- `UI_DESIGN_SYSTEM.md` - obowiazujace zasady budowy UI (design system), dos and donts, kolory, spacing, wymiary.

## Zasady dla deweloperow UI

Przy kazdej zmianie interfejsu nalezy pracowac zgodnie z `UI_DESIGN_SYSTEM.md`.

Minimalny standard:

- semantyka kolorow i ksztaltow telegraphow musi byc zachowana,
- touch targety maja minimum 44x44 px,
- HUD i kluczowe informacje pozostaja czytelne na 360x640,
- UI nie moze zaslaniac krytycznych elementow walki.
