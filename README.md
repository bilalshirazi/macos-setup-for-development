# macos-setup-for-development

A simple checklist to get a macOS machine ready for development.

## OS/User Accounts

- Complete macOS Setup Assistant and create a local user: [Create a user account on Mac](https://support.apple.com/en-ca/guide/mac-help/mh15191/mac)
- Install all available macOS updates: [Update macOS on Mac](https://support.apple.com/108382)

## Terminal + shell profile

- We’ll be using **Terminal** for most setup steps: [Terminal User Guide](https://support.apple.com/en-ca/guide/terminal/welcome/mac)
- Some installs (e.g. Homebrew) require updating your shell profile so tools are available on your `PATH`. On macOS (zsh), that’s typically `~/.zprofile`.
  - Overview: [Mac startup disk / shell startup files overview](https://support.apple.com/en-ca/102360)
  - View: `cat ~/.zprofile`
  - Edit (simple option): `nano ~/.zprofile`

## Tooling

- Install Homebrew (this also installs Xcode Command Line Tools if missing):
  - Install: `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
  - Homebrew: [brew.sh](https://brew.sh) · [homebrew/brew](https://github.com/homebrew/brew)
  - Xcode Command Line Tools: [Installing the Command Line Tools](https://developer.apple.com/documentation/xcode/installing-the-command-line-tools/)
- Add Homebrew to your `PATH` (so `brew` works in new shells). Run the “Next steps” commands Homebrew prints, typically:
  - `echo >> ~/.zprofile`
  - `echo 'eval "$(/opt/homebrew/bin/brew shellenv zsh)"' >> ~/.zprofile`
  - `eval "$(/opt/homebrew/bin/brew shellenv zsh)"`
  - Verify: `brew --version`


## Python

- We use Python for development and tooling (scripts, CLIs, automation) and we want control over versions: [Python on macOS](https://www.python.org/downloads/macos/)
- macOS includes an Apple-provided Python (`/usr/bin/python3`) that some system tools may depend on, so we **don’t modify or replace it**.
- Instead, we install and manage a separate Python for development using `uv` (isolated from the system Python).

## Python tooling (uv)

- Install `uv` with Homebrew: `brew install uv`
  - [Astral](https://astral.sh) · Reference: [astral-sh/uv](https://github.com/astral-sh/uv)
- Confirm it’s installed: `which uv` (should show `/opt/homebrew/bin/uv`)
- Install a Python CLI tool (example): `uv tool install pycowsay`
- If `uv` warns that `~/.local/bin` is not on your `PATH`, update your shell so installed tools work:
  - Option A (recommended): `uv tool update-shell` (then restart Terminal)
  - Option B (manual): `echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zprofile` (then restart Terminal or run `source ~/.zprofile`)
- Verify the installed tool runs: `pycowsay "Hello"`
- Install the latest version of python: `uv python install`
- Verify the Python you installed is available: `uv python list`
