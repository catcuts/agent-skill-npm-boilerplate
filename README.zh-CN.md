# Agent Skill NPM Boilerplate

[English](./README.md) | 中文

> **像发布 npm 包一样分发 AI Agent 技能**

AI 编程工具（Claude Code、Cursor、Windsurf）支持自定义"技能"（Skills）—— 可复用的指令，用于扩展 Agent 的能力。但手动分发技能意味着复制文件、没有版本控制、更新困难。

**本模板让你可以将技能发布到 npm：**

```bash
# 安装
npm install -g @your-org/your-skill

# 更新
npm update -g @your-org/your-skill

# 自动安装到 ~/.claude/skills/ 等
```

**为什么这很重要**：技能成为标准的软件构件，拥有语义化版本控制、依赖管理、私有仓库和全局发现能力。使用与 React 和 Express 相同的基础设施。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

**快速开始**：Fork 本模板，编辑 `SKILL.md`，运行 `npm publish`。你的技能现在可以全球安装了。

**支持平台**: 基于 [Vercel 开源的 skills 管理工具](https://github.com/vercel-labs/skills)，使用本模板创建的技能支持 Opencode、Claude Code、Codex、Cursor 及其他 [23 个工具](https://github.com/vercel-labs/add-skill?tab=readme-ov-file#supported-agents)。详见：`scripts` 代码。

## 💡 为什么用 npm 管理技能？

有多种方式可以分发 AI Agent 技能。让我们来比较一下：

### 1. 手动复制文件（❌ 不推荐）

```bash
# 下载文件
git clone https://github.com/user/skills

# 手动复制到 skills 目录
cp -r skills/my-skill ~/.claude/skills/

# 每次更新都要重复这些步骤
```

**问题**：
- 没有版本控制
- 没有依赖管理
- 需要手动更新
- 没有发现机制
- 容易出错

### 2. 命令行安装工具（✅ 适合 Git 仓库）

社区中流行的三种工具：

#### A. `npx skills`（Vercel 管理器）

```bash
# 安装 skills 包（管理层）
npm i -g skills

# 从 git 仓库安装
npx skills i vercel-labs/agent-skills
```

**[Skills](https://www.npmjs.com/package/skills)** 是 Vercel 的技能管理工具，封装了 [`add-skill`](https://github.com/vercel-labs/add-skill) 并提供额外功能。

#### B. `npx add-skill`（Vercel 核心工具）

```bash
# 直接从 git 仓库安装
npx add-skill vercel-labs/agent-skills

# 安装特定技能
npx add-skill vercel-labs/agent-skills --skill frontend-design

# 安装到特定工具
npx add-skill vercel-labs/agent-skills -a claude-code -a cursor
```

**[skills](https://github.com/vercel-labs/skills)** 是 Vercel 的底层安装工具。

#### C. `npx openskills`（社区替代方案）

```bash
# 全局安装 openskills
npm i -g openskills

# 安装技能
openskills install anthropics/skills --global
```

**[OpenSkills](https://www.npmjs.com/package/openskills)** 是社区开发的通用技能安装工具。

**命令行工具的优势**：
- ✅ 基于 Git 的分发
- ✅ 支持 23+ 种 AI 编程工具
- ✅ 无需配置
- ✅ 工具无关的生态系统
- ✅ 从任意 git 仓库快速安装

**局限**：
- ⚠️ 没有语义化版本（使用 git 提交）
- ⚠️ 没有自动依赖管理
- ⚠️ 没有中心化注册表/发现机制
- ⚠️ 需要 git 仓库访问权限

### 3. npm 包（✅ 发布技能的最佳选择）

```bash
# 使用标准命令安装/更新/卸载
npm install -g @your-org/skill-name
npm update -g @your-org/skill-name
npm uninstall -g @your-org/skill-name

# 语义化版本控制
npm install @your-org/skill@^2.1.0

# 项目级技能（版本锁定，提交到 git）
npm install --save-dev @your-org/skill-name
```

**核心优势**：
- ✅ **版本控制** - 语义化版本，轻松升级/回滚
- ✅ **全球分发** - 发布一次，通过 npm CDN 全球可用
- ✅ **可发现性** - 在 npmjs.com 上可搜索
- ✅ **企业级** - 支持私有仓库用于内部技能
- ✅ **生态集成** - 与 CI/CD、monorepos、现有工具集成
- ✅ **依赖管理** - 自动依赖解析
- ✅ **生命周期钩子** - 自动安装/卸载脚本

### 应该选择哪种方式？

**使用 npm 包，当你**：
- 希望发布稳定的、有版本控制的技能
- 需要依赖管理
- 想要全球可发现性
- 为企业/团队构建

**使用命令行工具，当你**：
- 本地开发技能
- 从 git 仓库测试技能
- 分发内部/团队技能
- 不需要版本控制

**工具推荐**：
- **大多数用户**：使用 `npx skills`（最简单，功能最丰富）
- **开发者**：使用 `npx add-skill`（更多控制，直接访问）
- **替代方案**：使用 `npx openskills`（社区驱动，通用性强）

**两全其美**：
本模板结合了两种方式！使用本模板创建的技能：
- ✅ 可以发布到 npm 进行版本化分发
- ✅ 也可以通过命令行工具从 git 仓库安装
- ✅ 内部使用 `add-skill` 进行自动安装

**示例工作流**：
```bash
# 开发阶段：使用命令行工具测试
npx skills i github.com/your-org/your-skill

# 生产环境：使用 npm 发布稳定版本
npm install -g @your-org/your-skill

# 更新：使用 npm 进行版本控制
npm update -g @your-org/your-skill
```

技能成为一流的软件构件，使用与 React、Express 等数百万包相同的基础设施。

## ✨ 特性

- ✅ **官方规范**：完全符合 Claude Code 技能格式规范
- ✅ **智能安装**：自动检测全局 vs 项目级安装
- ✅ **渐进式披露**：支持主 SKILL.md + 参考文件
- ✅ **生命周期管理**：包含安装、更新、卸载脚本
- ✅ **最佳实践**：遵循官方文档的所有推荐模式
- ✅ **发布就绪**：只需自定义并发布到 npm

## 🚀 快速开始

### 方式一：作为 GitHub 模板使用（推荐）

这是最简单的方式：

1. **点击"Use this template"按钮**（在本仓库顶部）
2. **命名你的新仓库**（如 `my-awesome-skill`）
3. **克隆你的新仓库**：
   ```bash
   git clone https://github.com/YOUR-USERNAME/my-awesome-skill.git
   cd my-awesome-skill
   ```
4. **自定义你的技能**（见[自定义指南](#-自定义指南)）
5. **发布到 npm**：
   ```bash
   npm login
   npm publish --access public
   ```

### 方式二：直接克隆

```bash
# 克隆本仓库
git clone https://github.com/YOUR-USERNAME/agent-skill-npm-boilerplate.git my-skill
cd my-skill

# 删除 git 历史并重新初始化
rm -rf .git
git init

# 安装依赖（开发用）
npm install

# 自定义你的技能
```

## 📁 项目结构

```
agent-skill-npm-boilerplate/
├── package.json                # npm 包配置
├── SKILL.md                   # 技能定义（必需）
├── scripts/                   # 工具脚本
│   ├── install-skill.js      # 安装脚本
│   └── uninstall-skill.js    # 卸载脚本
├── README.md                  # 本文件（为你的技能自定义）
├── LICENSE                    # 许可证文件
└── .gitignore                 # Git 忽略规则
```

## 🎨 自定义指南

### 步骤 1：更新 package.json

替换以下占位符：

```json
{
  "name": "@YOUR-ORG/YOUR-SKILL-NAME",        // 修改这个
  "version": "1.0.0",
  "description": "YOUR SKILL DESCRIPTION",     // 修改这个
  "author": "YOUR NAME",                       // 修改这个
  "repository": {
    "url": "YOUR-REPO-URL"                     // 修改这个
  }
}
```

**关于 npm scope**：
- 如果想在组织下管理技能，使用 scope（`@your-org/skill-name`）
- 如果是独立包，不使用 scope（`skill-name`）
- 常见的 scope：`@your-company`、`@your-username` 或自定义如 `@claude-skills`

### 步骤 2：更新 SKILL.md

编辑 `SKILL.md` 并替换占位符：

```yaml
---
name: your-skill-name              # 必须与目录名匹配
description: Your skill description here. Use when [scenarios].
allowed-tools: Read, Bash          # 你的技能可以使用的工具
---
```

**重要提示**：
- `description` 字段至关重要 —— 它决定了 Claude 何时使用你的技能
- 包含用户自然会说的关键词
- 说明具体的使用场景

❌ **不好的描述**：
```yaml
description: Helps with files
```

✅ **好的描述**：
```yaml
description: Analyzes TypeScript files for type errors. Use when checking types, debugging TypeScript issues, or validating .ts files.
```

### 步骤 3：编写任务指令

编辑 `SKILL.md` 的"任务指令"部分：

```markdown
## 任务指令

When the user [describes scenario]:

1. **First Step**: Do something
   - Additional details
   - Use bash, read files, etc.

2. **Second Step**: Do something else
   - How to process information
   - What to look for

3. **Final Step**: Complete the task
   - What output to provide
```

### 步骤 4：添加示例

在 `SKILL.md` 中添加具体的使用示例：

```markdown
## Examples

### Example 1: Basic Usage

**User asks**: "Check my commit message"

**What the skill does**:
1. Read the commit message
2. Validate format
3. Suggest improvements
```

### 步骤 5：本地测试

```bash
# 测试安装脚本
npm test

# 实际安装（项目级）
npm run install:local

# 检查是否正确安装
ls .claude/skills/YOUR-SKILL-NAME/SKILL.md
cat .claude/skills/YOUR-SKILL-NAME/SKILL.md

# 在 Claude Code 中验证
# 询问 Claude："What skills are available?"
```

### 步骤 6：发布到 npm

```bash
# 登录 npm（仅首次）
npm login

# 发布你的技能
npm publish --access public
```

## 📖 技能开发最佳实践

### 1. 编写清晰的描述

`SKILL.md` 中的 `description` 字段至关重要 —— 它决定了 Claude 何时使用你的技能：

```yaml
# ❌ 不好：太模糊
description: Helps with files

# ✅ 好：具体并包含触发关键词
description: Analyzes TypeScript files for type errors. Use when checking types, debugging TypeScript issues, or validating .ts files.
```

### 2. 使用渐进式披露

保持 SKILL.md 在 500 行以内。将详细内容放在单独的文件中：

```markdown
# 在 SKILL.md 中
For complete API reference, see [reference.md](reference.md)
For examples, see [examples.md](examples.md)
```

Claude 只在需要时加载这些文件，节省上下文。

### 3. 限制工具访问

使用 `allowed-tools` 限制你的技能可以做什么：

```yaml
# 只读技能
allowed-tools: Read, Grep, Glob

# 可以读取和执行（但不能修改文件）
allowed-tools: Read, Bash

# 完全访问
allowed-tools: Read, Edit, Write, Bash
```

### 4. 包含示例

在 SKILL.md 中展示具体示例：

```markdown
## Examples

### Example 1: Basic Usage

User asks: "Check my commit message"

Claude will:
1. Read the commit message
2. Validate format
3. Suggest improvements
```

## 📦 安装行为

### 全局安装（推荐）

```bash
npm install -g @your-org/your-skill
```

安装到：`~/.claude/skills/your-skill-name/`

可用范围：当前用户的所有项目

### 项目级安装

```bash
npm install --save-dev @your-org/your-skill
```

安装到：`.claude/skills/your-skill-name/`

可用范围：仅当前项目（可以提交到 git）

### 优先级顺序

当存在多个技能时：
1. 企业级（托管设置）
2. 个人级（`~/.claude/skills/`）
3. 项目级（`.claude/skills/`）
4. 插件

## 🔧 高级特性

### 多文件支持

支持丰富的文档结构：

```
your-skill/
├── SKILL.md           # 主技能定义（必需）
├── reference.md       # 详细参考文档
├── examples.md        # 使用示例
└── scripts/
    ├── setup.sh      # 安装后设置
    └── config.json   # 配置文件
```

### 配置

让用户自定义你的技能：

```bash
# scripts/setup.sh
cat > scripts/config.json <<EOF
{
  "option1": "default",
  "option2": true
}
EOF
```

## 🐛 故障排查

### 技能未出现

```bash
# 检查安装位置
ls -la ~/.claude/skills/

# 验证 SKILL.md 格式
cat ~/.claude/skills/your-skill/SKILL.md

# 检查 manifest
cat ~/.claude/skills/.skills-manifest.json
```

### 权限错误

```bash
# 修复 npm 权限（推荐）
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
export PATH=~/.npm-global/bin:$PATH

# 或使用 sudo（不推荐）
sudo npm install -g @your-org/your-skill
```

### 技能未触发

- 确保 `description` 包含用户自然会说到的关键词
- 直接测试：询问 Claude "Use the your-skill-name skill to..."

## 📚 资源

- [Claude Code 技能文档](https://code.claude.com/docs/en/skills)
- [技能最佳实践](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/best-practices)
- [npm 包发布指南](https://docs.npmjs.com/packages-and-modules/contributing-packages-to-the-registry)
- [语义化版本](https://semver.org/lang/zh-CN/)
- [Conventional Commits](https://www.conventionalcommits.org/zh-hans/)

## 🤝 贡献

欢迎贡献！请：

1. Fork 本仓库
2. 创建功能分支
3. 进行更改
4. 提交 Pull Request

## 📄 许可证

本模板采用 [MIT 许可证](LICENSE)。基于此模板创建的技能可以使用你选择的任何许可证。

## 💡 示例

使用本模板构建的技能：

- `@your-org/your-skill` - 生成符合规范的提交信息
- `@your-org/code-reviewer` - 自动代码审查辅助
- `@your-org/test-generator` - 从代码生成测试用例

*（发布后在这里添加你的技能！）*

## 🙋 获取帮助

- **问题**：[GitHub Issues](https://github.com/YOUR-USERNAME/agent-skill-npm-boilerplate/issues)
- **讨论**：[GitHub Discussions](https://github.com/YOUR-USERNAME/agent-skill-npm-boilerplate/discussions)
- **文档**：[Wiki](https://github.com/YOUR-USERNAME/agent-skill-npm-boilerplate/wiki)

## 🌟 支持本项目

如果你觉得本模板有帮助：
- ⭐ 点赞本仓库
- 🐛 报告 bug
- 💡 建议新功能
- 📝 改进文档

---

**使用 ❤️ 为 Claude Code 社区制作**
