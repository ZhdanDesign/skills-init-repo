# CATALOG.md — Каталог навыков

> Машиночитаемый каталог всех доступных навыков. Агент парсит этот файл для инициализации.

---

## Формат записи

```yaml
- id: unique-id
  name: Human Name
  category: core|communication|research|automation|creative
  description: Краткое описание
  platforms: [openclaw, opencode, codex, claude, generic]
  requires: []           # Зависимости от других навыков
  provides: []           # Что даёт (теги возможностей)
  priority: critical|high|medium|low
  source: local|url|github
  path: skills/git/SKILL.md  # Путь локально или URL
```

---

## Core — Базовые навыки

```yaml
- id: master-init
  name: Master Init
  category: core
  description: Навык самообучения для агентных систем — читает CATALOG.md, анализирует потребности, создаёт навыки
  platforms: [generic]
  requires: []
  provides: [self-learning, initialization, skill-creation]
  priority: critical
  source: local
  path: skills/core/master-init/SKILL.md

- id: git
  name: Git
  category: core
  description: Полный справочник Git — essentials, workflows, advanced, recovery
  platforms: [generic]
  requires: []
  provides: [version-control, branching, recovery, collaboration]
  priority: critical
  source: local
  path: skills/core/git/SKILL.md

- id: coding-style
  name: Coding Style Memory
  category: core
  description: Память стиля кодинга — учится предпочтениям разработчика
  platforms: [generic]
  requires: []
  provides: [coding-preferences, style-consistency]
  priority: high
  source: local
  path: skills/core/coding-style/SKILL.md

- id: memory-management
  name: Memory Management
  category: core
  description: Управление памятью агента — долгосрочная, краткосрочная, контекст
  platforms: [generic]
  requires: []
  provides: [memory, context-persistence, recall]
  priority: critical
  source: local
  path: skills/core/memory/SKILL.md

- id: self-recovery
  name: Self Recovery
  category: core
  description: Аварийное восстановление при сбоях — fallback модели, restart, repair
  platforms: [openclaw]
  requires: []
  provides: [resilience, fallback, recovery]
  priority: critical
  source: local
  path: skills/core/self-recovery/SKILL.md
```

---

## Communication — Коммуникации

```yaml
- id: messaging
  name: Messaging
  category: communication
  description: Отправка сообщений — Telegram, WhatsApp, Discord, Slack, Signal
  platforms: [openclaw]
  requires: []
  provides: [messaging, notifications, alerts]
  priority: high
  source: local
  path: skills/communication/messaging/SKILL.md

- id: email
  name: Email
  category: communication
  description: Работа с email — Gmail, IMAP, отправка, чтение, поиск
  platforms: [generic]
  requires: []
  provides: [email, gmail, imap]
  priority: medium
  source: local
  path: skills/communication/email/SKILL.md

- id: imessage
  name: iMessage
  category: communication
  description: iMessage/SMS на macOS — чтение, отправка, поиск
  platforms: [openclaw]
  requires: []
  provides: [imessage, sms, macos]
  priority: medium
  source: local
  path: skills/communication/imessage/SKILL.md
```

---

## Research — Исследования

```yaml
- id: web-search
  name: Web Search
  category: research
  description: Веб-поиск — Tavily, Brave, Google, DuckDuckGo
  platforms: [generic]
  requires: []
  provides: [search, web, research]
  priority: critical
  source: local
  path: skills/research/web-search/SKILL.md

- id: web-scrape
  name: Web Scraping
  category: research
  description: Извлечение контента с веб-страниц
  platforms: [generic]
  requires: []
  provides: [scraping, extraction, content]
  priority: medium
  source: local
  path: skills/research/web-scrape/SKILL.md

- id: summarize
  name: Summarize
  category: research
  description: Summarization текстов, видео, подкастов
  platforms: [generic]
  requires: []
  provides: [summarization, extraction, transcripts]
  priority: medium
  source: local
  path: skills/research/summarize/SKILL.md
```

---

