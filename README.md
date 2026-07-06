# Freud

A Claude Code skill for deep technical analysis of services — architecture
diagrams, database schemas, sequence flows, and critical code review, all
rendered into a single self-contained `ANALYSIS.html` document with a Gruvbox
theme.

There are many tools like this, but I have found them overly ambitious. My goal is a piercing and precise analysis of the code where it matters most.

## Install (Claude Code)

```
/plugin marketplace add iancullinane/freud
/plugin install freud
```

## Usage

Ask Claude Code to "analyze this service" (or "analyze service", "create
service documentation", "document this codebase", "service deep dive") inside
a project you want documented. See `skills/freud/SKILL.md` for the full
process the skill follows.

## Structure

The skill's content lives in `skills/freud/SKILL.md`, independent of any one
platform's manifest. `.claude-plugin/` wires it up for Claude Code. Other
agent platforms that support the same open `SKILL.md` format (e.g. Cursor,
Zed) can be added later as their own thin manifest files alongside
`.claude-plugin/`, without touching `skills/freud/SKILL.md`.

## License

MIT — see [LICENSE](LICENSE).
