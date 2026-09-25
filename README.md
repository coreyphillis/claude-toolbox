# claude-toolbox

Personal cross-project resources: Claude Code skills (as a plugin marketplace)
and shared assets like slide templates.

## One-time setup, per machine/account

From any repo where you're running Claude Code:

```
/plugin marketplace add coreyphillis/claude-toolbox
/plugin install slide-figure@corey-tools
/plugin install session-start-hook@corey-tools
/plugin install close-session@corey-tools
```

That makes the skills and commands available in that Claude Code session —
Claude loads a skill automatically when the work matches it (e.g. turning a
figure into a slide version), or you can call it directly (`/slide-figure`,
`/close-session`). Install only the plugins you want in a given project.

If you're on the hosted (browser) version of Claude Code, each fresh session
runs in a new sandboxed container. If the install doesn't carry over between
sessions, just re-run the two commands above — it takes a few seconds and
nothing needs to be re-created, only re-attached.

## Updating the skill

1. Edit `plugins/slide-figure/skills/slide-figure/SKILL.md` in this repo.
2. Bump the `version` field in `plugins/slide-figure/.claude-plugin/plugin.json`.
3. Commit and push.
4. In any project session:
   ```
   /plugin marketplace update
   /plugin update slide-figure@corey-tools
   /reload-plugins
   ```

Every project picks up the same version — no copy-pasting the file around.

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
