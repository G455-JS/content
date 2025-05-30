---
title: "`clip-path`"
description: "Красиво и быстро задаём элементу любую форму при помощи всего одного CSS-свойства."
baseline:
  - group: clip-path
    features:
      - css.properties.clip-path
      - css.properties.clip-path.basic_shape
      - css.properties.clip-path.html_elements
      - css.properties.clip-path.path
      - css.properties.clip-path.svg_elements
      - svg.global_attributes.clip-path
      - api.SVGClipPathElement
      - api.SVGClipPathElement.clipPathUnits
      - api.SVGClipPathElement.transform
      - svg.elements.clipPath
      - svg.elements.clipPath.clipPathUnits
      - svg.elements.clipPath.systemLanguage
authors:
  - spheno
  - starhamster
related:
  - tools/coordinates
  - css/opacity
  - css/box-model
tags:
  - doka
---

## Кратко

С помощью `clip-path` можно задавать видимую область элемента. Всё, что выходит за её пределы, скрывается.

## Пример

Обрежем изображение до круга:

```css
img {
  clip-path: circle(50%);
}
```

## Как пишется

### `url(SVG)`

Задавать область можно с помощью ссылки на SVG [`url()`](/css/url/). Для большей совместимости лучше всего ссылаться на элемент в разметке, а не на отдельный файл. Ссылки на другие домены не работают ни в одном браузере.

```html
<div style="clip-path: url(#clip-path)"></div>
<div style="clip-path: url(doka.svg#clip-path)"></div>

<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 140 45">
  <defs>
    <clipPath id="clip-path">
        <!-- Тут описание фигуры: path, circle и т. п. -->
    </clipPath>
  </defs>
</svg>
```

<iframe title="SVG-источник" src="demos/svg/" height="310"></iframe>

### Базовая форма

Задавать область можно с помощью следующих CSS функций:

- `inset()` — четырёхугольник,
- `circle()` — круг,
- `ellipse()` — эллипс,
- `polygon()` — многоугольник,
- `path()` — сложная фигура по правилам заполнения SVG.

<aside>

👻 В демках ниже для наглядности показан изначальный элемент с полупрозрачностью.

</aside>

#### `inset()`

У функции `inset()` может быть от одного до четырёх аргументов — отступов от краёв. После ключевого слова `round` можно задать скругление углов, которое работает по тем же правилам, что и шорткат [`border-radius`](/css/border-radius/).

```css
div {
  clip-path: inset(10% 50px 5rem round 10px 10%);
}
```

<iframe title="inset()" src="demos/inset/" height="320"></iframe>

#### `circle()`

Аргументом функции `circle()` выступает длина радиуса окружности или одно из ключевых слов: `closest-side` (в качестве длины радиуса используется расстояние от центра окружности до ближайшего края) или `farthest-side` (от центра окружности до самого дальнего края). После ключевого слова `at` можно указать центр фигуры (например, `top left` или `10%`).

```css
div {
  clip-path: circle(75% at 10px 10%);
}
```

<iframe title="circle()" src="demos/circle/" height="320"></iframe>

#### `ellipse()`

CSS-функция `ellipse()` очень похожа на [`circle()`](#circle) за исключением того, что у эллипса два радиуса.

```css
div {
  clip-path: ellipse(4rem farthest-side at top);
}
```

<iframe title="circle()" src="demos/ellipse/" height="320"></iframe>

#### `polygon()`

С помощью `polygon()` можно задавать многоугольники.

```css
div {
  clip-path: polygon(50% 0, 100% 50%, 50% 100%, 0 50%);
}
```

<iframe title="circle()" src="demos/polygon/" height="320"></iframe>

#### `path()`

Функция `path()` — ещё один способ задания видимой области. Поддержка браузеров немного хуже, чем у [`url()`](#url-svg).

```css
span {
  clip-path: path(/* Тут описание фигуры */);
}
```

<iframe title="path()" src="demos/path/" height="180"></iframe>

### Блочная модель

Областью фигуры может стать блочная модель:

- `margin-box` — включает отступы,
- `border-box` — по заданной рамке,
- `padding-box` — по контенту,
- `content-box` — по содержимому,
- `fill-box` — по ограничивающей рамке объекта,
- `stroke-box` — по обводке ограничивающей рамки,
- `view-box` — по окну просмотра SVG.

### Блочная модель с базовой формой

Можно комбинировать задание видимой области блочной моделью и базовой формой, их порядок не важен. В этом случае все значения для базовой формы будут рассчитываться от заданной блочной модели.

<iframe title="Сравнение разных значений свойства" src="demos/basic-shape-with-geometry-box/" height="750"></iframe>

## Подсказки

💡 Свойство не наследуется.

💡 Значение по умолчанию — `none`.

💡 Можно анимировать, если область задана с помощью [базовой формы](#bazovaya-forma).

💡 Свойство заменяет устаревшее свойство [`clip`](/css/clip/).

💡 Скрывается не только элемент, к которому применено свойство, но и вложенные в него элементы с псевдоэлементами.
