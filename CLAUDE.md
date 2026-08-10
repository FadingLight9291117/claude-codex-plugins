# CLAUDE.md

本仓库是个人插件市场,同时服务 Claude Code 与 Codex 两个生态。维护时的注意事项:

## 技能来源

- **hmos 系列技能**(崩溃/冻屏/泄漏分析等)来自华为可靠性技术实验室的 **HarmonyOS DFX Skills**:
  - GitCode: https://gitcode.com/openharmony-sig/developtools_dfx_skills
  - 更新技能内容时以官方仓库为准,注意官方技能名无 `hmos-` 前缀(如 `nativeleak-analysis`),本地统一加了 `hmos-` 前缀。
- **build-ios-apps** 来自 OpenAI plugins 仓库(github.com/openai/plugins),Claude 格式版,本地打包。

## 目录结构与格式

- `.claude-plugin/marketplace.json` — Claude 市场清单
- `.agents/plugins/marketplace.json` — Codex 市场清单
- `plugins/build-ios-apps/` — 仅 Claude 格式(`.claude-plugin/`)
- `plugins/hmos/` — 双格式(`.claude-plugin/` + `.codex-plugin/`)
- 技能内容改动需同步两端市场目录:`~/.claude/marketplaces/hmos/`、`~/.codex/marketplaces/hmos/`

## 大型二进制

- `hmos-jsleak-analysis/scripts/*/heap_cluster*` 为 Git LFS 托管(~423MB),推送前需 `git lfs install`。
- `hmos-native-memleak-analysis/scripts/trace_streamer*` 为普通大文件(13~18MB),勿改成 LFS。

## 已知限制

- `hmos-native-memleak-analysis` 的 scripts/ 曾因 LFS 指针存根损坏,已按官方仓库恢复;若再出现 100 字节指针文件,重新从官方 clone 恢复。
