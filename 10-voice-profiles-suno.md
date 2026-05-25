# Voice Profiles — фиксация голосов в Suno

Цель: чтобы Мия и NOX **всегда** пели одним и тем же голосом во всех треках. Suno из коробки случайно семплирует голос на каждой генерации — без фиксации каждый трек звучит как новый артист.

## Реальность Suno (2026)

Голос в Suno можно "пришить" к проекту тремя слоями. **Использовать все три одновременно** — иначе будет дрейф.

### Слой 1 — Persona (главный механизм)

Suno Personas — это сохранённый "слепок" голоса из одной конкретной генерации. Делается так:
1. Сгенерировать 8-12 версий первого трека с одинаковым style-промптом (см. ниже)
2. Прослушать, отобрать ту, где голос **максимально близок к желаемому профилю**
3. В Suno: "Create Persona from this song" → дать имя `MIYA_v1` / `NOX_v1`
4. **Все последующие треки** генерить с этим Persona, не с нуля

Persona фиксирует тембр, вибрато, общую характеристику. Без неё всё остальное — приближение.

### Слой 2 — Style/Description промпт

Краткое описание голоса в поле Style. Suno лучше всего понимает английский, даже если лирика на русском. Не больше ~400 символов — больше Suno игнорирует.

### Слой 3 — Lyrics tags

В Custom Mode прямо в лирике расставлять `[Female voice — Miya, breathy alto]`, `[Male voice — Nox, baritone whisper]`, `[Duet, both voices, harmony]`. Помогает Suno не путаться в дуэтных треках.

---

## Voice Profile — MIYA

**Suno Persona ID:** `MIYA_v1` (создать после отбора canonical-трека)

### Style-промпт (вставлять в каждый трек)

```
Female vocalist, mid-20s, Russian language lyrics. Breathy mezzo-soprano with
controlled alto delivery. Intimate close-mic timbre, slightly fragile.
Melancholic, restrained, never belted. Subtle controlled vibrato. Slight rasp
in lower register, clear and airy in upper. Cold studio reverb, very dry on
verses, wider on chorus. Faint digital glitch artifacts on consonants like
analog corruption. Russian post-punk meets dark synth-pop aesthetic. Reference
feel: Aigel, Hadn Dadn, Sky Ferreira, Lykke Li dark era.

Avoid: belting, opera, autotune warble, child-like brightness, american accent,
cheerful tone, rap delivery.
```

### Краткая версия (если место в поле жёстко лимитировано)

```
Female RU vocalist, breathy melancholic alto, intimate close-mic, subtle vibrato,
dark synth-pop, cold dry reverb, faint digital glitch on consonants. No belting,
no autotune.
```

### Lyrics tag

```
[Female voice — Miya, breathy alto, intimate close-mic, restrained]
```

---

## Voice Profile — NOX

**Suno Persona ID:** `NOX_v1` (создать после отбора canonical-трека)

### Style-промпт (вставлять в каждый трек)

```
Male vocalist, late 20s, Russian language lyrics. Baritone with mid-low chest
voice. Restrained, weighted, slightly haunted delivery. Smoky timbre with
occasional vocal fry. Whispered verses, controlled fullness in chorus, sometimes
sprechgesang spoken-sung delivery. Slightly more distant mic than female vocal.
Subtle low-end resonance. Cold studio reverb, dry on verses. Russian post-punk
darkwave aesthetic. Reference feel: Molchat Doma vocalist, Boy Harsher (male),
Ic3peak male parts, early Хадн дадн.

Avoid: bright tenor, growling, screaming, rap delivery, american accent,
boy-band brightness, aggressive belting.
```

### Краткая версия

```
Male RU vocalist, weighted baritone, smoky vocal fry, whispered verses,
sprechgesang, darkwave, cold dry reverb, slight low-end resonance. No tenor,
no growl, no rap.
```

### Lyrics tag

```
[Male voice — Nox, weighted baritone, whispered/spoken delivery]
```

---

## Дуэтные треки — voice profile

Когда поют вместе — Suno часто либо делает один голос громче, либо смешивает в неузнаваемое. Лечится явной разметкой.

### Style-промпт для дуэта

```
Duet between female and male Russian vocalists in dark synth-pop / darkwave style.
Female: breathy melancholic alto, intimate close-mic (Miya).
Male: weighted baritone, smoky vocal fry, whispered delivery (Nox).
Both voices keep their individual character — do not blend into one timbre.
Female slightly panned left, male slightly panned right.
Harmonies in chorus: female on melody, male a third below.
Cold studio reverb on both, dry verses, wider chorus. Subtle digital glitch
artifacts on both voices. No autotune warble, no belting, no rap.
```

### Lyrics tags для дуэта

```
[Verse — Female voice, Miya, breathy alto]
текст Мии
[Verse — Male voice, Nox, weighted baritone]
текст Нокса
[Chorus — Duet, both voices, harmony, Miya on melody, Nox third below]
общий припев
```

---

## Workflow фиксации (один раз на старте)

1. **Генерация canonical-трека для Мии:**
   - Custom Mode, Style = полный промпт MIYA, лирика короткая (1 куплет + припев)
   - Сгенерить **12 версий**
   - Прослушать все, отобрать одну с правильным тембром
   - Сохранить как Persona `MIYA_v1`
   - Сохранить .wav этого трека локально как референс

2. **То же для NOX** (отдельный трек, не дуэт):
   - Custom Mode, Style = полный промпт NOX
   - 12 версий → отбор → Persona `NOX_v1` → референс-wav

3. **Тестовый дуэт:**
   - Custom Mode, Style = промпт для дуэта, **выбрать оба Persona** одновременно (Suno позволяет до 2 персон)
   - 6-8 версий → проверить, что оба голоса узнаваемы и не сливаются
   - Если сливаются — увеличить контраст в описании (panning, harmony rules)

4. **Сохранить эталоны:**
   - Persona ID обоих → в этот файл
   - Референс-wav для каждого голоса → в папку `references/`
   - При любом дрейфе в будущем — возвращаться к этим эталонам, не к последней генерации

## Recovery — что делать, если голос поплыл

Симптомы дрейфа: Suno после обновления модели или после серии генераций начинает выдавать "не того" Мию или Нокса.

Лечение по нарастанию:
1. **Проверить, выбран ли Persona** — частая ошибка, забывают подцепить
2. **Перегенерить с тем же seed/Persona** — Suno иногда возвращает прошлый голос со второй попытки
3. **Уменьшить отвлекающие style-теги** — если в промпте много жанровых слов, Suno может "уплыть" в стилистический сем
4. **Создать новую Persona из старого canonical-трека** — если Suno потерял старый Persona (бывает при крупных апдейтах модели)
5. **Полная переинициализация** — заново прогнать workflow выше, обновить Persona ID

## Заметки

- Suno **не поддерживает voice cloning** в строгом смысле (как ElevenLabs). Persona — это вероятностное приближение, не точная копия. Допустимая вариативность между треками — есть всегда, цель — держать её в узких рамках, чтобы слушатель узнавал артиста.
- Если на каком-то этапе Persona перестанет работать (политика Suno может меняться) — fallback это **тяжёлый style-промпт + жёсткие lyrics tags + ручной отбор** из 10+ версий каждого трека.
- Все треки в одной серии (EP, альбом) генерить **подряд за короткое время** — Suno даёт более консистентные результаты в рамках одной сессии, чем когда генерации разнесены на недели.
