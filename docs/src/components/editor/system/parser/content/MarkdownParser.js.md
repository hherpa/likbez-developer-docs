# MarkdownParser

Класс `MarkdownParser` отвечает ТОЛЬКО за парсинг markdown элементов в тексте.

## Импорты

```javascript
import { PARSER_CONFIG } from '../core/ParserConfig.js';
import { detectElementType } from '../core/elementPatterns.js';
import { parseMarkdownBlocks, processInlineMarkdown as _processInlineMarkdown } from './MarkdownParserUtils.js';
import { parseMarkdownElementsFromOriginal as _parseOriginal } from './MarkdownOriginalParser.js';
```

## Методы

### parseMarkdownElements

Парсит markdown элементы из текста.

**Параметры:**
- `text` (string): Текст для парсинга

**Возвращает:**
- `Array`: Массив markdown элементов

**Описание:**
Метод анализирует текст и выделяет из него различные markdown элементы:
- Заголовки (h1, h2, h3)
- Списки (ul)
- Параграфы (p)

Каждый элемент содержит информацию о типе, содержимом и позиции в тексте.

### parseMarkdownBlocks

Парсит markdown блоки, разделенные горизонтальной линией (HR).

**Параметры:**
- `text` (string): Текст для парсинга

**Возвращает:**
- `Array`: Массив элементов

### parseMarkdownElementsFromOriginal

Парсит markdown элементы из исходного текста с правильными позициями.

**Параметры:**
- `content` (string): Исходный текст

**Возвращает:**
- `Array`: Массив markdown элементов

### processInlineMarkdown

Обрабатывает inline markdown элементы.

**Параметры:**
- `text` (string): Текст для обработки

**Возвращает:**
- `object`: Объект с типом и содержимым