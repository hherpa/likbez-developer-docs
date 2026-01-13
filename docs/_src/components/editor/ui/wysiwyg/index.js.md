# index.js

## Описание
Файл экспорта компонентов WYSIWYG редактора и утилит. Служит единой точкой входа для всех модулей wysiwyg.

## Экспортируемые компоненты
- `EditableElement` - редактируемый элемент
- `EditableContentRenderer` - рендерер редактируемого контента
- `EditorContentPreview` - предпросмотр контента редактора
- `updateContent` - функция обновления контента
- `updateContentWithMarkdown` - функция обновления контента с markdown
- `createMarkdownHandler` - обработчик markdown для тулбара
- `createElementHandler` - обработчик элементов для тулбара

## Структура
- Экспорт компонентов редактора:
  - `EditableElement` из `./editable/EditableElement`
  - `EditableContentRenderer` из `./editable/EditableContentRenderer`
  - `EditorContentPreview` из `./EditorContentPreview`
- Экспорт утилит обновления контента:
  - `updateContent` из `./updaters/ContentUpdater`
  - `updateContentWithMarkdown` из `./updaters/MarkdownUpdater`
- Экспорт обработчиков тулбара:
  - `createMarkdownHandler` из `../toolbar/handlers/MarkdownHandler`
  - `createElementHandler` из `../toolbar/handlers/ElementHandler`

## Взаимодействия
- Использует компоненты из подмодуля `editable`
- Использует утилиты обновления контента из подмодуля `updaters`
- Использует обработчики тулбара из подмодуля `toolbar/handlers`

## Зависимости
- `./editable/EditableElement` - редактируемый элемент
- `./editable/EditableContentRenderer` - рендерер редактируемого контента
- `./EditorContentPreview` - предпросмотр контента
- `./updaters/ContentUpdater` - утилиты обновления контента
- `./updaters/MarkdownUpdater` - утилиты обновления контента с markdown
- `../toolbar/handlers/MarkdownHandler` - обработчик markdown
- `../toolbar/handlers/ElementHandler` - обработчик элементов

## Архитектура
Файл служит точкой входа для модуля WYSIWYG редактора, обеспечивая централизованный экспорт всех необходимых компонентов и утилит. Соблюдает порядок экспорта: сначала базовые компоненты, затем зависимые. Это позволяет использовать все функции WYSIWYG редактора через единый импорт.