# useToolbarSelection

Управление видимостью тулбара при выделении.

## Описание

Отвечает ТОЛЬКО за показ тулбара при выделении текста (SRP).

## Параметры

- `isEditing` (boolean): Режим редактирования
- `editRef` (React.RefObject): ref элемента редактирования

## Возвращаемое значение

Объект с:
- `showFloatingToolbar`: Видимость тулбара
- `toolbarPosition`: Позиция тулбара {x, y}
- `setShowFloatingToolbar`: Функция управления видимостью тулбара

## Особенности

- Показывает тулбар при выделении текста в редактируемом элементе
- Скрывает тулбар при потере выделения
- Позиционирует тулбар относительно выделения
- Скрывает тулбар при клике вне элемента редактирования
- Использует debounce для оптимизации позиционирования
- Поддерживает задержку скрытия для предотвращения мигания

## Использование

```javascript
const { showFloatingToolbar, toolbarPosition, setShowFloatingToolbar } = useToolbarSelection(
  isEditing, 
  editRef
);

// В JSX:
{showFloatingToolbar && (
  <FloatingToolbar position={toolbarPosition} />
)}
```