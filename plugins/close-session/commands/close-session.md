---
description: Log this session's changes to the repo's changelog, then commit and push
---

Write a changelog entry summarizing everything we did this session that
materially affects this repository.

## Where to write it

1. Look for an existing changelog file at the repo root, in this order:
   `CHANGES.md`, `CHANGELOG.md`, `HISTORY.md`, `NEWS.md`. Use the first one
   that exists.
2. If one exists, **match its format exactly** — reuse whatever template,
   heading style, category tags, or ordering convention it already uses
   (read the top of the file to learn it). Add new entries newest-first,
   below any template/header block and above prior entries.
3. If none exists, create `CHANGES.md` with a short entry using a simple
   dated section (`## YYYY-MM-DD`) and bullet points.

## What to write

- One entry per distinct change — not one entry per file touched.
- Be specific: name the exact file, function, section, figure, table, or
  parameter affected, and give old vs. new values where a number changed.
- State what follow-up action (if any) the change implies.
- Keep it factual and scoped to changes made **this session**.

## Then

1. Stage and commit the changelog file with a clear message describing the
   log update (e.g. `"Log session changes"`).
2. Push to the branch currently checked out (`git push`), not a hardcoded
   branch. If no upstream is set, use `git push -u origin HEAD`.

If nothing we did this session affects the repository, say so explicitly
rather than writing a placeholder entry, and do not commit.
