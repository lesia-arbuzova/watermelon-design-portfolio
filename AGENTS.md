@RTK.md

### RTK (Rust Token Killer) - Token-Optimized Commands

Use native RTK wrappers for supported output-heavy commands; use `rtk pipe` filters for unsupported noisy commands.

**Hook автоматично переписує:** git, grep/rg output via pipe filters, ls, find, npm run, cargo, docker.
**Явно використовуй RTK для:** dotnet test/run/format, npm test, GitHub CLI, Docker/Kubernetes logs, Python tests.

```bash
rtk git status       rtk git diff         rtk git log --oneline -20
rtk ls               rtk read <file>      rtk grep <pattern> .
rtk find .           rtk npm run build    rtk npm test
rtk tsc --noEmit     rtk pytest -q        rtk docker ps
```

PowerShell/Python/Node у RTK 0.42.x часто дають `rtk fallback`; якщо output треба показати агенту, стискай через `rtk pipe -f log|find|grep`, див. `RTK.md`. Inline `python -c` / `node -e` та PowerShell `Get-Content`/`Get-ChildItem`/`Select-String` hooks блокують, щоб вони не проходили raw повз RTK.

Railway filters installed in `.rtk/filters.toml` for future RTK builds; current RTK does not expose custom filters via `rtk pipe -f`, so use `rtk summary railway ...` forms from `RTK.md` for Railway commands.
