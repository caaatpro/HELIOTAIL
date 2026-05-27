# Production Pipeline — «неотличимо от живого»

Глубокий гайд по post-production AI-треков, чтобы они звучали как запись живого исполнителя. Дополняет [pipeline.md](pipeline.md) (overview) и [suno-workflow.md](suno-workflow.md) (Suno-специфика).

> Этот документ — про **post-Suno работу**: как из generated MP3 сделать трек, который не сразу выдаёт себя как AI. Если нужен общий путь от идеи до стриминга — смотри [pipeline.md](pipeline.md).

> **DAW-варианты:** step-by-step pipeline дан параллельно для **REAPER** (универсальный, $60) и **FL Studio** (mac-native, $199 Producer). Главные принципы (генерация, stem separation, human-имитация) DAW-agnostic, отличия — в routing и native плагинах. Выбирай раздел под свой DAW.

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

### FL Studio native plugins (если уже куплен FL Producer Edition+)

FL Studio Producer Edition ($199 mac, lifetime free updates) включает почти весь нужный стек для AI cleanup. Если уже куплен — почти ничего дополнительно покупать не надо.

| Категория | FL native плагин | Замена для |
|---|---|---|
| DAW | **FL Studio** ($199 Producer / $499 Signature, mac-native) | REAPER |
| Cleanup / denoise / declick | **Edison** (built-in аудио-редактор) | базовый iZotope RX |
| Stem separation (FL 21+) | **Edison → Tools → AI Stem Separation** | UVR |
| EQ | **Fruity Parametric EQ 2** | TDR Nova / FabFilter Pro-Q |
| Compression | **Fruity Compressor / Maximus (multiband)** | TDR Kotelnikov / FabFilter Pro-C |
| Pitch correction | **NewTone** | Melodyne / Graillon |
| Saturation | **Soundgoodizer / Fruity Waveshaper** | Klanghelm IVGI / Decapitator |
| Reverb | **Fruity Reeverb 2 / Fruity Convolver** | Valhalla VintageVerb |
| Limiter | **Fruity Limiter** | TDR Limiter 6 / FabFilter Pro-L 2 |
| Multiband | **Maximus** | FabFilter Pro-MB |
| Stereo imaging | **Fruity Stereo Shaper** | (стандартный) |

**Что докупать вне FL:** ничего обязательного. Опционально free VST3 — Valhalla Supermassive (reverb), TDR Nova (dynamic EQ против резонансов AI-вокала — critical), YouLean Loudness Meter (LUFS analysis). Все ставятся в FL без проблем.

**Минусы FL для AI-cleanup:**
- Spectral editing в Edison грубее iZotope RX (для AI-cleanup хватит на 90% задач)
- Чуть менее удобная пакетная обработка (REAPER скриптуется на Lua, в FL — Patcher для цепочек)

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

## Step-by-step (FL Studio) для bedroom voice-memo трека

Параллель к REAPER-варианту выше, для тех у кого FL Studio (mac-native, рекомендованный DAW проекта, если уже куплен). Используем «первый закат» как пример.

### Шаг 1 — Suno генерация

Аналогично REAPER-варианту выше: минимум 4 версии, отбор по конкретным моментам (бридж проинтонирован чисто? пианино без щелчков? шёпот не сорвался в полное пение?).

### Шаг 2 — Stem separation

