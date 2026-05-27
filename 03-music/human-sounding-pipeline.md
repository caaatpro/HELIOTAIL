# Production Pipeline — «неотличимо от живого»

Глубокий гайд по post-production AI-треков, чтобы они звучали как запись живого исполнителя. Дополняет [pipeline.md](pipeline.md) (overview) и [suno-workflow.md](suno-workflow.md) (Suno-специфика).

> Этот документ — про **post-Suno работу**: как из generated MP3 сделать трек, который не сразу выдаёт себя как AI. Если нужен общий путь от идеи до стриминга — смотри [pipeline.md](pipeline.md).

> **DAW для HELIOTAIL — Logic Pro X** ($249, mac-native, Apple Silicon-only фичи, выбран Андреем 2026-05-28). Mastering Assistant встроен — заменяет ручной мастер-бас. Stem Splitter встроен. Lifetime free updates через App Store.
>
> Step-by-step ниже — под Logic Pro. REAPER-вариант оставлен как альтернатива для тех у кого нет mac.

## Реалистичный прогноз

Не для всех треков «неотличимо» одинаково достижимо. Зависит от инструментации:

| Тип трека | Достижимая «неотличимость» | Почему |
|---|---|---|
| **Felt piano + intimate voice** (как «первый закат») | 85-95% | Простая инструментация, voice-memo вайб прощает артефакты |
| **Acoustic singer-songwriter** (гитара + голос) | 80-90% | Аналогично, но гитара звучит более «генерик» у Suno |
| **Cinematic indie** (синты + пианино + soft drums) | 70-85% | Барабаны выдают AI-природу, синты часто стерильные |
| **Alt-metal / heavy band** (как Альбом 1) | 50-70% | Барабаны и гитары — самые сложные. Опытное ухо вычислит |
| **Электронщина / synth-pop** | 60-80% | Парадокс: «AI-вкус» в этом жанре уже стал нормой |

**Главный лимит:** AI-вокал (даже после полной обработки) можно вычислить опытным ухом по микро-артефактам в согласных и переходах. Чтобы пробить этот потолок — **переписать вокал собственным голосом**, используя Suno как референс.

## Три стратегии генерации

| Подход | Контроль | Сложность | Когда выбирать |
|---|---|---|---|
| **A. Whole-track лотерея** | низкий | минимум | прототип, тест концепта |
| **B. Section-by-section + Extend** | высокий | средне | финальная сборка, нужны точные переходы |
| **C. Гибрид (лотерея + замена кусков)** | средний | средне | **дефолт для большинства треков** |

**Стратегия C — рекомендованный дефолт:**

1. Сгенерить **4-6 полных версий** одной лирики (вариативность Suno)
2. Выбрать **лучший голос** (может быть в одной версии) и **лучшую аранжировку** (может быть в другой)
3. Если бридж/припев где-то проинтонирован сильно — этот кусок взять оттуда через **Replace Section** или вручную в DAW
4. Если общая структура одной версии 90% хороша — её основа, заменяешь только слабые места

**Когда стратегия B (sections):** Если трек длинный (>4 мин), сложная структура, нужна точная стыковка между секциями. Для bedroom voice-memo (<3:30) — overkill.

## Полный pipeline (7 шагов)

```
1. Suno генерация (4-6 версий с Persona)
   ↓
2. Cherry-pick кусков + базовый выбор
   ↓
3. Stem separation (вокал / инструментал отдельно)
   ↓
4. Cleanup вокала (артефакты, шум, резонансы)
   ↓
5. Замена / усиление инструментов (live VST или re-record)
   ↓
6. Human-имитация (дыхание, room tone, micro-pitch)
   ↓
7. Mix + Master
```

## Стек инструментов

### Бесплатный полный стек (хватит для старта)

| Категория | Инструмент | Заметка |
|---|---|---|
| DAW | **REAPER** | $60 пожизненно, 60 дней trial |
| Stem separation | **UVR (Ultimate Vocal Remover)** | GUI, модели MDX-Net, Demucs |
| Cleanup | **bertom Denoiser** | замена RX для базовых задач |
| Piano VST | **Spitfire LABS Soft Piano** | felt piano качества, ноль рублей |
| EQ | **TDR Nova** | динамический EQ |
| Compression | **TDR Kotelnikov** | mastering-уровень |
| Reverb | **Valhalla Supermassive** | один из лучших free reverb вообще |
| Saturation | **Klanghelm IVGI** | tape warmth |
| Pitch correction | **Graillon 2** | бесплатная альтернатива Auto-Tune |
| Limiter | **TDR Limiter 6 GE** | для мастеринга |

