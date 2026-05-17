# План: Blog Preview Card

## Контекст

Учебный проект уровня Newbie на Frontend Mentor. Цель — собрать карточку-превью блога точно по Figma-макету, изучив по дороге HTML-семантику, CSS box model, Flexbox и mobile-first подход. Сейчас в `index.html` только голый текст без разметки, файла `style.css` нет. Все ассеты (шрифт Figtree, изображения) на месте.

Каждый шаг: теория → лучшие практики → реализация → проверка кода.

---

## Этап 1 — Настройка окружения и структура HTML

**Цель:** создать правильный семантический скелет карточки.

**Теория для изучения:**
- Зачем нужен `<!DOCTYPE html>` и `<meta charset>`
- Семантические теги: `<main>`, `<article>`, `<header>`, `<footer>`, `<time>`, `<figure>`
- Разница между структурой (HTML) и внешним видом (CSS)
- Атрибут `alt` у изображений — зачем и как писать

**Структура HTML которую нужно написать:**
```
<body>
  <main>                          ← центрирование карточки на странице
    <article class="card">        ← семантический контейнер карточки
      <figure class="card__image">
        <img src="..." alt="...">
      </figure>
      <div class="card__body">
        <span class="card__tag">Learning</span>
        <time class="card__date" datetime="2023-12-21">Published 21 Dec 2023</time>
        <h2 class="card__title">...</h2>
        <p class="card__description">...</p>
        <div class="card__author">
          <img class="card__avatar" src="..." alt="Greg Hooper">
          <span class="card__author-name">Greg Hooper</span>
        </div>
      </div>
    </article>
  </main>
  <footer class="attribution">...</footer>
</body>
```

**Лучшие практики:**
- `<article>` — для самодостаточного контента, который можно вырвать из страницы
- `<time datetime="...">` — машиночитаемая дата для поисковиков и screen reader
- `<figure>` — семантическая обёртка для иллюстрации
- BEM для классов: `.card`, `.card__title`, `.card--active`

**Файлы:** `index.html`

**Проверка:** валидатор W3C, просмотр в браузере без CSS (должен быть понятен)

---

## Этап 2 — CSS: переменные, шрифт, сброс

**Цель:** подключить шрифт, задать CSS-переменные, обнулить браузерные стили.

**Теория для изучения:**
- Что такое CSS-переменные (`custom properties`) и зачем `:root`
- Как подключить локальный шрифт через `@font-face`
- CSS reset: зачем `box-sizing: border-box`, `margin: 0`, `padding: 0`
- Единица `rem` vs `px`

**Переменные из style-guide.md:**
```css
:root {
  --color-yellow:   hsl(47, 88%, 63%);
  --color-white:    hsl(0, 0%, 100%);
  --color-gray-500: hsl(0, 0%, 42%);
  --color-gray-950: hsl(0, 0%, 7%);
  --font-family: 'Figtree', sans-serif;
  --font-weight-medium: 500;
  --font-weight-extrabold: 800;
}
```

**Лучшие практики:**
- `*, *::before, *::after { box-sizing: border-box }` — размеры без сюрпризов
- `@font-face` с `font-display: swap` — текст видим пока шрифт грузится
- Переменные держать в `:root`, не хардкодить цвета внутри правил

**Файлы:** создать `style.css`, подключить в `<head>` через `<link>`

---

## Этап 3 — Фон страницы и центрирование карточки

**Цель:** серый фон, карточка по центру экрана — горизонтально и вертикально.

**Теория для изучения:**
- Как Flexbox (flex-контейнер) центрирует потомков
- `min-height: 100vh` — почему `height: 100vh` может привести к обрезанию
- `body` как flex-контейнер — стандартный паттерн для центрирования

**Реализация:**
```css
body {
  background-color: var(--color-yellow);
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 1.5rem;         /* отступы чтобы карточка не прилипала к краям */
  font-family: var(--font-family);
}
```

**Лучшие практики:**
- Mobile-first: сначала стили для телефона, потом `@media (min-width: ...)`
- `padding` на `body` защищает контент от краёв экрана на маленьких устройствах

**Файлы:** `style.css`

---

## Этап 4 — Карточка: размеры, скругления, тень

**Цель:** белая карточка с жёлтой смещённой тенью, скруглёнными углами.

**Теория для изучения:**
- Box model детально: content → padding → border → margin
- `border-radius` — скругление углов
- `box-shadow: offset-x offset-y blur spread color` — синтаксис и параметры
- Разница между `width` и `max-width`

