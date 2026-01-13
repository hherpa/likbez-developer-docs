# InlineLatexRenderer.js

## Описание
InlineLatexRenderer - рендерер для inline LaTeX. Соблюдает SOLID принципы.

## Экспортируемые компоненты
- `InlineLatexRenderer` - рендерер inline LaTeX
- `InlineLatexRendererComponent` - функциональный компонент для обратной совместимости
- `processLatexContent(content)` - функция обработки LaTeX контента

## Структура
- `constructor()` - инициализация рендерера для типа 'latex'
- `renderElement(element, context)` - рендерит inline LaTeX элемент
- `processLatexContent(content)` - обрабатывает LaTeX контент

## Взаимодействия
- Наследуется от BaseRenderer
- Использует react-katex для рендеринга формул
- Использует React для рендеринга элементов

## Зависимости
- `react` - для рендеринга React элементов
- `react-katex` - для рендеринга LaTeX формул
- `katex/dist/katex.min.css` - стили KaTeX
- `../core/BaseRenderer` - базовый класс рендерера

## Архитектура
Рендерер inline LaTeX реализует паттерн "Адаптер" для интеграции react-katex:
1. Метод `renderElement` принимает элемент и контекст рендеринга
2. Поддерживает разные форматы LaTeX элемента (content, text, строка)
3. Обрабатывает контент через вспомогательную функцию processLatexContent
4. Использует InlineMath из react-katex для рендеринга формулы
5. Обрабатывает ошибки рендеринга и отображает их пользователю
6. Поддерживает темизацию через контекст

Функция `processLatexContent` позволяет обрабатывать LaTeX контент перед рендерингом (например, для поддержки Unicode).

Функциональный компонент `InlineLatexRendererComponent` обеспечивает обратную совместимость для использования в JSX.

Класс следует принципу единственной ответственности, отвечая только за рендеринг inline LaTeX формул. Использует react-katex как внешнюю библиотеку для рендеринга формул.