# AGENTS.md

Instructions for AI coding agents (Claude Code, Codex and others) working in this repository. `CLAUDE.md` only imports
this file, so edit this one. [README.md](README.md) describes the project for people; this file lists what the code
alone does not tell you.

## Project Overview

Bert's fork of [YahboomTechnology/Motor-with-Encoder](https://github.com/YahboomTechnology/Motor-with-Encoder), kept
as reference material: Yahboom's documentation for their encoder TT motor (6 V, 0.3 A rated, 13-line Hall encoder)
and for their 2-channel (AT8236 / TB6612) and 4-channel motor driver modules, as PDF tutorials per controller
(Arduino, ESP32, STM32, MSPM0, Jetson Nano, Raspberry Pi 5, Raspberry Pi Pico 2, RDK X5, a PC host over serial).

There is no source code in the tree and nothing to build. Upstream is active (last change 2026-09-22); this fork
stays in Yahboom's fork network so it can follow it. Bert's own content is limited to the files listed under
Repository Layout as the fork's own.

## Commands

Lint (the only check):

```sh
npx markdownlint-cli2 "**/*.md"
```

Sync with upstream — through a pull request, merged with a merge commit (see Conventions for why):

```sh
git fetch upstream
git switch main && git pull
git switch -c chore/sync-upstream
git merge -m "chore: merge upstream/main" upstream/main
# Add a CHANGELOG entry (### Changed under [Unreleased]) and month sections for the new upstream commits, then commit.
git push -u origin chore/sync-upstream
gh pr create -R bberrevoets/Motor-with-Encoder --base main --head chore/sync-upstream --assignee @me --title "chore: sync with upstream"
gh pr merge <n> -R bberrevoets/Motor-with-Encoder --merge
```

## Repository Layout

- `1.Introduction/` — the encoder motor introduction.
- `2.2-channel motor drive module tutorials/` — 2-channel driver (AT8236 / TB6612): Arduino, STM32F103C8T6,
  MSPM0G3507 and MSPM0G3519 tutorials, and `Annex_Download_Link.txt` (Google Drive folder with the code).
- `3.4-channel motor drive module tutorials/` — 4-channel driver board: introduction, control command, and drive
  tutorials per controller over IIC and USART, and `Annex_Download_Link.txt`.
- `3.4-channel motor drive module tutorials-NEW/` — Yahboom's 2026 4-channel introduction, control command and
  firmware update guides.
- `Motor_with_Encoder.jpg`, `README.md` — Yahboom's product photo and README; the README ends with the fork's own
  sections, from `## This fork` down.
- The fork's own files: `AGENTS.md`, `CLAUDE.md`, `CHANGELOG.md`, `.gitattributes`, `.gitignore`,
  `.markdownlint.json`, `.markdownlint-cli2.jsonc`.

## Conventions

