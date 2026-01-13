# useBackspaceKeyHandler

Хук для обработки нажатия клавиши Backspace.

## Описание

Отвечает за обработку Backspace в начале параграфа (объединение с предыдущим).

## Параметры

- `element` (Object): Элемент для редактирования
- `elementPosition` (number): Позиция элемента в контенте
- `originalContent` (string): Исходный контент
- `onChange` (Function): Функция изменения контента
- `editRef` (Object): Ref на редактируемый элемент
- `setIsEditing` (Function): Функция установки состояния редактирования
- `setShowFloatingToolbar` (Function): Функция управления тулбаром

## Возвращаемое значение

- `handleBackspaceKey`: Обработчик события keyDown для Backspace

## Особенности

- Обрабатывает Backspace в начале параграфа
- Объединяет текущий параграф с предыдущим
- Удаляет пустые параграфы
- Автоматически активирует редактирование предыдущего элемента
- Сохраняет позицию курсора при объединении
- Поддерживает заголовки (h1, h2, h3)

## Использование

```javascript
const handleBackspaceKey = useBackspaceKeyHandler({
  element,
  elementPosition,
  originalContent,
  onChange,
  editRef,
  setIsEditing,
  setShowFloatingToolbar
});

// В обработчике keyDown:
const handleKeyDown = (e) => {
  if (handleBackspaceKey(e)) {
    return;
  }
  // Другие обработчики
};
```