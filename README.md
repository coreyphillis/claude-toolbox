# claude-toolbox

Personal cross-project resources: Claude Code skills (packaged as a plugin
marketplace for local use, and usable as claude.ai skills for cloud sessions)
and shared assets like slide templates.

## Setup

How you install depends on where you run Claude Code. Plugins work in the
terminal, desktop (local sessions), and VS Code — but **not** in cloud
sessions. Cloud sessions load skills a different way; see below.

### Terminal, desktop (local sessions), or VS Code

These surfaces support plugins. From any repo:

```
/plugin marketplace add coreyphillis/claude-toolbox
/plugin install slide-figure@corey-tools
/plugin install session-start-hook@corey-tools
/plugin install close-session@corey-tools
```

Install only the plugins you want in a given project. Claude loads a skill
automatically when the work matches it (e.g. turning a figure into a slide
version), or you can call it directly (`/slide-figure`, `/close-session`).

### Claude Code on the web / cloud sessions

Cloud sessions — claude.ai/code, the mobile and desktop apps' cloud sessions,
and `claude --cloud` — **do not support plugins**. `/plugin marketplace add`
returns *"plugins are not available in this environment,"* and marketplaces or
plugins a repo turns on in its `.claude/settings.json` are never installed.

Use **skills** instead, which cloud sessions do load:

- **Across every repo (recommended):** enable the skill on your claude.ai
  account — **Settings → Capabilities → Skills** — by uploading the skill's
  folder zipped as `<name>/SKILL.md` (e.g. a zip containing
  `slide-figure/SKILL.md`). Cloud sessions automatically load skills you
  enable there, in any repo, with nothing to install per session.
- **One repo only:** commit the skill into that repo at
  `.claude/skills/<name>/SKILL.md`. It's part of the clone, so it loads in
  that repo's cloud sessions.

The plugin's `SKILL.md` here is the source of truth for both paths — the
`.claude-plugin/` scaffolding is only used by the plugin (local) path.

## Updating the skill

1. Edit `plugins/slide-figure/skills/slide-figure/SKILL.md` in this repo.
2. Bump the `version` field in `plugins/slide-figure/.claude-plugin/plugin.json`.
3. Commit and push.

Then refresh wherever it's installed:

- **Plugin path** (terminal / desktop / VS Code) — in any project session:
  ```
  /plugin marketplace update
  /plugin update slide-figure@corey-tools
  /reload-plugins
  ```
  Every project picks up the same version — no copy-pasting the file around.
- **claude.ai skill path** (cloud sessions) — re-zip `slide-figure/SKILL.md`
  and re-upload it under **Settings → Capabilities → Skills**, replacing the
  old version. New cloud sessions pick it up automatically.

## What's in here

- `plugins/slide-figure/` — a skill that converts a publication R figure
  (ggplot2 or base R) into a presentation-ready version matching the deck theme.
- `plugins/session-start-hook/` — a skill for building SessionStart hooks so
  dependencies, tests, and linters work in Claude Code on the web sessions.
- `plugins/close-session/` — a `/close-session` command that logs the
  session's changes to the repo's changelog (matching its existing format),
  then commits and pushes. Repo-agnostic: it adapts to whatever changelog
  file and convention a project already uses.
- `templates/scientific-slide-template.pptx` — the storybook-style slide
  template (light + dark master layouts, colorblind-friendly water/earth
  palette). Not a plugin — just grab it directly, or ask Claude Code to fetch
  it from this repo when starting a new deck.

## Adding something new later

Any new skill goes in `plugins/<skill-name>/skills/<skill-name>/SKILL.md`
with its own `.claude-plugin/plugin.json`, then gets one more entry in
`.claude-plugin/marketplace.json`'s `plugins` array. Non-skill assets (more
templates, reference docs, etc.) can just live in their own top-level folder —
they don't need any plugin scaffolding.