- **A fork on purpose** (Bert's decision, 2026-10-11): it stays in Yahboom's fork network to follow upstream; do not
  detach it. Remotes: `origin` is this fork, `upstream` is Yahboom's repo, fetch only. `gh repo clone` marks
  `upstream` as gh's default repo, so a bare `gh pr create` would open the PR at Yahboom. In a fresh clone run
  `gh repo set-default bberrevoets/Motor-with-Encoder` and `git remote set-url --push upstream DISABLED`, and name
  the repo with `-R` in `gh` commands. Never open pull requests or issues at YahboomTechnology from here.
- **Upstream syncs** go through a pull request as in Commands, not the Sync fork button: `main` accepts changes only
  through pull requests. Merge a sync PR with a **merge commit**, never squash or rebase. Those give Yahboom's commits
  new hashes, so they never become ancestors of `main` and GitHub keeps listing them as "behind". The fork's own PRs
  are squash-merged as usual.
- **Sync conflicts:** only `README.md` is shared with upstream and changed here. Keep Yahboom's new text above
  `## This fork` and the fork's sections below it. The other fork files do not exist upstream.
- **Yahboom's files stay as upstream has them:** the PDFs, the photo, the `Annex_Download_Link.txt` files and the
  README text above `## This fork`. No lint fixes, no edits; they change only through upstream syncs. `README.md` is
  therefore excluded from markdownlint (`.markdownlint-cli2.jsonc`). "Update the documentation" (Workflow Rules
  below) means `AGENTS.md`, `CHANGELOG.md` and the README sections from `## This fork` down.
- **No Git LFS here — an exception to the Binaries rule in Workflow Rules below.** `.gitattributes` keeps the
  standard repo-init block, but its last line `* !filter !diff !merge` switches LFS off for every file (a later line
  wins per attribute). Tested 2026-10-11: with the block alone, `git add --renormalize .` turns all 31 PDFs and JPGs
  into LFS pointers; with the override, nothing changes. Never run `git lfs migrate` (it rewrites every commit hash
  and cuts the fork off from upstream) and never add a `filter=lfs` pattern. `git lfs track` still lists the
  block's patterns as tracked and `*` as excluded; `git check-attr filter -- <file>` is the check that counts
  (`unspecified`).
- **Code:** the current code is on Google Drive (`Annex_Download_Link.txt`). The older Arduino sketches and the
  STM32F103RCT6 and MSPM0 code archives were removed upstream on 2025-02-28; `0972395` (2024-12-28) is the last commit
  that has them: `git ls-tree -r --name-only 0972395`, then `git show "0972395:<path>"`.
- Upstream has no licence file: the material is Yahboom's. Keep this fork as a reference copy; do not relicense the
  tutorials or present them as Bert's.

<!-- repo-init:start -->
## Repository Info

- **Company:** Berrevoets Systems
- **Author:** Bert Berrevoets
- **Contact:** <bert@berrevoets.net>
- **Remote:** <https://github.com/bberrevoets/Motor-with-Encoder> (public)

## Workflow Rules

- **GitHub Flow:** `main` is the default and only long-lived branch. It is protected by the ruleset "Protect main":
  no direct pushes, no deletion, changes only through a pull request, and all PR conversations must be resolved
  before merging. Merged head branches are deleted automatically.
- After cloning, run `git config pull.rebase true` once, so `git pull` rebases instead of creating merge commits.
- Work on a branch per topic, push it, and open a PR to `main` only when Bert asks for it, assigned to him
  (`gh pr create --assignee bberrevoets`). PRs are squash-merged. After a merge: switch to `main` and pull, then delete the
  local branch with `git branch -D <branch>` (`-d` refuses after a squash merge) once
  `gh pr view <branch> --json state,headRefOid` shows `MERGED` and the same commit as `git rev-parse <branch>`.
- **"Update the documentation"** means `AGENTS.md`, the project's own `README.md` files (not vendored third-party ones)
  and `CHANGELOG.md`; then commit and push.
- [CHANGELOG.md](CHANGELOG.md) follows Keep a Changelog: the Attributors list at the top, and one `Author: *Name*`
  line under each section heading (`### Added`, `### Changed`, ...).
- Markdown must pass `markdownlint-cli2 "**/*.md"` with [.markdownlint.json](.markdownlint.json) (180-character
  lines) before every commit.
- Binaries go through Git LFS: every `filter=lfs` pattern in `.gitattributes` — the standard set (PDF, ZIP, PNG,
  JPEG, STEP/STP, STL, 3MF, F3D/F3Z) plus any pattern this repository adds. Add a pattern there before committing
  another binary type (GIF, BMP, ...). The patterns are lowercase and match `X.PNG` only where `core.ignorecase` is
  true (Windows, macOS); on a case-sensitive system check a new binary with `git check-attr filter -- <file>` before
  committing it.
- Commit messages use the conventional style (`feat:`, `fix:`, `docs:`, `chore:`).
<!-- repo-init:end -->
