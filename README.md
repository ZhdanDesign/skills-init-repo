# Skills Init Repo — Документация

## Что это?

**НЕ хранилище навыков** — а навык самообучения для агентных систем.

Одной командой агентная система:
1. Читает каталог навыков
2. Анализирует свои потребности
3. Создаёт/устанавливает нужные навыки
4. Организует их структуру

## Быстрый старт

### Вариант 1: Прямая инструкция агенту

```
Прочти https://github.com/ZhdanDesign/skills-init-repo и инициализируй навыки для OpenClaw.
Preset: developer
```

### Вариант 2: CLI ssi

```bash
# Скачать
git clone https://github.com/ZhdanDesign/skills-init-repo.git
cd skills-init-repo

# Запустить
./scripts/ssi auto --analyze              # Анализ
./scripts/ssi openclaw --preset developer # Установка
```

## Платформы

### OpenClaw

```bash
ssi openclaw --preset developer
```

**Что установится:**
- master-init — навык самообучения
- git — версионирование
- github-integration — работа с GitHub
- coding-style — память стиля кодинга
- memory-management — управление памятью
- web-search — поиск в интернете
- shell-exec — выполнение команд
- mcp — Model Context Protocol
- coding-agent — делегирование кодинга

**Структура:**
```
~/.openclaw/workspace/
├── MEMORY.md           # Долгосрочная память
├── memory/             # Дневники
│   └── YYYY-MM-DD.md
└── skills/             # Навыки
    ├── git/
    ├── github-integration/
    └── ...
```

### OpenCode

```bash
ssi opencode --preset developer
```

**Что установится:**
- Аналогично OpenClaw
- Навыки в `~/.config/opencode/skills/`

### Generic

```bash
ssi generic --preset minimal
```

**Что установится:**
- git, memory-management, web-search, shell-exec

## Presets

| Preset | Навыки | Для кого |
|--------|--------|----------|
| **minimal** | git, memory, web-search, shell-exec | Минимум для работы |
| **developer** | + github, coding-style, mcp, coding-agent | Разработчик |
| **assistant** | git, memory, imsg, web-search, summarize, healthcheck | Персональный ассистент |
| **researcher** | git, memory, web-search, summarize | Исследователь |

## Делегирование учителю

Если агент "глуповат" — делегировать учителю:

```bash
# Автовыбор лучшего учителя
ssi openclaw --teacher auto

# Явно указать
ssi openclaw --teacher pi
ssi opencode --teacher opencode
ssi codex --teacher codex
```

**Доступные учителя:**
1. **pi** — gpt-5.3-codex (ChatGPT Plus) — рекомендуется
2. **opencode** — plan + build агенты
3. **codex** — OpenAI Codex
4. **claude** — Claude Code
5. **gemini** — Google Gemini
6. **ollama** — локальный (фолбэк)

## Навыки

### Core (критичные)

- **master-init** — навык самообучения
- **git** — версионирование
- **memory-management** — управление памятью
- **shell-exec** — выполнение команд

### Automation

- **github-integration** — работа с GitHub
- **coding-agent** — делегирование кодинга
- **mcporter** — MCP support
- **healthcheck** — безопасность

### Communication

- **imsg** — iMessage/SMS

### Research

- **web-search** — поиск в интернете
- **summarize** — суммаризация

## Каталог навыков

Все навыки описаны в `CATALOG.md`:

```yaml
- id: skill-name
  name: Human Name
  category: core|automation|communication|research
  description: Описание
  platforms: [openclaw, opencode, generic]
  requires: [зависимости]
  provides: [возможности]
  priority: critical|high|medium|low
  source: local|url|github
  path: skills/category/name/SKILL.md
```

## Расширение

### Добавить навык

1. Создать `skills/<category>/<name>/SKILL.md`
2. Добавить запись в `CATALOG.md`
3. Протестировать
4. Запушить

### Ссылка на внешний репозиторий

В CATALOG.md:
```yaml
- id: external-skill
  name: External Skill
  source: github
  path: https://github.com/user/skill-repo
```

## Примеры использования

### Новая агентная система

```bash
# 1. Установить CLI
git clone https://github.com/ZhdanDesign/skills-init-repo.git
alias ssi='~/skills-init-repo/scripts/ssi'

# 2. Проанализировать
ssi auto --analyze

# 3. Установить
ssi auto --preset developer
```

### Инициализация через учителя

```bash
# Если агент не справляется сам
ssi openclaw --teacher pi --preset developer
```

### Только анализ

```bash
ssi openclaw --analyze
```

## Архитектура

```
skills-init-repo/
├── CATALOG.md              # Каталог навыков (машиночитаемый)
├── MASTER_INIT.md          # Мастер-навык (полная версия)
├── README.md               # Этот файл
├── scripts/
│   └── ssi                 # CLI
├── skills/
│   ├── core/               # Критичные навыки
│   ├── automation/         # Автоматизация
│   ├── communication/      # Коммуникации
│   └── research/           # Исследования
└── references/
    ├── openclaw.md         # Специфика OpenClaw
    ├── opencode.md         # Специфика OpenCode
    └── generic.md          # Универсальные паттерны
```

## Troubleshooting

### Навык не устанавливается

- Проверить зависимости (requires в CATALOG.md)
- Проверить совместимость платформы
- Попробовать учителя: `--teacher pi`

### Нет учителя

```bash
# Установить pi
npm install -g @mariozechner/pi-coding-agent

# Или использовать ollama
brew install ollama
ollama pull llama3.2:3b
```

### Memory не работает

- Проверить права на запись
- Создать директории вручную:
  ```bash
  mkdir -p ~/.openclaw/workspace/memory
  touch ~/.openclaw/workspace/MEMORY.md
  ```

## Contributing

1. Fork репозитория
2. Создать branch: `git checkout -b feature/my-skill`
3. Добавить навык в `skills/`
4. Обновить `CATALOG.md`
5. Протестировать
6. Создать PR

## License

MIT

---

**Репозиторий:** https://github.com/ZhdanDesign/skills-init-repo
**Версия:** 0.1.0
**Обновлено:** 2026-03-01
