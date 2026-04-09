# 前端开发行为准则

> 以下规则定义了前端开发中 Claude 应自动遵循的行为模式。

## 约定式提交

在前端项目中进行提交时，使用约定式提交前缀：`feat:`、`fix:`、`style:`、`refactor:`、`perf:`、`test:`、`docs:`、`chore:`。

- 约定式提交使变更日志自动化成为可能
- 清晰的提交分类有助于代码审查和问题追溯

## 组件文件命名

创建新的 React/Vue 组件时：

- 组件文件使用 **PascalCase** 命名（如 `UserProfile.tsx`）
- 自定义 Hooks 使用 **camelCase** 并以 `use` 开头（如 `useAuth.ts`）
- 工具函数使用 **camelCase**（如 `formatDate.ts`）

## TypeScript 严格模式

编写 TypeScript 代码时：

- 始终为组件 Props、API 响应和函数参数定义明确的类型
- 避免使用 `any`，优先使用 `unknown` 或具体类型
- 使用 `import type { ... }` 导入纯类型

## 组件测试

创建或修改组件时：

- 每个组件应有对应的测试文件（`*.test.tsx`）
- 使用 React Testing Library 测试用户行为而非实现细节
- 测试应覆盖：正常渲染、用户交互、边界状态（空、加载、错误）

## API 服务层

进行 API 调用时：

- 所有 API 调用通过 `services/` 层统一管理，不在组件中直接使用 `fetch` 或 `axios`
- 使用 React Query / SWR 等库管理服务端状态的缓存和同步

## 性能意识

实现列表、图片或大量数据展示时：

- 大列表使用虚拟滚动
- 图片使用懒加载
- 路由级组件使用 `React.lazy` + `Suspense` 进行代码分割
- 避免在渲染路径中进行昂贵计算（使用 `useMemo`）

## 可访问性（a11y）

开发交互式 UI 组件时：

- 交互元素必须支持键盘操作
- 使用语义化 HTML 标签
- 为图片添加 `alt` 属性
- 为自定义组件添加适当的 ARIA 属性
- 确保颜色对比度符合 WCAG 标准

## 状态管理策略

决定状态管理方案时：

- 优先使用组件本地状态（`useState`）
- 跨组件共享使用 Context 或轻量级状态库（Zustand）
- 服务端状态使用 React Query / SWR
- 仅在确实需要时才引入全局状态管理
