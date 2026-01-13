# useToolbarAnimation

Управление анимацией тулбара.

## Описание

Отвечает ТОЛЬКО за управление анимацией появления/исчезновения.

## Параметры

- `isVisible` (boolean): Видимость тулбара

## Возвращаемое значение

- `animationState`: Состояние анимации ('hidden', 'appearing', 'disappearing')

## Особенности

- Управляет анимацией появления/исчезновения тулбара
- Скрывает тулбар после анимации исчезновения
- Поддерживает три состояния: hidden, appearing, disappearing

## Использование

```javascript
const animationState = useToolbarAnimation(isVisible);

// В JSX:
<div className={`toolbar ${animationState}`}>
  {/* Содержимое тулбара */}
</div>

// CSS:
.toolbar.appearing {
  animation: fadeIn 0.2s ease-out;
}
.toolbar.disappearing {
  animation: fadeOut 0.2s ease-out;
}
```