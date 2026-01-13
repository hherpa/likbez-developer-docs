# useEditorNodeWidth

Хук для управления шириной узла редактора.

## Описание

Отвечает только за синхронизацию ширины узла с nodeData. Соблюдает принцип Single Responsibility Principle (SRP).

## Параметры

- `nodeData` (Object): Данные узла
- `onNodeDataChange` (Function): Функция изменения данных узла

## Возвращаемое значение

Объект с:
- `nodeWidth`: Текущая ширина узла
- `handleWidthChange`: Обработчик изменения ширины

## Особенности

- Синхронизирует ширину узла с nodeData
- Обрабатывает ввод числовых значений
- Поддерживает сброс ширины при пустом значении
- Валидация ввода (только числовые значения)

## Использование

```javascript
const { nodeWidth, handleWidthChange } = useEditorNodeWidth(nodeData, onNodeDataChange);

// В JSX:
<input
  type="number"
  value={nodeWidth}
  onChange={handleWidthChange}
  placeholder="Ширина узла"
/>
```