## Automation — Автоматизация

```yaml
- id: github-integration
  name: GitHub Integration
  category: automation
  description: Работа с GitHub через gh CLI — репозитории, issues, PRs, CI/CD. Использует существующие credentials.
  platforms: [generic]
  requires: []
  provides: [github, git, repositories, issues, pull-requests, ci-cd]
  priority: critical
  source: local
  path: skills/automation/github/SKILL.md

- id: mcp
  name: MCP Support
  category: automation
  description: Model Context Protocol — работа с MCP серверами
  platforms: [openclaw, claude, cursor]
  requires: []
  provides: [mcp, tools, integrations]
  priority: high
  source: local
  path: skills/automation/mcp/SKILL.md

- id: shell-exec
  name: Shell Execution
  category: automation
  description: Безопасное выполнение shell команд
  platforms: [generic]
  requires: []
  provides: [shell, commands, automation]
  priority: critical
  source: local
  path: skills/automation/shell/SKILL.md

- id: cron
  name: Cron Jobs
  category: automation
  description: Планирование задач — cron, periodic checks
  platforms: [openclaw]
  requires: []
  provides: [scheduling, automation, periodic]
  priority: medium
  source: local
  path: skills/automation/cron/SKILL.md
```

---

## Creative — Креатив

```yaml
- id: visual-explainer
  name: Visual Explainer
  category: creative
  description: Генерация HTML диаграмм с Mermaid
  platforms: [generic]
  requires: []
  provides: [diagrams, visualization, html]
  priority: medium
  source: local
  path: skills/creative/visual-explainer/SKILL.md

- id: tts
  name: Text-to-Speech
  category: creative
  description: Озвучка текста — ElevenLabs, OpenAI, локальные
  platforms: [generic]
  requires: []
  provides: [speech, audio, voice]
  priority: low
  source: local
  path: skills/creative/tts/SKILL.md

- id: image-gen
  name: Image Generation
  category: creative
  description: Генерация изображений — DALL-E, Midjourney, Stable Diffusion
  platforms: [generic]
  requires: []
  provides: [images, generation, art]
  priority: low
  source: local
  path: skills/creative/image-gen/SKILL.md
```

---

## External Sources — Внешние источники

```yaml
# ClawHub — каталог skills для OpenClaw
- id: clawhub-catalog
  name: ClawHub
  category: external
  description: Каталог навыков для OpenClaw
  platforms: [openclaw]
  source: url
  path: https://clawhub.com/api/catalog.json
  format: clawhub

# AgenticSkills — curated skills для coding agents
- id: agentic-skills
  name: AgenticSkills
  category: external
  description: 143+ curated skills для Claude Code, Codex, Cursor
  platforms: [opencode, codex, claude, cursor]
  source: url
  path: https://agenticskills.io/catalog.json
  format: agenticskills

# MCP Ecosystem — MCP servers
- id: mcp-servers
  name: MCP Servers
  category: external
  description: 8000+ MCP servers
  platforms: [claude, cursor, windsurf]
  source: url
  path: https://findmcp.dev/api/servers.json
  format: mcp
```

---

## Presets — Готовые наборы

```yaml
- id: preset-minimal
  name: Minimal
  description: Минимальный набор для начала работы
  includes: [git, memory-management, web-search, shell-exec]
  
- id: preset-developer
  name: Developer
  description: Для разработчика
  includes: [master-init, git, github-integration, coding-style, memory-management, web-search, shell-exec, mcp]

- id: preset-assistant
  name: Personal Assistant
  description: Персональный ассистент
  includes: [master-init, git, memory-management, messaging, email, web-search, cron, tts]

- id: preset-researcher
  name: Researcher
  description: Для исследований
  includes: [master-init, git, memory-management, web-search, web-scrape, summarize]
```

---

## Meta — Метаданные каталога

```yaml
version: 0.1.0
updated: 2026-03-01
maintainer: Hoton + Zhdan
repo: https://github.com/YOUR/skills-init-repo
```
