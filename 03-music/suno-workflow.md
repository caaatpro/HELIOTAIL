# Suno Workflow для HELIOTAIL

Полный справочник по работе с Suno на проекте. Собран из практики 2026-05-26 (первая продакшен-сессия). Версия Suno: **v5.5**, тариф: **Premier**.

## Лимиты Premier v5.5

| Поле | Лимит | Комментарий |
|---|---|---|
| **Style** | ~1000 символов | Первые 200-400 символов веcятся сильнее — info-dense начало решает |
| **Lyrics** | ~3000 символов | Stage directions в скобках едят лимит — держать их компактными |
| **Exclude Styles** | ~500 символов (?) | Comma-separated short descriptors |

При превышении Suno **молча обрезает**, не предупреждает.

## Принцип 1 — Style + Exclude Styles раздельно

В Suno v5.5 Advanced (Custom Mode) есть **два** поля для стиля:
- **Style** (основное) — что хотим (только позитивная часть)
- **Exclude Styles** (в More Options → раскрыть) — что НЕ хотим (negative comma-list)

**Exclude Styles работает на другом уровне модели** чем inline "NO X" внутри Style. Реально исключает дескрипторы из генерации, а не "советует избегать". **Это главный механизм против нежелательных элементов** (особенно crowd noise).

**Пример пары для соло-трека:**

```
[Style]
Solo female voice + acoustic piano only. Bedroom demo recording, voice
memo style, lo-fi intimate singer-songwriter. F minor, ~70 BPM, slow.
Russian. Whispered close-mic throughout, almost spoken delivery.

[Exclude Styles]
drums, bass, synth, pad, guitar, strings, electronic, second voice,
backing vocals, choir, harmonies, doubling, crowd, audience, cheering,
live recording, room ambience, applause, sing-along, festival, arena,
autotune, screams, growls, rap, American accent, alt-metal, upbeat
```

**Структура файла трека:** всегда два блока — `## Style для Suno` и `## Exclude Styles`. Применять ко всем трекам HELIOTAIL.

## Принцип 2 — Имена артистов в Style не использовать

Suno **тихо подменяет** имена групп/артистов на свою интерпретацию "похожих стилей" — возвращает системное сообщение: *"Artist names 'X, Y, Z' replaced. We don't reference artists directly..."*

В Style использовать **только descriptive vibe terms**:

| Не использовать | Использовать |
|---|---|
| "Sleep Token theatrical" | "modern progressive alt-metal with cinematic theatrical production, layered choir-style vocal stacks" |
| "Bad Omens clean" | "heavy melodic distorted guitars + emotional clean vocal soar" |
| "Bon Iver Holocene" | "layered vocal warmth with stacked falsetto-chest harmonies" |
| "Olafur Arnalds" | "intimate close-mic piano + sustained ambient synth pads, neoclassical electronic" |
| "Sigur Rós wordless" | "ethereal wordless vocal harmonies, ambient cinematic swells" |
| "The xx Crystalised" | "minimal alternating male+female dry close-mic duet, sparse arrangement" |
| "Vangelis cosmic pads" | "wide retrofuturistic analog synthesizer pads" |

**В секциях файла трека для людей** (Жанр и звук, Главный ход трека, Хуки) имена оставлять — это референс для тебя и меня. Запрет распространяется только на блок, который реально копипастится в Suno.

## Принцип 3 — Один слот Persona в v5.5 Advanced

Под Premier v5.5 Advanced — **только один Persona slot** (`+ Voice (New)` сверху формы). Мульти-Persona недоступен.

**Стратегия для HELIOTAIL:**
- По умолчанию — `MIYA_v1` (она протагонист 4 из 6 треков ХВОСТ-9, держит continuity)
- `NOX_v1` — только в ТРАНСЛЯЦИИ и СКОРО ВЕРНУСЬ (его соло / финальная анкер-фраза)
- Для остальных дуэтов — MIYA_v1, NOX через Style description (varies between gens, consistent within one gen)

**DAW-сшивка** (два прохода + Reaper/Logic) — для критичных дуэтов где нужны оба точных голоса:
- РАЗРЫВ (ХВОСТ-9 Эп.1)
- СЛЕД (ХВОСТ-9 Эп.6)
- СКОРО ВЕРНУСЬ (ГЕЛИОС Эп.6)

