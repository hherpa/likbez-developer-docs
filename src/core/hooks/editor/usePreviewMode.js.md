# usePreviewMode

Хук для управления режимом превью редактора.

## Описание

Отвечает только за выбор типа превью (flow или content). Соблюдает принцип Single Responsibility Principle (SRP).

## Параметры

- `defaultMode` (string): Режим превью по умолчанию ('flow' или 'content', по умолчанию 'flow')

## Возвращаемое значение

Объект с:
- `previewMode`: Текущий режим превью
- `setPreviewMode`: Функция установки режима превью
- `toggleMode`: Функция переключения режима превью

## Особенности

- Управляет выбором между режимами flow и content
- Предоставляет удобные методы для переключения режимов
- Поддерживает начальное состояние

## Использование

```javascript
const { previewMode, setPreviewMode, toggleMode } = usePreviewMode('flow');

// В JSX:
<button onClick={() => setPreviewMode('flow')}>
  Flow режим
</button>
<button onClick={() => setPreviewMode('content')}>
  Content режим
</button>
<button onClick={toggleMode}>
  Переключить режим
</button>

{previewMode === 'flow' && <FlowPreview />}
{previewMode === 'content' && <ContentPreview />}
```