# Soul (ASTRA Desktop)

Десктопный AI-компаньон для общения с LLM. Не просто чат-бот — живая персона с памятью, эмоциями, голосом и характером, который растёт из диалога.

**Платформа:** Electron + React + Vite  
**Язык:** TypeScript / JavaScript

---

## Возможности

### Чат и модели

- **Локальные модели (Ollama)** — работа полностью офлайн
- **Облачные API:**
  - OpenAI-совместимые (OpenAI, Groq)
  - OpenRouter (Llama, Mistral, Qwen, Gemini и др.)
  - Google Gemini
- **Стриминг** ответов в реальном времени
- **Расширенный контекст** — суммаризация, рефлексии, дневник

### Души (персоны)

- Несколько **душ** — разных персонажей с собственными именами, характером и историей
- Каждая душа — это промпт, память и эмоциональные триггеры
- **Онбординг** — опросник для создания персоны под пользователя
- **Уровень связи (Bond)** — механика «близости» с душой

### Память

- **LTM (Long-Term Memory)** — долгосрочные факты с векторным поиском (sqlite-vec)
- Категории: о пользователе, об ассистенте, о ваших отношениях
- Автоматическое извлечение фактов из диалога
- Ручные команды: «Запомни …» / «Забудь …»
- **Дедупликация** — факты не дублируются

### Эмоции и тон

- Определение **эмоции** пользователя (радость, грусть, злость, тревога, благодарность и др.)
- **Тон** и **подтон** — влияют на стиль ответа души
- **Триггеры** — фразы → эмоция/тон с семантическим поиском (эмбеддинги)

### Голос

- **TTS (синтез речи):**
  - Microsoft Edge TTS (бесплатно, без ключа)
  - ElevenLabs
  - Coqui TTS
- **STT (распознавание):**
  - Whisper (локально через Ollama или API)
- Настройка голоса, скорости и тона

### Прочее

- **Напоминания** — «Напомни завтра …», «Через час …»
- **Spotify** — интеграция с плейлистами и текущим треком
- **Облачная синхронизация** — ПК как сервер, доступ с телефона/браузера
- **Логи памяти** — просмотр LTM, дублей и архивистских операций

---

## Требования

- **Windows 10/11** (сборка под Windows)
- **Node.js 20+** (для разработки)
- **Ollama** — для локальных моделей: [ollama.ai](https://ollama.ai)
  ```bash
  ollama pull gemma2
  ollama serve
  ```

---

## Установка и запуск

### Готовый установщик (рекомендуется)

1. Скачай **Soul Setup** из [релизов](https://github.com/Lifekor/MySoul.ai/releases)
2. Установи и запусти
3. При первом запуске: Настройки → выбери модель (Ollama/OpenRouter/Gemini и т.д.)

### Сборка из исходников

```bash
git clone https://github.com/Lifekor/Soul.git
cd Soul
npm install
npm run desktop   # build + Electron
```

Для разработки без пересборки:
```bash
npm run dev       # Vite
npm run electron  # Electron (в другом терминале)
```

---

## Скрипты

| Команда | Описание |
|---------|----------|
| `npm run dev` | Vite dev server (интерфейс в браузере) |
| `npm run dev:network` | Vite с доступом по сети (`VITE_NETWORK=1`) |
| `npm run build` | Сборка фронтенда в `dist/` |
| `npm run electron` | Запуск Electron |
| `npm run desktop` | `build` + Electron |
| `npm run dist` | Сборка установщика Windows (NSIS) |
| `npm run server` | Облачный сервер (порт 3848) |
| `npm run re-embed-vault` | Переиндексация vault (эмбеддинги) |
| `npm run re-embed-ltm` | Переиндексация LTM |
| `npm run restore-soul` | Восстановление души из бэкапа |

---

## Облачный режим

1. Запусти сервер: `npm run server` (порт **3848**)
2. В Soul: **Настройки → Облако** — укажи URL (`http://localhost:3848` или LAN IP)
3. Зарегистрируйся или войди
4. С телефона: открой тот же URL в браузере — чат и данные синхронизируются

**Доступ извне сети:** ngrok, Tailscale, Cloudflare Tunnel и т.п. — см. [docs/REMOTE_ACCESS.md](docs/REMOTE_ACCESS.md)

---

## Структура проекта

```
Soul/
├── electron/           # Основной процесс Electron
│   ├── main.js         # Точка входа
│   ├── chat-engine.js  # Чат, промпты, роутинг по провайдерам
│   ├── memory.js       # LTM, факты, recall
│   ├── storage.js      # SQLite, настройки, души
│   ├── archivists.js   # Саммари, дневник, рефлексии, personality
│   ├── providers/      # Gemini, TTS (Edge, ElevenLabs, Coqui), STT (Whisper)
│   ├── patterns/      # Регулярки: напоминания, remember, LTM, Spotify
│   └── prompts/       # Системные промпты, archivists
├── src/                # React-интерфейс
│   ├── components/     # Чат, настройки, голос, напоминания и т.д.
│   └── hooks/
├── server/             # Облачный сервер (Express)
├── shared/             # Общие модули (emotion, constants)
├── build/              # Иконка, артефакты сборки
├── public/             # Статика (копируется в dist)
└── docs/               # Документация
```

---

## Документация

- [REMOTE_ACCESS.md](docs/REMOTE_ACCESS.md) — доступ к Soul извне локальной сети
- [EMOTIONAL_PERSONALITY_DESIGN.md](docs/EMOTIONAL_PERSONALITY_DESIGN.md) — дизайн эмоциональной системы

---

## Лицензия и автор

**Soul** — проект [Lifekor](https://github.com/Lifekor).
