# Документация для src/components/editor/system/parser/index.js

## Описание
Этот файл является центральным экспортером для всех компонентов парсера в системе редактора. Он объединяет функциональность из различных модулей парсера и предоставляет унифицированный интерфейс для использования в других частях приложения.

## Основные компоненты

### Core (Ядро)
- PARSER_CONFIG - Конфигурация парсера из './core/ParserConfig.js'
- Parser, markdownParser, parseContent, clearParserCache, getParserStats - Основные функции парсинга из './core/ParserCore.js'
- CacheManager - Менеджер кэширования из './core/CacheManager.js'

### Content (Контент)
- MarkdownParser - Парсер Markdown из './content/MarkdownParser.js'
- ContentCleaner - Очистка контента из './content/ContentCleaner.js'
- ResultBuilder - Построитель результатов из './content/ResultBuilder.js'

### Elements (Элементы)
- extractTitle - Извлечение заголовка из './elements/MarkdownExtractor.js'
- extractLatexElements - Извлечение LaTeX элементов из './elements/LatexExtractor.js'
- extractMediaElements - Извлечение медиа элементов из './elements/MediaExtractor.js'
- extractHandleElements - Извлечение handle элементов из './elements/HandleExtractor.js'
- extractSymbolElements - Извлечение символа элементов из './elements/SymbolExtractor.js'
- extractTagElements - Извлечение тегов из './elements/TagExtractor.js'
- extractLinkElements - Извлечение ссылок из './elements/LinkExtractor.js'
- extractColorElements - Извлечение цветовых элементов из './elements/ColorExtractor.js'

### Утилиты
- getElementColors, getEmptyColors, getColor, isSupportedColor - Функции работы с цветами из './core/ColorResolver.js'
- Функции определения типов элементов из './core/elementPatterns.js':
  - isLatexElement
  - isBoxLatexElement
  - isImageElement
  - isHandleElement
  - isSymbolElement
  - isTagElement
  - isLinkElement
  - isBgColorElement
  - isColorElement
  - detectElementType
- extractAllElements - Извлечение всех элементов из './core/ElementExtractor.js'

### Валидация
- validateSyntax, hasTags - Функции синтаксической валидации из './content/SyntaxValidation.js'

## Обратная совместимость
Файл также включает несколько функций для обеспечения обратной совместимости со старыми версиями API:
- PATTERNS и SUPPORTED_COLORS - константы конфигурации
- extractElementElements - алиас для extractTagElements
- Вспомогательные функции извлечения (extractTags, extractLinks, extractSymbols, extractHandles, extractImages)
- parseMarkdownContent - обертка для parseContent
- extractColorFromTag и createColorElement - функции работы с цветовыми элементами