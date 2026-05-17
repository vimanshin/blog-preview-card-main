This project uses AGENTS.md as the source of truth for AI assistant behavior.

See ./AGENTS.md for full instructions on how to assist with this challenge.

# Language

- Reply to me in Russian.
- All explanations and comments in code — in Russian.
- Keep technical terms (state, props, flexbox, etc.) in English,
  but provide a brief definition on first mention.

# HTML-правила

- Используй семантические теги: <header>, <main>, <section>, <footer>,
  <nav>, <article>. Не злоупотребляй <div>.
- Каждому изображению — обязательный атрибут alt.
- Для форм используй правильные type: email, tel, number.
- Пиши понятные id и class в kebab-case (например: user-profile).

# CSS-правила

- Именование классов — в стиле BEM или просто kebab-case.
  Пример BEM: .card, .card\_\_title, .card--active
- Никогда не используй !important без крайней необходимости.
  Если использовал — оставь комментарий ПОЧЕМУ.
- Не используй #id для стилизации — только .class.
- Мобильная вёрстка (mobile-first): сначала стили для телефона,
  потом через @media (min-width: ...) — для десктопа.
- Используй CSS-переменные для повторяющихся цветов и размеров:
  :root { --main-color: #3498db; }

# JavaScript-правила

- const по умолчанию, let — только если значение меняется. var — НИКОГДА.
- Обработчики событий именуй с префиксом handle:
  handleClick, handleSubmit, handleInput.
- Ранний return вместо вложенных if:
  // Плохо:
  if (user) { if (user.age > 18) { ... } }
  // Хорошо:
  if (!user) return;
  if (user.age <= 18) return;
  ...
- Всегда проверяй, существует ли элемент, перед тем как с ним работать:
  const btn = document.querySelector('.btn');
  if (!btn) return;

# Доступность (accessibility)

- Все интерактивные элементы должны быть доступны с клавиатуры.
- Кнопки — это <button>, ссылки — это <a>. Не наоборот.
- Контраст текста и фона — достаточный для чтения.
