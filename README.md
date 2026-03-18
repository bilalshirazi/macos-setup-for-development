# macos-setup-for-development

A simple checklist to get a macOS machine ready for development.

## OS/User Accounts

- Complete macOS Setup Assistant and create a local user. [Create local user on OS setup](https://support.apple.com/en-ca/guide/mac-help/mh15191/mac)
- Install all available macOS updates: [Update macOS on Mac](https://support.apple.com/108382)

 ## Terminal + shell profile

- We’ll be using **Terminal** for most setup steps: [Terminal User Guide](https://support.apple.com/en-ca/guide/terminal/welcome/mac)
- Some installs (e.g. Homebrew) require adding commands to your shell profile so tools are available on your `PATH`. On macOS (zsh), that’s typically `~/.zprofile`.
  - What a shell profile file is: [Mac startup disk / shell startup files overview](https://support.apple.com/en-ca/102360)
  - View your current profile: `cat ~/.zprofile`
  - Edit it (simple option): `nano ~/.zprofile`

## Tooling

- Install Homebrew (this also installs Xcode Command Line Tools if missing):
  - Install script: ` /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" `
  - Homebrew homepage: [brew.sh](https://brew.sh)
  - Homebrew GitHub: [homebrew/brew](https://github.com/homebrew/brew)
  - Xcode Command Line Tools docs: [Installing the Command Line Tools](https://developer.apple.com/documentation/xcode/installing-the-command-line-tools/)
- Open **Terminal** (Applications → Utilities → Terminal): [Terminal User Guide](https://support.apple.com/en-ca/guide/terminal/welcome/mac)
- Add Homebrew to your `PATH` (so `brew` works in new shells). **Run these commands in Terminal**:
  - `echo >> ~/.zprofile`
  - `echo 'eval "$(/opt/homebrew/bin/brew shellenv zsh)"' >> ~/.zprofile`
  - `eval "$(/opt/homebrew/bin/brew shellenv zsh)"`
  - Verify: `brew --version`

## Python tooling (uv)

- Install `uv` with Homebrew: `brew install uv`
  - Reference: [astral-sh/uv](https://github.com/astral-sh/uv)
- Confirm it’s installed: `which uv` (should show `/opt/homebrew/bin/uv`)
- Install a Python CLI tool (example): `uv tool install pycowsay`
- If `uv` warns that `~/.local/bin` is not on your `PATH`, update your shell so installed tools work:
  - Option A (recommended): `uv tool update-shell` (then restart Terminal)
  - Option B (manual): `echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zprofile` (then restart Terminal or run `source ~/.zprofile`)
- Verify the installed tool runs: `pycowsay "Hello"`
- List Python versions `uv` can manage/download: `uv python list`
