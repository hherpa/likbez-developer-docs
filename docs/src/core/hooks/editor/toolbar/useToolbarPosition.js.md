# useToolbarPosition

Управление позиционированием тулбара.

## Описание

Отвечает ТОЛЬКО за позиционирование и корректировку viewport.

## Параметры

- `position` (Object): Исходная позиция {x, y}
- `toolbarRef` (React.RefObject): ref тулбара

## Возвращаемое значение

- `adjustedPosition`: Скорректированная позиция

## Особенности

- Управляет позиционированием тулбара с учетом границ viewport
- Корректирует позицию для предотвращения выхода за границы экрана
- Использует constrainToViewport для корректировки
- Обновляет позицию при изменении размера окна
- Обеспечивает правильное позиционирование даже в крайних случаях

## Использование

```javascript
const adjustedPosition = useToolbarPosition(position, toolbarRef);

// В JSX:
<div 
  ref={toolbarRef}
  style={{
    position: 'absolute',
    left: adjustedPosition.x,
    top: adjustedPosition.y
  }}
>
  {/* Содержимое тулбара */}
</div>
```