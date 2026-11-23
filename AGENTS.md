# 安妮播放器 macOS Lite · AI 协作与仓库治理

本文件适用于整个仓库，包括后续导入的 `macos/` 快照。快照内旧文档如仍提及 Windows 仓、`mac-v*` / `mac-lite-v*` tag、自动发布或 prerelease，均为历史资料；与本文件、`RELEASING.md` 冲突时，以本仓库当前治理规则为准。

## 1. 产品边界与职责

- 本仓只负责 **安妮播放器 macOS Lite**，构建必须使用 **`-D LITE`**；完整版产品由独立仓库负责。
- 贡献者（包括 numb、其他开发者及任何 AI 助手）负责开发、复现、测试和提交交付材料。
- 章鱼（仓库 owner）负责审核、治理和发布；CODEOWNERS 按仓库配置参与审核。导入源码不等于完成验收，也不构成发布许可。
- 主要联系渠道：**QQ 群 `1023637098`**。需要交付、构建或发布协同时，在群内联系章鱼；安全问题和凭据细节必须改为私聊，不得在群内或 Issue 公开。

## 2. 人类与 AI 的统一流程

1. 从最新 `main` 创建主题分支，在 PR 中说明范围、验证结果和已知缺口。
2. **所有人和 AI 都必须走 PR，不得直接推送 `main`，不得绕过审核合并自己的改动。**
3. 贡献者与 AI 不得自行创建或推送 tag，不得自行创建、更新、发布或删除 Release，也不得修改仓库设置。
4. 提交前至少执行 `git diff --check`，并运行与改动相关的可用测试；无法执行的验证必须在 PR 中明确说明。
5. 所有开发、二进制和发布交付均填写 `CONTRIBUTING.md` 的「标准交付模板」；发布另须遵守 `RELEASING.md`。

## 3. CI 与发布边界

- 当前仓库未配置 CI 或 Release workflow，不得把源码导入解释为允许发布。
- 后续新增 **PR CI 只能构建、测试并上传 workflow artifacts**；不得创建 tag、Release，不得上传 Release 资产，不得发布或改动 Latest。
- 发布必须使用独立且受控的流程，并经过**人工 Environment 审批**。自动步骤只能创建或更新 **Draft Release**，不得自动 Publish。
- Draft 中的版本、源码 commit、依赖来源、安装包和 SHA256 经复核后，由**仓库 owner 最终手动 Publish**。贡献者和 AI 不得代替 owner 执行最终发布。

## 4. 版本与 Latest

- Lite 与完整版各自独立维护语义化版本和 `vX.Y.Z` tag，不沿用旧仓的 `mac-v*` / `mac-lite-v*` 规则，也不要求与 Windows 版同步。
- 本仓的版本、Release 和 Latest 只对应使用 `-D LITE` 构建的 macOS Lite；完整版仓的版本、Release 和 Latest 只对应完整版。
- Draft、CI artifacts 和历史迁移材料均不得成为 Latest；仅 owner 发布的正式 Release 可由 owner 设置为 Latest。

## 5. 安全与二进制

- 私钥、证书、Token、密码、公证凭据、用户数据及含凭据的配置一律禁止入库；必要凭据只能使用受控的 GitHub Secrets / Environment。
- 安装包、虚拟机镜像及任何 **>90 MiB（94,371,840 字节）** 的二进制禁止新增入库，分发使用 Release 资产并记录官方来源 URL 与 SHA256。
- 发现秘密或超大文件时立即停止相关导入/提交，不要复述秘密内容；按 `SECURITY.md` 联系 owner。

## 6. 导入快照的特别约束

- 初期两仓均保留完整 `macos/` 源码快照，不拆共享代码；这不改变各仓的产品边界，本仓仍只构建和发布 `-D LITE` 产品。
- 不得复制旧仓 `release-mac` workflow，不得实现或修复 macOS 功能来“顺手完成导入”。
- 当前人工分发的二进制与 Git 源码可能存在基线差异。numb 必须通过后续 PR 核对并补齐对应源码、构建脚本和依赖 URL，完成审核前不得发布。
