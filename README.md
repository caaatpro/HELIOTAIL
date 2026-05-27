# HELIOTAIL — проектная папка

**Имя проекта:** HELIOTAIL ⭐ (резерв — CISLUNAR)
Дуэт двух цифровых сознаний: **Мия** (женский вокал) + **NOX** (мужской вокал, рабочее имя).
Русскоязычный modern progressive alt / theatrical alt-metal.

**Альбомы:**
- **ХВОСТ-9** (дебютный EP, **5 эпизодов** — v2, genre whiplash) — разрыв нейро-линка и принятие. Тексты v2 готовы ✅
- **ГЕЛИОС** (второй EP, 6 эпизодов, prequel) — как они дошли до миссии, греческая трагедия. Story bible готов, тексты TBD

## Структура

### [01-concept/](./01-concept/) — общая концепция артиста

- [01-project-concept.md](./01-concept/01-project-concept.md) — концепция дуэта, жанр, имя артиста и альбомов, палитра
- [02-name-shortlist.md](./01-concept/02-name-shortlist.md) — пул имён для проекта/дуэта

> Story bible каждого альбома живёт внутри папки альбома (например, [ХВОСТ-9 story bible](./04-albums/01-khvost-9/story-bible.md)).

### [02-characters/](./02-characters/) — идентичности персонажей

- [miya.md](./02-characters/miya.md) — мастер-промпт идентичности Мии (оригинал)
- [miya-nano-banana.md](./02-characters/miya-nano-banana.md) — адаптированный промпт Мии под Nano Banana
- [nox.md](./02-characters/nox.md) — мастер-промпт идентичности NOX
- [nox-nano-banana.md](./02-characters/nox-nano-banana.md) — адаптированный промпт NOX под Nano Banana

### [03-music/](./03-music/) — звук, голоса, Suno

- [pipeline.md](./03-music/pipeline.md) — Suno → постобработка → мастеринг → дистрибуция
- [suno-workflow.md](./03-music/suno-workflow.md) — **главный практический справочник** по работе с Suno: лимиты, Persona, Style+Exclude, trigger words, DAW pipeline, чеклисты
- [voice-profiles-suno.md](./03-music/voice-profiles-suno.md) — фиксация голосов Мии и NOX в Suno (Personas + style + tags)
- [voice-casting-miya.md](./03-music/voice-casting-miya.md) — кастинг голоса Мии: тестовая лирика + 3 варианта Style
- [voice-casting-nox.md](./03-music/voice-casting-nox.md) — кастинг голоса NOX: тестовая лирика + 3 варианта Style

### [04-albums/](./04-albums/) — альбомы

Каждый альбом — своя подпапка со story-bible, треками и album-specific материалами. Нумерация треков по эпизодам сюжетной арки альбома.

#### [01-khvost-9/](./04-albums/01-khvost-9/) — Альбом #1: ХВОСТ-9 ✅ (v2 — 5 треков, genre whiplash)

