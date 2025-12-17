<p align="center">
  <img src="./images/logo.svg" width="600" />
</p>

# md-structure

生成 **清晰、可读的 Markdown 项目目录结构**。

一个小而专注的 CLI 工具，用于将项目文件夹转换为 **规范的 Markdown 结构文档**，适用于 README、项目文档、代码评审以及 AI 上下文输入。

<p align="center">
  <a href="https://www.npmjs.com/package/md-structure">
    <img src="https://img.shields.io/npm/v/md-structure.svg" alt="npm version">
  </a>
  <a href="https://www.npmjs.com/package/md-structure">
    <img src="https://img.shields.io/npm/dm/md-structure.svg" alt="downloads">
  </a>
  <a href="https://github.com/tomatobybike/md-structure/blob/master/LICENSE">
    <img src="https://img.shields.io/github/license/tomatobybike/md-structure.svg" alt="license">
  </a>
  <a href="https://github.com/tomatobybike/md-structure">
    <img src="https://img.shields.io/github/stars/tomatobybike/md-structure.svg?style=social" alt="GitHub stars">
  </a>
  <a href="https://github.com/tomatobybike/md-structure/issues">
    <img src="https://img.shields.io/github/issues/tomatobybike/md-structure.svg" alt="issues">
  </a>
</p>

---

### 简体中文 | [English](./README.md)

---

## ✨ 特性

* ✅ 跨平台支持（Windows / macOS / Linux）
* 📁 生成清晰、易读的 Markdown 目录结构
* 🧾 标准 Markdown 列表格式（适用于 README / 文档）
* 🎯 目录优先排序（文件夹在前）
* 📏 最大目录深度限制（`--depth`）
* 🔍 文件扩展名过滤（`--only`）
* 🚫 目录排除（`--exclude`）
* 🧩 通过标记自动插入 README
* 🧪 仅预览模式（`--dry-run`）
* 🤖 机器可读 JSON 输出（`--json`）
* 🩺 内置 `doctor` 环境自检命令
* ⚡ 零运行时依赖（仅依赖 `commander`）

---

## 📦 安装

```bash
npm i -g md-structure
```

```bash
yarn global add md-structure
```

或无需安装直接使用：

```bash
npx md-structure generate
```

---

## 🚀 使用方式

```bash
md-structure <命令> [选项]
```

---

## 命令说明

### generate

生成 Markdown 目录结构。

```bash
md-structure generate [options]
```

#### 可用选项

| 选项                      | 说明          | 默认值                        |
| ----------------------- | ----------- | -------------------------- |
| `--dry-run`             | 仅预览，不写入文件   | `false`                    |
| `-s, --stdout`          | 输出到 stdout  | `false`                    |
| `-c, --clipboard`       | 复制结果到剪贴板    | `false`                    |
| `-r, --root <dir>`      | 扫描的根目录      | `.`                        |
| `-d, --depth <number>`  | 最大目录深度      | `Infinity`                 |
| `-b, --bullet <symbol>` | Markdown 符号 | `├──`                      |
| `-o, --output <file>`   | 输出文件名       | `STRUCTURE.md`             |
| `--only <exts>`         | 仅包含指定扩展名    | —                          |
| `--exclude <dirs>`      | 排除目录        | —                          |
| `-i, --insert`          | 插入到 README  | `false`                    |
| `--start <marker>`      | README 起始标记 | `<!-- STRUCTURE_START -->` |
| `--end <marker>`        | README 结束标记 | `<!-- STRUCTURE_END -->`   |

---

### doctor

检查运行环境与配置状态。

```bash
md-structure doctor [--json]
```

| 选项       | 说明              |
| -------- | --------------- |
| `--json` | 输出机器可读的 JSON 结果 |

---

### init

交互式项目初始化。

```bash
md-structure init
```

* 引导生成默认配置
* 在项目中创建 `md-structure.config.json`

---

## 🧠 配置文件

你可以通过以下命令生成配置文件：

```bash
md-structure init
```

或手动创建 `md-structure.config.json`：

```json
{
  "root": "src",
  "depth": Infinity,
  "only": [".mjs", ".ts"],
  "exclude": ["node_modules", "dist", "test"],
  "output": "STRUCTURE.md",
  "insert": true,
  "start": "<!-- STRUCTURE_START -->",
  "end": "<!-- STRUCTURE_END -->"
}
```

CLI 参数始终优先生效。

---

## 📌 插入到 README

在 README 中添加标记：

```md
<!-- STRUCTURE_START -->
<!-- STRUCTURE_END -->
```

然后执行：

```bash
md-structure generate --insert
```

---

## 📤 Stdout / JSON 行为说明

* 使用 `--stdout` 时，仅输出到 stdout
* 不会写入任何文件
* `--json` 会自动启用安静模式，适合脚本与 CI

适用于：

* CI 流程
* Shell 脚本
* 编辑器 / Web 工具

---
## 📤 输出到 stdout（推荐）

默认情况下，`md-structure generate` 会将结果写入文件
（例如 `STRUCTURE.md`）。

如果你希望 **仅输出到标准输出（stdout）**，请使用：

```bash
md-structure generate --stdout
```

### 常见使用场景

#### 管道传递给其他命令

```bash
md-structure generate --stdout | pbcopy   # macOS
md-structure generate --stdout | clip     # Windows
md-structure generate --stdout | xclip    # Linux
```

#### 重定向到文件

```bash
md-structure generate --stdout > STRUCTURE.md
```

#### 脚本 / CI 使用

```bash
md-structure generate --stdout --json
```

### 行为说明

-   使用 `--stdout` 时：

    -   ❌ 不会写入任何文件

    -   ❌ 不会执行 README 插入

    -   ✅ 仅输出到 stdout

-   非常适合：

    -   CI 流水线

    -   Shell 脚本

    -   编辑器或 Web 集成

---

## 🧠 为什么 stdout 很重要

`md-structure` 将 **stdout 视为一等输出方式**，这是一个有意的设计选择。

这一设计遵循 **Unix 哲学**：

> *让程序只做好一件事，并且可以彼此协作。*

通过支持 `--stdout`：

-   `md-structure` 具备良好的可组合性

-   输出可以被管道、转换、复制或存储

-   工具不会对你的工作流做任何假设

示例：

```bash
# 直接复制目录结构
md-structure generate --stdout | pbcopy

# 后处理或转换
md-structure generate --stdout | sed 's/src/source/'

# 在脚本中使用
STRUCTURE=$(md-structure generate --stdout)
```

这使得 `md-structure` 非常适合：

-   CI 系统

-   编辑器插件

-   Web 工具

-   AI 辅助工作流

`md-structure` 只负责生成结构 ——
**如何使用，由你决定。**
---

## 📄 License

[MIT](./LICENSE)

---

## 🔍 关键词

<!-- cli, markdown, directory, structure, tree, readme -->
