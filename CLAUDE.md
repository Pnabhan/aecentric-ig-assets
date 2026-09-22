# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Public image hosting for AECentric's Instagram posts. This repo holds only generated output — no
source code, no logic. It exists so Instagram's Graph API can fetch post images over
`raw.githubusercontent.com/Pnabhan/aecentric-ig-assets/main/...` (the Graph API needs a publicly
fetchable URL, and image URLs only resolve from `main`).

All content here is produced by the sibling repo, `aecentric-ig-automation` — its `PIPELINE.md` is
the authoritative spec for how and when files land here. Don't hand-edit or regenerate anything in
this repo directly; changes come from running that pipeline.

## Structure

- `posts/<topic-id>/` — one directory per published (or pre-rendered but not yet published) post:
  `slide-N.png` (1080x1080 renders), `<topic-id>.pdf` (LinkedIn carousel export, uploaded by Peter
  by hand), `linkedin-caption.txt` (LinkedIn version of the caption, "we" voice), and
  `posted.json` (permalink + UTC/Central post time, written only after a successful Instagram
  publish).
- `videos/` — Digital Twin video output (HeyGen pipeline), same posting model as `posts/`.

A `posts/<id>/` folder existing with no matching `posted.json` does not mean the post went out —
it can mean artwork was pre-rendered ahead of time and not yet published. What actually went live
is only ever determined by reconciling against the Instagram account itself
(`aecentric-ig-automation/scripts/check_recent_duplicate.py`), never by the presence of files here.

## Working conventions

No build, lint, or test tooling — this repo is a content mirror. Commits are pushed directly to
`main` (no branches, no pull requests), since Instagram only reads images from `main`; see
`aecentric-ig-automation/PIPELINE.md` for why.