**Vocal Gender toggle** (More Options):
- Solo Мии трек → **Female** принудительно
- Solo NOX трек → **Male** принудительно
- Дуэт → **ни один** не выбран (даёт Suno слушать `[F]`/`[M]` теги в лирике)
- ⚠️ Если MIYA_v1 + **Female toggle** + `[M]` теги — Suno будет питч-шифтить мужские строки в Мию, не использовать свежий мужской голос. На дуэтах оставлять gender ни один.

## Принцип 4 — Гендер-теги в дуэтных секциях

Префиксы `Miya:` / `Nox:` Suno **не интерпретирует** как сигнал смены голоса. Использовать **`[F]` / `[M]` теги** перед каждой строкой:

```
[F] Ты спишь?
[M] Уже нет
[F] Долго ждала?
[M] Я знаю что недолго
```

Это работает в:
- Куплетах с чередованием
- Bridge-диалогах
- Interlude диалогах
- Intro spoken dialogue

**Дуэтные секции** (припев в унисон, pre-chorus с обоими) — без тегов, Suno делает оба голоса вместе.

## Принцип 5 — Trigger words в Style

Некоторые слова провоцируют Suno добавлять нежелательные элементы (особенно crowd noise / live feel). **Убирать или заменять:**

| Триггер (избегать) | Замена |
|---|---|
| `layered with self` | `double-tracked (one singer twice)` |
| `vocal stacks` | `subtle backing layer of same vocalist` |
| `choir-style harmonies` | (убрать упоминание layers вообще) |
| `soaring chorus` | `controlled rise` / `gentle dynamic rise` |
| `cinematic drums` | `programmed electronic drums` (NOT live, NOT arena) |
| `swell` | `gentle rise` |
| `stadium-like reverb` | `cinematic hall reverb (studio production, NOT live audience reverb)` |
| `theatrical` | оставлять можно — не триггерит crowd сам по себе |

## Принцип 6 — Позитивные studio-маркеры

Эти фразы в позитивной части Style **сильно** отбивают live-feel и crowd noise:

- `STUDIO BOOTH recording`
- `ASMR-close mic placement`
- `headphone-monitored`
- `bedroom production aesthetic`
- `ONE singer, ISOLATED vocal track`
- `recorded direct, no room sound`
- `programmed electronic drums NOT live drums NOT arena drums`
- `voice memo style`
- `lo-fi intimate demo recording`
- `singer-songwriter solo`

Эти маркеры работают **сильнее**, чем чистый negative list — они задают **контекст записи**, в котором crowd noise физически невозможен.

## Принцип 7 — Spoken секции / TTS / DAW pipeline

Suno **плохо делает** spoken-word с альтернацией голосов (intro-диалоги, outro-объявления). Особенно если просим robotic TTS (cyber voice Программы).

**Правило:** spoken-секции **выносить в DAW**, не пытаться через Suno.

**Pipeline:**

1. **В Suno генерим только основную музыку** — без spoken intro, без TTS outro. Финал на `[End]`.

2. **TTS-генерация для spoken** через внешние инструменты:
   - **Yandex SpeechKit** — лучший русский, есть robotic пресеты
   - **ElevenLabs** — voice cloning + robotic preset
   - **macOS `say` + vocoder** — бесплатный fallback

3. **Обработка TTS:**
   - Bandlimit-фильтр 300-3500 Гц (имитация интерком)
   - Лёгкий низкобитный дисторшн
   - **NO reverb** на TTS — звук "из динамика", не из пространства

4. **DAW сборка** (Reaper / Audacity / Logic):
   - TTS-intro (если есть)
   - Suno-track основная музыка
   - TTS-outro (если есть, например голос Программы)
   - Резкий cut в тишину после последнего слова — не fade

## Принцип 8 — Compact lyrics format

Stage directions в скобках **едят лимит** Lyrics. Держать их короткими:

❌ Так не делать:
```
[Verse 1 — Mia lead close-mic intimate, NOX echoes/finishes lines through soft neuro-link filter from WITHIN Mia's vocal space (not L/R panning — he's literally inside her head). Sub-bass drone continues, sparse glockenspiel motif underneath, no drums yet]
```

