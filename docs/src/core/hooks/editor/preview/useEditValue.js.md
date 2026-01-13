# useEditValue

Управление значением редактирования.

## Описание

Отвечает ТОЛЬКО за инициализацию и синхронизацию editValue (SRP).

## Параметры

- `element` (Object): Элемент
- `elementType` (string): Тип элемента
- `elementPosition` (number): Позиция элемента
- `originalContent` (string): Исходный контент

## Возвращаемое значение

- `[editValue, setEditValue]`: Значение для редактирования и функция его установки

## Особенности

- Инициализирует значение для редактирования элемента
- Обрабатывает различные типы элементов (ul, hr, block, заголовки, параграфы)
- Для списков добавляет маркеры "-" перед каждым элементом
- Для hr элементов берет значение из originalContent
- Для block элементов берет content напрямую
- Для заголовков показывает текст с префиксом markdown
- Для параграфов показывает полный markdown с LaTeX синтаксисом

## Использование

```javascript
const [editValue, setEditValue] = useEditValue(element, elementType, elementPosition, originalContent);

// В JSX:
<div contentEditable>
  {editValue}
</div>
```