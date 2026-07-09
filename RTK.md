# RTK - Rust Token Killer (Hermes / Codex / Claude Code)

## Rule
Use native RTK wrappers for stable output-heavy commands; use `rtk pipe` filters for unsupported noisy commands. Full-file shell reads are blocked because recent RTK history showed 0% savings for unbounded `cat`/`rtk read`.

```bash
rtk git status       rtk git diff         rtk git log --oneline -20
rtk ls               rtk grep <pattern> . rtk find .
rtk npm run build    rtk npm test         rtk tsc --noEmit
rtk pytest -q        rtk docker ps
rtk read --max-lines 120 index.html
rtk read --tail-lines 80 logs/app.log
```

## Blocked / avoided

- Do not use full-file `cat` or unbounded `rtk read <file>` for model-visible output. Use the agent file-reading tool, `rtk read --max-lines N <file>`, or `rtk read --tail-lines N <file>`.
- Do not use PowerShell `Get-Content`, `Get-ChildItem`, `Resolve-Path`, or `Select-String` for inspection; hooks block these.
- Do not use inline `python -c`, `node -e`, or `node -p`; hooks block these unless `# rtk-raw-ok` is explicitly present for break-glass debugging.
- Do not use `rtk proxy` for normal work. It gives 0% savings.

## RTK 0.43.0 gaps

RTK 0.43.0 still does not expose custom TOML filters through `rtk pipe -f`, and PowerShell/Python/Node wrappers can still be poor for noisy scripts. Use pipe filters instead:

```bash
set -o pipefail; rg --files -g "*.png" 2>&1 | rtk pipe -f find
set -o pipefail; rg "pattern" . 2>&1 | rtk pipe -f grep
set -o pipefail; node qa-script.mjs 2>&1 | rtk pipe -f log
set -o pipefail; python script.py 2>&1 | rtk pipe -f log
```

## GitHub Pages / static site workflow
This repository is a static HTML/CSS/JS portfolio site published from GitHub. Use compact commands when inspecting it:

```bash
rtk git status
rtk git diff
rtk ls
rtk read --max-lines 160 index.html
rtk grep "section" .
```

## Railway filters
Project-local Railway filters live in `.rtk/filters.toml` and are kept for future RTK builds. Current RTK does not expose custom filters through `rtk pipe -f`, so use the working compact fallback:

```bash
rtk summary railway status --json
rtk summary railway whoami --json
rtk summary railway service
rtk summary railway logs
```

## Meta
```bash
rtk --version
rtk verify
rtk gain
rtk gain --history
rtk gain --daily
rtk hook check "git status"
```
