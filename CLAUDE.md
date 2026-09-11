# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A documentation project, not a codebase: `README.md` is a manual checklist for setting up a macOS machine for development, and `Brewfile` is the Homebrew manifest it drives. There is no source code, build system, linter, or test suite — there is nothing to build, lint, or test.

## Working in this repo

- Edits are almost always changes to `README.md`, sometimes paired with a `Brewfile` change.
- The checklist is organized as top-level `##` sections in the order a user would actually perform setup: OS/accounts → terminal/shell → Homebrew+Brewfile → dotfiles → containers → shell customization → fonts → Python → Node.js → shell tooling (direnv) → IDE & agents → iOS → Android → version control → ML tooling. Keep new sections in a sensible place in that sequence rather than appending at the end.
- Any tool installable via `brew install`/`brew install --cask` goes in `Brewfile`, not as an inline command in `README.md` — the README section explains the *why* and says "installed via the Brewfile above," then covers whatever config/verification steps aren't brew's job (PATH exports, `.zprofile` hooks, post-install commands). Non-brew installs (curl scripts, `npm install -g`, `uv tool install`, App Store via `mas`) stay inline in the relevant README section.
- Each step generally follows the pattern: a short description, the exact shell command in a code span or fenced block, and a reference link to official docs. Match this pattern for new entries.
- Commands should be copy-pasteable as-is (no placeholders that require silent editing) — this repo documents one person's real machine, so use their actual values (name, email, etc.) rather than generic placeholders like "Your Name".
