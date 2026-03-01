# OpenClaw — Специфика платформы

## Структура

```
~/.openclaw/
├── config.json          # Конфигурация
├── gateway.log          # Логи gateway
└── workspace/
    ├── MEMORY.md        # Долгосрочная память
    ├── AGENTS.md        # Правила агента
    ├── SOUL.md          # Личность
    ├── USER.md          # Информация о пользователе
    ├── TOOLS.md         # Локальные заметки
    ├── HEARTBEAT.md     # Периодические задачи
    ├── memory/          # Дневники
    │   └── YYYY-MM-DD.md
    └── skills/          # Кастомные навыки

/opt/homebrew/lib/node_modules/openclaw/skills/
                        # Системные навыки
```

## Skills

### Установка

```bash
# Через ClawHub
clawhub install <slug> --workdir ~/.openclaw/workspace

# Локально
cp -r skills/<name> ~/.openclaw/workspace/skills/

# Симлинк для системного доступа
ln -s ~/.openclaw/workspace/skills/<name> /opt/.../openclaw/skills/
```

### Формат

```markdown
---
name: skill-name
description: "Описание. Использовать когда: (1) условие, (2) условие."
---

# Skill Name

Инструкции...
```

## Memory

- **MEMORY.md** — только в main session (direct chat)
- **memory/YYYY-MM-DD.md** — дневники
- **HEARTBEAT.md** — периодические проверки

## Tools

- `openclaw gateway status|start|stop|restart`
- `openclaw status`
- `/model <model_id>` — смена модели

## MCP Support

Через mcporter:
```bash
mcporter list
mcporter call <server.tool> key=value
```

## Полезные навыки

| Навык | Назначение |
|-------|------------|
| coding-agent | Делегирование кодинга |
| github | PR/Issues/CI |
| obsidian | Заметки |
| apple-notes | Apple Notes |
| imsg | iMessage |
| tavily | Веб-поиск |
| peekaboo | macOS UI |
