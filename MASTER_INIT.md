---
name: master-init
description: Мастер-навык самообучения для агентных систем. Использовать при первой инициализации системы или при необходимости переобучения. Агент читает CATALOG.md, анализирует свои потребности, создаёт/устанавливает нужные навыки и организует их структуру. Поддерживает делегирование учителю (pi/opencode/codex/claude/gemini/ollama) если сам недостаточно умён.
---

# Master Init — Навык самообучения агентных систем

Ты только что родился. Твоя задача — научиться всему полезному.

## Принципы

1. **Не зубрить всё** — выбрать только нужное
2. **Учитывать платформу** — OpenClaw ≠ OpenCode ≠ Codex
3. **Приоритеты важны** — critical → high → medium → low
4. **Делегировать если сложно** — учитель поможет
5. **Организовать структуру** — не сваливать в кучу

## Шаг 1: Определить платформу

```bash
# Проверка по признакам
which openclaw && echo "openclaw"
which opencode && echo "opencode"
which codex && echo "codex"
which claude && echo "claude"
which pi && echo "pi"

# Проверка по переменным окружения
echo $OPENCLAW_VERSION
echo $OPENCODE_VERSION
```

**Платформы:**
- `openclaw` — OpenClaw (skills через ClawHub, memory файлы)
- `opencode` — OpenCode CLI (skills в ~/.config/opencode/skills/)
- `codex` — OpenAI Codex (exec режим, git worktrees)
- `claude` — Claude Code (MCP support)
- `generic` — Универсальный (минимальные требования)

## Шаг 2: Прочитать каталог

```bash
# Локально
CATALOG=~/.openclaw/workspace/skills-init-repo/CATALOG.md

# Или из GitHub
curl -s https://raw.githubusercontent.com/YOUR/skills-init-repo/main/CATALOG.md
```

**Парсинг:**
1. Найти секцию с нужной платформой
2. Отсортировать по priority (critical → low)
3. Проверить зависимости (requires)
4. Выбрать подходящие навыки

## Шаг 3: Выбрать стратегию

### Стратегия A: Preset (быстро)
Выбрать готовый набор из секции Presets:
- `minimal` — минимум для работы
- `developer` — для разработки
- `assistant` — персональный ассистент
- `researcher` — для исследований

### Стратегия B: Custom (точно)
Проанализировать потребности:
1. Что я умею? (проверить tools)
2. Что мне нужно? (задачи пользователя)
3. Что могу установить? (зависимости)

### Стратегия C: Incremental (постепенно)
Установить только critical, затем добавить по необходимости.

## Шаг 4: Установить навыки

### Для OpenClaw

```bash
# Через ClawHub
clawhub install <slug> --workdir ~/.openclaw/workspace

# Локальный skill
cp -r skills/<name> ~/.openclaw/workspace/skills/

# Создать симлинк для системного доступа
ln -s ~/.openclaw/workspace/skills/<name> /opt/homebrew/lib/node_modules/openclaw/skills/
```

### Для OpenCode

```bash
# Skills в ~/.config/opencode/skills/
cp -r skills/<name> ~/.config/opencode/skills/
```

### Для Codex / Claude

```bash
# Создать .skills/ в проекте
mkdir -p .skills
cp -r skills/<name> .skills/
```

## Шаг 5: Создать структуру памяти

```bash
# OpenClaw
mkdir -p ~/.openclaw/workspace/memory
touch ~/.openclaw/workspace/MEMORY.md
touch ~/.openclaw/workspace/memory/$(date +%Y-%m-%d).md

# Generic
mkdir -p ~/.agent/memory
touch ~/.agent/MEMORY.md
```

## Шаг 6: Настроить heartbeat (если применимо)

```bash
# OpenClaw
cat > ~/.openclaw/workspace/HEARTBEAT.md << 'EOF'
# Heartbeat Tasks

- Check memory files for recent updates
- Review pending tasks
- Update MEMORY.md with learnings
EOF
```

## Шаг 7: Валидация

Проверить что всё работает:

```bash
# Проверить навыки
ls -la ~/.openclaw/workspace/skills/

# Проверить память
cat ~/.openclaw/workspace/MEMORY.md

# Тестовый запрос к навыку
# (зависит от платформы)
```

---

