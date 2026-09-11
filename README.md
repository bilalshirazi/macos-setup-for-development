# macos-setup-for-development

A simple checklist to get a macOS machine ready for development.

## OS/User Accounts

- Complete macOS Setup Assistant and create a local user: [Create a user account on Mac](https://support.apple.com/en-ca/guide/mac-help/mh15191/mac)
- Install all available macOS updates: [Update macOS on Mac](https://support.apple.com/108382)
- Enable FileVault (disk encryption), since this machine will hold SSH keys, signing keys, and API tokens: [Turn on FileVault](https://support.apple.com/en-ca/guide/mac-help/mh11785/mac)
- Enable the built-in firewall: [Turn on the firewall on Mac](https://support.apple.com/en-ca/guide/mac-help/mh34041/mac)

## Terminal + shell profile

- We’ll be using **Terminal/iTerm** for most setup steps: [Terminal User Guide](https://support.apple.com/en-ca/guide/terminal/welcome/mac)
- Almost every step below assumes basic shell comfort. If Bash/shell scripting isn't second nature yet, work through: [Learn the Bash Shell (course.ysap.sh)](https://course.ysap.sh)
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
- Install the rest of the CLI tools and apps used throughout this checklist from the repo's [Brewfile](Brewfile):
  - `brew bundle install --file=Brewfile`
  - Reference: [Homebrew Bundle](https://docs.brew.sh/Brew-Bundle-and-Brewfile)

## Dotfiles management

- Manage `~/.zprofile`, `~/.zshrc`, `~/.tmux.conf`, etc. as version-controlled files with `chezmoi` (installed via the Brewfile above), instead of editing them in place forever:
  - `chezmoi init`
  - Reference: [chezmoi](https://www.chezmoi.io/)
- Useful once you're syncing config across more than one Mac, or want your shell setup backed up in git.

## Containers / Virtualization

- Apple Containers (`container`, installed via the Brewfile above): native, lightweight container runtime.
  - Reference: https://formulae.brew.sh/formula/container
- Colima + Docker CLI (`colima`, `docker`, `docker-compose`, installed via the Brewfile above): for workflows that assume Docker specifically (e.g. `docker-compose.yml` files, CI reproduction).
  - Start the VM: `colima start`
  - Reference: [Colima](https://github.com/abiosoft/colima)
  - Alternative: if you'd rather have the full GUI, `brew install --cask docker` ([Docker Desktop for Mac](https://docs.docker.com/desktop/setup/install/mac-install/))

## Terminal Customization

- Install Oh My Zsh (a community-driven framework for managing your zsh themes and plugins):
  - `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`
  - Reference: [Oh My Zsh](https://ohmyz.sh/)
- *Note: Oh My Zsh will create a new `~/.zshrc` file to manage your terminal's appearance. It will not interfere with the `PATH` variables you already set up in your `~/.zprofile`.*
- **To uninstall:** If you ever want to revert to the default macOS terminal, simply run `uninstall_oh_my_zsh`.
- Install `tmux` (terminal multiplexer, installed via the Brewfile above) and its plugin manager:
  - `git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm`
  - Reference: [tmux](https://github.com/tmux/tmux) · [Tmux Plugin Manager](https://github.com/tmux-plugins/tpm)
  - Optional: add `tmux` to the Oh My Zsh `plugins=(...)` line in `~/.zshrc` for auto-attach behavior: [Oh My Zsh tmux plugin](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/tmux)
- Add `zsh-autosuggestions` and `zsh-syntax-highlighting` (installed via the Brewfile above) to the Oh My Zsh `plugins=(...)` line in `~/.zshrc`:
  - Reference: [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions) · [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

## Developer Fonts (Required for Terminal Themes)

- Themes like Oh My Zsh's `agnoster` require a patched Nerd Font to render the prompt arrows and icons correctly.
- Hack Nerd Font is installed via the Brewfile above.
  - Reference: [Nerd Fonts](https://www.nerdfonts.com/)
- **Configuration:**
  - **Terminal.app:** Go to `Terminal > Settings > Profiles > Text > Font`, click `Change...`, and select `Hack Nerd Font`.
  - **iTerm2:** Go to `iTerm2 > Settings > Profiles > Text > Font`, and select `Hack Nerd Font`.

## Python

- We use Python for development and tooling (scripts, CLIs, automation) and we want control over versions: [Python on macOS](https://www.python.org/downloads/macos/)
- macOS includes an Apple-provided Python (`/usr/bin/python3`) that some system tools may depend on, so we **don’t modify or replace it**.
- Instead, we install and manage a separate Python for development using `uv` (isolated from the system Python).

## Python tooling (uv/ruff)

- `uv` and `ruff` are installed via the Brewfile above.
  - [Astral](https://astral.sh) · Reference: [astral-sh/uv](https://github.com/astral-sh/uv) · [astral-sh/ruff](https://github.com/astral-sh/ruff)
- Confirm `uv` is installed: `which uv` (should show `/opt/homebrew/bin/uv`)
- Install a Python CLI tool (example): `uv tool install pycowsay`
- If `uv` warns that `~/.local/bin` is not on your `PATH`, update your shell so installed tools work:
  - Option A (recommended): `uv tool update-shell` (then restart Terminal)
  - Option B (manual): `echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zprofile` (then restart Terminal or run `source ~/.zprofile`)
- Verify the installed tool runs: `pycowsay "Hello"`
- Install the latest version of python: `uv python install`
- Verify the Python you installed is available: `uv python list`

## Node.js tooling (fnm/pnpm)

- `fnm` (Fast Node Manager, installed via the Brewfile above) manages Node versions per-project, the same way `uv` manages Python versions.
  - Reference: [fnm](https://github.com/Schniz/fnm)
- Install the latest LTS Node and switch to it:
  - `fnm install --lts`
  - `fnm use lts-latest`
- Add to `~/.zprofile` so `fnm` activates automatically: `eval "$(fnm env --use-on-cd)"`
- Enable `pnpm`/`yarn` via Node's built-in shim: `corepack enable`
  - Reference: [Corepack](https://nodejs.org/api/corepack.html)

## Shell tooling (direnv)

- `direnv` (installed via the Brewfile above) auto-loads/unloads per-project environment variables from a local `.envrc` file when you `cd` into a project directory, instead of managing everything globally in `.zprofile`.
  - Reference: [direnv](https://direnv.net/)
- Add to `~/.zprofile`: `eval "$(direnv hook zsh)"`

## IDE & Terminal

- iTerm2 (a highly customizable replacement for the default macOS Terminal) and Visual Studio Code (a powerful, extensible code editor) are installed via the Brewfile above.
  - Reference: [iTerm2](https://iterm2.com/) · [Visual Studio Code](https://code.visualstudio.com/)
- Verify you can launch VS Code from the terminal: `code .`
  - *Note: If the command is not found, open VS Code, press `Cmd+Shift+P`, type "shell command", and select **Shell Command: Install 'code' command in PATH**.*
- Install Claude Code (AI coding agent; requires Node from the section above): `npm install -g @anthropic-ai/claude-code`
  - Reference: [Claude Code docs](https://docs.claude.com/en/docs/claude-code/overview)
- Install Pi (minimal agent harness, installed via the Brewfile above): adapt Pi to your workflows, not the other way around.
  - Reference: [pi.dev](https://pi.dev)

## iOS Development

- Install Xcode via the Mac App Store CLI (`mas`, installed via the Brewfile above):
  - `mas install 497799835`
  - Open Xcode once to accept the license and let it install additional components.
  - Reference: [Xcode on the App Store](https://apps.apple.com/us/app/xcode/id497799835)
- Install the Xcode Command Line Tools if not already present: `sudo xcode-select --install`
- CocoaPods (dependency manager for iOS projects, installed via the Brewfile above).
  - Reference: [CocoaPods](https://cocoapods.org/)
- Optional: `xcodes` for managing multiple installed Xcode versions: `brew install xcodesorg/made/xcodes`
  - Reference: [xcodes](https://github.com/XcodesOrg/xcodes)

## Android Development

- Install Android Studio (installed via the Brewfile above), which bundles a JDK and the Android SDK manager.
  - Reference: [Android Studio](https://developer.android.com/studio)
- Add the SDK's command-line tools to your `PATH` so `adb`/Gradle work outside the IDE. Add to `~/.zprofile`:
  - `export ANDROID_HOME="$HOME/Library/Android/sdk"`
  - `export PATH="$ANDROID_HOME/platform-tools:$ANDROID_HOME/cmdline-tools/latest/bin:$PATH"`
  - Reference: [Set up the SDK command-line tools path](https://developer.android.com/tools/variables)
- Verify: `adb --version`

## Version Control

- `gh` (GitHub's official command line tool) is installed via the Brewfile above.
  - Reference: [GitHub CLI](https://cli.github.com/) · [cli/cli](https://github.com/cli/cli)
- Set your git identity:
  - `git config --global user.name "Bilal Shirazi"`
  - `git config --global user.email "bilal.shirazi@gmail.com"`
  - Reference: [Set your username in Git](https://docs.github.com/en/get-started/getting-started-with-git/setting-your-username-in-git) · [Set your commit email address](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/setting-your-commit-email-address)
- Generate an SSH key and register it with GitHub:
  - `ssh-keygen -t ed25519 -C "bilal.shirazi@gmail.com"`
  - `gh ssh-key add ~/.ssh/id_ed25519.pub`
  - Reference: [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) · [Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
- Sign your commits with the same SSH key:
  - `git config --global gpg.format ssh`
  - `git config --global user.signingkey ~/.ssh/id_ed25519.pub`
  - `git config --global commit.gpgsign true`
  - `gh gpg-key add ~/.ssh/id_ed25519.pub --type signing`
  - Reference: [About commit signature verification](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification) · [Telling Git about your signing key (SSH)](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key)
- Authenticate the CLI with your GitHub account: `gh auth login`

## Machine Learning

- Hugging Face CLI (for downloading models and datasets, installed via the Brewfile above).
  - Reference: [Hugging Face](https://huggingface.co/docs/huggingface_hub/guides/cli)
- Install `mlx-lm` (Apple's framework for running and fine-tuning text-based Large Language Models): `uv tool install mlx-lm`
  - Reference: [ml-explore/mlx-lm](https://github.com/ml-explore/mlx-lm)
- Install `mlx-vlm` (for running Vision Language Models and multimodal models): `uv tool install --with torch --with torchvision mlx-vlm`
  - Reference: [Blaizzy/mlx-vlm](https://github.com/Blaizzy/mlx-vlm)
- Install `mlx-audio` (for working with audio models on MLX): `uv tool install mlx-audio`
  - Reference: [ml-explore/mlx](https://github.com/ml-explore/mlx)
- Core MLX framework overview: [ml-explore/mlx](https://github.com/ml-explore/mlx)
