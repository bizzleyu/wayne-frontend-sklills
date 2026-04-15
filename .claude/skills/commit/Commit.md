---
name: commitmsg
description: 分析 git 工作区变更，自动生成中文 commit message 并提交。使用 Conventional Commits 格式（feat/fix/chore/refactor/docs/style/test），描述用中文。
---

# Commit Message 自动生成

分析当前 git 工作区的所有变更（staged + unstaged + untracked），生成规范的 commit message 并提交。

## 执行步骤

1. 运行 `git status` 和 `git diff` 查看所有变更
2. 将相关文件加入暂存区
3. 根据变更内容生成 commit message
4. 执行 commit
5. 执行 `git push` 推送到远程仓库

## Commit Message 规范

- 格式：`<type>: <简短中文描述>`
- type 可选：feat / fix / chore / refactor / docs / style / test
- 描述用中文，简洁说明"为什么"而非"改了什么"
- 如果变更较多，在 body 中用要点列出关键改动
- 通过 HEREDOC 传递 message 确保格式正确

## 安全规则

- **禁止提交**：.env、credentials.json 等敏感文件，发现时警告用户
- **跳过**：node_modules、dist 等生成文件
- 如果没有任何变更，告知用户无需提交