### Платный апгрейд (когда серьёзно)

| Категория | Инструмент | Цена | Зачем |
|---|---|---|---|
| Audio repair | **iZotope RX Standard** | $400 | спасает любые артефакты |
| Felt piano | **Spitfire Felt Piano** или **NI Una Corda** | $30 / $170 | референсный тембр |
| Pitch | **Melodyne Studio** | $849 | «ну точно живой певец» уровень |
| EQ + Comp | **FabFilter Pro-Q3 + Pro-C2** | $350 | стандарт индустрии |
| Resonance | **Soothe2** | $210 | критично для AI-вокала |
| Reverb | **Valhalla VintageVerb** | $50 | лучший reverb за свои деньги |

### Logic Pro X native plugins (⭐ рекомендуется для mac, Apple Silicon)

Logic Pro X ($249 разово, lifetime free updates через App Store) — основной выбор DAW для HELIOTAIL. На Apple Silicon (M1/M2/M3/M4) **Mastering Assistant** и **Stem Splitter** работают полноценно и заменяют большую часть post-production цепочки одним кликом.

| Категория | Logic native плагин | Альтернатива (если нет Logic) |
|---|---|---|
| DAW | **Logic Pro X** ($249 разово, App Store, lifetime updates) | REAPER ($60, универсальный) |
| **AI auto-master** | **Mastering Assistant** (один клик → Analyze → 3 слайдера) | Ozone Master Assistant ($249) |
| Stem separation | **Stem Splitter** (Apple Silicon-only, в редакторе аудио) | UVR (free) |
| EQ | **Channel EQ** (8-band parametric) | TDR Nova / FabFilter Pro-Q |
| Compression | **Compressor** (VCA/FET/Optical/Class A модели) | TDR Kotelnikov / Pro-C |
| Multiband compression | **Multipressor** | FabFilter Pro-MB |
| Limiter | **Adaptive Limiter** | TDR Limiter 6 |
| Pitch correction | **Flex Pitch** (Melodyne-стиль) | Melodyne / Graillon |
| Reverb (algorithmic) | **ChromaVerb** | Valhalla Supermassive |
| Reverb (convolution) | **Space Designer** + Apple IR library | Valhalla Convolution |
| Tape saturation | **Tape Delay** (saturation mode), **Phat FX** | Klanghelm IVGI / Decapitator |
| Live drums (AI) | **Drummer** (AI session drummer, выбор по жанрам) | (нет аналога — это эксклюзив Logic) |
| LUFS metering | встроенный **Loudness Meter** | YouLean Loudness Meter |
| Pitch shift / time stretch | **Flex Time** | Stock REAPER stretching |

**Что докупать вне Logic:** в большинстве случаев — ничего. Опционально free AU плагины — Valhalla Supermassive (более интересные reverb-character чем ChromaVerb), TDR Nova (dynamic EQ против резонансов AI-вокала).

**Минусы Logic для AI-cleanup:**
- Mastering Assistant требует **Apple Silicon** — на Intel Mac недоступен
- Стандартный Logic Drummer не работает с русскоязычными жанрами prog-alt (нет пресета "Sleep Token-style") — но live drums для heavy треков всё равно сильный апгрейд
- Steeper learning curve чем GarageBand (но проще FL для начинающих)

## Step-by-step (Logic Pro X) для bedroom voice-memo трека ⭐

**Основной recommended pipeline для HELIOTAIL** на 2026-05-28+. Используя «первый закат» как пример.

### Шаг 1 — Suno генерация

Аналогично всем вариантам: минимум 4-6 версий, отбор по конкретным моментам (бридж проинтонирован чисто? пианино без щелчков? шёпот не сорвался?).

### Шаг 2 — Создание проекта

1. `File → New → Empty Project`
2. Sample rate: 48 kHz (`File → Project Settings → Audio`)
3. Drag `.wav` из Suno прямо в Logic — он создаст Audio track автоматически

### Шаг 3 — Минимальная обработка через Mastering Assistant (release-ready за 2 минуты)

**Это весь "минимум-effort pipeline" в Logic — один плагин на master, и трек готов к экспорту.**

