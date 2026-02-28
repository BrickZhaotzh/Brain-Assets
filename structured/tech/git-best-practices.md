---
title: Git 版本控制最佳实践
category: tech
tags: [git, version-control, best-practices]
created: 2024-02-28
updated: 2024-02-28
---

# Git 版本控制最佳实践

## 概览
本文档介绍 Git 版本控制的最佳实践，包括提交规范、分支管理、工作流程等，帮助团队高效协作。

## 核心概念

### 什么是 Git
Git 是一个分布式版本控制系统，用于追踪文件变化、协调多人协作、管理项目版本。

### 基本原则
- **原子提交**：每次提交只做一件事
- **清晰信息**：提交信息描述变更内容
- **频繁提交**：小步快跑，减少冲突
- **及时同步**：定期拉取远程更新

## 提交规范

### 提交信息格式
```
<type>(<scope>): <subject>

<body>

<footer>
```

### 类型（Type）
- `feat`: 新功能
- `fix`: 修复 bug
- `docs`: 文档更新
- `style`: 代码格式调整
- `refactor`: 重构代码
- `test`: 测试相关
- `chore`: 构建/工具配置

### 示例
```
feat(auth): 添加用户登录功能

- 实现用户名密码登录
- 添加 JWT token 验证
- 集成第三方登录（GitHub/Google）

Closes #123
```

## 分支管理

### 主分支
- `main/master`: 生产环境代码
- `develop`: 开发分支
- `release/*`: 发布分支
- `hotfix/*`: 紧急修复分支

### 功能分支
```
feature/user-authentication
feature/payment-integration
feature/search-optimization
```

### 分支命名规范
- 使用小写字母
- 单词用连字符连接
- 清晰描述功能

## 工作流程

### Git Flow
```
main (生产)
  ↑
release (发布)
  ↑
develop (开发)
  ↑
feature/* (功能)
```

### GitHub Flow
```
main (生产)
  ↑
feature/* (功能) → Pull Request → 合并
```

### 操作步骤
```bash
# 1. 创建功能分支
git checkout -b feature/new-feature

# 2. 开发并提交
git add .
git commit -m "feat: 添加新功能"

# 3. 推送到远程
git push origin feature/new-feature

# 4. 创建 Pull Request
# 在 GitHub 上创建 PR，请求代码审查

# 5. 合并后删除分支
git checkout main
git pull origin main
git branch -d feature/new-feature
```

## 代码审查

### 审查要点
- 代码逻辑是否正确
- 是否符合团队规范
- 是否有潜在 bug
- 是否需要添加测试
- 是否有性能问题

### 审查流程
1. **自动化检查**：CI/CD 运行测试
2. **同行审查**：至少一人 Review
3. **修改反馈**：根据意见调整
4. **最终确认**：Maintainer 批准合并

## 常用命令

### 日常操作
```bash
# 查看状态
git status

# 查看提交历史
git log --oneline --graph

# 暂存变更
git add file.txt
git add .

# 提交变更
git commit -m "feat: 添加功能"

# 拉取最新代码
git pull origin main

# 推送到远程
git push origin main
```

### 分支操作
```bash
# 创建分支
git branch feature-new

# 切换分支
git checkout feature-new

# 创建并切换
git checkout -b feature-new

# 删除本地分支
git branch -d feature-new

# 删除远程分支
git push origin --delete feature-new
```

### 合并与变基
```bash
# 合并分支
git merge feature-new

# 变基分支
git rebase main

# 解决冲突后继续
git add .
git rebase --continue

# 放弃变基
git rebase --abort
```

## 常见问题

### Q: 什么时候使用 rebase？
A: 仅在本地分支整理提交历史时使用，避免在共享分支上使用。

### Q: 如何处理合并冲突？
A:
1. 查看冲突文件：`git status`
2. 手动解决冲突
3. 标记解决：`git add <file>`
4. 继续合并：`git commit`

### Q: 如何撤销提交？
A:
```bash
# 撤销最后一次提交（保留修改）
git reset --soft HEAD~1

# 撤销最后一次提交（丢弃修改）
git reset --hard HEAD~1

# 撤销指定提交（保留历史）
git revert <commit-hash>
```

### Q: 如何清理无用分支？
A:
```bash
# 删除已合并的本地分支
git branch --merged | grep -v main | xargs git branch -d

# 删除远程已删除的本地分支
git fetch --prune
```

## 最佳实践总结

### 提交原则
- ✅ 频繁提交，小步快跑
- ✅ 清晰描述变更内容
- ✅ 遵循提交规范
- ❌ 避免大文件提交
- ❌ 避免敏感信息提交

### 分支原则
- ✅ 主分支保持稳定
- ✅ 功能分支及时合并
- ✅ 合并前确保测试通过
- ❌ 避免长期未合并的分支
- ❌ 避免直接修改主分支

### 协作原则
- ✅ 及时同步远程更新
- ✅ 创建 Pull Request 前自测
- ✅ 认真处理代码审查意见
- ❌ 避免强制推送（force push）
- ❌ 避免合并冲突

## 参考资源
- [Git 官方文档](https://git-scm.com/doc)
- [Pro Git Book](https://git-scm.com/book/zh/v2)
- [GitHub Flow](https://guides.github.com/introduction/flow/)
- [Conventional Commits](https://www.conventionalcommits.org/)

## 更新日志
- 2024-02-28: 创建文档
