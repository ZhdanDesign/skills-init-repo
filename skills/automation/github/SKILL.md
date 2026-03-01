---
name: github-integration
description: Работа с GitHub через gh CLI и git. Создание репозиториев, issues, PRs, CI/CD, push/pull. Автоматически использует существующие credentials пользователя.
platforms: [generic]
requires: []
provides: [github, git, repositories, issues, pull-requests, ci-cd]
priority: critical
source: local
path: skills/automation/github/SKILL.md
---

# GitHub Integration

## Текущая конфигурация

```bash
# Проверка
gh auth status           # ✓ Logged in
git config user.name     # Имя пользователя
git config user.email    # Email
```

## Основные команды

### Репозитории
```bash
gh repo create <name> --public|--private --clone
gh repo clone <owner>/<repo>
gh repo fork <owner>/<repo> --clone
```

### Issues
```bash
gh issue create --title "Title" --body "Description"
gh issue list --state open
gh issue view <number>
gh issue close <number>
```

### Pull Requests
```bash
gh pr create --title "Title" --body "Description" --base main
gh pr list --state open
gh pr merge <number> --squash
```

### CI/CD
```bash
gh workflow list
gh workflow run <name>
gh run list --limit 10
gh run view <run-id> --log
```

## Workflow

### Создать репо и запушить
```bash
git init && git add . && git commit -m "Initial commit"
gh repo create <name> --public --source=. --push
```

### Feature branch
```bash
git checkout -b feature/my-feature
# ... work ...
git push -u origin feature/my-feature
gh pr create --title "feat: description"
```

## Безопасность

1. **Никогда не коммитить secrets** — использовать GitHub Secrets
2. **SSH protocol** — `git@github.com:`
3. **Force push только в feature branches**
4. **Проверять branch** перед destructive operations

---

**Зависимости:** `gh` CLI (https://cli.github.com), git, SSH keys