1. Откроется Mixer (`X`). Выбери канал **Stereo Out** (мастер-бас, самый правый)
2. В Audio FX слот → `Mastering → Mastering Assistant`
3. Нажми **Analyze** в плагине → запусти playback всего трека → дождись окончания (Mastering Assistant слушает весь файл, ~30-60 секунд для 3-минутного трека)
4. После анализа подкрути 3 слайдера в плагине:
   - **Loudness:** для intimate (ПЕРВЫЙ ЗАКАТ) — низкий, target ~–16 LUFS; для general (alt-metal треков) — средний, target ~–14 LUFS
   - **Character:** `Clean` (минимум обработки) / `Warm` (analog-style, **дефолт для HELIOTAIL voice-memo**) / `Valve` (tube-style) / `Punchy` (агрессивный)
   - **Width:** оставь среднее (для intimate треков не расширяй; для **ФРАГМЕНТа** с hard L/R panning — НЕ ТРОГАТЬ width, чтобы не сломать стерео-метафору)
5. `File → Bounce → Project or Section` → формат WAV 24-bit для DistroKid, дополнительно MP3 320 kbps для соцсетей

**Всё.** Mastering Assistant сам выставил EQ, многополосную компрессию, лимитер. Никаких ручных EQ-band-настроек, никаких mastering-пресетов руками. Если результат устраивает — это весь твой pipeline.

### Шаг 4 — Если хочешь больше: Stem Splitter

Раз хочешь обработать стемы отдельно (vocal и piano по отдельным цепочкам):

1. Правый клик на Audio Clip → `Edit in Stem Splitter`
2. Выбери mode: `Vocals / Drums / Bass / Other` (для intimate piano+voice → `Vocals + Other`)
3. Logic создаст новые tracks с отдельными stems
4. Vocal track на `Track 1`, Other (piano) на `Track 2`, новый Bus 1 для reverb

### Шаг 5 — Vocal chain (если делаешь больше минимума)

На vocal track в Channel Strip Audio FX:

| Слот | Logic native плагин | Параметры | Зачем |
|---|---|---|---|
| 1 | **Channel EQ** | HPF 80 Hz / cut –3 dB at 250 Hz / shelf +1 dB at 12 kHz | базовый тон |
| 2 | **DeEsser 2** | 5-8 kHz зона, threshold по слуху | убрать AI-шипение |
| 3 | **Compressor** (VCA model) | ratio 4:1, attack 20ms, release 200ms | выравнивание динамики |
| 4 | **Channel EQ** (второй, dynamic mode) | найти резонанс 2-4 kHz, gain reduction 3-5 dB | замена Soothe2 — против "пластика" AI |
| 5 | **Send** → Bus 1 (reverb) | send level ~12% | пространство |

### Шаг 6 — Piano chain (Вариант B без MIDI-клавы)

На piano track:

| Слот | Logic native плагин | Параметры | Зачем |
|---|---|---|---|
| 1 | **Channel EQ** | HPF 100 Hz / low-shelf –2 dB at 8 kHz | мягкость |
| 2 | **Phat FX** или **Tape Delay** (saturation mode) | drive 25% | tape warmth |
| 3 | **Chorus** | depth 1-2% only | едва ощутимый live feel |
| 4 | **Send** → Bus 1 | send level ~18% | больше пространства чем у вокала |

### Шаг 7 — Reverb bus (Bus 1)

- **ChromaVerb** на insert
- Preset `Small Room` или `Vocal Studio Reverb`, decay 1.2s
- Mix 100% (sends контролируют объём)
- Альтернатива: **Space Designer** с IR-семплом реальной комнаты (Apple включает Apple IR Library)

### Шаг 8 — Human-имитация (новый Audio track для textures)

Минимум 3 элемента, **обязательно** room tone:

| Элемент | Где взять / как в Logic | Уровень |
|---|---|---|
| **Breath sounds** | Запиши на iPhone (Voice Memos) → drag .m4a в Logic между фразами | –24 dB |
| **Room tone** | Запиши 30 сек тишины в комнате на iPhone, drag в Logic, зациклишь под весь трек | –50 dB |
| **Micro-pitch jitter** | **Flex Pitch** на vocal track → расстроить идеальные ноты ±5 cents | едва заметно |
| Mouth clicks (опц.) | Logic Sampler с .wav cliks, импорт между фразами | –30 dB |
| AC hum (опц.) | Logic `Test Oscillator` → 50 Hz sine, очень тихо фоном | –55 dB |

**Главное правило:** между фразами **никогда не должно быть цифровой тишины 0 dB**. Room tone льёт под весь трек.

### Шаг 9 — Финальный мастер

Если использовал Mastering Assistant в Шаге 3 — он уже на месте. Если делал stems и хочешь полный контроль:

| Слот на Stereo Out | Logic native | Параметры |
|---|---|---|
| 1 | **Channel EQ** | финальная коррекция, HPF 60 Hz |
| 2 | **Multipressor** | preset `Mastering`, gentle 1-2 dB сжатия |
| 3 | **Adaptive Limiter** | ceiling –1.0 dB, "Out Ceiling" — режим по слуху |
| 4 | **Loudness Meter** (последним) | мониторишь integrated LUFS → target **–16 LUFS** для intimate |

