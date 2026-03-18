# macos-setup-for-development

A simple checklist to get a macOS machine ready for development.

## Base (done)

- Complete macOS Setup Assistant and create a local user. [Create local user on OS setup](https://support.apple.com/en-ca/guide/mac-help/mh15191/mac)
- Install all available macOS updates: [Update macOS on Mac](https://support.apple.com/108382)

## Homebrew + Xcode Command Line Tools (done)

- Install Homebrew (this also installs Xcode Command Line Tools if missing):
  - Install script: ` /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" `
  - Homebrew homepage: [brew.sh](https://brew.sh)
  - Homebrew GitHub: [homebrew/brew](https://github.com/homebrew/brew)
  - Xcode Command Line Tools docs: [Installing the Command Line Tools](https://developer.apple.com/documentation/xcode/installing-the-command-line-tools/)

- Add Homebrew to your PATH (so `brew` works in new shells):
  - `echo >> ~/.zprofile`
  - `echo 'eval "$(/opt/homebrew/bin/brew shellenv zsh)"' >> ~/.zprofile`
  - `eval "$(/opt/homebrew/bin/brew shellenv zsh)"'`
  - Verify: `brew --version`

## Workspace (done)

- Create a dev folder: `mkdir -p ~/Workspace`

## Python (observed)

- `python` is not available by default on macOS (expected).
- `python3` is available:
  - Verify: `python3 --version`

## Next

- Install `uv` (attempted, not installed yet): [astral-sh/uv](https://github.com/astral-sh/uv)
