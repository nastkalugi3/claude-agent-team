# Команда ИИ-агентов с дирижёром (Claude Code)

Ты даёшь задачу дирижёру. Он сам решает, кому из агентов её отдать, запускает их
(параллельно, если можно), проверяет результат через ревьюера и отдаёт тебе готовое.
Всё работает на твоём компьютере: агенты читают и пишут файлы, запускают код и ищут в интернете.

## Состав
- `CLAUDE.md` — правила дирижёра (главный Claude читает их автоматически)
- `.claude/agents/` — 13 агентов в 8 отделах:
  - Исследования и наука: researcher, scientist
  - Аналитика и DS: data-scientist, data-analyst
  - Разработка: developer, frontend-developer
  - Дизайн: designer
  - Тексты: copywriter, editor
  - Стратегия и философия: strategist, philosopher
  - Образование: teacher
  - Контроль качества: reviewer
- `.claude/commands/team.md` — команда `/team <задача>`
- `.claude/commands/council.md` — команда `/council <вопрос>`: совет из 3 экспертов для важных решений
- `PERSONALIZATION.md` — настройка Claude в обычном чате (claude.ai)
- `output/` — сюда складываются результаты

## Установка (один раз)
1. Установи Claude Code: https://docs.claude.com/en/docs/claude-code (нужен Node.js 18+).
   Есть расширение для VS Code.
2. Распакуй архив в любую папку, например `~/ai-team`.
3. Открой терминал в этой папке и запусти `claude`.
4. Проверь, что агенты видны: введи `/agents`.

Хочешь, чтобы команда работала в любом проекте: скопируй `.claude/agents/*` и
`.claude/commands/*` в `~/.claude/agents/` и `~/.claude/commands/`.

## Как пользоваться
```
/team сделай прогноз оттока по data/churn.csv, сравни 3 модели, напиши README
/team найди актуальные вакансии junior data scientist в LA и сделай сводку требований
/team план урока по теме «Тригонометрический круг», 10 класс, с самостоятельной на 10 минут
/team сделай сайт-портфолио с моими DS-проектами и тексты к нему
/council стоит ли мне идти в магистратуру или сразу искать работу в DS?
```
Можно и без команды, обычным текстом — дирижёр всё равно следует CLAUDE.md.
Конкретного агента можно позвать по имени: «пусть reviewer проверит train.py».

## Подключение навыков и готовых агентов с GitHub
Внутри Claude Code:
```
/plugin marketplace add anthropics/skills
/plugin marketplace add anthropics/knowledge-work-plugins
/plugin marketplace add wshobson/agents
/plugin marketplace add VoltAgent/awesome-claude-code-subagents
/plugin
```
В меню `/plugin` выбираешь, что поставить. Ставь точечно (2–5 плагинов),
иначе дирижёр путается в сотне похожих агентов.

Полезное для тебя:
- `anthropics/skills` — официальные навыки: docx, xlsx, pptx, pdf, frontend-design и др.
- `anthropics/knowledge-work-plugins` — официальные плагины по профессиям: data, engineering, design, marketing, product-management
  (подробнее в PERSONALIZATION.md)
- wshobson/agents → `python-development`, `data-validation-suite`, плагин MLOps (точное имя смотри в `/plugin`)
- VoltAgent → `voltagent-data-ai`, `voltagent-research`, `voltagent-meta` (оркестраторы)

## Важно
- Субагент не может запускать других субагентов. Координирует только дирижёр.
- Каждый агент стартует «с нуля», поэтому дирижёр передаёт ему весь контекст.
- Больше агентов → больше токенов. Простые задачи дирижёр делает сам.
- Результат всё равно проверяй, особенно цифры и метрики.
