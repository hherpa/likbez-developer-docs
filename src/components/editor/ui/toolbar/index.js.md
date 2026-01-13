# index.js

## Описание
Этот файл предоставляет реэкспорт утилит для обратной совместимости.

## Ответственность
Только реэкспорт функций из специализированных модулей.

## Экспорты


## Структура
- Импорт функции `insertElement` из `./utils/elementInsertion`
- Реэкспорт функций:
  - `getSelectedText` из `./utils/textareaUtils`
  - `insertElement` из `./utils/elementInsertion`
  - `insertMarkdown` из `./utils/markdownInsertion`
- Создание алиаса `insertTag` для функции `insertElement`

## Взаимодействия
- Использует утилиты из подмодулей:
  - `./utils/textareaUtils` для работы с выделенным текстом
  - `./utils/elementInsertion` для вставки элементов
  - `./utils/markdownInsertion` для вставки markdown

## Зависимости
- `./utils/textareaUtils` - утилиты для работы с текстовой областью
- `./utils/elementInsertion` - утилиты для вставки элементов
- `./utils/markdownInsertion` - утилиты для вставки markdown

## Архитектура
Файл служит точкой входа для модуля Toolbar, обеспечивая обратную совместимость путем реэкспорта функций из специализированных модулей. Это позволяет использовать функции из разных утилитных файлов через единый импорт.