# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A single-file documentation project: `README.md` is a manual checklist for setting up a macOS machine for development (Homebrew, shell profile, Oh My Zsh, Nerd Fonts, Python via `uv`/`ruff`, iTerm2, VS Code, GitHub CLI, MLX tooling). There is no source code, build system, linter, or test suite — there is nothing to build, lint, or test.

## Working in this repo

- Edits are almost always changes to `README.md`.
- The checklist is organized as top-level `##` sections in the order a user would actually perform setup (OS/accounts → terminal/shell → Homebrew → containers → shell customization → fonts → Python → IDE → version control → ML tooling). Keep new sections in a sensible place in that sequence rather than appending at the end.
- Each step generally follows the pattern: a short description, the exact shell command in a code span or fenced block, and a reference link to official docs. Match this pattern for new entries.
- Commands should be copy-pasteable as-is (no placeholders that require silent editing).
