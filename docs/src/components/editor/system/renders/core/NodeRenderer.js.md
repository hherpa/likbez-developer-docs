# NodeRenderer.js

## Описание
NodeRenderer - рендерер узла (заменяет BaseNodeRenderer). Соблюдает SOLID принципы:
- SRP: только рендеринг узла (заголовок, контент, футер, handles)
- OCP: легко расширяется новыми типами узлов
- LSP: работает с любыми конфигурациями узлов
- ISP: только необходимые методы для рендеринга узла
- DIP: зависит от абстракций (ContentRenderer, парсер)

## Экспортируемые компоненты
- `NodeRenderer` - класс рендерера узла

## Структура
- Класс `NodeRenderer`, наследующий `BaseRenderer`
- Метод `render` для рендеринга всего узла
- Методы `renderHandles`, `renderContent`, `renderMainContent`, `renderEmptyNode`, `renderHeader`, `renderFooter` для рендеринга отдельных частей узла
- Методы `updateConfig`, `updateStyles` для обновления конфигурации и стилей

## Взаимодействие
- Наследует от `BaseRenderer` и реализует метод `renderElement`
- Использует `RenderContext` из './BaseRenderer'
- Использует `contentRenderer` из '../content/ContentRenderer'
- Использует `parseMarkdownContent` из '../../parser'
- Использует `renderHeader` и `renderFooter` из './NodeHeader' и './NodeFooter'
- Принимает данные узла, контекст и стили для рендеринга

## Зависимости
- `react` для создания компонентов
- `reactflow` для работы с handles
- `BaseRenderer` и `RenderContext` из './BaseRenderer'
- `contentRenderer` из '../content/ContentRenderer'
- `parseMarkdownContent` из '../../parser'
- `renderHeader` и `renderEmptyNode` из './NodeHeader'
- `renderFooter` из './NodeFooter'

## Архитектура
Класс `NodeRenderer` наследует от `BaseRenderer` и реализует рендеринг узлов. Компонент отвечает за рендеринг всего узла, включая handles, контент, заголовок и футер. Использует ContentRenderer для рендеринга основного контента узла. Реализует методы для рендеринга отдельных частей узла, а также методы для обновления конфигурации и стилей.