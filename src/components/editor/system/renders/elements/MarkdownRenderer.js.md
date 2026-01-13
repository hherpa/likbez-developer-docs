# MarkdownRenderer.js

## Описание
MarkdownRenderer - рендерер для markdown элементов. Соблюдает SOLID принципы:
- SRP: только рендеринг markdown элементов
- OCP: легко расширяется новыми markdown типами
- LSP: наследует от BaseRenderer
- ISP: только необходимые методы для markdown
- DIP: зависит от абстракций (BaseRenderer)

## Экспортируемые компоненты
- `MarkdownRenderer` - рендерер markdown элементов
- `MarkdownRendererComponent` - функциональный компонент для обратной совместимости

## Структура
- `constructor()` - инициализация рендерера для типа 'markdown'
- `canRender(element)` - проверяет, может ли рендерер обработать элемент
- `renderMarkdownElements(markdownElements, darkMode)` - рендерит массив markdown элементов
- `renderMarkdownElement(element, index, darkMode)` - рендерит отдельный markdown элемент
- `renderElement(element, context)` - переопределение для совместимости с BaseRenderer

## Взаимодействия
- Наследуется от BaseRenderer
- Использует вспомогательные функции для рендеринга inline markdown
- Использует вспомогательные функции для рендеринга списков
- Использует вспомогательные функции для рендеринга заголовков
- Использует палитру цветов
- Использует React для рендеринга элементов

## Зависимости
- `react` - для рендеринга React элементов
- `../core/BaseRenderer` - базовый класс рендерера
- `../../../constants/ColorPalette` - палитра цветов
- `./MarkdownInlineParser` - парсер inline markdown
- `./MarkdownListRenderer` - рендерер списков
- `./MarkdownHeadingRenderers` - рендереры заголовков

## Архитектура
Рендерер markdown реализует паттерн "Стратегия" для рендеринга различных типов markdown элементов:
1. Метод `canRender` определяет, может ли рендерер обработать элемент (поддерживает h1, h2, h3, p, ul, hr, markdown)
2. Метод `renderMarkdownElements` рендерит массив markdown элементов с общими стилями
3. Метод `renderMarkdownElement` реализует фабричный метод для рендеринга отдельных элементов:
   - h1, h2, h3 - через вспомогательные функции рендеринга заголовков
   - ul - рендерит список с элементами через вспомогательную функцию рендеринга содержимого
   - hr - рендерит горизонтальную линию
   - p - рендерит параграф с inline markdown через вспомогательную функцию
4. Метод `renderElement` обеспечивает совместимость с BaseRenderer

Класс следует принципу единственной ответственности, отвечая только за рендеринг markdown элементов. Делегирует специфичную логику вспомогательным функциям:
- Inline рендеринг через MarkdownInlineParser
- Рендеринг списков через MarkdownListRenderer
- Рендеринг заголовков через MarkdownHeadingRenderers

Функциональный компонент `MarkdownRendererComponent` обеспечивает обратную совместимость для использования в JSX.