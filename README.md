# promptup

**Compile a rough prompt into a precise, codebase-grounded Claude Code prompt — without executing it.**

`promptup` is a Claude Code skill. You slap out a rough, messy, half-formed prompt; it reads your real codebase, works out what you actually mean, and hands back a clean, specific, file-aware prompt that's ready to run. It never edits code or runs the task — **the rewritten prompt is the deliverable.**

## Install

From the community marketplace (once published):

```
/plugin marketplace add anthropics/claude-plugins-community
/plugin install promptup@claude-community
```

Or test this repo locally:

```
/plugin marketplace add /path/to/promptup
/plugin install promptup@promptup-marketplace
```

## Usage

```
/promptup make teh login thing retry when it fails idk where it is
```

You get back a polished, copy-pasteable prompt plus a short note on what changed. Reply `go` to run it, or tell it what to adjust.

## How it works

- Runs on **Sonnet** at **medium effort** — fast and cheap; reverts to your session model when you run the result, so execution happens on your normal model.
- **Read-only** (`Read`, `Grep`, `Glob`, `Agent`) — it structurally cannot edit your code.
- **Explicit invocation only** (`/promptup`) — never auto-triggers, so it won't hijack a prompt you meant to execute.
- Grounds file references against your real code and only cites paths it has verified; fans out to read-only `Explore` agents only for large, multi-subsystem repos.

## License

MIT — see [LICENSE](LICENSE).