## Делегирование учителю

Если агент "глуповат" или задача сложная — делегировать учителю.

### Доступные учителя (по приоритету)

1. **pi** — pi-coding-agent (gpt-5.3-codex через ChatGPT Plus)
2. **opencode** — OpenCode CLI (plan + build агенты)
3. **codex** — OpenAI Codex
4. **claude** — Claude Code
5. **gemini** — Google Gemini CLI
6. **ollama** — Локальный (llama3.2, всегда доступен)

### Проверка доступности

```bash
# Проверить кто установлен
for teacher in pi opencode codex claude gemini; do
  which $teacher &>/dev/null && echo "✅ $teacher" || echo "❌ $teacher"
done

# Проверить Ollama
curl -s http://localhost:11434/api/tags &>/dev/null && echo "✅ ollama" || echo "❌ ollama"
```

### Промпт для учителя

```
Ты — учитель для агентной системы. Твоя задача — помочь инициализировать навыки.

1. Прочитай CATALOG.md: <ссылка или путь>
2. Определи платформу: <openclaw/opencode/codex/...>
3. Выбери подходящие навыки (preset: <minimal/developer/assistant>)
4. Создай SKILL.md файлы для каждого навыка
5. Организуй структуру директорий
6. Создай MEMORY.md с базовым контекстом

Выведи пошаговый план и выполни его.
```

### Запуск учителя

```bash
# pi (рекомендуется для сложных задач)
pi "Прочитай ~/.openclaw/workspace/skills-init-repo/CATALOG.md и инициализируй навыки для OpenClaw. Preset: developer. Создай все SKILL.md файлы и организуй структуру."

# opencode
opencode run "Инициализируй навыки для OpenClaw из каталога ~/.openclaw/workspace/skills-init-repo/CATALOG.md"

# codex (нужен git repo)
cd ~/.openclaw/workspace && codex exec "Инициализируй навыки из CATALOG.md"

# ollama (фолбэк)
ollama run llama3.2:3b "Помоги создать структуру навыков для агента. Вот каталог: $(cat CATALOG.md)"
```

---

## Автоматическое определение потребностей

### Анализ существующих инструментов

```bash
# Проверить какие tools уже есть
# (платформо-зависимо)

# OpenClaw — проверить доступные skills
ls /opt/homebrew/lib/node_modules/openclaw/skills/
ls ~/.openclaw/workspace/skills/

# Проверить MCP servers
mcporter list
```

### Анализ частых задач

Если есть история чатов — проанализировать:
- Какие типы запросов частые?
- Какие навыки нужны для их выполнения?
- Чего не хватает?

---

## Примеры использования

### Быстрая инициализация (preset)

```
Прочти https://github.com/YOUR/skills-init-repo и инициализируй навыки для OpenClaw.
Preset: developer.
```

### Кастомная инициализация

```
Прочти https://github.com/YOUR/skills-init-repo и инициализируй навыки для OpenClaw.
Мне нужны: git, coding-style, web-search, mcp, messaging.
```

### Через CLI

```bash
# Автоопределение платформы + preset minimal
ssi auto --preset minimal

# Явно указать платформу + делегировать учителю
ssi openclaw --teacher pi --preset developer

# Только проанализировать (dry-run)
ssi openclaw --analyze
```

---

## Расширение репозитория

### Добавить новый навык

1. Создать `skills/<category>/<name>/SKILL.md`
2. Добавить запись в CATALOG.md
3. Протестировать
4. Запушить в репозиторий

### Ссылка на внешний репозиторий

В CATALOG.md:
```yaml
- id: external-skill
  name: External Skill
  source: github
  path: https://github.com/user/skill-repo
  platforms: [generic]
```

Агент скачает и интегрирует при инициализации.

---

## Troubleshooting

### Навык не устанавливается
- Проверить зависимости (requires)
- Проверить совместимость платформы
- Попробовать учителя

### Нет учителя
- Установить pi: `npm install -g @mariozechner/pi-coding-agent`
- Или opencode: `npm install -g opencode`
- Или использовать ollama как фолбэк

### Память не работает
- Проверить права на запись
- Создать директории вручную
- Проверить путь в конфигурации

---

**Версия:** 0.1.0
**Обновлено:** 2026-03-01
