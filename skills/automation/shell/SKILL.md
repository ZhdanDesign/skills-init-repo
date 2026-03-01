---
name: shell-exec
description: Безопасное выполнение shell команд. Использовать для: (1) системных операций, (2) работы с файлами, (3) запуска скриптов, (4) автоматизации. Всегда проверять команды перед выполнением.
---

# Shell Execution

Безопасное выполнение shell команд через bash tool.

## Основные правила

1. **Всегда проверять команду** — особенно rm, mv, sudo
2. **Использовать trash вместо rm** — recoverable > gone forever
3. **Не выполнять слепо** — анализировать последствия
4. **Логировать важные операции** — для отладки

## Безопасные команды

```bash
# Чтение
ls, cat, head, tail, grep, find, wc

# Информация
pwd, whoami, date, uname, df, du

# Файловые операции (осторожно)
cp, mv, mkdir, touch

# Git
git status, git log, git diff
```

## Опасные команды (требуют подтверждения)

```bash
# Удаление
rm, rm -rf, rmdir

# Системные
sudo, chmod, chown

# Сеть
curl, wget (с upload)

# Критичные
dd, mkfs, fdisk
```

## Примеры

### Чтение файла
```bash
cat ~/.openclaw/workspace/MEMORY.md
```

### Поиск
```bash
find ~/.openclaw/workspace -name "*.md" -type f
grep -r "search query" ~/.openclaw/workspace/memory/
```

### Создание структуры
```bash
mkdir -p ~/.openclaw/workspace/memory
touch ~/.openclaw/workspace/memory/$(date +%Y-%m-%d).md
```

### Удаление (безопасно)
```bash
# Вместо rm -rf
trash ~/.openclaw/workspace/old-file.md

# Или mv в temp
mv ~/.openclaw/workspace/old-file.md /tmp/
```

## Best Practices

### 1. Проверять перед выполнением
```bash
# Что будет удалено?
find . -name "*.tmp" -type f

# Затем удалять
find . -name "*.tmp" -type f -delete
```

### 2. Использовать dry-run где возможно
```bash
# rsync dry-run
rsync -av --dry-run source/ dest/

# Без dry-run
rsync -av source/ dest/
```

### 3. Резервные копии
```bash
# Перед изменением
cp important.file important.file.bak

# Или git
git add .
git commit -m "Before changes"
```

## Интеграция с OpenClaw

OpenClaw имеет встроенный bash tool с параметрами:

| Параметр | Описание |
|----------|----------|
| `command` | Shell команда |
| `workdir` | Рабочая директория |
| `timeout` | Таймаут в секундах |
| `background` | Запустить в фоне |
| `pty` | PTY режим (для интерактивных) |

**Примеры:**
```bash
# Простая команда
bash command:"ls -la"

# С рабочей директорией
bash workdir:~/.openclaw/workspace command:"git status"

# В фоне
bash background:true command:"long-running-script.sh"

# С таймаутом
bash timeout:60 command:"slow-command.sh"
```

## Отладка

### Проверить что выполняется
```bash
# Dry-run (echo)
echo "rm -rf $DIR"

# Пошагово
set -x  # включить trace
command
set +x  # выключить
```

### Логирование
```bash
# Сохранить вывод
command > output.log 2>&1

# И на экран, и в файл
command 2>&1 | tee output.log
```

---

**Важно:** Всегда думай перед выполнением. Лучше спросить подтверждение, чем удалить важные данные.
