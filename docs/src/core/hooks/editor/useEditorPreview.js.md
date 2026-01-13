# useEditorPreview

Хук для управления состоянием предпросмотра редактора.

## Описание

Отвечает только за управление видимостью превью. Соблюдает принцип Single Responsibility Principle (SRP).

## Параметры

- `defaultShow` (boolean): Начальное состояние видимости превью (по умолчанию true)

## Возвращаемое значение

Объект с:
- `showPreview`: Состояние видимости превью
- `setShowPreview`: Функция установки состояния видимости
- `togglePreview`: Функция переключения видимости

## Особенности

- Управляет видимостью предпросмотра редактора
- Предоставляет удобные методы для переключения состояния
- Поддерживает начальное состояние

## Использование

```javascript
const { showPreview, setShowPreview, togglePreview } = useEditorPreview(true);

// В JSX:
{showPreview && <PreviewComponent />}
<button onClick={togglePreview}>
  {showPreview ? 'Скрыть превью' : 'Показать превью'}
</button>
```