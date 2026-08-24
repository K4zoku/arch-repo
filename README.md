# 📦 K4zoku Arch Repository

Personal Arch Linux binary repository, built and published automatically via GitHub Actions and GitHub Releases.

---

## 🚀 How to use this repository

Add the repository to your `pacman` configuration, then install packages like any official Arch package.

### 1. Edit your `pacman.conf`

Append the following to the bottom of `/etc/pacman.conf`:

```ini
[k4zoku]
SigLevel = Optional TrustAll
Server = https://github.com/K4zoku/arch-repo/releases/download/repository
```

### 2. Sync and install

```bash
sudo pacman -Sy
sudo pacman -S <package-name>
```

**Disclaimer:** `SigLevel = Optional TrustAll` means packages are not GPG-signed. Only use this configuration for repositories you fully control or trust.

---

## 📦 Packages

| Package | Description |
| :--- | :--- |
| [webhid](https://github.com/K4zoku/FF-WebHID) | WebHID implementation for Firefox via a native-messaging bridge and hidraw daemon (`x86_64`, `aarch64`) |
| [webhid-git](https://github.com/K4zoku/FF-WebHID) | WebHID implementation for Firefox (git build) (`x86_64`, `aarch64`) |
| [webhid-addon](https://github.com/K4zoku/FF-WebHID) | WebHID browser extension for Firefox and Zen (`any`) |
| [webhid-addon-git](https://github.com/K4zoku/FF-WebHID) | WebHID browser extension for Firefox and Zen (git build, unsigned) (`any`) |
| [tosu-overlay](https://github.com/K4zoku/tosu-overlay-qt) | Overlay for osu! powered by tosu (`x86_64`) |
| [tosu-overlay-git](https://github.com/K4zoku/tosu-overlay-qt) | Overlay for osu! powered by tosu (git build) (`x86_64`) |
| [dearsql](https://github.com/dunkbing/dearsql) | Cross-platform SQL database client (`x86_64`) |
