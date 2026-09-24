# mcpJihaz

Плагин для мебельных проектов JIHAZ: облачный MCP, 13 навыков агента, правила цеха, справочники и рецепты. Каждый пользователь входит в собственный аккаунт JIHAZ; в пакете нет ключей и пользовательских данных.

**Скачать:** [последний релиз](https://github.com/logiqakz/mcpJihaz-plugin/releases/latest) — файл `mcpJihaz-web-<версия>.zip`.

**Адрес сервера:** `https://jihaz-mcp-361817417980.us-central1.run.app/mcp`

## ChatGPT

MCP в ChatGPT подключается как **приложение**, а не из архива: плагин с `mcp.json` в вебе помечается «Desktop only».

1. Settings → **Apps** → Advanced settings → **Developer mode** (Business: только админ; Pro: только чтение; Free/Plus/Go: недоступно).
2. Settings → **Apps** → **Create**, адрес сервера выше, Scan Tools, Create. Админ Business публикует приложение на пространство.
3. Скиллы для пространства: Workspace settings → Plugins → Add → **Import marketplace** → `https://github.com/logiqakz/mcpJihaz-plugin`, либо Admin → Plugins → Upload plugin с этим ZIP.
4. В чате выберите приложение через `@` и войдите в JIHAZ при первом запросе.

Установка одной кнопкой для всех появится после публикации в каталоге OpenAI.

## Codex Desktop

В версиях с поддержкой маркетплейсов:

```sh
codex plugin marketplace add logiqakz/mcpJihaz-plugin
codex plugin add mcp-jihaz@jihaz-public
```

Или добавьте этот репозиторий через **Plugins → Add marketplace**, затем установите `mcp-jihaz`. Войдите в JIHAZ при первом запросе. Если CLI сообщает, что команды `codex plugin` нет, обновите клиент или подключите MCP вручную.

## Другие агенты

Установите каталог [`plugins/mcp-jihaz`](plugins/mcp-jihaz) как плагин Agent Plugins 1.0. Для Claude Code доступен совместимый манифест. Если клиент не поддерживает плагины, добавьте HTTP MCP по адресу выше, импортируйте папку `skills/` и передайте агенту `AGENTS.md`.

ZIP с тем же содержимым публикуется в [Releases](https://github.com/logiqakz/mcpJihaz-plugin/releases). В [инструкции](plugins/mcp-jihaz/README.md) есть подробности по конфигурации и OAuth.

Права на проекты и записи проверяет JIHAZ по аккаунту пользователя. Установка плагина сама по себе не даёт доступ к чужим заказам.
