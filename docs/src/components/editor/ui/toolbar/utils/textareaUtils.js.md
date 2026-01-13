# textareaUtils.js

## Назначение
Утилиты для работы с textarea в редакторе, обеспечивающие получение выделенного текста и управление курсором.

## Экспортируемые компоненты
- `getSelectedTextFromTextarea` - получение выделенного текста из textarea
- `getSelectedText` - получение выделенного текста по селектору
- `calculateCursorOffset` - расчет смещения курсора для markdown элементов
- `setCursorPosition` - установка позиции курсора в textarea

## Структура
1. Функция `getSelectedTextFromTextarea` для получения выделенного текста из textarea
2. Функция `getSelectedText` для получения выделенного текста по селектору
3. Функция `calculateCursorOffset` для расчета смещения курсора
4. Функция `setCursorPosition` для установки позиции курсора

## Взаимодействия
1. Работает с HTMLTextAreaElement
2. Использует document.querySelector для поиска textarea по классу
3. Работает с selectionStart и selectionEnd свойствами textarea
4. Использует setTimeout для асинхронной установки фокуса и позиции курсора

## Зависимости
- Нет внешних зависимостей

## Архитектура
Следует принципу единственной ответственности (SRP), предоставляя только утилиты для работы с textarea.

Функция `getSelectedTextFromTextarea` реализует логику:
1. Проверяет наличие textarea
2. Получает позиции выделения (selectionStart и selectionEnd)
3. Возвращает подстроку из значения textarea

Функция `getSelectedText` реализует логику:
1. Находит textarea по селектору '.editor-textarea'
2. Вызывает getSelectedTextFromTextarea с найденным элементом

Функция `calculateCursorOffset` реализует логику:
1. Использует таблицу смещений для различных типов markdown
2. Возвращает смещение в зависимости от типа markdown и наличия выделенного текста

Функция `setCursorPosition` реализует логику:
1. Проверяет наличие textarea
2. Использует setTimeout для асинхронной установки фокуса
3. Устанавливает позицию курсора с помощью setSelectionRange