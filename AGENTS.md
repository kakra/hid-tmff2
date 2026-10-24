# Guide for AI agents

This file is the work contract for AI coding agents in this repository. The
rules for all contributors are in
[docs/CONTRIBUTING.md](./docs/CONTRIBUTING.md), section "Submitting changes".
This file adds what is specific to agents.

## Before you change anything

+ Read `docs/CONTRIBUTING.md` completely, and `docs/AGENTS.md` before touching
  documentation or hardware evidence.
+ For force feedback work, read `docs/FFBEFFECTS.md` and the T300RS driver in
  `src/tmt300rs/` to see how effects are encoded and how the core driver
  `src/hid-tmff2.c` is used.
+ Check open pull requests, issues and the human's queue branch for work on the
  same wheel or code.
+ Larger restructuring (shared backends, wheel detection, renames across
  drivers) needs an issue with the maintainer first. Don't start it on your own.

## Queue workflow

+ Keep all work on the human's local queue branch. Each commit covers a single
  concern and builds on its own.
+ Propose the next ready single-concern series to the human, with a short
  reason why it is ready and what it depends on. Prepare it on a new branch
  from the current `master`.
+ Address review feedback with `fixup!` commits folded into the commits they
  fix. Keep the same pull request branch. Never squash a series into one
  commit, never open a replacement pull request.
+ After a merge, rebase the queue onto `master` and re-cut the remaining
  series.

## Evidence

+ Don't invent protocol details. Every packet field, constant and device ID
  must come from captures, descriptor dumps or tests the human has done.
+ Record the evidence in `docs/` as described in `docs/AGENTS.md`, separate
  measured facts from assumptions, and reference it in the commit message.
+ Don't add workarounds for behavior you can't explain.

## Commits

+ Write kernel-style commit messages: driver prefix, why before what, `Link:`
  or `Fixes:` trailers with full URLs to issues or commits you have checked.
+ The human adds their own `Signed-off-by` after reviewing and testing. Don't
  add `Co-authored-by` or similar trailers for AI tools.

## Working with the human

+ The human submits the change and must be able to explain it. Explain your
  changes so they can review them and answer review questions themselves.
+ Don't open pull requests, post comments, resolve review threads or answer
  reviews on GitHub. Prepare the branch and text, the human submits it.
+ Fill in the pull request template as instructed there, and leave the
  declaration checkboxes to the human.

## Verification

+ Build the module for each commit (`make`).
+ Run `checkpatch.pl --no-tree` on the series.
+ Check new or changed files for non-ASCII characters with
  `grep -P -n "[\x80-\xFF]" <file>`.
+ Report what could not be tested, in particular on hardware.
