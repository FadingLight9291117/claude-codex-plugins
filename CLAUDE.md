# CLAUDE.md

本仓库是个人插件市场,同时服务 Claude Code 与 Codex 两个生态。维护时的注意事项:

## 技能来源

- **hmos 系列技能**(崩溃/冻屏/泄漏分析等)来自华为可靠性技术实验室的 **HarmonyOS DFX Skills**:
  - GitCode: https://gitcode.com/openharmony-sig/developtools_dfx_skills
  - 更新技能内容时以官方仓库为准,注意官方技能名无 `hmos-` 前缀(如 `nativeleak-analysis`),本地统一加了 `hmos-` 前缀。
  - 也可用 `devecocli skills add --all --path <dir>` 获取官方分发版(已含 `hmos-` 前缀与 CHANGELOG;devecocli 目录可能滞后于 GitCode,如 apifault/jank,此时以 GitCode 为准)。
- **android 系列技能**来自 Android CLI 官方 catalog(`android skills add <name> --project <dir>` 安装,2026-09 更新)。
- **build-ios-apps** 已移至独立仓库 github.com/FadingLight9291117/build-ios-apps(来源:openai/plugins,MIT)。

## 官方更新同步流程(必做)

官方仓库更新后,按以下步骤同步 hmos 技能:

1. `git clone --depth 1 https://gitcode.com/openharmony-sig/developtools_dfx_skills.git /tmp/dfx_skills_check`(或拉取现有克隆)
2. 对照官方目录(`01-fault-analysis/` 等)与 `plugins/hmos-perf/skills/`,找出更新/新增/删除的技能
3. 同步到各副本,保持完全一致:
   - `~/claude-codex-plugins/plugins/hmos*/skills/`(本仓库,commit + push)
   - `~/.claude/marketplaces/hmos/plugins/hmos/skills/` 与 `~/.claude/marketplaces/hmos-perf/plugins/hmos-perf/skills/`
   - `~/.codex/marketplaces/hmos/plugins/hmos/skills/` 与 `~/.codex/marketplaces/hmos-perf/plugins/hmos-perf/skills/`
   - 插件缓存(重装插件刷新:`claude plugin install hmos` / `claude plugin install hmos-perf`)
4. 同步后校验:`shasum -a 256` 对比关键文件,或直接 diff 目录
5. 官方文件若为 Git LFS 指针(100 字节文本),需在有 git-lfs 的环境 clone 才能拿到真实内容

## 目录结构与格式

- `.claude-plugin/marketplace.json` — Claude 市场清单
- `.agents/plugins/marketplace.json` — Codex 市场清单
- `plugins/hmos-arkts/` — 双格式(`.claude-plugin/` + `.codex-plugin/`),ArkTS 语言技能 5 个
- `plugins/hmos-arkui/` — 双格式,ArkUI 界面开发技能 3 个
- `plugins/hmos-multidevice/` — 双格式,多设备适配技能 7 个
- `plugins/hmos-kits/` — 双格式,Kit 集成技能 1 个(push-kit)
- `plugins/hmos-perf/` — 双格式,性能/故障分析技能 10 个(官方 v1.3.0 含新增 perf-analysis)
- `plugins/android-ui/` — 双格式,Android Compose UI 技能 9 个
- `plugins/android-tooling/` — 双格式,Android 构建与工具链技能 4 个
- `plugins/android-profiler/` — 双格式,Android 性能分析技能 1 个
- `plugins/hmos-testing/` — 双格式,HarmonyOS 测试技能 2 个(instrument-test / local-test)
- 技能内容改动需同步两端市场目录:`~/.claude/marketplaces/hmos/`、`~/.claude/marketplaces/hmos-perf/`、`~/.codex/marketplaces/hmos/`、`~/.codex/marketplaces/hmos-perf/`

## 大型二进制

- `hmos-perf/skills/hmos-jsleak-analysis/` 官方 v1.3.0 已不再附带编译版 `heap_cluster*` 二进制(原 ~423MB LFS,2026-09-03 同步时已删除),改用 `rawheap_translator`。`scripts/node/heap_cluster.js`(普通文件)曾因 `.gitattributes` 的 `scripts/*/heap_cluster*` LFS glob 被误匹配、且本机 `git-lfs clean` 生效而无法正常提交;现已在 `.gitattributes` 显式加 `scripts/node/heap_cluster.js !filter !diff !merge -text` 排除,提交前仍可用 `git lfs ls-files` 确认其未入 LFS。若后续重新引入 heap_cluster 二进制,推送前需 `git lfs install`。
- `hmos-perf/skills/hmos-jank-analysis/scripts/analysis.exe`(132MB)为 Git LFS 托管。
- `hmos-perf/skills/hmos-native-memleak-analysis/scripts/trace_streamer*` 为普通大文件(13~18MB),勿改成 LFS。
- `hmos-perf/skills/hmos-cppcrash-analysis/scripts/{linux,windows,macos}/` 二进制为普通大文件提交(官方为 LFS,本仓库未启用 lfs)。

## 已知限制

- `hmos-native-memleak-analysis` 的 scripts/ 曾因 LFS 指针存根损坏,已按官方仓库恢复;若再出现 100 字节指针文件,重新从官方 clone 恢复。
