---
name: tech-research
description: 前端技术选型和调研的工作流命令。
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /tech-research（技术调研）

当任务涉及技术选型、框架对比、API 调研或需要广泛的前端知识时使用此工作流。

## 默认设置

- 优先引用官方文档和 MDN Web Docs。
- 检查浏览器兼容性时使用 Can I Use 数据。
- 为每个技术建议提供简短的优劣分析。
- 注明信息的时效性（前端生态变化快）。

## 建议步骤

1. **检查项目现状**：先了解项目已有的技术栈和约束。
2. **查阅官方文档**：React/Vue/Next.js 等框架的官方文档是第一来源。
3. **对比方案**：列出 2-3 个候选方案，从性能、包体积、社区活跃度、学习曲线等维度对比。
4. **验证兼容性**：检查浏览器支持、TypeScript 支持、与现有工具链的兼容性。
5. **总结建议**：给出明确的推荐方案和理由。

## 常用参考资源

- **MDN Web Docs** — Web API 和 HTML/CSS/JS 标准
- **Can I Use** — 浏览器兼容性数据
- **React 官方文档** — React 最新 API 和最佳实践
- **TypeScript 手册** — 类型系统参考
- **npm trends** — 包下载趋势对比
- **Bundlephobia** — 包体积分析
- **Web.dev** — Google 的 Web 性能和最佳实践指南

## 技术选型维度

| 维度 | 考量因素 |
|------|---------|
| 性能 | 包体积、运行时性能、Tree-shaking 支持 |
| 开发体验 | TypeScript 支持、文档质量、调试工具 |
| 社区 | GitHub Stars、npm 下载量、Issue 响应速度 |
| 维护 | 最近更新时间、主要维护者、版本发布频率 |
| 兼容性 | 浏览器支持、框架版本要求、与现有工具链集成 |
