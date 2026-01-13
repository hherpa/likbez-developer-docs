# Logger.js

## Назначение
Централизованный логгер для Content Preview в редакторе, отвечающий за логирование различных событий и ошибок.

## Экспортируемые компоненты
- `log` - объект логгера с методами для различных компонентов

## Структура
1. Константа DEBUG для включения/выключения логирования
2. Объект `log` с методами:
   - `updater` - для ContentUpdater
   - `remover` - для TextRemover
   - `finder` - для TextFinder
   - `inserter` - для ElementInserter
   - `toolbar` - для ToolbarHandlers
   - `dropdown` - для Dropdowns
   - `editable` - для EditableElement
   - `preview` - для EditorContentPreview
   - `error` - для ошибок
   - `warn` - для предупреждений

## Взаимодействия
1. Предоставляет методы логирования для различных компонентов редактора
2. Использует console.log, console.error и console.warn для вывода сообщений
3. Проверяет флаг DEBUG для включения/выключения логирования
4. Принимает сообщения и данные для логирования
5. Экспортирует объект логгера как default

## Зависимости
- Нет внешних зависимостей

## Архитектура
Следует принципу единственной ответственности (SRP), отвечая только за логирование. Предоставляет отдельные методы для различных компонентов системы.

Объект `log` содержит методы:
1. `updater` - логирование для ContentUpdater
2. `remover` - логирование для TextRemover
3. `finder` - логирование для TextFinder
4. `inserter` - логирование для ElementInserter
5. `toolbar` - логирование для ToolbarHandlers
6. `dropdown` - логирование для Dropdowns
7. `editable` - логирование для EditableElement
8. `preview` - логирование для EditorContentPreview
9. `error` - логирование ошибок
10. `warn` - логирование предупреждений

Все методы (кроме error и warn) проверяют флаг DEBUG перед выводом сообщений.
Методы error и warn всегда выводят сообщения независимо от флага DEBUG.