---
name: frontend-development-conventions
description: 前端开发约定和模式。基于 TypeScript + React 技术栈的现代前端项目。
---

# 前端开发约定

> 适用于现代前端项目的 Claude Code 技能

## 概述

此技能教会 Claude 前端开发中使用的开发模式和约定，涵盖 React/Vue 组件开发、TypeScript 类型系统、样式方案、状态管理、API 集成和性能优化等核心领域。

## 技术栈

- **主要语言**：TypeScript
- **UI 框架**：React（也适用于 Vue、Svelte 等）
- **构建工具**：Vite / Next.js / Webpack
- **样式方案**：Tailwind CSS / CSS Modules / Styled Components
- **状态管理**：Zustand / Redux Toolkit / Pinia
- **测试框架**：Vitest / Jest + React Testing Library
- **包管理器**：pnpm / bun / npm

## 何时使用此技能

在以下情况下激活此技能：
- 开发 React/Vue/Svelte 组件
- 编写 TypeScript 类型定义
- 实现页面路由和布局
- 处理 API 集成和数据获取
- 编写前端单元测试和集成测试
- 优化前端性能（懒加载、代码分割等）
- 处理样式和响应式设计

## 提交约定

### 提交风格：约定式提交

### 使用的前缀

- `feat` — 新功能
- `fix` — 修复 Bug
- `style` — 样式调整（不影响逻辑）
- `refactor` — 代码重构
- `perf` — 性能优化
- `test` — 测试相关
- `docs` — 文档更新
- `chore` — 构建/工具链变更

### 消息指南

- 平均消息长度：约 65 个字符
- 保持首行简洁且具描述性
- 使用祈使语气（"Add feature" 而非 "Added feature"）

*提交消息示例*

```text
feat(components): add DatePicker component with range selection
```

```text
fix(auth): resolve token refresh race condition
```

```text
style(layout): adjust sidebar responsive breakpoints
```

```text
perf(images): implement lazy loading for product gallery
```

```text
refactor(hooks): extract useDebounce from search component
```

## 架构

### 项目结构

```
src/
├── components/          # 可复用 UI 组件
│   ├── ui/              # 基础 UI 组件（Button, Input, Modal...）
│   └── business/        # 业务组件
├── pages/               # 页面组件（路由级别）
│   └── [page]/
│       ├── index.tsx     # 页面入口
│       ├── components/   # 页面私有组件
│       └── hooks/        # 页面私有 hooks
├── hooks/               # 全局自定义 Hooks
├── stores/              # 状态管理
├── services/            # API 服务层
├── utils/               # 工具函数
├── types/               # 全局类型定义
├── styles/              # 全局样式
├── assets/              # 静态资源
└── constants/           # 常量定义
```

### 指南

- 组件按功能模块组织，而非按文件类型
- 页面私有组件放在页面目录下，而非全局 components
- 共享逻辑提取为自定义 Hooks
- API 调用统一通过 services 层

## 代码风格

### 语言：TypeScript

### 命名约定

| 元素 | 约定 | 示例 |
|------|------|------|
| 组件文件 | PascalCase | `UserProfile.tsx` |
| Hook 文件 | camelCase（use 前缀） | `useAuth.ts` |
| 工具函数文件 | camelCase | `formatDate.ts` |
| 样式文件 | 与组件同名 | `UserProfile.module.css` |
| 类型文件 | camelCase | `user.types.ts` |
| 常量 | SCREAMING_SNAKE_CASE | `MAX_RETRY_COUNT` |
| 组件名 | PascalCase | `UserProfile` |
| 函数/变量 | camelCase | `getUserInfo` |
| 接口/类型 | PascalCase（I 前缀可选） | `UserInfo` / `IUserInfo` |
| 枚举 | PascalCase | `UserRole` |

### 导入风格

```typescript
// 1. 第三方库
import React, { useState, useEffect } from 'react'
import { useQuery } from '@tanstack/react-query'

// 2. 内部别名路径
import { Button } from '@/components/ui/Button'
import { useAuth } from '@/hooks/useAuth'

// 3. 相对路径（同模块内）
import { UserAvatar } from './UserAvatar'
import { formatName } from './utils'

// 4. 类型导入
import type { UserInfo } from '@/types/user'
```

### 导出风格

```typescript
// 组件：命名导出（推荐）
export function UserProfile({ user }: UserProfileProps) { ... }

// 页面组件：默认导出
export default function HomePage() { ... }

// Hooks：命名导出
export function useAuth() { ... }

// 工具函数：命名导出
export function formatDate(date: Date): string { ... }

// 类型：命名导出
export interface UserInfo { ... }
export type UserRole = 'admin' | 'user' | 'guest'
```

## 组件开发

### React 组件模式

```tsx
import type { ReactNode } from 'react'

// Props 类型定义
interface UserCardProps {
  user: UserInfo
  showAvatar?: boolean
  onEdit?: (id: string) => void
  children?: ReactNode
}

// 函数组件（推荐箭头函数或 function 声明）
export function UserCard({ user, showAvatar = true, onEdit, children }: UserCardProps) {
  const [isExpanded, setIsExpanded] = useState(false)

  const handleEdit = useCallback(() => {
    onEdit?.(user.id)
  }, [onEdit, user.id])

  return (
    <div className="user-card">
      {showAvatar && <Avatar src={user.avatar} />}
      <h3>{user.name}</h3>
      {children}
      <button onClick={handleEdit}>编辑</button>
    </div>
  )
}
```

### 自定义 Hook 模式

