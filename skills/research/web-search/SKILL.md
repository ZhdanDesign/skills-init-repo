---
name: web-search
description: Веб-поиск через Tavily API (AI-optimized). Использовать для поиска актуальной информации в интернете.
---

# Web Search — Tavily

## Использование

```bash
# Активировать venv
source ~/.openclaw/workspace/skills/tavily/venv/bin/activate

# Поиск
python3 ~/.openclaw/workspace/skills/tavily/scripts/tavily_search.py "query"

# С параметрами
python3 ~/.openclaw/workspace/skills/tavily/scripts/tavily_search.py "query" \
  --max-results 5 \
  --search-depth advanced \
  --include-domains example.com,docs.com
```

## Параметры

| Параметр | Описание | Default |
|----------|----------|---------|
| `--max-results N` | Кол-во результатов | 5 |
| `--search-depth` | basic / advanced | basic |
| `--include-domains` | Фильтр доменов | - |
| `--json` | Сырой JSON | false |

## API Key

Файл: `~/.openclaw/tavily_key`
Получить: https://app.tavily.com/api-keys

```bash
# Setup
bash ~/.openclaw/workspace/skills/tavily/scripts/setup_key.sh
```

---

**Альтернативы:** Brave Search (требует API key), DuckDuckGo (без API)
