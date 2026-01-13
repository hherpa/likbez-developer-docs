# useTextareaView

Хук для управления видимостью textarea.

## Описание

Отвечает только за переключение между content preview и textarea. Соблюдает принцип Single Responsibility Principle (SRP).

## Параметры

- `defaultShow` (boolean): Начальное состояние видимости textarea (по умолчанию false)

## Возвращаемое значение

Объект с:
- `showTextarea`: Состояние видимости textarea
- `setShowTextarea`: Функция установки состояния видимости
- `toggleTextarea`: Функция переключения видимости

## Особенности

- Управляет видимостью textarea в режиме редактирования
- Предоставляет удобные методы для переключения состояния
- Поддерживает начальное состояние

## Использование

```javascript
const { showTextarea, setShowTextarea, toggleTextarea } = useTextareaView(false);

// В JSX:
{showTextarea ? (
  <textarea value={content} onChange={handleChange} />
) : (
  <Preview content={content} />
)}
<button onClick={toggleTextarea}>
  {showTextarea ? 'Показать превью' : 'Показать редактор'}
</button>
```