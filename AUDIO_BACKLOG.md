# Audio Implementation Backlog

## Faza 1 - Core Audio System (MVP)
- [x] **1.1** Create `AudioManager` class in `index.html`
  - Web Audio API context initialization
  - Master volume control
  - Mute/unmute functionality
  - Preload sound assets (synth-based)

- [x] **1.2** Implement `Sound` class
  - Load audio files (mp3/ogg/wav)
  - Play with volume control
  - Pool system for overlapping sounds (via createOsc)
  - Stop/fade functionality

- [x] **1.3** Add UI sounds
  - `ui_click` - button clicks
  - `ui_hover` - button hover
  - `mutation_select` - card selection
  - `item_pickup` - coin/item pickup
  - `upgrade` - upgrade confirm

- [x] **1.4** Add basic combat sounds
  - `player_sword_swing`
  - `player_sword_hit`
  - `player_bow_shoot`
  - `player_arrow_hit`

- [x] **1.5** Add wave notifications
  - `wave_start`
  - `wave_complete`

- [ ] **1.6** Add enemy sounds
  - `enemy_death`
  - `enemy_hit`

---

## Faza 2 - Combat Audio Polish
- [ ] **2.1** Player defensive sounds
  - `player_dash` - dodge sound
  - `player_block` - shield block
  - `player_dodge` - roll dodge

- [ ] **2.2** Boss audio
  - Individual attack sounds per boss
  - Phase change sounds
  - Death sounds

- [ ] **2.3** Projectile sounds
  - Fire projectile sounds
  - Impact sounds by type

- [ ] **2.4** Status effect sounds
  - `burn`
  - `freeze` 
  - `poison`
  - `shock`
  - `heal`

- [ ] **2.5** Environment sounds
  - `door_open`
  - `chest_open`
  - `lava_damage`

---

## Faza 3 - Music & Immersion
- [ ] **3.1** BGM system
  - `MusicManager` class
  - Crossfade between tracks
  - Volume control independent of SFX
  - Loop management

- [ ] **3.2** World music
  - Popielna Kuznia theme
  - Zelazne Pogranicze theme
  - Sztormowe Iglice theme
  - Mutageniczne Mokradla theme
  - Zlote Katakumby theme

- [ ] **3.3** Boss music
  - Mini boss theme
  - Final boss theme (with phase 2 variation)

- [ ] **3.4** Ambient sounds
  - Per-biome ambient loops
  - Dynamic volume based on proximity

- [ ] **3.5** Footstep system
  - Terrain-based footstep sounds
  - Player movement audio

---

## Faza 4 - Polish & Optimization
- [ ] **4.1** Sound variations
  - Randomization for hits/deaths
  - Pitch variation system

- [ ] **4.2** Audio mixing
  - Volume presets per scene type
  - Ducking for important sounds
  - Compression settings

- [ ] **4.3** Performance
  - Audio pooling optimization
  - Lazy loading for unused sounds
  - Memory management

- [ ] **4.4** Settings UI
  - Master volume slider
  - Music volume slider
  - SFX volume slider
  - Mute toggle
  - Save to localStorage

---

## Technical Notes

### Audio Format Recommendations
- **SFX:** OGG (better compression), 128kbps
- **Music:** OGG, 192kbps
- **Fallback:** MP3 for Safari compatibility

### Web Audio API Implementation
```javascript
// Basic structure
class AudioManager {
  constructor() {
    this.ctx = new (window.AudioContext || window.webkitAudioContext)();
    this.sounds = {};
    this.musicGain = this.ctx.createGain();
    this.sfxGain = this.ctx.createGain();
  }
  
  async loadSound(name, url) { ... }
  play(name, volume = 1) { ... }
  playMusic(name, fadeTime = 1) { ... }
}
```

### Sound Naming Convention
`{category}_{action}_{variant}`
- `player_sword_swing_01`
- `enemy_death_squelch_02`
- `boss_fire_explode_large`

### File Organization
```
/audio/
  /sfx/
    /ui/
    /combat/
    /boss/
    /environment/
  /music/
    /world1_popielna_kuznia.ogg
    /world2_zelazne_pogranicze.ogg
    ...
    /boss_mini.ogg
    /boss_final.ogg
```

---

## Dependencies & Tools

### Sound Sources (to create or license)
-.bfxr.net - generate 8-bit sounds
- freesound.org - ambient/sfx
- In-house composition or royalty-free

### Implementation Checklist
- [ ] Test on Chrome, Firefox, Safari
- [ ] Test on mobile (touch + audio context resume)
- [ ] Verify no audio memory leaks
- [ ] Test audio with game running for 30+ minutes