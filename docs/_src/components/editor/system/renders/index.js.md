# index.js

## Описание
Файл экспорта всех рендереров элементов. Реализует новую архитектуру согласно заданию 1.

## Экспортируемые компоненты
### Основные компоненты (core/)
- `BaseRenderer` - базовый рендерер
- `RendererFactory` - фабрика рендереров
- `RenderContext` - контекст рендеринга
- `RendererManager` - менеджер рендереров
- `rendererManager` - экземпляр менеджера рендереров
- `NodeRenderer` - рендерер узлов

### Рендеринг контента (content/)
- `ContentRenderer` - рендерер контента
- `contentRenderer` - экземпляр рендерера контента
- `ElementBuilder` - строитель элементов
- `ElementSorter` - сортировщик элементов

### Элементы (elements/)
- `MarkdownRenderer` - рендерер markdown
- `MarkdownRendererComponent` - компонент рендерера markdown
- `SymbolRenderer` - рендерер символов
- `SymbolRendererComponent` - компонент рендерера символов
- `ColorRenderer` - рендерер цвета
- `ColorRendererComponent` - компонент рендерера цвета
- `TagRenderer` - рендерер тегов
- `TagRendererComponent` - компонент рендерера тегов
- `LinkRenderer` - рендерер ссылок
- `LinkRendererComponent` - компонент рендерера ссылок
- `InlineLatexRenderer` - рендерер inline latex
- `InlineLatexRendererComponent` - компонент рендерера inline latex
- `BoxLatexRenderer` - рендерер блочного latex
- `BoxLatexRendererComponent` - компонент рендерера блочного latex
- `ImageRenderer` - рендерер изображений
- `ImageRendererComponent` - компонент рендерера изображений
- `HandleRenderer` - рендерер хендлов
- `HandleRendererComponent` - компонент рендерера хендлов

## Структура
- Импорт инициализатора рендерера из `./core/RendererInitializer`
- Экспорт компонентов из подмодулей:
  - `./core/BaseRenderer` - основные компоненты
  - `./core/RenderContext` - контекст рендеринга
  - `./core/RendererManager` - менеджер рендереров
  - `./core/NodeRenderer` - рендерер узлов
  - `./content/ContentRenderer` - рендеринг контента
  - `./content/ElementBuilder` - строитель элементов
  - `./content/ElementSorter` - сортировщик элементов
  - `./elements/MarkdownRenderer` - рендерер markdown
  - `./elements/SymbolRenderer` - рендерер символов
  - `./elements/ColorRenderer` - рендерер цвета
  - `./elements/TagRenderer` - рендерер тегов
  - `./elements/LinkRenderer` - рендерер ссылок
  - `./elements/InlineLatexRenderer` - рендерер inline latex
  - `./elements/BoxLatexRenderer` - рендерер блочного latex
  - `./elements/ImageRenderer` - рендерер изображений
  - `./elements/HandleRenderer` - рендерер хендлов

## Взаимодействия
- Импортирует и инициализирует рендереры
- Экспортирует все рендереры элементов для использования в других модулях

## Зависимости
- `./core/RendererInitializer` - инициализатор рендерера
- `./core/BaseRenderer` - базовые компоненты рендеринга
- `./core/RenderContext` - контекст рендеринга
- `./core/RendererManager` - менеджер рендереров
- `./core/NodeRenderer` - рендерер узлов
- `./content/ContentRenderer` - рендеринг контента
- `./content/ElementBuilder` - строитель элементов
- `./content/ElementSorter` - сортировщик элементов
- `./elements/MarkdownRenderer` - рендерер markdown
- `./elements/SymbolRenderer` - рендерер символов
- `./elements/ColorRenderer` - рендерер цвета
- `./elements/TagRenderer` - рендерер тегов
- `./elements/LinkRenderer` - рендерер ссылок
- `./elements/InlineLatexRenderer` - рендерер inline latex
- `./elements/BoxLatexRenderer` - рендерер блочного latex
- `./elements/ImageRenderer` - рендерер изображений
- `./elements/HandleRenderer` - рендерер хендлов

## Архитектура
Файл служит точкой входа для модуля рендеринга, обеспечивая централизованный экспорт всех рендереров элементов. Следует новой архитектуре согласно заданию 1. Организация экспорта разделена на три категории:
1. Основные компоненты (core/)
2. Рендеринг контента (content/)
3. Элементы (elements/)

Это позволяет использовать все рендереры через единый импорт.