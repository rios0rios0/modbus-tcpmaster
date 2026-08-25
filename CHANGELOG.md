# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

This file is not edited by hand. Every change writes its own fragment under
`.changes/unreleased/` with [chlog](https://github.com/luizjhonata/chlog), and a release compiles
the pending fragments into a version section here — so two branches each adding an entry no
longer touch the same lines, and a rebase that used to conflict on this file now conflicts on
nothing.

When a new release is proposed:

1. Create a new branch `bump/x.x.x` (this isn't a long-lived branch!!!);
2. The fragments pending under `.changes/unreleased/` are compiled into a version section by `chlog batch auto && chlog merge` (AutoBump does this for you — it reads the fragments directly);
3. Open a Pull Request with the bump version changes targeting the `main` branch;
4. When the Pull Request is merged, a new Git tag must be created using <LINK TO THE PLATFORM TO OPEN THE PULL REQUEST>.

Releases to productive environments should run from a tagged version.
Exceptions are acceptable depending on the circumstances (critical bug fixes that can be cherry-picked, etc.).

## [Unreleased]

## [0.2.0] - 2026-05-25

### Added

- added `CLAUDE.md` with build commands, type-alias conventions, and architecture guidance for Claude Code sessions

## [0.1.2] - 2026-05-19

### Changed

- refreshed `.github/copilot-instructions.md` to add `release.yaml` to the repository structure and document the CI/release pipeline

## [0.1.1] - 2026-04-28

### Changed

- refreshed `.github/copilot-instructions.md` to add `CHANGELOG.md` and `.gitignore` to the repository structure and correct tracked-file annotations

## [0.1.0] - 2026-03-24

The changes weren't tracked until this version.
