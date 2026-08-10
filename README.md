# Claude Codex Plugins

个人插件市场仓库,同时服务 **Claude Code** 和 **Codex** 两个生态。

## 包含的插件

| 插件 | 内容 | Claude | Codex |
|---|---|---|---|
| `hmos` | HarmonyOS 开发:ArkTS/ArkUI 开发、多设备适配等 16 个技能 | ✅ | ✅ |
| `hmos-perf` | HarmonyOS 性能/故障分析:卡顿、卡死、内存泄漏、崩溃、API 故障等 8 个技能 | ✅ | ✅ |

> build-ios-apps(iOS 开发)已移至独立仓库:github.com/FadingLight9291117/build-ios-apps

> **hmos-native-memleak-analysis**:scripts/ 原生内存分析工具已按官方版本恢复(2026-08-10)。官方来源:`OpenHarmony-SIG/developtools_dfx_skills`(GitCode)

## 技能来源

本仓库的 hmos 系列技能(崩溃/冻屏/泄漏分析等)源自华为可靠性技术实验室发布的 **HarmonyOS DFX Skills**,官方仓库:

- GitCode: https://gitcode.com/openharmony-sig/developtools_dfx_skills

升级技能内容时建议对照官方仓库。

## 安装

### Claude Code

```bash
claude plugin marketplace add FadingLight9291117/claude-codex-plugins
claude plugin install build-ios-apps
claude plugin install hmos
```

### Codex

```bash
codex plugin marketplace add FadingLight9291117/claude-codex-plugins
codex plugin add hmos
```

## 目录结构

```
├── .claude-plugin/marketplace.json    # Claude 市场清单
├── .agents/plugins/marketplace.json   # Codex 市场清单
└── plugins/
    ├── build-ios-apps/                # Claude 格式(.claude-plugin/)
    └── hmos/                          # 双格式(.claude-plugin/ + .codex-plugin/)
```

## 维护

更新技能内容后,同步到 `plugins/*/skills/` 并提交推送;两端分别执行 `claude plugin marketplace upgrade claude-codex-plugins` / `codex plugin marketplace upgrade claude-codex-plugins` 刷新。
