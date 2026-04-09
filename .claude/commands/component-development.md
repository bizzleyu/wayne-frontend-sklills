---
name: component-development
description: 前端组件开发的工作流命令脚手架。
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /component-development（组件开发）

在前端项目中处理**可复用组件开发**相关工作时使用此工作流。

## 目标

创建高质量、可复用、可测试的 UI 组件，遵循组件设计最佳实践。

## 常用文件

- `src/components/**/*.tsx` — 组件实现
- `src/components/**/*.test.tsx` — 组件测试
- `src/components/**/*.module.css` — 组件样式（CSS Modules）
- `src/components/**/*.stories.tsx` — Storybook stories（如有）
- `src/types/**/*.ts` — 相关类型定义

## 建议步骤

1. **确定组件职责**：明确组件的功能边界，是基础 UI 组件还是业务组件。
2. **定义 Props 接口**：设计清晰的 Props 类型，包含必选和可选属性、默认值。
3. **实现组件 UI**：先实现静态渲染，确保视觉正确。
4. **添加交互逻辑**：事件处理、状态管理、副作用。
5. **处理边界情况**：空状态、加载状态、错误状态、长文本溢出等。
6. **编写测试**：渲染测试、交互测试、边界情况测试。
7. **可访问性检查**：确保键盘导航、ARIA 属性、屏幕阅读器兼容。

## 组件模板

```tsx
import { type ReactNode } from 'react'

interface ComponentNameProps {
  /** 必选属性说明 */
  requiredProp: string
  /** 可选属性说明 */
  optionalProp?: boolean
  /** 子元素 */
  children?: ReactNode
  /** 事件回调 */
  onChange?: (value: string) => void
}

export function ComponentName({
  requiredProp,
  optionalProp = false,
  children,
  onChange,
}: ComponentNameProps) {
  return (
    <div role="region" aria-label={requiredProp}>
      {children}
    </div>
  )
}
```

## 典型提交序列

```
feat(components): define Button props interface and variants
feat(components): implement Button component with size and color variants
style(components): add Button styles with hover and focus states
test(components): add Button rendering and interaction tests
docs(components): add Button usage examples to Storybook
```

## 备注

- 组件应遵循单一职责原则。
- 优先使用组合（composition）而非继承。
- 确保组件在受控和非受控模式下都能正常工作。
- 如果工作流发生实质性变化，请更新此命令。
