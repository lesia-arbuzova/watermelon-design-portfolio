# RTK — Rust Token Killer (Codex CLI / Hermes)

## Rule
Always prefix supported shell commands with `rtk` to reduce AI context usage by 60–90%.

```bash
rtk git status       rtk git diff         rtk git log --oneline -20
rtk ls               rtk read <file>      rtk grep <pattern> .
rtk gh pr list       rtk npm run build    rtk npm test
rtk tsc --noEmit     rtk pytest -q        rtk docker ps
```

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
Project-local Railway filters live in `.rtk/filters.toml` and are trusted locally. If Railway CLI is used here, prefer:

```bash
railway status --json 2>&1 | rtk pipe -f railway-status
railway whoami --json 2>&1 | rtk pipe -f railway-status
railway service 2>&1 | rtk pipe -f railway-service
railway logs 2>&1 | rtk pipe -f railway-logs
```

## Meta
```bash
rtk gain
rtk gain --history
rtk gain --daily
rtk hook check "git status"
rtk proxy <cmd>
```
