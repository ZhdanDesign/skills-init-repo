# Примеры использования

## OpenClaw

### Быстрая инициализация

```bash
# Скачать и запустить
git clone https://github.com/ZhdanDesign/skills-init-repo.git
cd skills-init-repo
./scripts/ssi openclaw --preset developer
```

### Прямая инструкция агенту

```
Прочти https://github.com/ZhdanDesign/skills-init-repo
и инициализируй навыки для OpenClaw.
Preset: developer.
Создай MEMORY.md с описанием установленных навыков.
```

### Через учителя (рекомендуется для новых систем)

```bash
# Pi как учитель
ssi openclaw --teacher pi --preset developer

# OpenCode как учитель
ssi openclaw --teacher opencode --preset developer
```

### Только анализ

```bash
ssi openclaw --analyze
```

**Вывод:**
```
═══════════════════════════════════════════════════════
               АНАЛИЗ СИСТЕМЫ
═══════════════════════════════════════════════════════

Платформа: openclaw
Учителя: pi opencode codex claude gemini ollama
Рекомендуемый учитель: pi
Каталог: ~/.openclaw/workspace/skills-init-repo/CATALOG.md
Preset 'developer':
  • coding-agent
  • coding-style
  • git
  • github-integration
  • master-init
  • mcp
  • memory-management
  • shell-exec
  • web-search
Существующие навыки:
  (список уже установленных)
```

### Кастомный набор

```bash
# Выбрать конкретные навыки
# (пока через правку CATALOG.md или ручную установку)
```

---

## OpenCode

### Инициализация

```bash
./scripts/ssi opencode --preset developer
```

**Что произойдёт:**
1. Навыки скопируются в `~/.config/opencode/skills/`
2. Создастся базовая структура памяти
3. OpenCode сможет использовать навыки сразу

### Прямая инструкция

```
Прочти https://github.com/ZhdanDesign/skills-init-repo
и инициализируй навыки для OpenCode.
Preset: minimal.
```

### Проверка

```bash
ls ~/.config/opencode/skills/
```

---

## Codex

### Инициализация

```bash
./scripts/ssi codex --preset developer
```

**Что произойдёт:**
1. Создастся `.skills/` в текущей директории
2. Навыки будут доступны Codex при работе в этом проекте

### В конкретном проекте

```bash
cd ~/my-project
ssi codex --preset developer
codex exec "Прочитай .skills/master-init/SKILL.md"
```

---

## Claude Code

### Инициализация

```bash
./scripts/ssi claude --preset developer
```

### MCP Support

Claude Code имеет встроенный MCP support, поэтому навык `mcporter` особенно полезен.

```bash
# После инициализации
claude "Используй mcporter для подключения Linear MCP server"
```

---

## Generic (любая платформа)

### Минимальный набор

```bash
ssi generic --preset minimal
```

**Установится:**
- git
- memory-management
- web-search
- shell-exec

### Для несовместимых платформ

Если платформа не определяется автоматически:

```bash
# Создать структуру вручную
mkdir -p ~/.agent/{skills,memory}

# Установить навыки
ssi generic --preset minimal

# Переместить в нужное место
mv ~/.openclaw/workspace/skills/* ~/.agent/skills/
```

---

## Делегирование учителю

### Pi (рекомендуется)

```bash
ssi openclaw --teacher pi --preset developer
```

**Что произойдёт:**
1. Pi запустится с промптом учителя
2. Прочитает CATALOG.md
3. Проанализирует потребности
4. Создаст все SKILL.md файлы
5. Организует структуру
6. Создаст MEMORY.md

### OpenCode

```bash
ssi opencode --teacher opencode --preset developer
```

### Ollama (фолбэк)

```bash
# Если нет API ключей
ssi generic --teacher ollama --preset minimal
```

**Ограничения Ollama:**
- Слабее reasoning
- Нет web search
- Медленнее

---

## Примеры сценариев

### Сценарий 1: Новый разработчик

```bash
# Установить OpenClaw
npm install -g openclaw

# Инициализировать навыки
git clone https://github.com/ZhdanDesign/skills-init-repo.git
cd skills-init-repo
./scripts/ssi openclaw --teacher pi --preset developer

# Готово! OpenClaw умеет:
# - Работать с git
# - Создавать репозитории на GitHub
# - Искать в интернете
# - Делегировать кодинг Codex/Pi
# - Работать с MCP servers
```

### Сценарий 2: Персональный ассистент

```bash
# Установить preset assistant
ssi openclaw --preset assistant

# Навыки:
# - imsg (iMessage)
# - summarize
# - healthcheck
# - git, memory, web-search
```

### Сценарий 3: Исследователь

```bash
ssi openclaw --preset researcher

# Навыки:
# - web-search
# - summarize
# - git, memory
```

### Сценарий 4: Minimal setup

```bash
ssi generic --preset minimal

# Только базовые навыки:
# - git
# - memory
# - web-search
# - shell-exec
```

---

## Интеграция с существующими навыками

### Проверка что уже установлено

```bash
ls ~/.openclaw/workspace/skills/
```

### Добавить к существующим

```bash
# Только недостающие навыки
ssi openclaw --analyze
# Сравнить с уже установленными
# Установить недостающие вручную
```

### Обновить навыки

```bash
cd skills-init-repo
git pull
ssi openclaw --preset developer
```

---

## Troubleshooting примеры

### Проблема: Нет учителя

```bash
# Установить pi
npm install -g @mariozechner/pi-coding-agent
pi auth  # ChatGPT Plus OAuth

# Проверить
pi --help
```

### Проблема: Skills не грузятся

```bash
# Проверить путь
ls ~/.openclaw/workspace/skills/*/SKILL.md

# Проверить frontmatter
head -5 ~/.openclaw/workspace/skills/git/SKILL.md
# Должно начинаться с ---
```

### Проблема: Memory не работает

```bash
# Создать вручную
mkdir -p ~/.openclaw/workspace/memory
touch ~/.openclaw/workspace/MEMORY.md

# Добавить базовый контент
cat > ~/.openclaw/workspace/MEMORY.md << 'EOF'
# MEMORY.md

## Навыки
- git
- memory
- web-search
EOF
```
