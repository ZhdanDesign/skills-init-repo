---
name: git
description: Полный справочник Git — essentials, workflows, advanced, recovery. Использовать при любых операциях с Git: commit, branch, merge, rebase, recovery, collaboration.
---

# Git — Справочник

## Essential Commands

```bash
# Статус
git status

# История
git log --oneline -20
git log --graph --all

# Diff
git diff
git diff --staged
git diff main...feature
```

## Safe Practices

1. **Never force push to shared branches**
2. **Commit early, commit often**
3. **`--force-with-lease` instead of `--force`**
4. **`git pull --rebase` before push**
5. **`git rebase -i` for squash fixups**

## Recovery

```bash
# Reflog (keeps ~90 days)
git reflog

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Recover deleted branch
git checkout -b recovered-branch <sha-from-reflog>
```

## Workflows

### Feature Branch
```bash
git checkout -b feature/my-feature main
# ... work ...
git push -u origin feature/my-feature
gh pr create
```

### Git Worktrees (parallel work)
```bash
git worktree add ../project-feature feature/my-feature
cd ../project-feature
# ... work ...
git worktree remove ../project-feature
```

---

**Источник:** ClawHub git skill v1.0.7
