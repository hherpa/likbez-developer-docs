# useTextExtraction

Извлечение текста из contentEditable.

## Описание

Отвечает ТОЛЬКО за извлечение текста (SRP).

## Параметры

- `editRef` (HTMLElement): ref элемента contentEditable
- `elementType` (string): тип элемента

## Возвращаемое значение

- `extractTextFromContentEditable`: Функция извлечения текста из contentEditable

## Особенности

- Извлекает текст из contentEditable в зависимости от типа элемента
- Для заголовков берет весь текст (включая префикс markdown)
- Для параграфов сохраняет переносы строк (Shift+Enter создает <br>)
- Для списков сохраняет переносы строк и маркеры
- Для hr элементов нормализует ввод дефисов
- Для block элементов берет текст напрямую
- Для остальных использует innerText

## Использование

```javascript
const extractTextFromContentEditable = useTextExtraction();

// В обработчике onBlur:
const handleBlur = () => {
  const newText = extractTextFromContentEditable(editRef, element.type);
  // Обработка извлеченного текста
};
```