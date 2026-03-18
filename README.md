# macos-setup-for-development

A step-by-step checklist for setting up (and maintaining) macOS for development.

## Setup (order of operations)

### 1) First boot + local user
- Complete the macOS setup assistant and create a local user account.

### 2) Update macOS
- Run Software Update and install the latest available updates.
- Reference: [Update macOS on Mac](https://support.apple.com/en-ca/108382)

### 3) (Optional) Enroll in Apple Beta Software Program
Only do this if you intentionally want beta OS releases on this machine.
- Reference: [Apple Beta Software Program](https://beta.apple.com)

### 4) (Optional) Enable Apple Intelligence
Availability depends on macOS version, region/language, and supported hardware.
- Reference: [Apple Intelligence](https://www.apple.com/apple-intelligence/)

### 5) Install Homebrew (package manager)
Homebrew simplifies installing and keeping CLI tools up to date.
- Primary site: [brew.sh](https://brew.sh)
- Source repo: [homebrew/brew](https://github.com/homebrew/brew)

## Ongoing maintenance

### Keep macOS current
- Check Software Update regularly (especially security updates).
- If enrolled in beta, expect more frequent updates and occasional breakage.

### Keep Homebrew packages current
```sh
brew update
brew upgrade
brew cleanup
brew doctor
```

## Notes / future steps to add
- Xcode / Command Line Tools
- Language runtimes (Node, Python, etc.)
- SSH keys, Git signing, password manager, backups
- Dotfiles + reproducible setup (Brewfile)
