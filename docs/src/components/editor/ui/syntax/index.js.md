# index.js

## Описание
Файл экспорта для модуля подсветки синтаксиса.

## Экспортируемые компоненты
- `SyntaxHighlighter` - компонент подсветки синтаксиса
- `HighlightOverlay` - компонент оверлея подсветки
- `LineNumbers` - компонент нумерации строк
- `tokenize` - функция токенизации
- `escapeHtml` - функция экранирования HTML
- `getTokenColor` - функция получения цвета токена
- `Token` - класс токена
- `TOKEN_TYPES` - типы токенов
- `TOKEN_PRIORITIES` - приоритеты токенов

## Структура
- Экспорт компонентов подсветки синтаксиса:
  - `SyntaxHighlighter` из `./SyntaxHighlighter`
  - `HighlightOverlay` из `./HighlightOverlay`
  - `LineNumbers` из `./LineNumbers`
  - Утилиты из `./SyntaxHighlighterUtils`:
    - `tokenize`
    - `escapeHtml`
    - `getTokenColor`
  - `Token` из `./Token`
  - Константы из `./SyntaxTokenTypes`:
    - `TOKEN_TYPES`
    - `TOKEN_PRIORITIES`

## Взаимодействия
- Использует компоненты и утилиты из подмодулей синтаксической подсветки

## Зависимости
- `./SyntaxHighlighter` - компонент подсветки синтаксиса
- `./HighlightOverlay` - компонент оверлея подсветки
- `./LineNumbers` - компонент нумерации строк
- `./SyntaxHighlighterUtils` - утилиты подсветки синтаксиса
- `./Token` - класс токена
- `./SyntaxTokenTypes` - типы токенов

## Архитектура
Файл служит точкой входа для модуля подсветки синтаксиса, обеспечивая централизованный экспорт всех необходимых компонентов и утилит. Это позволяет использовать функции подсветки синтаксиса через единый импорт.