# 安妮播放器 macOS Lite

> 当前状态：**源码迁移快照，尚未完成构建与发布验收，不代表允许发布。**

## 迁移来源

| 项目 | 记录 |
|---|---|
| 来源仓库 | [Zhou1019-1/AnniePlayer-LXversion](https://github.com/Zhou1019-1/AnniePlayer-LXversion)（Windows 旧仓） |
| 完整基线 SHA | [`8adef6b3c79a5432eeb17fa85e9aa22a5b512005`](https://github.com/Zhou1019-1/AnniePlayer-LXversion/commit/8adef6b3c79a5432eeb17fa85e9aa22a5b512005) |
| 导入日期 | **2026-11-23** |
| 提取方式 | 从上述提交以 `git archive` 只读提取，不使用旧仓当前工作区内容 |
| 导入内容 | 完整 `macos/` 相对目录，以及构建和许可所需的 `THIRDPARTY/` |
| LICENSE | 保留本仓初始 `LICENSE`，未覆盖；其 Git blob 与基线 `LICENSE` 一致 |

历史 tag、Release、Release 资产和 Latest 均留在 [Windows 旧仓 Releases](https://github.com/Zhou1019-1/AnniePlayer-LXversion/releases)，没有迁移到本仓。旧仓 `release-mac` workflow 未复制，本提交也没有新增任何 CI / Release workflow。

## 产品边界

- **本仓只负责 macOS Lite**，Lite 构建必须显式使用 **`-D LITE`**；完整版由 `AnniePlayer-LXversion-macOS` 独立维护并独立发布。
- 完整版与 Lite 两仓在初期均保留同一份完整 `macos/` 源码快照，暂不拆共享代码。快照中包含完整版源码不表示本仓负责完整版产品或发布。
- 两仓后续分别使用独立的 `vX.Y.Z` 版本、Draft、正式 Release 和 Latest，不沿用旧仓的 `mac-v*` / `mac-lite-v*` 发布线。
- 仓库治理、PR 审核和发布约束以治理 PR 合入后的根 `AGENTS.md`、`CONTRIBUTING.md`、`RELEASING.md` 为准；`macos/` 内旧文档中的仓库地址、tag 和自动发布说明仅作历史参考。

## 基线差异与后续工作

**当前人工分发的 macOS Lite 二进制与 Git 源码可能存在基线差异。** 本次导入只建立可审计的源码起点，不证明人工二进制可由该快照复现，不构成发布授权，也不创建 tag、Draft、Release 或 Latest。

numb 必须在后续独立 PR 中核对并补齐与当前人工二进制对应的：

1. 完整源码及来源基线；
2. 可复现构建脚本与包含 `-D LITE` 的构建说明；
3. 外部依赖的官方 URL、版本及 SHA256；
4. 构建、测试证据和仍未解决的差异。

在上述材料完成审核前不得发布。本提交未实现或修复任何 macOS 功能，也未进行 macOS 构建或功能验收。
