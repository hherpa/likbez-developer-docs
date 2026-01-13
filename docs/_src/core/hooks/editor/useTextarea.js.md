# useTextarea

Хук для управления textarea элементом.

## Описание

Инкапсулирует все утилиты для работы с текстовым полем.

## Параметры

- `content` (string): Контент для textarea
- `onChange` (Function): Функция изменения контента

## Возвращаемое значение

Объект с:
- `internalValueRef`: Ref на внутреннее значение
- `syncContent`: Функция синхронизации контента
- `removeFocusStyles`: Функция удаления стилей фокуса
- `addEventListeners`: Функция добавления обработчиков событий
- `handleInput`: Обработчик ввода текста
- `handleContentChange`: Обработчик изменения контента
- `handleDragOver`: Обработчик drag over

## Особенности

- Нормализует контент при синхронизации и вводе
- Сохраняет позицию курсора при обновлении контента
- Удаляет стили фокуса для кастомного оформления
- Добавляет обработчики событий для textarea
- Обрабатывает drag over события
- Интегрируется с ContentNormalizer для нормализации контента

## Использование

```javascript
const {
  internalValueRef,
  syncContent,
  handleInput,
  handleDragOver
} = useTextarea(content, onChange);

// В JSX:
<textarea
  ref={syncContent}
  onInput={handleInput}
  onDragOver={handleDragOver}
  value={content}
/>
```