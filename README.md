# Claude Codex Plugins

**专门收录移动开发相关插件**的插件市场仓库(当前涵盖 HarmonyOS `hmos-*` 与 Android `android-*`),同时服务 **Claude Code** 和 **Codex** 两个生态。所有插件均为双格式(`.claude-plugin/` + `.codex-plugin/`),技能内容完全一致,改动需两端市场同步。非移动类插件不在本仓库收录(如 iOS 的 build-ios-apps 已移至独立仓库)。

## 包含的插件

| 插件 | 内容 | 技能数 |
|---|---|---|
| `hmos-arkts` | HarmonyOS ArkTS 语言:编译错误修复、语法规范、运行时修复、知识检索、语法检查 | 5 |
| `hmos-arkui` | HarmonyOS ArkUI 界面:ArkUI 开发、知识检索、MVVM 架构模式 | 3 |
| `hmos-multidevice` | HarmonyOS 多设备适配:折叠屏、屏幕窗口、避让区、硬件访问、交互方式、自然方向、场景入口 | 7 |
| `hmos-kits` | HarmonyOS Kit 集成:Push Kit 推送服务集成 | 1 |
| `hmos-perf` | HarmonyOS 性能/故障分析:卡顿、卡死、性能分析、JS/ArkTS/native 内存泄漏、fd 泄漏、C++/JS 崩溃、API 故障 | 10 |
| `android-ui` | Android Compose UI:自适应布局、全面屏、Styles、Navigation 3、Compose 迁移、TV/Camera/XR/Wear | 9 |
| `android-tooling` | Android 构建与工具链:CLI 使用、AGP 9 升级、测试策略、R8 混淆分析 | 4 |
| `android-profiler` | Android 性能分析:系统 trace、堆转储、方法采样、卡顿/内存泄漏/启动定位、SQL 调试 | 1 |
| `hmos-testing` | HarmonyOS 测试:Instrument Test、Local Test 运行与覆盖率统计 | 2 |

> hmos 系列技能包 `hmos`(开发)与 `hmos-perf`(分析)原为单体插件,现已按主题拆分为上表的 `hmos-*` 插件;`build-ios-apps`(iOS 开发)已移至独立仓库:github.com/FadingLight9291117/build-ios-apps。

## 技能来源

- **hmos 系列**(崩溃/冻屏/泄漏分析等)源自华为可靠性技术实验室发布的 **HarmonyOS DFX Skills**:
  - GitCode: https://gitcode.com/openharmony-sig/developtools_dfx_skills
  - 官方技能名无 `hmos-` 前缀,本仓库统一加了 `hmos-` 前缀;升级技能内容以官方仓库为准。
- **android 系列**来自 Android CLI 官方 catalog(`android skills add <name> --project <dir>` 安装,2026-09 更新)。

## 安装

### Claude Code

```bash
claude plugin marketplace add FadingLight9291117/claude-codex-plugins
claude plugin install hmos-arkts        # 及 hmos-arkui / hmos-multidevice / hmos-kits / hmos-perf / hmos-testing
claude plugin install android-ui         # 及 android-tooling / android-profiler
```

### Codex

```bash
codex plugin marketplace add FadingLight9291117/claude-codex-plugins
codex plugin add hmos-arkts
codex plugin add android-ui
```

## 目录结构

```
├── .claude-plugin/marketplace.json    # Claude 市场清单
├── .agents/plugins/marketplace.json   # Codex 市场清单(需与 Claude 清单保持同名同源)
└── plugins/
    ├── hmos-arkts/                    # 双格式(.claude-plugin/ + .codex-plugin/)
    ├── hmos-arkui/
    ├── hmos-multidevice/
    ├── hmos-kits/
    ├── hmos-perf/
    ├── android-ui/
    ├── android-tooling/
    ├── android-profiler/
    └── hmos-testing/
```

## 维护

1. 新增/删除插件需同步修改 `.claude-plugin/marketplace.json` 与 `.agents/plugins/marketplace.json`(两清单 schema 不同,但插件 name/source 必须一致)。
2. 技能内容改动后同步到各副本市场目录:`~/.claude/marketplaces/hmos*/` 与 `~/.codex/marketplaces/hmos*/`,并在各插件 `plugin.json` 中递增 `version`。
3. 提交推送后,两端分别执行 `claude plugin marketplace upgrade claude-codex-plugins` / `codex plugin marketplace upgrade claude-codex-plugins` 刷新;如未生效,重装插件(`claude plugin install <name>`)刷新缓存。

> 详细同步流程与大型二进制(LFS)注意事项见仓库根目录 `CLAUDE.md`,以该文件为准。
