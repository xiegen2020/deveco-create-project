# DevEco Create Project

> 面向 HarmonyOS / OpenHarmony 开发的 AI 编程技能包 —— ArkTS 项目脚手架

通过内置脚本一键创建标准 ArkTS 工程，自动处理模板复制、占位符替换、API Level 检测和开发包路径验证。适用于 Claude Code、DevEco Code 等支持技能脚本执行的 AI 编程工具。

## 功能特性

- 使用 Node.js 脚本自动创建完整的 ArkTS 项目，无需手动复制模板
- 自动从 `DEVECO_HOME/sdk/default/sdk-pkg.json` 检测 API Level
- 支持自定义 `projectPath`、`appName`、`bundleName`、`apiLevel`
- 中文项目名自动转换为 UpperCamelCase ASCII 候选项
- 项目目录冲突检测与交互确认
- 创建后自动切换会话上下文到新生成的项目

## 参数说明

| 参数 | 必填 | 默认值 | 示例 |
|------|------|--------|------|
| `projectPath` | 是 | — | `D:\projects` |
| `appName` | 是 | — | `HelloWorld`（必须匹配 `^[A-Za-z][A-Za-z0-9_]{0,127}$`） |
| `bundleName` | 自动派生 | `com.example.{appName小写}` | `com.example.helloworld` |
| `apiLevel` | 可选 | 自动检测 | `21` |

## 使用示例

在 Claude Code 或 DevEco Code 中直接描述需求即可触发：

```
帮我创建一个叫 ShoppingCart 的鸿蒙项目，放在 D:\projects 下
```

技能脚本会自动执行：

```bash
node "{SKILL_DIR}/scripts/copy-template.mjs" \
  --project-path "D:\projects" \
  --app-name "ShoppingCart" \
  --bundle-name "com.example.shoppingcart"
```

## 安装

### Claude Code / DevEco Code

```bash
npx skills add xiegen2020/deveco-create-project
```

或手动复制到技能目录：

```bash
# Claude Code
cp -r deveco-create-project ~/.claude/skills/

# DevEco Code
cp -r deveco-create-project ~/.config/deveco/skills/
```

> **注意**：本技能依赖 Node.js 运行时和 `DEVECO_HOME` 环境变量（指向 DevEco Studio 安装目录）。

## 目录结构

```
deveco-create-project/
├── SKILL.md                    # 技能主文件（AI 工具自动加载）
├── README.md
├── application/                # ArkTS 项目模板
│   ├── AppScope/
│   │   └── app.json5
│   ├── entry/
│   │   ├── src/main/
│   │   │   ├── ets/
│   │   │   │   ├── entryability/EntryAbility.ets
│   │   │   │   ├── entrybackupability/EntryBackupAbility.ets
│   │   │   │   └── pages/Index.ets
│   │   │   ├── resources/
│   │   │   ├── module.json5
│   │   │   └── ...
│   │   ├── build-profile.json5
│   │   └── oh-package.json5
│   ├── build-profile.json5
│   ├── hvigorfile.ts
│   └── oh-package.json5
└── scripts/
    ├── copy-template.mjs       # 项目创建脚本（可执行）
    ├── copy-template.ts        # 脚本源码
    ├── detect-sdk.mjs          # SDK 检测脚本（可执行）
    └── detect-sdk.ts           # 脚本源码
```

## 来源

本技能提取自 [DevEco Code](https://gitcode.com/openharmony-sig/deveco-code) 开源项目（MIT 协议），由华为官方内置的 HarmonyOS 开发技能包。

## 相关技能

- [arkts-error-fixes](https://github.com/xiegen2020/arkts-error-fixes) — 编译错误修复
- [arkts-grammar-standards](https://github.com/xiegen2020/arkts-grammar-standards) — ArkTS 语法规范
- [arkts-runtime-fix](https://github.com/xiegen2020/arkts-runtime-fix) — 运行时崩溃诊断
- [arkui-knowledge](https://github.com/xiegen2020/arkui-knowledge) — ArkUI 组件知识库

## License

MIT
