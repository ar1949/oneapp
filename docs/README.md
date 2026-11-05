# 通道说明（v1.0.0 重建版）

旧的 `00-文件与读取关系 / 01-版本号规则 / 02-发版流程 / 03-资源通道与测速基线`
已归档到项目库 `06-发布与分发/旧GitHub备份-20261106/`，需要查历史口径去那里。

## 客户端怎么取东西

```
启动器 ──读──> res/latest.json ──> assets[kind=shell, id=shell-launcher-*]
                              └──> assets[kind=patch]（内容补丁链）

下载器 ──读──> res/latest.json ──> assets[kind=baseline]  → 136 卷
                              ├──> assets[kind=shell]     → 换壳
                              └──> res/sources.enc        → 解密后覆盖 assets[].sources
```

## 版本号规则

- **客户端**：`1.0.0`（基础包）→ 补丁包递增 `1.0.1`、`1.0.2`…
- **启动器壳 / 下载器壳**：`1.0.0` 起，独立递增，与客户端版本无关
- **release tag**：`v<客户端版本>`，只是容器标签，不等于任何版本号
