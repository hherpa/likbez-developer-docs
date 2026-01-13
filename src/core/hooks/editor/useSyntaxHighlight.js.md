# useSyntaxHighlight

Хук для управления подсветкой синтаксиса.

## Описание

Оптимизирует производительность подсветки через мемоизацию и debounce.

## Параметры

- `content` (string): Контент для подсветки
- `enabled` (boolean): Включена ли подсветка (по умолчанию true)
- `debounceMs` (number): Задержка debounce в миллисекундах (по умолчанию 50)

## Возвращаемое значение

Объект с:
- `content`: Контент с подсветкой
- `enabled`: Включена ли подсветка
- `isLoading`: Выполняется ли обработка подсветки

## Особенности

- Оптимизирует производительность через мемоизацию
- Использует debounce для больших документов
- Предотвращает повторную обработку неизмененного контента
- Поддерживает включение/выключение подсветки

## Использование

```javascript
const { content: highlightedContent, enabled, isLoading } = useSyntaxHighlight(
  content, 
  true, 
  100
);

// В JSX:
{isLoading ? (
  <div>Загрузка...</div>
) : (
  <pre dangerouslySetInnerHTML={{ __html: highlightedContent }} />
)}
```