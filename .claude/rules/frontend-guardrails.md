# 前端开发护栏

前端项目的代码质量和安全护栏规则。

## 技术栈偏好

- **主要语言**：TypeScript
- **UI 框架**：React
- **包管理器** pnpm
 **组件库** 如果是pc端就用antd 如果是移动端则推荐技术栈

## 提交工作流

- 使用约定式提交消息，前缀如 `feat`、`fix`、`style`、`refactor`、`perf`、`test`、`docs`。
- 提交前运行 `lint`、`type-check` 和 `test`。
- PR 必须通过 CI 检查后才能合并。

## 架构

- 组件按功能模块组织，而非按文件类型。
- 共享逻辑提取为自定义 Hooks，放在 `hooks/` 目录。
- API 调用统一通过 `services/` 层，不在组件中直接调用。
- 全局状态最小化，优先使用组件本地状态和 Context。

## 代码风格

- 组件文件使用 PascalCase，工具函数使用 camelCase。
- 使用路径别名（`@/`）进行导入，同模块内使用相对路径。
- 组件使用命名导出，页面组件使用默认导出。
- 所有 Props 必须有 TypeScript 类型定义。

## TypeScript

- 启用严格模式（`strict: true`）。
- 禁止使用 `any` 类型，使用 `unknown` 或具体类型替代。
- 使用 `import type` 导入纯类型。
- API 响应必须有完整的类型定义。

## 安全

- 不在前端代码中硬编码 API 密钥或敏感信息。
- 使用环境变量管理配置（`.env` 文件不提交到版本控制）。
- 对用户输入进行验证和清理，防止 XSS 攻击。
- 使用 CSP（Content Security Policy）头部。

## 性能

- 路由级组件使用代码分割（`React.lazy`）。
- 图片使用懒加载和适当的格式（WebP/AVIF）。
- 避免不必要的重渲染（`React.memo`、`useMemo`、`useCallback`）。
- 监控 Core Web Vitals（LCP、FID、CLS）。

## 可访问性

- 使用语义化 HTML 标签。
- 交互元素支持键盘操作。
- 颜色对比度符合 WCAG AA 标准。
- 表单元素有关联的 label。

## 审查提醒

- 当项目技术栈发生变化时，更新此护栏文件。
- 定期审查并更新安全相关规则。
