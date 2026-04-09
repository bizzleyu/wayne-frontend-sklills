---
name: bug-fix
description: 前端 Bug 修复的工作流命令脚手架。
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /bug-fix（Bug 修复）

在前端项目中处理 **Bug 修复**相关工作时使用此工作流。

## 目标

系统化地定位、修复和验证前端 Bug，确保修复不引入新问题。

## 常用文件

- `src/components/**/*.tsx` — 组件代码
- `src/hooks/**/*.ts` — 自定义 Hooks
- `src/services/**/*.ts` — API 服务
- `src/stores/**/*.ts` — 状态管理
- `**/*.test.tsx` / `**/*.test.ts` — 测试文件

## 建议步骤

1. **复现问题**：在开发环境中复现 Bug，记录预期行为和实际行为。
2. **定位根因**：通过 DevTools、日志或断点定位问题代码。
3. **编写失败测试**：先写一个能暴露 Bug 的测试用例。
4. **修复代码**：做最小化修复，避免引入不相关的变更。
5. **验证修复**：确认失败测试变为通过，运行完整测试套件。
6. **回归检查**：检查是否有类似模式的代码需要一并修复。

## 典型提交序列

```
test(auth): add failing test for token refresh race condition
fix(auth): resolve token refresh race condition with mutex lock
test(auth): verify concurrent refresh requests are properly queued
```

## 常见 Bug 类型

- **渲染问题**：组件未更新、闪烁、布局错乱
- **状态问题**：状态不同步、竞态条件、内存泄漏
- **类型问题**：运行时类型错误、null/undefined 访问
- **样式问题**：响应式断点、浏览器兼容性
- **性能问题**：无限重渲染、内存泄漏、卡顿

## 备注

- 修复 Bug 时必须附带测试用例。
- 优先修复根因，而非症状。
- 如果工作流发生实质性变化，请更新此命令。
