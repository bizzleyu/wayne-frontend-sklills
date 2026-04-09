---
name: feature-development
description: 前端功能开发的工作流命令脚手架。
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /feature-development（功能开发）

在前端项目中处理**功能开发**相关工作时使用此工作流。

## 目标

标准前端功能实现工作流，从需求分析到组件实现、测试和文档。

## 常用文件

- `src/components/**/*.tsx` — UI 组件
- `src/pages/**/*.tsx` — 页面组件
- `src/hooks/**/*.ts` — 自定义 Hooks
- `src/services/**/*.ts` — API 服务层
- `src/stores/**/*.ts` — 状态管理
- `src/types/**/*.ts` — 类型定义
- `**/*.test.tsx` / `**/*.test.ts` — 测试文件

## 建议步骤

1. **需求分析**：理解功能需求，确定涉及的组件、页面和数据流。
2. **类型定义**：先定义 TypeScript 接口和类型。
3. **组件实现**：从 UI 组件开始，先静态后交互。
4. **数据集成**：实现 API 调用、状态管理和数据绑定。
5. **测试编写**：为组件和逻辑编写单元测试和集成测试。
6. **验证优化**：运行 lint、类型检查和测试，优化性能和可访问性。
7. **总结变更**：总结变更内容以及仍需审查的部分。

## 典型提交序列

```
feat(types): define UserProfile interface and API response types
feat(services): add user profile API service
feat(hooks): implement useUserProfile data fetching hook
feat(components): create UserProfile component with avatar and info
feat(pages): integrate UserProfile into settings page
test(components): add UserProfile component tests
```

## 备注

- 将此视为脚手架，而非硬编码脚本。
- 优先实现最小可用版本，再迭代完善。
- 如果工作流发生实质性变化，请更新此命令。
