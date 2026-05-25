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

## Жанровая база проекта

Проект HELIOTAIL пишется в **modern progressive alt / theatrical alt-metal** русле — Sleep Token, Loathe, Spiritbox (clean parts), Bad Omens, Bring Me The Horizon POST HUMAN era. Голоса оптимизированы под динамику этого жанра: **интимный куплет с dry close-mic → soaring full voice в припеве со стеной гитар**. Это влияет на профили — Мия и NOX должны уметь обе крайности, не только одну.

---

## Voice Profile — MIYA

**Suno Persona ID:** `MIYA_v1` (создать после отбора canonical-трека)

### Style-промпт (вставлять в каждый трек)

```
Female vocalist, mid-20s, Russian language lyrics. Mezzo-soprano with rich alto
foundation. Two-mode delivery for modern alt-metal: (1) intimate restrained
close-mic in verses — almost spoken-sung, fragile, dry; (2) soaring full voice
in choruses with layered harmonies, cinematic and emotional, no screams.
Subtle controlled vibrato. Slight rasp in lower register, clear and powerful in
upper. Cold studio reverb, very dry on verses, wider stadium-like on choruses.
Modern theatrical alt-metal aesthetic in the vein of Sleep Token (female
counterpart), Spiritbox (clean parts), Loathe female vocals. Russian language.

Avoid: belting beyond cinematic alt range, opera, autotune warble, child-like
brightness, american accent, cheerful tone, rap delivery, screams, growls.
```

### Краткая версия (если место в поле жёстко лимитировано)

```
Female RU vocalist, dual-mode: intimate dry close-mic in verses, soaring layered
choruses. Modern alt-metal (Sleep Token / Spiritbox clean). No autotune,
no screams, no rap.
```

### Lyrics tag

```
[Female voice — Miya, intimate restrained verse / soaring layered chorus]
```

---

## Voice Profile — NOX

**Suno Persona ID:** `NOX_v1` (создать после отбора canonical-трека)

### Style-промпт (вставлять в каждый трек)

```
Male vocalist, late 20s, Russian language lyrics. Baritone with strong upper
extension to tenor. Two-mode delivery for modern alt-metal: (1) intimate
restrained close-mic in verses — weighted, almost spoken, slight rasp; (2)
soaring full voice in choruses with layered harmonies, cinematic and emotional,
no screams. Modern theatrical alt-metal aesthetic in the vein of Sleep Token
(Vessel), Loathe (clean parts), Bad Omens (Noah Sebastian clean). Russian
language. Slightly more distant mic than female vocal for duo contrast.

Avoid: bright tenor pop, growling, screaming, rap delivery, american accent,
boy-band brightness, harsh vocals, opera, autotune warble.
```

### Краткая версия

```
Male RU vocalist, dual-mode: weighted intimate verse, soaring layered chorus.
Modern alt-metal (Sleep Token Vessel / Bad Omens clean). No screams, no growls,
no rap, no autotune.
```

### Lyrics tag

```
[Male voice — Nox, weighted intimate verse / soaring layered chorus]
```

---

## Дуэтные треки — voice profile

Когда поют вместе — Suno часто либо делает один голос громче, либо смешивает в неузнаваемое. Лечится явной разметкой + жанровой опорой на theatrical layering (Sleep Token, Loathe).

### Style-промпт для дуэта

```
Duet between female and male Russian vocalists in modern progressive alt /
theatrical alt-metal (Sleep Token, Loathe, BMTH POST HUMAN).
Female (Miya): intimate restrained close-mic in verses, soaring full voice in
chorus with layered harmonies.
Male (Nox): weighted intimate close-mic in verses, soaring full voice in chorus
with layered harmonies.
Both voices keep their individual character — do not blend into one timbre.
Female slightly panned left, male slightly panned right.
Harmonies in chorus: female on melody, male a third below, choir-style stacks
in final chorus for theatrical lift.
Verses dry close-mic with sparse instrumentation. Choruses wide cinematic
reverb with wall of distorted guitars. Bridge: total instrumental drop, dry
intimate vocals only.
No autotune warble, no belting beyond cinematic range, no rap, no screams or
growls.
```

### Lyrics tags для дуэта

```
[Verse — Female voice, Miya, intimate restrained]
текст Мии
[Verse — Male voice, Nox, weighted intimate]
текст Нокса
[Chorus — Duet, both voices, layered harmonies, Miya melody, Nox third below]
общий припев
[Final Chorus — Duet, choir-style stacks, theatrical peak]
финальный припев
[Bridge — Both voices, dry intimate, instruments out]
диалог в мосте
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
