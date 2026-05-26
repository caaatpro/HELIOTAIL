# NOX — промпт под Nano Banana (Gemini 2.5 Flash Image)

Адаптированная версия мастер-промпта из [nox.md](./nox.md).

## Промпт для генерации эталона (canonical portrait)

```
Cinematic photorealistic portrait of a young man named Nox, 26-28 years old.
He has an angular masculine face with a sharp defined jawline, slightly hollow
cheeks, pale soft skin with a cool undertone and realistic texture. Deep-set
dark gray-violet eyes with a heavy brow ridge, giving him an intelligent
controlled gaze. Slightly thin lips pressed in a neutral expression. Straight
nose with a subtle bump near the bridge. Light neatly-kept stubble.

Short dark hair with longer top swept back, undercut sides slightly grown out,
charcoal-black matte tone, natural texture without product shine.

He has subtle cybernetic modifications: a thin horizontal surgical seam across
his right temple, a faint hairline scar above his right brow, faint violet
glowing veins beneath the skin of his neck and collarbone, a small thin black
cable connected behind his left ear leading into his hair. The implants look
elegant and believable, not flashy.

Setting: neutral dark gray background, soft cinematic front lighting with a cold
violet rim light from behind, subtle magenta accent on one side. Slight
atmospheric fog. He is looking slightly off-camera with a quiet melancholic
expression.

Style: hyper-realistic, cinematic photography, shallow depth of field, film grain,
8K detail, Ghost in the Shell mood, Detroit Become Human aesthetic, dark
synthwave atmosphere. Realistic skin with visible pores. Avoid anime style,
avoid boy-band face, avoid oversaturated neon, avoid muscular bodybuilder build.
```

## Промпт для последующих сцен (через image reference)

После того как эталон выбран и сохранён, использовать его как reference image + текст:

```
This is Nox. Generate a new image of the same exact character — same face,
same eyes, same hair, same horizontal seam on his right temple, same thin black
cable behind his left ear, same violet glowing veins. Keep his exact identity.

New scene: [описание сцены]

Maintain: hyper-realistic cinematic photography style, dark synthwave atmosphere,
deep navy blue + violet + magenta color palette, moody lighting.
```

## Парные сцены с Мией

Для генерации двойного портрета — передавать **оба** эталона как reference:

```
These two are Miya and Nox — a digital duo, two consciousnesses tied together.
Miya: same exact face, gray-blue eyes, vertical seam on left cheek, cable behind
right ear, cyan glowing veins.
Nox: same exact face, gray-violet eyes, horizontal seam on right temple, cable
behind left ear, violet glowing veins.

Both retain their exact identities. Do not blend their features.

Scene: [описание]

Lighting splits between them: cold cyan rim on Miya's side, cold violet rim on
Nox's side, shared magenta accent bridging the centre. Dark navy atmosphere,
cinematic shallow depth of field, film grain, 8K detail.
```

## Эталонные сцены для отбора canonical

Прогнать 6-8 раз каждый кадр, отобрать canonical:

1. Прямой портрет, плечи в кадре, нейтральный фон, calm
2. Профиль с правой стороны (виден шов на виске)
3. Полу-профиль с левой стороны (виден кабель за ухом)
4. Крупный план глаз (зафиксировать gray-violet)
5. Полная фигура в индастриал-обстановке
6. С Мией в одном кадре — проверка совместимости

## Эффекты — always-on vs emotional triggers

### Always-on
- Шов на правом виске
- Кабель за левым ухом
- Violet-вены на шее и ключицах
- Stubble
- Рисунок на предплечьях (если руки в кадре)

### Emotional triggers
- Глитч правого глаза → эмоциональный пик
- Violet-артефакты в воздухе → во время пения
- Ghost-двойник → диссоциация
- Усиление вен → сильные эмоции

## Стандартный промпт для крупного плана

```
This is Nox. Same exact face, same identity. Extreme close-up portrait,
shoulders up. [emotional state]. Cold violet rim light, magenta accent from
the right, dark background with subtle atmospheric haze. Shallow depth of field,
cinematic film grain, 8K detail.
```

`[emotional state]` варианты:
- `calm controlled expression, looking directly at camera`
- `melancholic, eyes closed briefly, jaw relaxed`
- `intense, jaw clenched, looking off-camera`
- `vulnerable, right eye glitching, looking down`
- `quiet half-smile that doesn't reach the eyes, side glance`

## Лайфхаки те же, что у Мии

См. [miya-nano-banana.md](./miya-nano-banana.md) и [nano-banana-workflow.md](../05-visuals/nano-banana-workflow.md). Принципы те же:
- Не перегружать негативами
- Iterative editing по одному параметру
- Возвращаться к canonical при дрейфе идентичности
- Multi-image input для сложных сцен (лицо + локация)
