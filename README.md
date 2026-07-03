# promptup

**Compile a rough prompt into a precise, codebase-grounded Claude Code prompt — without executing it.**

`promptup` is a Claude Code skill. You slap out a rough, messy, half-formed prompt; it reads your real codebase, works out what you actually mean, and hands back a clean, specific, file-aware prompt that's ready to run. It never edits code or runs the task — **the rewritten prompt is the deliverable.**

## Install

Once accepted into the community marketplace:

```
/plugin marketplace add anthropics/claude-plugins-community
/plugin install promptup@claude-community
```

Or test this repo locally. Clone it, then in Claude Code:

```
/plugin marketplace add /path/to/promptup
/plugin install promptup@promptup-marketplace
```

## Usage

```
/promptup:promptup make teh login thing retry when it fails idk where it is
```

(The command is doubled because plugin skills are namespaced `plugin:skill` — here the plugin and the skill are both `promptup`.)

You get back a polished, ready-to-run prompt plus a short note on what changed:

```
── Improved prompt ─────────────────────────────
Add retry logic to the login request in src/auth/login.ts. Wrap the
fetch in `signIn()` to retry up to 3× on network/5xx errors with
exponential backoff; do not retry on 401/403. Done when a flaky
network recovers within 3 attempts and auth failures still surface.
─────────────────────────────────────────────────
```

Reply `go` to run it, or tell it what to adjust — the improved prompt is
already in context, so there's nothing to copy.

## How it works

- Runs on **Sonnet** at **medium effort** — fast and cheap; reverts to your session model when you run the result, so execution happens on your normal model.
- **Read-only** (`Read`, `Grep`, `Glob`, `Agent`) — it structurally cannot edit your code.
- **Explicit invocation only** (`/promptup`) — never auto-triggers, so it won't hijack a prompt you meant to execute.
- Grounds file references against your real code and only cites paths it has verified; fans out to read-only `Explore` agents only for large, multi-subsystem repos.

## License

MIT — see [LICENSE](LICENSE).
