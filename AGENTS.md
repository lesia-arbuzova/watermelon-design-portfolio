@RTK.md

### RTK (Rust Token Killer) - Token-Optimized Commands

Use native RTK wrappers for stable output-heavy commands; use `rtk pipe` filters for unsupported noisy commands.

**Hook автоматично переписує або блокує:** git, grep/rg output, ls, find, npm run, cargo, docker, full-file `cat`, unbounded `rtk read`, inline Python/Node, PowerShell inspection commands.

```bash
rtk git status       rtk git diff         rtk git log --oneline -20
rtk ls               rtk grep <pattern> . rtk find .
rtk npm run build    rtk npm test         rtk tsc --noEmit
rtk read --max-lines 120 index.html
rtk read --tail-lines 80 logs/app.log
```

PowerShell/Python/Node у RTK 0.43.0 все ще можуть давати `rtk fallback`; якщо output треба показати агенту, стискай через `rtk pipe -f log|find|grep`, див. `RTK.md`.

Не використовуй full-file `cat` або unbounded `rtk read <file>`: остання RTK-статистика показала 0% savings і великий token waste. Використовуй файл-інструмент або bounded read.

Railway filters installed in `.rtk/filters.toml` for future RTK builds; current RTK does not expose custom filters via `rtk pipe -f`, so use `rtk summary railway ...` forms from `RTK.md` for Railway commands.