- **FL 21+:** `Edison → Tools → AI Stem Separation` → output WAV в проектную папку
- **FL 20 или ниже / нет встроенного AI:** [UVR](https://github.com/Anjok07/ultimatevocalremovergui) отдельно (модель `MDX-Net Inst HQ 3`), импортируешь `vocals.wav` и `instrumental.wav` в FL как Audio Clips

### Шаг 3 — Mixer routing

```
Mixer:
  Track 1 — VOCAL      → Master
  Track 2 — PIANO      → Master
  Track 3 — TEXTURES   → Master  (room tone / breath / human-имитация)
  Track 4 — REVERB BUS → Master  (send-эффект, sidechain'и сюда vocal + piano)
  Master               → output
```

Грузишь стемы в **Playlist** как Audio Clips. Каждый клип route'ишь на свой Mixer track: правый клик на клипе → **Track properties → Route to this track only**.

### Шаг 4 — Vocal chain (Mixer Track 1)

| Слот | Плагин | Параметры | Зачем |
|---|---|---|---|
| 1 | **Edison** (insert mode) | Tools → Clean up → Noise reduction, learn 0.5s тишины из начала, apply 8-10 dB | срезать AI-шипение |
| 2 | **Fruity Parametric EQ 2** | HPF 80 Hz / cut –3 dB at 250 Hz (мутность) / shelf +1 dB at 12 kHz (воздух) | базовый тон |
| 3 | **Fruity Multiband Compressor** или **Maximus** | preset «Vocal de-esser», 5-8 kHz зону зажать | замена платного de-esser'а |
| 4 | **TDR Nova** (free VST3) | dynamic mode, найти резонанс 2-4 kHz, gain reduction 3-5 dB | замена Soothe2 — critical против «пластика» AI |
| 5 | **Fruity Compressor** | ratio 4:1, attack 20ms, release 200ms, threshold по слуху на –6 dB | выравнивание динамики |
| 6 | **Send** → Reverb bus (Track 4) | send level ~12% | пространство |

### Шаг 5 — Piano chain (Mixer Track 2)

**Вариант B — обрабатываем Suno-пианино (без MIDI-клавы):**

| Слот | Плагин | Параметры | Зачем |
|---|---|---|---|
| 1 | **Fruity Parametric EQ 2** | HPF 100 Hz / low-shelf –2 dB at 8 kHz | мягкость |
| 2 | **Klanghelm IVGI** (free VST3) | drive 25% | tape warmth, убирает «AI-стерильность» |
| 3 | **Fruity Chorus** | depth 1-2% only | едва ощутимый live feel |
| 4 | **Send** → Reverb bus | send level ~18% | больше пространства чем у вокала |

**Вариант A — переиграть самому (если есть MIDI-клава, *самый сильный апгрейд*):**

- В новом MIDI channel: **Spitfire LABS Soft Piano** (free VST3)
- F minor, 70 BPM, аккорды Fm / Ab / Db / Eb
- 4 паттерна: куплеты / припев / бридж (один зависающий) / outro
- Suno-пианино заглушить до –18 dB как texture layer (или совсем выкинуть)

### Шаг 6 — Reverb bus (Mixer Track 4)

- **Valhalla Supermassive** (free VST3) на insert
- Preset «Skylab» или вручную: size 30%, decay 1.2s, mix 100% (sends контролируют объём)
- **НЕ plate, НЕ hall** — нужен intimate room
- Альтернатива на native FL: **Fruity Convolver** + IR-семпл реальной комнаты (можно скачать free IR библиотеки)

### Шаг 7 — Human-имитация (Mixer Track 3)

Минимум 3 элемента, **обязательно** room tone.

| Элемент | Где взять / как сделать в FL | Уровень |
|---|---|---|
| **Breath sounds** | Запиши вдохи на телефон, импортируй как Audio Clip между фразами | –24 dB |
| **Room tone** | Запиши 30 сек тишины в комнате, зациклишь Audio Clip под весь трек | –50 dB |
| **Micro-pitch jitter** | **NewTone** (FL native) на vocal track → расстроить идеальные ноты ±5 cents | едва заметно |
| Mouth clicks (опц.) | Edison → Sample → лёгкие клики, импорт между фразами | –30 dB |
| AC hum (опц.) | Сгенерируй sine 50 Hz в Edison, очень тихо фоном | –55 dB |
| Pedal noise (опц., если играешь сам) | Записи клика педали отдельно | –35 dB |

**Главное правило (повторяется из REAPER-варианта):** между фразами **никогда не должно быть цифровой тишины 0 dB**. Это #1 маркер AI. Room tone льёт под весь трек.

### Шаг 8 — Master bus

| Слот | Плагин | Параметры |
|---|---|---|
| 1 | **Fruity Parametric EQ 2** | HPF 60 Hz, low-shelf –1 dB at 200 Hz (мутность), air shelf +1 dB at 10 kHz (осторожно — может выявить AI-артефакты) |
| 2 | **Maximus** | preset «Mastering — gentle», ratio 2:1, slow attack, gentle 1-2 dB сжатия |
| 3 | **Fruity Limiter** | ceiling –1.0 dB, target gain by ear |
| 4 | **YouLean Loudness Meter** (free VST3, последним) | мониторишь integrated LUFS → target **–16 LUFS** для intimate трека |

**Loudness target для intimate трека:** –16 LUFS (не пушить до –14, потеряешь дыхание и динамику).

### Шаг 9 — Export

- File → Export → MP3 (для соцсетей) и WAV 24-bit (для дистрибьютора)
- True peak проверить — не выше –1 dB
- Прогнать через Quality check (см. ниже)

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
