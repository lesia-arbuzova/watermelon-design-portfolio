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
