@RTK.md

### RTK (Rust Token Killer) — Token-Optimized Commands

Always prefix supported shell commands with `rtk` to reduce context usage by 60–90%.

**Hook автоматично переписує:** git, grep, ls, find, npm run, cargo, docker.
**Явно використовуй RTK для:** dotnet test/run/format, npm test, GitHub CLI, Docker/Kubernetes logs, Python tests.

```bash
rtk git status       rtk git diff         rtk git log --oneline -20
rtk ls               rtk read <file>      rtk grep <pattern> .
rtk gh pr list       rtk npm run build    rtk npm test
rtk tsc --noEmit     rtk pytest -q        rtk docker ps
```

Railway filters installed in `.rtk/filters.toml` for future RTK builds; current RTK does not expose custom filters via `rtk pipe -f`, so use `rtk summary railway ...` forms from `RTK.md` for Railway commands.