```typescript
export function useDebounce<T>(value: T, delay: number = 300): T {
  const [debouncedValue, setDebouncedValue] = useState(value)

  useEffect(() => {
    const timer = setTimeout(() => setDebouncedValue(value), delay)
    return () => clearTimeout(timer)
  }, [value, delay])

  return debouncedValue
}
```

## 测试

### 测试框架：Vitest + React Testing Library

### 文件模式：`*.test.tsx` / `*.test.ts`

### 测试类型

- **单元测试**：工具函数、自定义 Hooks
- **组件测试**：UI 组件渲染和交互
- **集成测试**：页面级别的用户流程

### 测试示例

```tsx
import { render, screen, fireEvent } from '@testing-library/react'
import { describe, it, expect, vi } from 'vitest'
import { UserCard } from './UserCard'

describe('UserCard', () => {
  const mockUser = { id: '1', name: 'Alice', avatar: '/alice.png' }

  it('renders user name', () => {
    render(<UserCard user={mockUser} />)
    expect(screen.getByText('Alice')).toBeInTheDocument()
  })

  it('calls onEdit when edit button clicked', () => {
    const onEdit = vi.fn()
    render(<UserCard user={mockUser} onEdit={onEdit} />)
    fireEvent.click(screen.getByText('编辑'))
    expect(onEdit).toHaveBeenCalledWith('1')
  })

  it('hides avatar when showAvatar is false', () => {
    render(<UserCard user={mockUser} showAvatar={false} />)
    expect(screen.queryByRole('img')).not.toBeInTheDocument()
  })
})
```

## API 集成

### 数据获取模式

```typescript
// services/api.ts — 统一的 API 客户端
const api = {
  async get<T>(url: string): Promise<T> {
    const response = await fetch(`${BASE_URL}${url}`, {
      headers: { Authorization: `Bearer ${getToken()}` },
    })
    if (!response.ok) throw new ApiError(response.status, await response.text())
    return response.json()
  },
}

// services/user.ts — 业务 API
export const userService = {
  getList: (params: UserListParams) => api.get<UserListResponse>('/users', { params }),
  getById: (id: string) => api.get<UserInfo>(`/users/${id}`),
}

// hooks/useUsers.ts — 数据获取 Hook（使用 React Query）
export function useUsers(params: UserListParams) {
  return useQuery({
    queryKey: ['users', params],
    queryFn: () => userService.getList(params),
    staleTime: 5 * 60 * 1000,
  })
}
```

## 错误处理

### 错误边界

```tsx
import { ErrorBoundary } from 'react-error-boundary'

function ErrorFallback({ error, resetErrorBoundary }: FallbackProps) {
  return (
    <div role="alert">
      <p>出错了：{error.message}</p>
      <button onClick={resetErrorBoundary}>重试</button>
    </div>
  )
}

// 使用
<ErrorBoundary FallbackComponent={ErrorFallback}>
  <UserProfile />
</ErrorBoundary>
```

### API 错误处理

```typescript
try {
  const data = await userService.getById(userId)
  return data
} catch (error) {
  if (error instanceof ApiError) {
    if (error.status === 401) redirectToLogin()
    if (error.status === 404) return null
  }
  console.error('获取用户信息失败:', error)
  throw error
}
```

## 性能优化

### 常用优化手段

- **React.memo** — 避免不必要的重渲染
- **useMemo / useCallback** — 缓存计算结果和回调
- **React.lazy + Suspense** — 路由级代码分割
- **虚拟列表** — 大数据量列表渲染
- **图片懒加载** — Intersection Observer
- **防抖/节流** — 搜索输入、滚动事件

### 代码分割示例

```typescript
const UserProfile = React.lazy(() => import('./pages/UserProfile'))

function App() {
  return (
    <Suspense fallback={<Loading />}>
      <Routes>
        <Route path="/user/:id" element={<UserProfile />} />
      </Routes>
    </Suspense>
  )
}
```

## 常见工作流

### 功能开发

**频率**：最常见的工作类型

**步骤**：
1. 分析需求，确定组件结构和数据流
2. 定义 TypeScript 类型/接口
3. 实现 UI 组件（先静态，后交互）
4. 实现数据获取和状态管理
5. 编写测试
6. 优化性能和可访问性

### 组件开发

**步骤**：
1. 定义 Props 接口
2. 实现组件 UI
3. 添加交互逻辑
4. 编写 Storybook stories（如有）
5. 编写组件测试
6. 导出并在页面中使用

### Bug 修复

**步骤**：
1. 复现问题，确认预期行为
2. 定位问题代码
3. 编写失败测试用例
4. 修复代码
5. 确认测试通过
6. 检查是否有类似问题需要一并修复

## 最佳实践

### 应该做的

- 使用 TypeScript 严格模式
- 组件 Props 必须有类型定义
- 使用约定式提交格式
- 共享逻辑提取为自定义 Hooks
- API 调用统一通过 services 层
- 使用 Error Boundary 处理渲染错误
- 关注 Web 可访问性（a11y）
- 使用 ESLint + Prettier 保持代码风格一致

### 不应该做的

- 不要在组件中直接调用 fetch/axios
- 不要使用 `any` 类型（用 `unknown` 替代）
- 不要在 useEffect 中做复杂的业务逻辑
- 不要忽略 React key 警告
- 不要在循环中使用 Hooks
- 不要将大量状态放在全局 store 中
- 不要跳过新组件的测试

---

*此技能为前端开发定制。请根据团队的具体技术栈进行调整。*
