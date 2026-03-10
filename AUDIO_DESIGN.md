# Audio Design - Mutacje Mocy

## Muzyka (BGM)

### World 1 - Popielna Kuznia
- **Klimat:** Gorący, dynamiczny
- **Propozycja:** Epic metal z bębnami, ciężkie gitary, motywy ognia
- **Referencje:** Doom Eternal (fire levels), older diablo fire themes

### World 2 - Zelazne Pogranicze
- **Klimat:** Wojenny, mroczny
- **Propozycja:** Military Drum & Fife, metalowe rytmy, chóralne harmonie
- **Referencje:** Dark Souls military themes, The Witcher combat

### World 3 - Sztormowe Iglice
- **Klimat:** Burzowy, napięty
- **Propozycja:** Synthwave + orkiestralne, elektryczne syntezatory, echo
- **Referencje:** Hyper Light Drifter, Furi boss themes

### World 4 - Mutageniczne Mokradla
- **Klimat:** Niepokojący, organiczny
- **Propozycja:** Ambient + dissonant strings, squelchy, heartbeat bass
- **Referencje:** Amnesia sound design, Subnautica bioluminescence

### World 5 - Zlote Katakumby
- **Klimat:** Tajemniczy, bogaty
- **Propozycja:** Barokowy jazz, ciemne organy, złote dzwony
- **Referencje:** Darkest Dungeon, Dishonored mystery themes

### Boss Music
- **Mini Boss:** Intensywny, krótki loop (30s), high energy
- **Final Boss:** Epicki, dwufazowy (phase 2 = faster + more instruments)

---

## SFX - Efekty dźwiękowe

### UI/Menu
| Sound | Opis |
|-------|------|
| `ui_click` | Metalowy clic przy naciśnięciu przycisku |
| `ui_hover` | Cichy click przy najechaniu |
| `mutation_select` | Szelest kartki/pergaminu |
| `item_pickup` | Dzwonek/monety (pitch varies by rarity) |
| `upgrade` | Pozytywny jingle, powerup feeling |

### Walka - Gracz
| Sound | Opis |
|-------|------|
| `player_sword_swing` | Cięcie metalu + smagnięcie |
| `player_sword_hit` | Tępe uderzenie + krew |
| `player_bow_shoot` | Cięcie powietrza + trzask cięciwy |
| `player_arrow_hit` | Trafienie w ciało |
| `player_dash` | Podmuch wiatru |
| `player_block` | Metaliczny clang (tarcza) |
| `player_dodge` | Szybki whoosh + echem |

### Walka - Wrogowie
| Sound | Opis |
|-------|------|
| `enemy_hit` | Tępe uderzenie |
| `enemy_death` | Various: ciało pada, dyszenie, zniknięcie |
| `enemy_spawn` | Pojawienie się (growl/summon sound) |
| `projectile_fire` | Wystrzelenie pocisku |

### Bossowie
| Boss | Sounds |
|------|--------|
| Krol Zaru | Syczenie ognia, trzask płomieni, ryk, krok magmy |
| General Ostrzy | Brzęk metalu, wirujące ostrza, metaliczny chód |
| Wladca Burzy | Grzmot, trzask pioruna, szum elektryczny, teleport whoosh |
| Hydra Genow | Buluot, siorbanie, skrzypienie, multi-head roar |
| Poborca Cieni | Dzwonienie monet, szepty, echo, ink vortex |

### Środowisko
| Sound | Opis |
|-------|------|
| `footstep_player` | Stąpanie po kamieniu (looped, varies by terrain) |
| `wave_start` | Dzwon zegara/notify |
| `wave_complete` | Pozytywny fanfar |
| `door_open` | Ciężkie otwieranie (kamień/metal) |
| `chest_open` | Złoto/magiczny unlock |
| `lava_damage` | Syczenie, płomień |
| `trap_trigger` | Różne w zależności od pułapki |

### Status Effects
| Effect | Sound |
|--------|-------|
| `burn` | Trzask ognia + krzyk |
| `freeze` | Lód pęka |
| `poison` | Siorbanie + kaszel |
| `shock` | Elektryczny trzask |
| `heal` | Magiczny dzwonek + ulgę |

---

## Implementation Priority

### Faza 1 - Core (MVP)
1. UI sounds (click, hover, mutation select)
2. Player combat (sword swing, hit, bow shoot)
3. Wave notifications (start, complete)
4. Basic enemy death

### Faza 2 - Combat Polish
5. Player dash/block/dodge
6. Boss attack sounds
7. Projectile sounds
8. Status effect sounds

### Faza 3 - Immersion
9. Ambient world sounds per biome
10. Footstep system
11. Boss music integration
12. Dynamic music transitions

### Faza 4 - Polish
13. Randomization variations
14. Volume balancing
15. Audio mixing per scene