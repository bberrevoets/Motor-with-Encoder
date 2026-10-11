# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). The dated sections below
`[Unreleased]` are Yahboom's upstream history, summarised per month from the commits.

## Attributors

- Bert Berrevoets (<bert@berrevoets.net>) — Berrevoets Systems — fork maintainer
- Claude Opus 5.5 — co-author of the 2026 fork setup
- Yahboom Technology — the tutorials, documents, photo and README
  ([YahboomTechnology/Motor-with-Encoder](https://github.com/YahboomTechnology/Motor-with-Encoder))

## [Unreleased]

### Added

Author: *Bert Berrevoets*

- AI agent setup: [AGENTS.md](AGENTS.md) as the single instruction file, a [CLAUDE.md](CLAUDE.md) stub that imports it,
  markdownlint (180 characters; Yahboom's `README.md` excluded), a `.gitattributes` that keeps every file out of
  Git LFS so the history stays shared with upstream, and this changelog.
- `README.md`: the fork's own sections after Yahboom's text (This fork, Conventions, Authors).

### Changed

Author: *Bert Berrevoets*

- Synced with upstream on 2026-10-11: a fast-forward from Yahboom's 2022-01-24 README commit to their 2026-09-22
  commit, bringing in the 2023-06 to 2026-09 history below.

## 2026-09

### Added

Author: *Yahboom Technology*

- 2-channel module: separate AT8236 and TB6612 drive tutorials for the MSPM0G3507 and the MSPM0G3519.

### Changed

Author: *Yahboom Technology*

- 4-channel module (`-NEW` folder): control command tutorial updated.

### Removed

Author: *Yahboom Technology*

- 2-channel module: the single `3.For MSPM0` folder, replaced by the two MCU folders above.
- The drive tutorials added in 2026-06 (the top-level `2.Drive tutorials` folder and the one in the `-NEW` folder).

## 2026-06

### Added

Author: *Yahboom Technology*

- `3.4-channel motor drive module tutorials-NEW`: introduction to the 4-channel drive board, control command and
  firmware update guides, and a set of drive tutorials.
- A top-level `2.Drive tutorials` folder: motor introduction, PC host, Arduino, ESP32 and Jetson Nano.

## 2025-02

### Added

Author: *Yahboom Technology*

- Tutorials reorganised per driver module: `1.Introduction`, `2.2-channel motor drive module tutorials` (Arduino,
  STM32, MSPM0) and `3.4-channel motor drive module tutorials` (board introduction, control command, and drive
  tutorials for a PC host, Arduino, ESP32, Jetson Nano, MSPM0, Raspberry Pi Pico 2, RDK X5, Raspberry Pi 5 and STM32).
- `Annex_Download_Link.txt` in both module folders: the source code moved to Google Drive.

### Removed

Author: *Yahboom Technology*

- The code folders: the TT motor introduction, the Arduino sketches, the STM32F103RCT6 code and the MSPM0 code. They
  remain in the git history.

## 2024-12

### Added

Author: *Yahboom Technology*

- `4.MSPM0 code`: encoder data acquisition tutorial and code archive.

### Changed

Author: *Yahboom Technology*

- README and product photo cover only the black 13-line motor; the blue 3-line motor was dropped.

## 2023-06

### Added

Author: *Yahboom Technology*

- `3.STM32 Code/STM32F103RCT6`: code archive, readme, wiring diagram and tutorial (the Word document was replaced by a
  PDF the next day).

## 2022-01

### Added

Author: *Yahboom Technology*

- README and product photo for two encoder TT motors: the black 13-line and the blue 3-line motor.
- TT motor introduction, and Arduino sketches for both motors (`13_Channel_motor`, `3_Channel_motor`) with a
  tutorial PDF.
