# useEnterKeyHandler

Хук для обработки нажатия клавиши Enter.

## Описание

Отвечает за обработку всех вариантов нажатия Enter в редактируемом элементе.

## Параметры

- `element` (Object): Элемент для редактирования
- `elementPosition` (number): Позиция элемента в контенте
- `originalContent` (string): Исходный контент
- `onChange` (Function): Функция изменения контента
- `editRef` (Object): Ref на редактируемый элемент
- `setIsEditing` (Function): Функция установки состояния редактирования
- `setShowFloatingToolbar` (Function): Функция управления тулбаром

## Возвращаемое значение

- `handleEnterKey`: Обработчик события keyDown для Enter

## Особенности

- Обрабатывает Ctrl/Cmd+Enter для закрытия редактирования
- Обрабатывает Shift+Enter для переноса строки внутри параграфа или заголовка
- Обрабатывает Enter для создания нового параграфа (для параграфов и заголовков)
- Для заголовков: обрабатывает markdown префикс
- Для параграфов: обычная логика создания нового параграфа
- Автоматически начинает редактирование нового параграфа
- Сохраняет позицию курсора при разделении текста

## Использование

```javascript
const handleEnterKey = useEnterKeyHandler({
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
  if (handleEnterKey(e)) {
    return;
  }
  // Другие обработчики
};
```