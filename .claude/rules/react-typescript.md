# 前端 TypeScript + React 规则

> 适用于现代前端项目的编码规则。

## 技术栈

- **语言**：TypeScript（严格模式）
- **UI 框架**：React 18+（函数组件 + Hooks）
- **构建工具**：Vite / Next.js
- **样式**：Tailwind CSS / CSS Modules
- **测试**：Vitest + React Testing Library
- **代码检查**：ESLint + Prettier
- **包管理**：pnpm / bun

## 文件约定

- `src/components/` — React 组件，PascalCase 命名（`UserProfile.tsx`）
- `src/pages/` — 页面组件，按路由组织
- `src/hooks/` — 自定义 Hooks，camelCase + `use` 前缀（`useAuth.ts`）
- `src/services/` — API 服务层（`userService.ts`）
- `src/stores/` — 状态管理（`useUserStore.ts`）
- `src/types/` — 类型定义（`user.types.ts`）
- `src/utils/` — 工具函数（`formatDate.ts`）
- `**/*.test.tsx` — 测试文件，与源文件同目录或 `__tests__/` 下

## TypeScript 规则

- 启用 `strict: true`，不允许隐式 `any`
- 组件 Props 必须定义 `interface`，不使用内联类型
- 使用 `import type { ... }` 导入纯类型
- 枚举优先使用 `const enum` 或字面量联合类型
- 泛型参数使用有意义的名称（`TData` 而非 `T`）

```typescript
// ✅ 推荐
interface UserCardProps {
  user: UserInfo
  onEdit?: (id: string) => void
}

// ❌ 避免
function UserCard(props: { user: any; onEdit?: Function }) { ... }
```

## React 规则

- 仅使用函数组件，不使用 class 组件
- Hooks 调用必须在组件顶层，不在条件/循环中
- 事件处理函数以 `handle` 开头（`handleClick`、`handleSubmit`）
- 回调 Props 以 `on` 开头（`onClick`、`onSubmit`）
- 使用 `React.memo` 包裹纯展示组件（仅在有性能问题时）
- 列表渲染必须提供稳定的 `key`（不使用 index）

```tsx
// ✅ 推荐
export function UserList({ users, onSelect }: UserListProps) {
  const handleSelect = useCallback((id: string) => {
    onSelect?.(id)
  }, [onSelect])

  return (
    <ul>
      {users.map(user => (
        <li key={user.id} onClick={() => handleSelect(user.id)}>
          {user.name}
        </li>
      ))}
    </ul>
  )
}
```

## 样式规则

- Tailwind CSS：使用工具类组合，避免自定义 CSS
- CSS Modules：类名使用 camelCase（`styles.userCard`）
- 响应式设计：移动优先（`min-width` 媒体查询）
- 避免内联样式，除非是动态计算值

## 测试规则

- 测试文件命名：`ComponentName.test.tsx`
- 使用 `screen` 查询 DOM，不使用 `container.querySelector`
- 优先使用 `getByRole`、`getByText`，避免 `getByTestId`
- 异步操作使用 `waitFor` 或 `findBy*`
- Mock 外部依赖，不 Mock 内部实现

```tsx
// ✅ 推荐
it('shows error message on failed login', async () => {
  render(<LoginForm />)
  await userEvent.click(screen.getByRole('button', { name: '登录' }))
  expect(await screen.findByText('用户名或密码错误')).toBeInTheDocument()
})
```

## 提交前检查

```bash
# 类型检查
npx tsc --noEmit

# 代码检查
npx eslint src/ --ext .ts,.tsx

# 格式化
npx prettier --check src/

# 测试
npx vitest run
```
