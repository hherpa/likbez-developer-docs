# useEditableElement

Главный хук для редактируемого элемента.

## Описание

Координирует работу специализированных хуков для редактирования элемента. Отвечает за координацию всех хуков редактирования элемента.

## Параметры

- `element` (Object): Элемент для редактирования
- `elementType` (string): Тип элемента
- `elementPosition` (number): Позиция элемента в контенте
- `originalContent` (string): Исходный контент
- `onChange` (Function): Функция изменения контента
- `darkMode` (boolean): Режим темной темы

## Возвращаемое значение

Объект с:
- `isEditing`: Состояние редактирования
- `editValue`: Значение для редактирования
- `editRef`: Ref на элемент редактирования
- `showFloatingToolbar`: Видимость тулбара
- `toolbarPosition`: Позиция тулбара
- `handleDoubleClick`: Обработчик двойного клика
- `handleBlur`: Обработчик потери фокуса
- `handleKeyDown`: Обработчик нажатия клавиш
- `handleToolbarInsertMarkdown`: Обработчик вставки markdown
- `handleToolbarInsertElement`: Обработчик вставки элемента
- `setIsEditing`: Функция установки состояния редактирования

## Особенности

- Координирует работу всех под-хуков редактирования
- Интегрирует обработчики клавиш Enter и Backspace
- Управляет состоянием редактирования
- Обрабатывает двойной клик для начала редактирования
- Управляет тулбаром при выделении текста
- Обрабатывает вставку markdown и элементов через тулбар

## Использование

```javascript
const {
  isEditing,
  editValue,
  editRef,
  showFloatingToolbar,
  toolbarPosition,
  handleDoubleClick,
  handleBlur,
  handleKeyDown,
  handleToolbarInsertMarkdown,
  handleToolbarInsertElement,
  setIsEditing
} = useEditableElement({
  element,
  elementType,
  elementPosition,
  originalContent,
  onChange,
  darkMode
});

// В JSX:
<div
  onDoubleClick={handleDoubleClick}
  onBlur={handleBlur}
  onKeyDown={handleKeyDown}
  ref={editRef}
  contentEditable={isEditing}
>
  {editValue}
</div>
```