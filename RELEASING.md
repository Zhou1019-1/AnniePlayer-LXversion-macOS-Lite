# 发布治理

## 当前状态

本仓处于源码迁移与治理建设阶段，当前没有 CI 或 Release workflow。导入源码、上传构建 artifacts 或存在人工二进制，都不代表允许发布。贡献者与 AI 不得自行创建 tag 或 Release。

## 职责和独立版本线

- 贡献者（含 numb 与 AI）负责源码、可复现构建材料、测试和交付信息。
- 章鱼负责审核、发布治理、Environment 审批控制和最终发布；最终 **Publish 只能由仓库 owner 执行**。
- 本仓只发布使用 **`-D LITE`** 构建的 macOS Lite，使用独立 `vX.Y.Z` 版本和 tag。完整版仓只发布完整版，也独立使用 `vX.Y.Z`；两仓 Latest 互不共享，不与 Windows 旧仓混用。

## 后续发布 workflow 的强制设计

1. **PR CI**：仅构建、测试和上传 workflow artifacts；禁止 tag、Release 上传、Publish 和 Latest 变更。
2. **发布准备**：通过已审核 PR 锁定版本、完整 commit SHA、依赖 URL / SHA256、包含 `-D LITE` 的构建脚本、测试证据和 Draft notes。
3. **人工审批**：发布 workflow 必须由受保护的 **Environment 人工审批**后才能使用发布凭据或写 Release。审批不是最终 Publish。
4. **仅 Draft**：自动发布步骤只能创建或更新 Draft Release 并上传候选资产，不得自动 Publish，不得自动设置 Latest。
5. **owner 发布**：owner 核对下述清单后，最终手动 Publish，并决定是否将正式 Release 设为 Latest。

任何 workflow 若会直接 Publish、绕过 Environment 或让 PR CI 写 Release，均不得合入。

## 发布前核对清单

- [ ] 产品确为使用 `-D LITE` 构建的 macOS Lite，版本为独立 `vX.Y.Z`，不与完整版或 Windows 线冲突。
- [ ] 源码 commit 已审核合入，人工二进制与 Git 源码的基线差异已经说明并解决。
- [ ] numb 已通过后续 PR 核对并补齐对应源码、构建脚本和依赖 URL。
- [ ] 构建可复现，目标系统与架构、`-D LITE` 开关和测试结果已记录。
- [ ] 所有外部依赖具有官方来源 URL、版本和 SHA256，无私钥、Token、密码或 >50 MiB 新二进制入库。
- [ ] 候选产物名称、大小和 SHA256 已核对，Draft notes 包含已知问题和回退方式。
- [ ] 已经人工 Environment 审批，自动步骤仍只产生 Draft。
- [ ] 仓库 owner 完成最终复核并亲自 Publish / 设置 Latest。

## 标准发布交付

发布请求和 Draft 交接必须使用 `CONTRIBUTING.md` 的「标准交付模板」，并附 Draft URL、Environment 审批记录、候选资产 SHA256 和最终核对结果。主要协同渠道为 **QQ 群 `1023637098`**；审批记录以 GitHub 为准，QQ 沟通不能替代审批。
