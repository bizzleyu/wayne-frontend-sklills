# 前端开发 Skills 使用说明

> 本文档说明 `.claude/` 目录下所有配置文件的用途和使用场景，专为**前端开发**定制。
> 所有目录均符合 **Claude Code 官方规范**。

---

## 📁 文件结构

```
.claude/
├── commands/                                         # 斜杠命令（/命令名 触发）
│   ├── feature-development.md                        # 功能开发命令
│   ├── component-development.md                      # 组件开发命令
│   ├── bug-fix.md                                    # Bug 修复命令
│   ├── tech-research.md                              # 技术调研命令
│   └── project-planning.md                           # 项目规划命令
├── rules/                                            # 规则（自动加载）
│   ├── frontend-guardrails.md                        # 代码质量护栏 + 技术栈偏好
│   ├── frontend-instincts.md                         # 前端行为准则
│   └── react-typescript.md                           # React + TypeScript 规则
└── skills/                                           # 技能定义
    └── frontend-development/
        └── SKILL.md                                  # 核心前端技能
```

---

## 🔍 各目录详解

### 1. `commands/` — 斜杠命令

Claude Code **原生支持**的命令目录。在 Claude Code 终端中输入 `/命令名` 即可触发对应工作流。

| 命令 | 触发方式 | 用途 |
|------|---------|------|
| 功能开发 | `/feature-development` | 按标准流程开发新功能：需求分析 → 类型定义 → 组件实现 → 测试 |
| 组件开发 | `/component-development` | 创建高质量可复用 UI 组件，含 Props 设计、测试、可访问性 |
| Bug 修复 | `/bug-fix` | 系统化修复 Bug：复现 → 定位 → 失败测试 → 修复 → 验证 |
| 技术调研 | `/tech-research` | 技术选型和框架对比，含调研流程和评估维度 |
| 项目规划 | `/project-planning` | 拆解功能需求，生成结构化开发计划 |

### 2. `rules/` — 自动加载规则

Claude Code **自动加载**此目录下的所有 `.md` 文件。无需手动触发，每次对话都会生效。

| 文件 | 内容 |
|------|------|
| `frontend-guardrails.md` | 技术栈偏好、提交规范、架构规则、安全、性能、可访问性底线 |
| `frontend-instincts.md` | 8 条前端行为准则：提交规范、命名、TS 严格、测试、API 层、性能、a11y、状态管理 |
| `react-typescript.md` | React + TypeScript 编码规则，含文件约定、代码示例、测试规范 |

### 3. `skills/` — 技能定义

Claude Code **原生支持**的技能系统。定义 Claude 在特定领域的完整知识体系。

| 文件 | 内容 |
|------|------|
| `SKILL.md` | 前端开发核心技能：技术栈、提交规范、项目结构、代码风格、组件模式、测试策略、API 集成、性能优化 |

---

## 🚀 快速开始

1. **了解规范**：`rules/` 下的文件会自动生效，Claude 会自动遵循其中的规则
2. **开发功能**：输入 `/feature-development` 开始新功能开发
3. **创建组件**：输入 `/component-development` 创建可复用组件
4. **修复 Bug**：输入 `/bug-fix` 系统化修复问题
5. **技术调研**：输入 `/tech-research` 进行技术选型
6. **项目规划**：输入 `/project-planning` 拆解开发任务

## 🔧 自定义

这些配置基于 **React + TypeScript + Tailwind CSS** 技术栈设计。如需调整：

- **修改技术栈偏好**：编辑 `rules/frontend-guardrails.md` 中的「技术栈偏好」部分
- **修改编码规则**：编辑 `rules/react-typescript.md`
- **添加新命令**：在 `commands/` 下创建新的 `.md` 文件
- **修改技能定义**：编辑 `skills/frontend-development/SKILL.md`