### Шаг 10 — Export

- `File → Bounce → Project or Section`
- Format: WAV, 24-bit, 48 kHz (для DistroKid) + MP3 320 kbps опционально
- True peak проверить — не выше –1 dB (Adaptive Limiter ceiling –1.0 dB это гарантирует)
- Прогнать через Quality check (см. ниже)

## Step-by-step (REAPER) для bedroom voice-memo трека

(Используя «первый закат» как пример. Для других форматов — аналогично с корректировками)

### Шаг 1 — Suno генерация

- **Persona:** прикрепить (MIYA_v1 для соло Мии, NOX_v1 для соло NOX)
- **Vocal Gender toggle:** Female / Male / ни один (см. [suno-workflow.md](suno-workflow.md), Принцип 3)
- **Style + Exclude Styles + Lyrics:** copy-paste из файла трека
- **Минимум 4 версии**, лучше 6. Слушать в наушниках
- **Выбор по конкретным моментам**, не по общему впечатлению:
  - У какой бридж лучше всего проинтонирован?
  - У какой outro не сорвался в хор?
  - У какой пианино без щелчков / помех?
  - У какой шёпот не превратился в полное пение?

### Шаг 2 — Stem separation

Скачать выбранную версию (WAV если доступен, иначе MP3 высокого битрейта).

**В UVR:**
- Модель: **MDX-Net Inst HQ 3** (для вокал/инструментал) или **Demucs v4 htdemucs_ft** (если нужны 4 стема — vocal/drums/bass/other)
- Output: WAV
- Получаешь `vocals.wav` и `instrumental.wav`

### Шаг 3 — Cleanup вокала

В REAPER загрузить `vocals.wav`. Цепочка плагинов на канале:

| # | Плагин | Настройка | Зачем |
|---|---|---|---|
| 1 | **Denoiser** (RX / bertom) | reduction 6-10 dB | убрать шипение/гудение Suno |
| 2 | **De-esser** (Pro-DS / TDR Nova dynamic) | 5-8 kHz, threshold по слуху | Suno часто свистит на «с»/«ш» |
| 3 | **High-pass EQ** | 80 Hz | режет грязь снизу |
| 4 | **Soothe2** (если платный) | gain reduction 3-6 dB | убирает резонансы — critical для AI-вокала |
| 5 | **Compression** | 4:1, attack 20ms, release 200ms | выравниваешь динамику |

### Шаг 4 — Замена пианино (КЛЮЧЕВОЙ ШАГ)

Это место где «неотличимо от живого» **реально решается**. У Suno felt piano — компромисс. Три варианта:

**Вариант A — сыграть самому (рекомендую если есть MIDI-клава):**
- Загрузить **Spitfire LABS Soft Piano** как VST в новый трек
- Сыграть аккорды поверх Suno вокала
- F minor, 70 BPM, простые аккорды: Fm, Ab, Db, Eb
- 4 паттерна за трек: куплеты, припев, бридж (один зависающий аккорд), outro
- **Преимущество:** живая динамика, human timing, реальные педаль-щелчки

**Вариант B — оставить Suno пианино, обработать:**
- EQ: режешь низы (HPF 100 Hz), смягчаешь верх (low-shelf -2 dB на 8 kHz)
- Tape saturation (Klanghelm IVGI, drive 25%) — убирает «AI-стерильность»
- Лёгкий chorus (1-2%) — добавляет live feel
- **Минус:** AI-сигнатура в attack пианино остаётся

**Вариант C — гибрид:**
- Свой VST-пианино как основа
- Suno-инструментал тихо снизу как texture layer (–18 dB)
- Дает богатство без потери human feel

### Шаг 5 — Human-имитация (важно для «неотличимо»)

Это то, что отличает AI-аудио от живого:

| Элемент | Как добавить | Уровень |
|---|---|---|
| **Breath sounds** | Записать на телефон свои вдохи между фразами; вставить между строками | –24 dB |
| **Room tone** | Записать **30 сек тишины** в своей комнате; зациклить под весь трек | –50 dB |
| **Micro-pitch jitter** | В Melodyne/Graillon **немного расстроить** идеальные ноты ±5 cents | едва заметно |
| **Mouth noise** | Лёгкие clicks/lip sounds — RX генератор или своя запись | –30 dB |
| **Page turn** | Один shuffle paper sound за 1 сек до intro | –20 dB |
| **Pedal noise** | Если играешь пианино — записать клик педали отдельно | –35 dB |
| **Chair creak** | Один тихий creak между секциями | –40 dB |
| **AC hum** | Низкое гудение 50 Hz фоном (если в записи нет своего) | –55 dB |

