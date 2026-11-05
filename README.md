# ONETAP 分发仓库

> 本仓库只做**配置源 + 壳分发**，不放客户端本体（13 GB 走网盘）。
> 2026-11-06 重建，版本号从 **v1.0.0** 重新起算。

## 目录

| 路径 | 作用 |
|---|---|
| `res/latest.json` | 统一清单：客户端分卷 + 启动器壳 + 下载器壳 |
| `res/sources.enc` | **加密**的真实下载源（123 / fj / 蓝奏）。明文在本地，不进仓库 |
| `res/netdisk.json` | 网盘分流入口（百度网盘 / 夸克网盘） |
| `app/launcher/latest.json` | 启动器壳元数据（版本 / 大小 / sha256 / 下载地址） |
| `app/downloader/latest.json` | 下载器壳元数据 |
| `releases/v1.0.0` | 两个壳的二进制（`.bin`，因为 jsDelivr 对 `.exe` 返 403） |

## 为什么不把源地址明文放在这里

仓库是公开的，明文写 123 / fj / 蓝奏 的分享链接和提取码等于把带宽送人。
所以真实地址放在 `res/sources.enc`：

```
b"OT1" + salt(16) + iv(16) + AES-128-CTR 密文 + HMAC-SHA256(32)
key = PBKDF2-SHA256(口令, salt, 60000, 32) 前 16 字节
```

口令编译在客户端里，防的是普通用户，不是逆向。

## 发版要改的文件

1. `res/latest.json`（`client_version` / `parts[]` / `released`）
2. `app/*/latest.json`（壳版本三件套：version / size / sha256）
3. `res/sources.enc`（换源时）
