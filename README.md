# GKD 镜像仓库

[![同步状态](https://github.com/hopol/gkd-mirror/actions/workflows/sync.yml/badge.svg)](https://github.com/hopol/gkd-mirror/actions/workflows/sync.yml)
[![镜像发布](https://github.com/hopol/gkd-mirror/actions/workflows/release.yml/badge.svg)](https://github.com/hopol/gkd-mirror/actions/workflows/release.yml)
[![许可证](https://img.shields.io/badge/license-GPL--3.0-blue.svg)](LICENSE)

## 简介

这是 [gkd-kit/gkd](https://github.com/gkd-kit/gkd) 的自动镜像仓库。

**GKD** 是一款基于 Android 无障碍服务的自定义屏幕点击应用，可以自动跳过开屏广告、关闭弹窗等。

**本项目不做任何修改**，仅提供：
- 📦 **源码同步**：每5天自动备份上游源代码
- 🚀 **发布镜像**：自动镜像上游的 APK 和构建产物
- 📝 **中文日志**：每个版本附带中文更新说明

## 为什么需要镜像？

GitHub 上的开源项目可能因为维护调整、作者归档等原因变得不可访问。本镜像仓库确保即使上游项目出现问题，源码和客户端仍然可用。

## 下载

前往 [Releases](https://github.com/hopol/gkd-mirror/releases) 页面下载最新版本。

| 文件 | 说明 |
|------|------|
| `gkd-v{版本}.apk` | Android 安装包（推荐） |
| `outputs-v{版本}.zip` | 构建产物 |

## 功能特性

- ✅ 自动跳过应用开屏广告
- ✅ 自动关闭弹窗/对话框
- ✅ 基于订阅规则的高级选择器
- ✅ 覆盖数百款国内外热门应用
- ✅ 支持自定义规则

## 工作原理

### 源码同步（每5天）

```
上游仓库 (gkd-kit/gkd)
    ↓ git fetch
对比提交哈希
    ↓ 有变化
git archive 导出 → upstream/
    ↓
提交 & 推送 & 创建标签
```

### 发布镜像（每5天检查）

```
检查上游最新 Release
    ↓
是否已镜像？
    ├─ 是 → 跳过
    └─ 否 ↓
下载 APK 和构建产物
    ↓
生成中文 Changelog + 原始日志
    ↓
创建镜像 Release（mirror-v{版本号}）
```

## 标签说明

| 标签格式 | 说明 | 示例 |
|----------|------|------|
| `mirror-v{版本}-{哈希}` | 源码同步标签 | `mirror-v1.12.1-abc1234` |
| `mirror-{版本}` | 发布镜像标签 | `mirror-1.12.1` |

## 项目结构

```
gkd-mirror/
├── .github/
│   └── workflows/
│       ├── sync.yml           # 源码同步工作流（每5天）
│       └── release.yml        # 发布镜像工作流（每5天检查）
├── upstream/                  # 上游源码（运行时生成）
├── sync.sh                    # 本地同步脚本
├── README.md                  # 本文档
├── .gitignore
└── LICENSE
```

## 本地同步

```bash
git clone https://github.com/hopol/gkd-mirror.git
cd gkd-mirror
git remote add upstream https://github.com/gkd-kit/gkd.git
chmod +x sync.sh
./sync.sh
```

## 上游项目信息

- **项目名称**：GKD
- **上游仓库**：https://github.com/gkd-kit/gkd
- **官网**：https://gkd.li
- **技术栈**：Kotlin + Jetpack Compose + Android Gradle
- **上游许可证**：GPL-3.0
- **核心功能**：基于无障碍服务的 Android 自动点击应用

## 许可证

本镜像仓库采用 [GPL-3.0 许可证](LICENSE)，与上游项目一致。

## 致谢

感谢 [gkd-kit](https://github.com/gkd-kit) 创建了优秀的 GKD 项目。