> **Принцип:** реальные записи **никогда не идеально тихие** между фразами. Если у тебя цифровая тишина 0 dB между строками — это сразу выдаёт AI. Любая «грязь» делает звук живым.

### Шаг 6 — Mix

Цепочка на мастер-шине:

1. **EQ (TDR Nova / Pro-Q3):**
   - High-pass 60 Hz
   - Low shelf –1 dB на 200 Hz (убрать мутность)
   - Air shelf +1 dB на 10 kHz (осторожно — может выявить AI-артефакты)
2. **Tape saturation (Klanghelm IVGI / Decapitator):**
   - Drive ~25%
   - Дает аналоговое тепло
3. **Reverb (Valhalla Supermassive / VintageVerb):**
   - Размер **small room**, decay 1.2 sec
   - Send-эффект, mix ~15%
   - **НЕ plate, НЕ hall** — нужен интимный room
4. **Glue compression (SSL-style):**
   - Ratio 2:1
   - Медленный attack (30ms)
   - Gentle 1-2 dB сжатия

### Шаг 7 — Master

Target loudness:

| Площадка | Integrated LUFS | True peak |
|---|---|---|
| Spotify | –14 (но для intimate — лучше **–16**) | –1 dB |
| Apple Music | –16 | –1 dB |
| YouTube Music | –13 | –1 dB |
| TIDAL | –14 | –1 dB |

**Для intimate трека (как «первый закат»):** целиться в **–16 LUFS**, оставит динамику и дыхание. Не пушить.

**Лимитер:** TDR Limiter 6 GE (free) или FabFilter Pro-L 2 ($169).

## Quality check — критерии «неотличимо»

Прогнать финальный mp3 через тесты:

1. **Слепое сравнение** с reference треком (Bon Iver «715 — CRΣΣKS», Sufjan Stevens «Fourth of July», Ólafur Arnalds «Near Light»). Твой трек на их фоне **не должен резко отличаться** по «свежести воздуха»
2. **Спектральный анализ (SPAN free):** не должен быть подозрительно гладкий спектр. Реальные записи имеют **micro-roughness**
3. **Авто-колонки:** прокатать в машине — там AI-артефакты вылезают сразу
4. **Mono sum (sum to mono):** если стерео-картина разваливается — значит искусственная
5. **Друг без контекста:** дать послушать без анонса. Если первая реакция «а кто это?», а не «это AI?» — победа
6. **Phone speaker test:** если на телефонном динамике звучит «как обычная песня» — финал

## Когда пробивать 95% порог

Чтобы перейти из 85-95% в **истинное неотличимо**:

1. **Переписать пианино самой** — живая клавиатура с MIDI, свой VST, своё исполнение
2. **Записать reference vocal своим голосом** — даже плохо, как guide track
3. **Финал: гибрид Suno-вокала + своего голоса** — Suno держит тембр Мии, ты добавляешь human articulation
4. Или **полностью переспеть** — Suno использовать только как melodic/phrasing референс

Для альбомов HELIOTAIL это пока **избыточно** (Мия — вокал-протагонист, и стилистически voice-memo прощает AI). Но для финальных синглов «качества для редакторских плейлистов» — стоит рассматривать.

## Чек-лист — production check (per трек)

- [ ] Сгенерено минимум 4 версии в Suno
- [ ] Выбрана лучшая (или собран гибрид из нескольких)
- [ ] Stems отделены через UVR
- [ ] Вокал прогнан через cleanup chain (denoise → de-ess → soothe → comp)
- [ ] Пианино либо переиграно (Вариант A), либо обработано (Вариант B)
- [ ] Добавлены **минимум 3 элемента** human-имитации (breath + room tone + ещё)
- [ ] Mix chain применён (EQ → saturation → reverb → glue comp)
- [ ] Loudness в target диапазоне для целевой площадки
- [ ] True peak не выше –1 dB
- [ ] Прогнан через **3 теста** quality check (mono / car / phone / blind A/B)

## Связь с остальной документацией

- [pipeline.md](pipeline.md) — общий путь Suno → стриминг (overview)
- [suno-workflow.md](suno-workflow.md) — Suno-специфика (Persona, Style, Exclude, лимиты)
- [voice-profiles-suno.md](voice-profiles-suno.md) — настройки MIYA_v1 / NOX_v1
- Этот документ — **post-production до состояния «неотличимо от живого»**
