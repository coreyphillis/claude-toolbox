# claude-toolbox

Personal cross-project resources: Claude Code skills (as a plugin marketplace)
and shared assets like slide templates.

## One-time setup, per machine/account

From any repo where you're running Claude Code:

```
/plugin marketplace add <your-github-username>/claude-toolbox
/plugin install slide-figure@corey-tools
```

That makes the `slide-figure` skill available in that Claude Code session —
Claude will load it automatically when you ask to turn a figure into a slide
version, or you can call it directly with `/slide-figure`.

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

- `plugins/slide-figure/` — the SKILL.md that converts a publication R figure
  (ggplot2 or base R) into a presentation-ready version matching the deck theme.
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
