# QA Backlog (fatal + high)

## Done in this pass
- [x] Crash on enemy spawn (`size` was undefined in `spawnEnemy`)
- [x] Canvas state leak in `drawEnemySprite` (`ctx.save()` without guaranteed `ctx.restore()`)
- [x] Enemy melee range bug (enemies could hit player from behind with no real contact)
- [x] Boss contact range bug (distance check ignored sprite widths)
- [x] Input stuck after window focus loss (movement/shield remained active)
- [x] Limit toast spam during multi-hit blocks (`BLOKADA` throttled)
- [x] Clamp knockback positions to arena bounds for enemies and bosses

## Next fixes
- [ ] Add lightweight runtime sanity checks for critical entities (enemy/boss hp, size, coords)
- [ ] Audit mutation effects: many are drafted in DB but not applied in gameplay logic

## QA smoke checks
- Start run, survive to wave 3, verify no spawn crash
- Let enemy pass player, confirm it turns and re-engages instead of phantom-hitting
- Hold shield in melee crowd, confirm blocked hits do not deal damage
- Alt-tab / switch window while holding movement, confirm no stuck input after return
