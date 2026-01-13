# useFloatingToolbar

Хук для координации между textarea и FloatingToolbar.

## Описание

Управляет состоянием видимости и позиционированием плавающего тулбара.

## Параметры

- `textareaRef` (React.RefObject): Ref на textarea элемент
- `content` (string): Контент редактора
- `onInsertMarkdown` (Function): Функция вставки markdown
- `onInsertElement` (Function): Функция вставки элемента

## Возвращаемое значение

Объект с:
- `showFloatingToolbar`: Состояние видимости тулбара
- `toolbarPosition`: Позиция тулбара {x, y}
- `handleSelectionChange`: Обработчик изменения выделения
- `handleFloatingInsertMarkdown`: Обработчик вставки markdown
- `handleFloatingInsertElement`: Обработчик вставки элемента
- `handleBlur`: Обработчик потери фокуса

## Особенности

- Автоматически показывает тулбар при выделении текста
- Позиционирует тулбар относительно выделения
- Скрывает тулбар при клике вне textarea и тулбара
- Скрывает тулбар при изменении контента (переключение вкладок)
- Интегрируется с утилитами позиционирования из toolbar/
- Поддерживает вставку markdown и элементов через тулбар

## Использование

```javascript
const {
  showFloatingToolbar,
  toolbarPosition,
  handleSelectionChange,
  handleFloatingInsertMarkdown,
  handleFloatingInsertElement,
  handleBlur
} = useFloatingToolbar(textareaRef, content, onInsertMarkdown, onInsertElement);

// В JSX:
<textarea
  ref={textareaRef}
  onSelect={handleSelectionChange}
  onBlur={handleBlur}
  ...
/>
{showFloatingToolbar && (
  <FloatingToolbar
    position={toolbarPosition}
    onInsertMarkdown={handleFloatingInsertMarkdown}
    onInsertElement={handleFloatingInsertElement}
  />
)}
```