- [story-bible.md](./04-albums/01-khvost-9/story-bible.md) — сценарий альбома: мир, 5 эпизодов, мотивы
- [01-razryv.md](./04-albums/01-khvost-9/01-razryv.md) — дуэт, открывающий, peak alt-metal (heaviest, B minor)
- [02-sorvu.md](./04-albums/01-khvost-9/02-sorvu.md) — Мия соло, **industrial rage** (fastest, G minor, ~135 BPM)
- [03-translyaciya.md](./04-albums/01-khvost-9/03-translyaciya.md) — NOX соло, **обманчиво-светлый synth-pop** (D major, единственный мажор)
- [04-fragment.md](./04-albums/01-khvost-9/04-fragment.md) — **параллельный дуэт**, hard L/R panning, alt-rock с электронкой (E minor)
- [05-sled.md](./04-albums/01-khvost-9/05-sled.md) — дуэт, финал, theatrical пик (F# minor)
- [_archive/](./04-albums/01-khvost-9/_archive/) — вырезанные из v1: ПЕРВАЯ ТИШИНА, ПОМЕХИ В ГОЛОВЕ

#### [02-gelios/](./04-albums/02-gelios/) — Альбом #2: ГЕЛИОС (в разработке)

- [story-bible.md](./04-albums/02-gelios/story-bible.md) — prequel к ХВОСТ-9, 6 эпизодов до миссии, заканчивается стартом корабля
- [01-vdvoem-v-golove.md](./04-albums/02-gelios/01-vdvoem-v-golove.md) — Эп.1 ВДВОЁМ В ГОЛОВЕ (дуэт, intimate indie/ambient, warm opener) ✅
- Эпизоды TBD: ПРЕДЛОЖЕНИЕ → ВЫБОР → РЕПЕТИЦИЯ ОДИНОЧЕСТВА → ПОСЛЕДНИЙ ДЕНЬ → СКОРО ВЕРНУСЬ

#### [singles/](./04-albums/singles/) — синглы вне альбомов

- [README.md](./04-albums/singles/README.md) — индекс синглов и парковочные идеи
- [01-pervyy-zakat.md](./04-albums/singles/01-pervyy-zakat.md) — **"ПЕРВЫЙ ЗАКАТ"** ✅ Mia solo, intimate indie/ambient, межэпизод между РАЗРЫВом и ПЕРВОЙ ТИШИНОЙ

### [05-visuals/](./05-visuals/) — генерация изображений

- [nano-banana-workflow.md](./05-visuals/nano-banana-workflow.md) — workflow фиксации эталона и генерации сцен
- [scene-library.md](./05-visuals/scene-library.md) — библиотека из 20 типовых сцен

## Текущий статус

- [x] Концепция артиста (дуэт, два вокала, нарратив "потерянной связи")
- [x] Мастер-промпт Мии
- [x] Мастер-промпт NOX
- [x] Имя проекта-дуэта — HELIOTAIL (предварительно, нужна финальная проверка занятости)
- [x] Voice-профили для Suno (Мия + NOX + дуэт) — спецификация
- [x] Story bible: мир, 6 эпизодов v1 → переработан в 5 эпизодов v2 (genre whiplash)
- [x] Все 5 треков v2 написаны (РАЗРЫВ ✅ + СОРВУ ✏️ + ТРАНСЛЯЦИЯ v2 ✏️ + ФРАГМЕНТ v2 ✏️ + СЛЕД ✅)
- [x] Кастинг-сессия голосов проведена, варианты выбраны
- [x] Имя альбома выбрано: ХВОСТ-9 (нужна проверка занятости на Spotify/Apple Music)
- [ ] Создать Suno Persona MIYA_v1 из выбранного варианта
- [ ] Создать Suno Persona NOX_v1 из выбранного варианта
- [ ] HELIOTAIL: дочекать Apple Music, соцсети, домен, торговый знак
- [ ] Утвердить имя NOX (или выбрать альтернативу: VEX, RYO, ASH)
- [ ] Эталонный портрет Мии в Nano Banana — сгенерировать 6-8 раз, отобрать canonical
- [ ] Эталонный портрет NOX в Nano Banana — сгенерировать 6-8 раз, отобрать canonical
- [ ] Зафиксировать пианинный мотив EP (короткая фигура 3-4 ноты, лейтмотив)
- [ ] Финализировать порядок релиза (по нарративу или сингл-стратегия)
- [ ] Сгенерировать все 5 треков v2 в Suno с залоченными Personas
- [ ] Дистрибьютор и оформление прав

## Следующий шаг

Зафиксировать Personas MIYA_v1 и NOX_v1 из выбранных вариантов кастинга. Дальше — генерить все 6 треков в Suno с залоченными голосами в одной продакшен-сессии (Suno даёт более консистентные результаты в рамках одной сессии).



Синглы
Разрыв - пресобрать, попробовать разбавить крики своим голосом
Первая тишина - заменить пианино, пересобрать
След