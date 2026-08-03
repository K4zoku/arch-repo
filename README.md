# 📦 K4zoku Arch Repository

Personal Arch Linux binary repository, built and published automatically via GitHub Actions and GitHub Releases.

[🇻🇳 Xem bản tiếng Việt](#-hướng-dẫn-tiếng-việt)

---

## 🚀 How to use this repository

Add the repository to your `pacman` configuration, then install packages like any official Arch package.

### 1. Check CPU compatibility

Packages are built with generic `x86-64` optimizations in a CachyOS container, so any `x86-64` CPU can use this repository.

### 2. Edit your `pacman.conf`

Append the following to the bottom of `/etc/pacman.conf`:

```ini
[k4zoku]
SigLevel = Optional TrustAll
Server = https://github.com/K4zoku/arch-repo/releases/download/repository
```

### 3. Sync and install

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

---

## 🇻🇳 Hướng dẫn tiếng Việt

Kho gói nhị phân Arch Linux cá nhân, được build và phát hành tự động bằng GitHub Actions và GitHub Releases.

### 🚀 Cách dùng repository này

Chỉ cần thêm repository vào cấu hình `pacman` rồi cài gói như gói chính thức của Arch.

#### 1. Kiểm tra khả năng tương thích CPU

Các gói được build với mức tối ưu generic `x86-64` bên trong container CachyOS, nên mọi CPU `x86-64` đều dùng được repository này.

#### 2. Chỉnh sửa `pacman.conf`

Thêm đoạn sau vào cuối file `/etc/pacman.conf`:

```ini
[k4zoku]
SigLevel = Optional TrustAll
Server = https://github.com/K4zoku/arch-repo/releases/download/repository
```

#### 3. Đồng bộ và cài đặt

```bash
sudo pacman -Sy
sudo pacman -S <tên-gói>
```

**Lưu ý:** `SigLevel = Optional TrustAll` nghĩa là gói không được ký GPG. Chỉ nên dùng cấu hình này cho repository do chính bạn kiểm soát hoặc bạn thực sự tin tưởng.

---

### 📦 Danh sách gói

| Gói | Mô tả |
| :--- | :--- |
| [webhid](https://github.com/K4zoku/FF-WebHID) | Triển khai WebHID cho Firefox qua native-messaging bridge và hidraw daemon (`x86_64`, `aarch64`) |
