# Claude Codex Plugins

个人插件市场仓库,同时服务 **Claude Code** 和 **Codex** 两个生态。

## 包含的插件

| 插件 | 内容 | Claude | Codex |
|---|---|---|---|
| `build-ios-apps` | iOS 开发:App Intents、SwiftUI、性能分析、泄漏排查、模拟器调试 | ✅ | — |
| `hmos` | HarmonyOS 开发:ArkTS/ArkUI、崩溃/内存分析、多设备适配等 23 个技能 | ✅ | ✅ |

> ⚠️ **hmos-native-memleak-analysis 技能说明**:该技能的 `scripts/` 目录(原生内存分析 Python 工具)在原分发版本中为 LFS 指针存根,真实内容不可恢复,已从本仓库移除。SKILL.md 与参考资料完整,但脚本部分暂不可用,待从原始来源恢复。

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