✅ Так делать:
```
[Verse 1 — F lead, M echoes via soft link-filter from within F's reverb]
```

Production-нюансы (что Suno должен и не должен делать в каждой секции) держать в **отдельных секциях файла трека**: "Главный ход трека", "Что проверить", "Возможные правки". Эти секции для нас, не для Suno.

## Принцип 9 — Outro обработка

Если outro — простое музыкальное завершение (как ПЕРВЫЙ ЗАКАТ: "Свет ушёл / Я ещё здесь" + fade) — оставить в Lyrics с тегом `[End]` после.

Если outro — диегетический элемент (TTS Программы, chime, специальный звук) — **вынести в DAW**, в lyrics завершить на `[End]` после Final Chorus.

В файле трека для DAW-outro делать отдельную секцию `## Outro (постпродакшен в DAW — не в Suno)` с инструкциями: какой звук, через какой TTS, какая обработка, как стыковать.

## Принцип 10 — Checklist перед каждой генерацией

1. ✅ **Persona прикреплён** в `+ Voice (New)` (MIYA_v1 или NOX_v1 в зависимости от трека)
2. ✅ **Vocal Gender toggle** правильно настроен (Female/Male/ни один — см. Принцип 3)
3. ✅ **Style** скопирован из файла (compact, без артист-имён, без trigger words, со studio-маркерами)
4. ✅ **Exclude Styles** скопирован из файла (comma-separated)
5. ✅ **Lyrics** скопированы из файла (compact stage directions, `[F]`/`[M]` теги где нужно)
6. ✅ **Song Title** — установлен вручную (иначе Suno возьмёт что-то странное из первой строки лирики)
7. ✅ Spoken intro/outro — **убраны** из лирики если планируется DAW-сшивка

## Что делать если не получилось

| Проблема | Решение |
|---|---|
| Шум толпы / подпевание | Усилить Exclude Styles, убрать trigger words из Style, добавить studio-маркеры. Если не помогает — **план Б**: убрать все инструменты кроме пианино + голос (acoustic demo aesthetic) |
| Мужские строки звучат как Мия в низком регистре | Снять Female toggle, оставить Vocal Gender ни один |
| Дуэт сливается в один голос | Использовать `[F]`/`[M]` теги в дуэтных секциях явно |
| Голос неузнаваемый между генерациями | Проверить что Persona прикреплён (часто забывают) |
| Голос артиста замещён "похожим стилем" | Убрать имена артистов из Style, заменить на descriptive vibe |
| Style/Lyrics не влезает | Compact: убрать stage directions из лирики, перенести в `## Главный ход трека` секцию файла; в Style — оставить только info-dense начало |
| Outro обрывается некрасиво | Убрать outro из Suno, сделать в DAW |
| Spoken dialogue Suno поёт | Spoken-секции в DAW через TTS |

## Структура файла трека (стандарт)

Каждый трек .md в проекте имеет следующую структуру:

```
# Track — "НАЗВАНИЕ"

[Эпизод инфо]

## Сцена
[Нарративный контекст]

## Жанр и звук
[Bulleted — BPM, тональность, инструментация, динамика, длина]
[Здесь можно использовать имена артистов для нашего референса]

## Style для Suno (copy-paste в поле Style — только позитив)
```
[compact ~600-1000 chars, descriptive vibe only, NO artist names, studio-markers]
```

## Exclude Styles (copy-paste в поле Exclude Styles в More Options)
```
[comma-separated short descriptors, ~200-500 chars]
```

## Лирика (copy-paste в Lyrics field Suno)
```
[compact lyrics with brief section tags, [F]/[M] in alternating sections, [End] at finish]
```

## Outro (постпродакшен в DAW — не в Suno)  [если применимо]
[Инструкции для DAW: TTS, chime, обработка, стыковка]

## Структура и тайминг
[Таблица: секция | длина | что звучит]

## Главный ход трека
[Архитектурные и драматургические нюансы — для нас, не для Suno]

## Хуки (для соцсетей / тизеров)
[Цитатник]

## Что проверить после первой генерации
[Чеклист]

## Возможные правки
[Fallback варианты если что-то не зашло]

## Связь с альбомным аркой
[Контекст в проекте]
```
