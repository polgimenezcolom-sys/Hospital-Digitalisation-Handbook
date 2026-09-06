# Contributing

This handbook is version 0.2. It is wrong in places nobody has found yet, and the only way those get
found is by teams using it and saying what did not match.

**Your project's feedback is the most valuable thing you can send back.** More valuable than the
deployment, in some cases — a deployment helps one hospital, a correction helps every team after you.

## The smallest useful contribution

Fix one thing. A wrong figure, a step that does not work, a piece of advice that turned out to be
bad. Every page has an edit pencil at the top right: click it, change the text, describe what you
changed. You do not need to clone anything or install anything.

## Adding your deployment

The most useful contribution is a written-up deployment. Follow the
[case study template](case-study.md) — it is four questions and it explicitly asks what went wrong.

## Adding or changing a page

```bash
git clone https://github.com/aucoop/Hospital-Digitalisation-Handbook
cd Hospital-Digitalisation-Handbook
pip install -r requirements.txt
mkdocs serve
```

Then open <http://127.0.0.1:8000>. Edit the Markdown under `docs/`; the page reloads as you save.
Add new pages to the `nav:` section of `mkdocs.yml` so they appear in the navigation, then open a
pull request.

## House style

- **Second person, present tense.** *"You arrive at the ward and…"* — not *"the implementer should"*.
- **Story explains why; guide explains how; instruments are what you fill in.** Keep them separate. A
  reader looking for a command should not have to read an argument.
- **Chapter titles in the story are the reader's own words**, in quotes, describing a problem they
  will actually have.
- **Concede what did not work.** A handbook that only records successes teaches nothing and nobody
  believes it.
- **Expand an abbreviation once per page**, then use it. Everything is in the [glossary](../glossary.md).
- **Do not put credentials anywhere.** Not in an example, not in a screenshot, not redacted.

## What to do with an open question

Several pages carry a "not yet settled" box. If your deployment resolves one — say, by calibrating
the B-1 thresholds, or by establishing whether the feedback form can be attached to the closure
report — that is a significant contribution. Change the box into an answer and say who decided it.
