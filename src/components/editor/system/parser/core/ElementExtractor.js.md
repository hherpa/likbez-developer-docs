# ElementExtractor.js

## Общее описание
Файл `ElementExtractor.js` содержит функцию для извлечения всех типов элементов из текстового контента. Вместо создания отдельного класса используется простая функция, которая координирует работу различных специализированных экстракторов.

## Основная функция

### extractAllElements(content)
Извлекает все элементы из контента, используя специализированные функции для каждого типа элемента.

**Параметры:**
- `content` (string): Контент для анализа

**Возвращает:**
- `Object`: Объект с извлеченными элементами, содержащий следующие поля:
  - `title` (string): Заголовок документа
  - `latexElements` (Array): Массив LaTeX элементов
  - `mediaElements` (Array): Массив медиа элементов
  - `handleElements` (Array): Массив элементов-маркеров
  - `symbolElements` (Array): Массив символьных элементов
  - `elementElements` (Array): Массив элементов-тегов
  - `linkElements` (Array): Массив ссылок
  - `colorElements` (Array): Массив цветовых элементов

## Зависимости
Файл импортирует функции извлечения для различных типов элементов:
- `extractTitle` из `../elements/MarkdownExtractor.js`
- `extractLatexElements` из `../elements/LatexExtractor.js`
- `extractMediaElements` из `../elements/MediaExtractor.js`
- `extractHandleElements` из `../elements/HandleExtractor.js`
- `extractSymbolElements` из `../elements/SymbolExtractor.js`
- `extractTagElements` из `../elements/TagExtractor.js`
- `extractLinkElements` из `../elements/LinkExtractor.js`
- `extractColorElements` из `../elements/ColorExtractor.js`

## Использование
Функция используется в основном процессе парсинга для извлечения всех элементов из текста перед их дальнейшей обработкой и построением результата.