**Параметры карточки (из макета):**
- `max-width: 384px`
- `border-radius: 20px`
- `border: 1px solid var(--color-gray-950)`
- `box-shadow: 8px 8px 0 var(--color-gray-950)` — жёсткая смещённая тень
- `background-color: var(--color-white)`
- `overflow: hidden` — чтобы изображение не вылезало за скруглённые углы

**Файлы:** `style.css` — блок `.card`

**Проверка:** сравнить с `design/desktop-design.jpg` в браузере

---

## Этап 5 — Изображение-обложка

**Цель:** изображение занимает всю ширину карточки, не деформируется.

**Теория для изучения:**
- `width: 100%` vs `max-width: 100%`
- `object-fit: cover` — как изображение заполняет контейнер
- `border-radius` только на нужных углах (`border-radius: 10px`)
- Зачем `display: block` у `<img>` (убирает inline gap)

**Файлы:** `style.css` — блоки `.card__image`, `.card__image img`

---

## Этап 6 — Тело карточки: тег, дата, заголовок, описание

**Цель:** верстка внутреннего контента с правильными отступами и типографикой.

**Теория для изучения:**
- Flexbox direction column для вертикального стека элементов
- `gap` вместо `margin` между дочерними элементами в flex-контейнере
- `font-size`, `font-weight`, `line-height` — основы типографики
- Семантика `<span>` для тега-категории, `<time>` для даты

**Элементы и их стили:**
- `.card__body`: `padding: 1.5rem`, `display: flex`, `flex-direction: column`, `gap: 0.75rem`
- `.card__tag`: жёлтый фон, `border-radius`, padding, font-weight 800
- `.card__date`: серый цвет `var(--color-gray-500)`, font-size 0.875rem
- `.card__title`: font-weight 800, font-size 1.5rem, тёмный цвет
- `.card__description`: `var(--color-gray-500)`, line-height 1.5

**Файлы:** `style.css`

---

## Этап 7 — Строка автора

**Цель:** аватар и имя в одну строку с выравниванием по центру вертикально.

**Теория для изучения:**
- Flexbox `align-items: center` для вертикального выравнивания
- Как задать размер аватара и сделать его круглым (`border-radius: 50%`)

**Реализация:**
- `.card__author`: `display: flex`, `align-items: center`, `gap: 0.75rem`
- `.card__avatar`: `width: 2rem`, `height: 2rem`, `border-radius: 50%`
- `.card__author-name`: `font-weight: 800`, `font-size: 0.875rem`

**Файлы:** `style.css`

---

## Этап 8 — Hover и Focus состояния

**Цель:** заголовок меняет цвет на жёлтый при наведении; доступность с клавиатуры.

**Теория для изучения:**
- Псевдоклассы `:hover`, `:focus`, `:focus-visible`
- `cursor: pointer` — когда ставить
- `transition` для плавного изменения
- Доступность: `outline` не убирать, только стилизовать

**Реализация:**
```css
.card__title:hover {
  color: var(--color-yellow);
  cursor: pointer;
}
```

**Лучшие практики:**
- `transition: color 0.2s ease` — плавный переход
- Не убирать `outline` у фокуса — это нарушение доступности

**Файлы:** `style.css`

---

## Этап 9 — Финальная проверка

**Чеклист:**
- [ ] Сравнить с `design/mobile-design.jpg` на 375px
- [ ] Сравнить с `design/desktop-design.jpg` на 1440px
- [ ] Сравнить с `design/active-states.jpg` — hover заголовка
- [ ] Проверить в DevTools: Lighthouse → Accessibility ≥ 90
- [ ] Проверить alt-текст изображений
- [ ] Keyboard navigation: Tab → заголовок должен получать фокус
- [ ] Заполнить `README.md` — секции "Built with", "What I learned"
- [ ] Вписать своё имя в attribution footer

---

## Критические файлы

| Файл | Что делаем |
|------|-----------|
| `index.html` | Полностью переписываем — семантическая структура |
| `style.css` | Создаём с нуля |
| `assets/images/illustration-article.svg` | Изображение обложки |
| `assets/images/image-avatar.webp` | Аватар автора |
| `assets/fonts/Figtree-VariableFont_wght.ttf` | Шрифт через `@font-face` |
| `style-guide.md` | Справочник цветов и типографики |
| `design/` | Эталонные скриншоты для сверки |
