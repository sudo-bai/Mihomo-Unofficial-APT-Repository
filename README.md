# Mihomo Smart分支 非官方 APT 软件源 (Unofficial Repository)

[](https://www.google.com/search?q=https://github.com/sudo-bai/Mihomo-Unofficial-APT-Repository/actions/workflows/update_repo.yml)

这是一个自动化的 APT 软件源，用于在 Debian/Ubuntu 系统上方便地安装和更新 [Mihomo](https://www.google.com/search?q=https://github.com/vernesong/mihomo) 内核。

本仓库通过 GitHub Actions 定时追踪上游的 **Prerelease (Alpha)** 版本，自动下载 `.deb` 包并更新 APT 索引。

-----

## 🚀 使用方法

只需三步即可配置此软件源。请在终端中以 `root` 权限或使用 `sudo` 执行以下命令：

### 1\. 导入 GPG 公钥

首先，下载并信任此软件源的签名公钥：

```bash
curl -fsSL https://sudo-bai.github.io/Mihomo-Unofficial-APT-Repository/public.key | sudo gpg --dearmor -o /usr/share/keyrings/mihomo-archive-keyring.gpg
```

### 2\. 添加软件源列表

将软件源地址添加到系统的源列表中：

```bash
echo "deb [signed-by=/usr/share/keyrings/mihomo-archive-keyring.gpg arch=amd64,arm64] https://sudo-bai.github.io/Mihomo-Unofficial-APT-Repository/ stable main" | sudo tee /etc/apt/sources.list.d/mihomo.list
```

### 3\. 安装或更新

更新索引并安装 Mihomo：

```bash
sudo apt update
sudo apt install mihomo
```

以后如果有新版本发布，你只需要运行 `sudo apt update && sudo apt upgrade` 即可自动更新。

-----

## 📦 支持架构

本软件源目前自动同步上游 Release 中的以下架构包：

  * `amd64` (x86\_64)
  * `arm64` (aarch64)
  * `armhf` (armv7)

*(具体取决于上游 Release 包含哪些架构的 deb 包)*

-----

## ⚙️ 工作原理

1.  **定时检查**：GitHub Actions 每隔 4 小时检查一次 `vernesong/mihomo` 的最新 Release（包含 Alpha/Prerelease）。
2.  **自动构建**：如果有新版本（通过 Release ID 变更判断），脚本会自动下载对应的 `.deb` 文件。
3.  **生成索引**：使用 `apt-ftparchive` 生成 `Packages` 和 `Release` 文件。
4.  **GPG 签名**：使用仓库管理员的私钥对索引文件进行签名，确保安全性。
5.  **发布**：所有文件通过 GitHub Pages 静态托管。

## ⚠️ 免责声明

  * 本仓库是非官方构建，与 Mihomo 官方团队无关。
  * 安装包直接来源于上游 GitHub Release，未做任何修改。
  * 请确保你信任上游代码以及本仓库的自动化构建过程。
