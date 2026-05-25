# Мия — промпт под Nano Banana (Gemini 2.5 Flash Image)

Адаптированная версия мастер-промпта из [01-character-miya.md](01-character-miya.md).
Nano Banana хуже ест "промпт-простыни" из тегов и сильнее реагирует на естественный язык + reference image.

## Промпт для генерации эталона (canonical portrait)

```
Cinematic photorealistic portrait of a young woman named Miya, 23-25 years old.
She has a feminine appearance with a subtle androgynous undertone. Oval face with
a slightly sharp jawline, pale soft skin with realistic texture and tiny imperfections.
Large tired intelligent dark gray-blue eyes with slightly heavy eyelids, giving her
a melancholic expression. Natural full lips, straight nose, subtly asymmetrical features.
Long messy black hair, slightly wavy, matte texture, falling naturally around her face.

She has subtle cybernetic modifications: a thin vertical surgical seam across her left
cheek, faint cyan glowing veins beneath the skin of her neck and collarbone, a small
thin black cable connected behind her right ear leading into her hair. The implants
look elegant and believable, not flashy.

Setting: neutral dark gray background, soft cinematic front lighting with a cold cyan
rim light from behind, subtle magenta accent on one side. Slight atmospheric fog.
She is looking slightly off-camera with a calm neutral expression.

Style: hyper-realistic, cinematic photography, shallow depth of field, film grain,
8K detail, Ghost in the Shell mood, Detroit Become Human aesthetic, dark synthwave
atmosphere. Realistic skin with visible pores. Avoid anime style, avoid smiling
influencer face, avoid oversaturated neon.
```

## Промпт для последующих сцен (через image reference)

После того как эталон выбран и сохранён, использовать его как reference image + текст:

```
This is Miya. Generate a new image of the same exact character — same face,
same eyes, same hair, same vertical seam on her left cheek, same thin black
cable behind her right ear, same cyan glowing veins. Keep her exact identity.

New scene: [описание сцены — см. 06-scene-library.md]

Maintain: hyper-realistic cinematic photography style, dark synthwave atmosphere,
deep navy blue + cyan + magenta color palette, moody lighting.
```

## Эффекты — always-on vs emotional triggers

### Always-on (в каждой генерации)

- Шов на левой щеке (вертикальный, тонкий)
- Кабель за правым ухом
- Цианоген-вены на шее и ключицах
- Биомеханический рисунок на руках (если руки в кадре)

### Emotional triggers (добавляем только в эмоциональных сценах)

- Глитч левого глаза → активен при эмоциональном пике, плаче, гневе
- Магента-артефакты в воздухе → во время пения, на сцене
- Свечение вен усиливается → сильные эмоции
- Парящие частицы сигнала → драматические моменты
- Голографический шум → моменты "сбоя"

Не активируй всё разом — будет визуальная каша. Один-два эффекта на сцену максимум.

## Стандартный промпт для портрета крупного плана

```
This is Miya. Same exact face, same identity. Extreme close-up portrait,
shoulders up. [emotional state]. Cold cyan rim light, magenta accent from
the left, dark background with subtle atmospheric haze. Shallow depth of field,
cinematic film grain, 8K detail.
```

`[emotional state]` варианты:
- `calm neutral expression, looking directly at camera`
- `melancholic, eyes slightly closed, head tilted down`
- `intense, jaw clenched, looking off-camera`
- `vulnerable, tears welling up, left eye glitching`
- `confident, half-smile, side glance`

## Лайфхаки Nano Banana

- **Не перегружай негативами** — модель плохо ест длинные `avoid:` списки. Лучше позитивные формулировки.
- **Iterative editing** — генерируй базу, потом дорабатывай по одному параметру: "make the lighting colder", "add subtle rain in the background".
- **Multi-image input** — давай два референса для сложных сцен: лицо Мии + референс освещения/локации.
- **Возвращайся к canonical** — если идентичность поплыла за несколько итераций, всегда стартуй с эталонного портрета, а не последней генерации. Иначе ошибки накапливаются.

См. полный workflow в [05-nano-banana-workflow.md](05-nano-banana-workflow.md).
