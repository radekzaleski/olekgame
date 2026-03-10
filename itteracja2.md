# Iteracja 2 - propozycje zmian (game design + grafika)

Cel: ograniczyc monotonnosc walki, zwiekszyc roznorodnosc runu i poprawic czytelnosc wizualna.

## Krytyczne obserwacje (dlaczego teraz bywa nudno)

- Normalne fale sa zbyt podobne: glownie skalowanie statystyk zamiast nowych decyzji taktycznych.
- Przeciwnicy maja malo zroznicowane zachowania, przez co walka szybko staje sie rutyna.
- Bossowie maja mocne liczby i opisy, ale bez wyraznych roznic wzorcow arena-fight moze byc odczuwalnie podobny.
- Drop/chest loop nie daje regularnych "momentow wow" ani sytuacji ryzyko-nagroda.
- Swiaty roznia sie kolorami, ale kompozycja i rytm sceny sa prawie stale.

## Backlog (priorytety)

### Wazne

| ID | Obszar | Zadanie | Efekt dla gracza | Kryterium akceptacji |
|---|---|---|---|---|
| I2-H1 | AI/Fale | Dodac role przeciwnikow: `charger`, `ranged`, `buffer`, `summoner` | Kazda fala wymaga innej reakcji | Min. 3 role aktywne do fali 6, kazda z odrebnym patternem ataku/ruchu |
| I2-H2 | AI/Fale | Dodac "motyw fali" (rush/zoning/mixed) z telegraph info przed spawnem | Lepszy pacing i czytelny kontekst walki | Przed fala toast/baner + spawn zgodny z motywem |
| I2-H3 | Bossy | Dodac po 1 unikalnym "signature move" na bossa + mocny telegraph | Bossy beda wyraznie rozne | 5 bossow, kazdy ma 1 ruch niepowtarzalny w innych walkach |
| I2-H4 | Bossy/Arena | Dodac po 1 mechanice areny na bossa (np. lava cracks, pylony burzy) | Walka "zyje" i zmienia warunki | Mechanika aktywuje sie min. w jednej fazie i jest widoczna na scenie |
| I2-H5 | Feedback | Poprawic hit feedback: krotki freeze-frame, directional trails, impact decals | Mocniejsze odczucie trafien i unikow | Ciezkie trafienie ma odczuwalny impact bez spadku responsywnosci |
| I2-H6 | Czytelnosc | Ustandaryzowac telegraph shape language (kolor + ksztalt + obrys) | Latwiejsze czytanie zagrozen | Wszystkie ataki bossow i elite maja spojny telegraph |

### Srednie

| ID | Obszar | Zadanie | Efekt dla gracza | Kryterium akceptacji |
|---|---|---|---|---|
| I2-M1 | System runu | Dodac "wave mutators" co 2 fale (np. low gravity, toxic ground, fast projectiles) | Wieksza roznorodnosc miedzy runami | Min. 6 mutatorow, aktywny max 1 naraz, jasny komunikat w HUD |
| I2-M2 | System runu | Dodac fale celowe (objective waves): obrona punktu, totem destroy, zbierz rdzenie | Przerwanie monotonii "tylko zabij" | Min. 2 typy objective wave, uruchamiane np. fala 3/6/9 |
| I2-M3 | AI | Dodac stany zachowania: flank, odskok po trafieniu, panic przy low HP | Potwory sa mniej przewidywalne | Co najmniej 2 stany AI aktywne u min. 2 klas enemy |
| I2-M4 | Ekonomia | Rozszerzyc skrzynki o ryzyko-nagroda (bezpieczna vs przekleta) | Decyzje strategiczne poza walka | Gracz wybiera typ nagrody i ponosi czytelny koszt/ryzyko |
| I2-M5 | Build UX | Dodac mini panel tagow buildu (fire/blade/storm/defense/mobility/attack) | Gracz rozumie kierunek builda | HUD pokazuje aktualne stacki tagow + aktywne synergie |
| I2-M6 | Audio/Tempo | Zwiekszyc roznice warstw audio miedzy exploration/combat/boss phase | Lepszy rytm emocji runu | Slyszalne przejscia miedzy 3 trybami bez restartu audio |

### Nice to have

| ID | Obszar | Zadanie | Efekt dla gracza | Kryterium akceptacji |
|---|---|---|---|---|
| I2-N1 | Grafika swiatow | Dodac 3-warstwowy parallax backgrounds per world | Glebszy klimat swiata | Kazdy world ma warstwe far/mid/fore z ruchem |
| I2-N2 | Grafika enemy | Rozroznienie roli po sylwetce (ksztalt helmu, bron, aura) | Lepsza czytelnosc bez patrzenia na kolor | Gracz odroznia role enemy po samym ksztalcie |
| I2-N3 | VFX | Dodac world-specific ambient FX (iskry, pyl, deszcz iskier, muta mgla) | Scena jest bardziej zywa | 1-2 ambient FX stale aktywne per world |
| I2-N4 | UI/Reward | Dodac mini eventy lootowe (np. oltarz, hazard chest, kontrakt) | Wiecej "momentow wow" i decyzji | Min. 2 eventy z unikalnym UI i konsekwencja |
| I2-N5 | Progressja | Keystone mutation slot (1 super mutacja z kosztem) | Build bardziej unikalny miedzy runami | Gracz wybiera 1 keystone, koszt widoczny i odczuwalny |

## Kolejnosc wdrozenia (rekomendacja)

1. `I2-H1` + `I2-H2` (role + motywy fal)
2. `I2-H3` + `I2-H4` + `I2-H6` (boss identity + telegraph)
3. `I2-H5` (combat feel)
4. `I2-M1` + `I2-M2` (roznorodnosc runu)
5. `I2-M5` (czytelnosc builda)
6. Pozostale `Srednie` i `Nice to have`

## Definicja sukcesu iteracji 2 (KPI gameplay)

- Gracz raportuje wyraznie rozne odczucie co najmniej 3 kolejnych fal.
- Bossowie sa rozpoznawalni po zachowaniu po 10-15 sekundach walki.
- Mniejsza liczba sytuacji "stoi i spamuje atak" jako dominujaca strategia.
- Lepsza czytelnosc zagrozen (mniej "nie wiedzialem skad dmg").

## Status wdrozenia (snapshot)

Zrobione:

- `I2-H1`, `I2-H2`, `I2-H3`, `I2-H4`, `I2-H5`, `I2-H6`
- `I2-M1`, `I2-M2`

Do zrobienia (reszta backloga):

- `I2-M3` AI: flank/odskok/panic
- `I2-M4` Ekonomia: skrzynki ryzyko-nagroda
- `I2-M5` Build UX: panel tagow + synergie
- `I2-M6` Audio/Tempo: rozne warstwy exploration/combat/boss
- `I2-N1` Grafika: parallax backgrounds per world
- `I2-N2` Grafika enemy: role po sylwetce
- `I2-N3` VFX: ambient world FX
- `I2-N4` UI/Reward: mini eventy lootowe
- `I2-N5` Progressja: keystone mutation slot
