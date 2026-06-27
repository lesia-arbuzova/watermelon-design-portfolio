# RTK - Rust Token Killer (Codex CLI / Hermes)

## Rule
Use native RTK wrappers for supported output-heavy commands; use `rtk pipe` filters for unsupported noisy commands.

```bash
rtk git status       rtk git diff         rtk git log --oneline -20
rtk ls               rtk read <file>      rtk grep <pattern> .
rtk find .           rtk npm run build    rtk npm test
rtk tsc --noEmit     rtk pytest -q        rtk docker ps
```

RTK 0.42.x часто дає `rtk fallback` для PowerShell/Python/Node. Не форсуй `rtk powershell`, `rtk python`, `rtk node` для цих команд; якщо output треба показати агенту, стискай його pipe-фільтром. Inline `python -c` / `node -e` краще не використовувати - hooks блокують їх, щоб не було raw bypass.

```bash
set -o pipefail; rg --files -g "*.png" 2>&1 | rtk pipe -f find
set -o pipefail; rg "pattern" . 2>&1 | rtk pipe -f grep
set -o pipefail; node qa-script.mjs 2>&1 | rtk pipe -f log
set -o pipefail; python script.py 2>&1 | rtk pipe -f log
```

Для читання файлів не використовуй PowerShell `Get-Content`, `cat`, `head`, `tail`; використовуй `rtk read <file>` / `rtk read --max-lines N <file>` / `rtk read --tail-lines N <file>` або файл-інструмент.
## GitHub Pages / static site workflow
This repository is a static HTML/CSS/JS portfolio site published from GitHub. Use compact commands when inspecting it:

```bash
rtk git status
rtk git diff
rtk ls
rtk read index.html
rtk grep "section" .
```

## Railway filters
Project-local Railway filters live in `.rtk/filters.toml` and are trusted locally for future RTK builds. Current RTK does not expose custom filters through `rtk pipe -f`, so use the working compact fallback:

```bash
rtk summary railway status --json
rtk summary railway whoami --json
rtk summary railway service
rtk summary railway logs
```

## Meta
```bash
rtk gain
rtk gain --history
rtk gain --daily
rtk hook check "git status"
rtk proxy <cmd>
```
