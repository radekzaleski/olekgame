# Animation Implementation Backlog

## Faza 1: Core Animations (MVP)

### Task 1.1: Player Animation System
- [x] **1.1.1** Add animation state machine to player (idle, run, jump, fall, attack, land)
- [x] **1.1.2** Implement idle breathing animation (Y scale oscillation)
- [x] **1.1.3** Implement run animation (leg/arm swing)
- [x] **1.1.4** Implement jump/fall poses
- [x] **1.1.5** Implement landing dust particles

### Task 1.2: Enhanced Attack Effects
- [x] **1.2.1** Extend sword swing arc (144° → 270°)
- [x] **1.2.2** Add sword trail particles
- [x] **1.2.3** Add arrow release particles
- [ ] **1.2.4** Add shield pulse effect

### Task 1.3: Enemy Hit/Death
- [x] **1.3.1** Add hit flash effect (white → normal)
- [x] **1.3.2** Add knockback on hit
- [ ] **1.3.3** Add death animation (fall + fade)
- [x] **1.3.4** Add blood/damage particles

### Task 1.4: Particle System Expansion
- [x] **1.4.1** Add dust particle type
- [x] **1.4.2** Add blood particle type  
- [ ] **1.4.3** Add fire particle type
- [x] **1.4.4** Add sword trail particle type
- [ ] **1.4.5** Implement object pooling for particles

---

## Faza 2: Boss & Environment

### Task 2.1: Boss Animations
- [ ] **2.1.1** Add boss movement animation (heavy sway)
- [ ] **2.1.2** Add fire boss attack particles
- [ ] **2.1.3** Add blade boss spin effect
- [ ] **2.1.4** Add storm boss lightning effects
- [ ] **2.1.5** Add phase change flash effect

### Task 2.2: Environment Effects
- [ ] **2.2.1** Add weather particles per world
- [ ] **2.2.2** Add background lightning flashes
- [ ] **2.2.3** Enhance cloud animations
- [ ] **2.2.4** Add world-specific ambient particles

---

## Faza 3: Polish

### Task 3.1: Screen Effects
- [ ] **3.1.1** Add screen shake on heavy hits
- [ ] **3.1.2** Add screen shake on boss attacks
- [ ] **3.1.3** Add block flash effect

### Task 3.2: UI Animations
- [ ] **3.2.1** Smooth HP bar transitions
- [ ] **3.2.2** Coin/XP pop animations
- [ ] **3.2.3** Toast slide effects

### Task 3.3: Sprite Upgrade (Future)
- [ ] **3.3.1** Create sprite sheets for player
- [ ] **3.3.2** Create sprite sheets for enemies
- [ ] **3.3.3** Create sprite sheets for bosses

---

## Progress: Faza 1 - In Progress

### Done
- Animation design doc created
- Backlog created
- Phase 1 partial implementation started in game code

### Current Sprint Tasks
- [x] 1.1.2 Idle breathing animation
- [x] 1.1.3 Run animation  
- [x] 1.1.5 Landing dust
- [ ] 1.2.4 Shield pulse polish
- [ ] 1.3.3 Full death fall + fade animation
- [ ] 1.4.3 Fire particles
- [ ] 1.4.5 Particle object pooling

## Notes
- Use delta-time for all animations
- Keep under 100 active particles
- Target 60fps performance
- Start with simple rect-based, upgrade to sprite later
