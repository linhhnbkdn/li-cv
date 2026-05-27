# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A personal CV for Hoàng Ngọc Linh. Not a traditional codebase — there's no application logic or tests, but the repo does host a Jekyll site on GitHub Pages. The repo holds three artifacts:

- `README.md` — the canonical source of the CV, written in Markdown. Edit this when the CV content changes.
- `HOANG_NGOC_LINH_CV.pdf` — an exported PDF rendering of the CV, generated externally (not from a script in this repo). Treat it as a build output: regenerate it after meaningful changes to `README.md` so the two stay in sync.
- `docs/` — Jekyll site published to GitHub Pages at `https://linhhnbkdn.github.io/li-cv/`. Uses the `sharu725/online-cv` remote theme. Content lives in `docs/_data/data.yml`; the site is rebuilt automatically on push.

When the CV changes, update **both** `README.md` and `docs/_data/data.yml` — they share the same content but use different schemas (Markdown vs YAML).

## Editing conventions

- The CV is bilingual-friendly but written in English. Preserve diacritics in the name and Vietnamese place names (e.g. "Hoàng Ngọc Linh", "Đà Nẵng").
- Section order in `README.md` is intentional (Summary → Education → Certifications → Awards → Skills → Experience → Projects → Languages → Additional Info). Keep it.
- Dates use the `Mon YYYY – Mon YYYY` format (en-dash, not hyphen). "Present" for current roles.
- When updating experience or skills, also check whether the **Professional Summary** at the top still reflects reality — it tends to drift.

## PDF regeneration

The PDF is not produced by anything in this repo. If you change `README.md` and the user wants the PDF refreshed, ask which tool they use (e.g. pandoc, a Markdown-to-PDF web service, manual export) rather than guessing — the visual style of the current PDF must be preserved.
