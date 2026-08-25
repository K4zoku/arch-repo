# 📦 K4zoku Arch Repository

Personal Arch Linux binary repository, built and published automatically via GitHub Actions and GitHub Releases.

---

## 🚀 How to use this repository

Add the repository to your `pacman` configuration, then install packages like any official Arch package.

### 1. Trust the repository signing key

**Fast path (no key setup):** skip this whole section and use `SigLevel = Optional` for the repository in step 2. Signatures are verified when present but never required, so it just works.

Packages and the repository database are signed with the key `Kazoku <k4zoku@disr.it>` (fingerprint `787C 5932 BF4C DF5C 36E0 71B9 798F BBB0 5FCD D531`). Import it, verify the fingerprint, then locally sign it. Note that importing alone is not enough: `pacman-key --lsign-key` is what actually grants trust.

**Method A: from a keyserver** (this key is hosted on keys.openpgp.org; specify it explicitly since it does not propagate to other keyservers):

```bash
sudo pacman-key --recv-keys --keyserver hkps://keys.openpgp.org 787C5932BF4CDF5C36E071B9798FBBB05FCDD531
sudo pacman-key --finger 787C5932BF4CDF5C36E071B9798FBBB05FCDD531
sudo pacman-key --lsign-key 787C5932BF4CDF5C36E071B9798FBBB05FCDD531
```

**Method B: fast, from this repository** (no keyserver needed; the key file is bundled here):

```bash
curl -fsSL -o /tmp/k4zoku.asc https://raw.githubusercontent.com/K4zoku/arch-repo/main/k4zoku.asc
sudo pacman-key --add /tmp/k4zoku.asc
sudo pacman-key --finger 787C5932BF4CDF5C36E071B9798FBBB05FCDD531
sudo pacman-key --lsign-key 787C5932BF4CDF5C36E071B9798FBBB05FCDD531
```

### 2. Edit your `pacman.conf`

Append the following to the bottom of `/etc/pacman.conf`:

```ini
[k4zoku]
SigLevel = Required DatabaseOptional
Server = https://github.com/K4zoku/arch-repo/releases/download/repository
```

### 3. Sync and install

```bash
sudo pacman -Sy
sudo pacman -S <package-name>
```

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
| [tosu-git](https://github.com/tosuapp/tosu) | Memory reader and PP counters provider for osu! and osu! Lazer (git build) (`x86_64`) |
| [dearsql](https://github.com/dunkbing/dearsql) | Cross-platform SQL database client (`x86_64`) |
| [dearsql-git](https://github.com/dunkbing/dearsql) | Cross-platform SQL database client (git build) (`x86_64`) |

---

## 🔧 Use as an AUR source (build from source)

Every package is also mirrored as a git branch carrying its full AUR history, exactly like the official `archlinux/aur` mirror. This works even when the AUR is unreachable.

Clone a package and build it yourself (requires `base-devel`):

```bash
git clone --depth 1 --single-branch --branch <package> \
  https://github.com/K4zoku/arch-repo.git <package>
cd <package>
makepkg -si
```

Always review the `PKGBUILD` before building, as you would with any AUR package.

Example with `webhid`:

```bash
git clone --depth 1 --single-branch --branch webhid \
  https://github.com/K4zoku/arch-repo.git webhid
cd webhid
makepkg -si
```
