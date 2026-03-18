# macos-setup-for-development

A step-by-step guide for setting up macOS for development. Follow the steps in order — each one builds on the previous.

---

## Setup steps

### Step 1 — Initial login / create local user

Power on your Mac and complete the out-of-box setup wizard to create your local user account.

---

### Step 2 — Update macOS

Bring the OS fully up to date before installing anything else.

1. Open **System Settings → General → Software Update**
2. Install all available updates and restart if prompted

Reference: [Update macOS on Mac — Apple Support](https://support.apple.com/en-ca/108382)

---

### Step 3 — Enroll in the Apple Beta Software Program *(optional)*

If you want access to pre-release macOS updates, enroll your device in the Beta Software Program.

1. Visit the [Apple Beta Software Program](https://beta.apple.com) and sign in with your Apple ID
2. Follow the on-screen instructions to enrol your device
3. Return to **System Settings → General → Software Update** to download the latest beta

> See the [Notes](#notes) section below for caveats on running beta software.

---

### Step 4 — Enable Apple Intelligence *(optional)*

[Apple Intelligence](https://www.apple.com/apple-intelligence/) provides on-device AI writing tools, summaries, and more.

1. Open **System Settings → Apple Intelligence & Siri**
2. Turn on **Apple Intelligence** and follow any prompts to download required models

> Apple Intelligence requires Apple Silicon (M1 or later) and macOS Sequoia 15.1+. Some features are only available in English (US) initially. See the [Notes](#notes) section.

---

### Step 5 — Install Homebrew

[Homebrew](https://brew.sh) is the standard package manager for macOS. Install it before any development tools so you can manage everything from one place.

1. Open **Terminal**
2. Run the official install script:
   ```sh
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```
3. Follow the post-install instructions printed in the terminal (adds Homebrew to your `PATH`)
4. Verify the install:
   ```sh
   brew doctor
   ```

References: [brew.sh](https://brew.sh) · [Homebrew on GitHub](https://github.com/Homebrew/brew)

---

## Ongoing maintenance

Keep your system and packages up to date with these canonical commands:

| Task | Command |
|------|---------|
| Update Homebrew and package index | `brew update` |
| Upgrade all installed packages | `brew upgrade` |
| Remove old versions | `brew cleanup` |
| Check for problems | `brew doctor` |
| Check for macOS updates | System Settings → General → Software Update |

---

## Notes

- **Beta software** — Beta macOS releases may contain bugs and are not recommended for production machines or primary work devices. Enrol a secondary machine or a partition when possible.
- **Apple Intelligence availability** — Requires Apple Silicon (M1 or later) and macOS Sequoia 15.1+. Availability of specific features varies by language and region. Check [Apple's Apple Intelligence page](https://www.apple.com/apple-intelligence/) for the latest requirements.
- **Adding more steps** — As you install more tooling (e.g. Xcode Command Line Tools, a language runtime, an IDE), add a new numbered step under [Setup steps](#setup-steps) in the appropriate order.
