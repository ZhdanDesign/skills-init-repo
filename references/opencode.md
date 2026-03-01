# OpenCode — Специфика платформы

## Структура

```
~/.config/opencode/
├── config.json          # Конфигурация
├── skills/              # Навыки
│   └── <skill-name>/
│       └── SKILL.md
└── history/             # История сессий
```

## Skills

### Установка

```bash
# Локально
cp -r skills/<name> ~/.config/opencode/skills/
```

### Формат

Аналогичен OpenClaw:
```markdown
---
name: skill-name
description: "Описание"
---

# Skill Name
```

## Agents

OpenCode имеет два типа агентов:
- **Plan Agent** — планирование, анализ
- **Build Agent** — реализация, кодинг

Переключение: `/agents`

## Models

- `/models` — список моделей
- `/model <id>` — выбор модели

## Sessions

- `/sessions` — список сессий
- `/new` — новая сессия

## Полезные навыки

| Навык | Назначение |
|-------|------------|
| openclaw-buddy | Обратная связь с OpenClaw |
| git | Git справочник |
| coding | Стиль кодинга |
