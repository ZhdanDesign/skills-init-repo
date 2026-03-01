---
name: master-init
description: Мастер-навык самообучения для агентных систем. Использовать при первой инициализации системы, при необходимости переобучения, или когда нужно быстро настроить новую агентную платформу. Поддерживает presets (minimal/developer/assistant/researcher) и делегирование учителю (pi/opencode/codex/claude/gemini/ollama).
---

# Master Init — Навык самообучения

Ты только что родился. Твоя задача — научиться всему полезному.

## Быстрый старт

### Вариант 1: Прямая инструкция
```
Прочти https://github.com/YOUR/skills-init-repo и инициализируй навыки для [платформа]
Preset: [minimal|developer|assistant|researcher]
```

### Вариант 2: CLI ssi
```bash
ssi auto                    # Автоопределение + minimal
ssi openclaw --preset dev   # OpenClaw + developer
ssi opencode --teacher pi   # Делегировать pi
```

## Шаги инициализации

### 1. Определить платформу

```bash
# Проверка по признакам
which openclaw && echo "openclaw"
which opencode && echo "opencode"
which codex && echo "codex"
which claude && echo "claude"
```

### 2. Прочитать каталог

```bash
# Локально
CATALOG=~/.openclaw/workspace/skills-init-repo/CATALOG.md

# Из GitHub
curl -s https://raw.githubusercontent.com/YOUR/skills-init-repo/main/CATALOG.md
```

### 3. Выбрать preset

| Preset | Навыки | Для кого |
|--------|--------|----------|
| minimal | git, memory, web-search, shell | Минимум для работы |
| developer | + coding-style, mcp | Разработчик |
| assistant | + messaging, email, cron | Ассистент |
| researcher | + web-scrape, summarize | Исследователь |

### 4. Установить навыки

**OpenClaw:**
```bash
clawhub install <slug> --workdir ~/.openclaw/workspace
# или
cp -r skills/<name> ~/.openclaw/workspace/skills/
```

**OpenCode:**
```bash
cp -r skills/<name> ~/.config/opencode/skills/
```

### 5. Настроить память

```bash
mkdir -p ~/.openclaw/workspace/memory
touch ~/.openclaw/workspace/MEMORY.md
```

## Делегирование учителю

Если задача сложная — делегировать учителю.

### Проверка учителей

```bash
for t in pi opencode codex claude gemini; do
  which $t &>/dev/null && echo "✅ $t"
done
curl -s http://localhost:11434/api/tags &>/dev/null && echo "✅ ollama"
```

### Приоритет учителей

1. **pi** — gpt-5.3-codex (ChatGPT Plus)
2. **opencode** — plan + build агенты
3. **codex** — OpenAI Codex
4. **claude** — Claude Code
5. **gemini** — Google Gemini
6. **ollama** — локальный (фолбэк)

### Промпт для учителя

```
Ты — учитель для агентной системы. Инициализируй навыки.

1. Прочитай CATALOG.md: <путь>
2. Платформа: <openclaw/opencode/...>
3. Preset: <minimal/developer/...>
4. Создай SKILL.md файлы
5. Организуй структуру
6. Создай MEMORY.md

Выведи план и выполни.
```

## Репозиторий

```
skills-init-repo/
├── CATALOG.md           # Каталог навыков
├── MASTER_INIT.md       # Этот навык
├── skills/              # Готовые навыки
│   ├── core/            # Базовые
│   ├── communication/   # Коммуникации
│   ├── research/        # Исследования
│   └── automation/      # Автоматизация
└── references/          # Референсы по платформам
```

## Расширение

1. Создать навык в `skills/<category>/<name>/SKILL.md`
2. Добавить запись в CATALOG.md
3. При необходимости — ссылка на внешний репозиторий

---

**Версия:** 0.1.0
**Репозиторий:** https://github.com/YOUR/skills-init-repo
