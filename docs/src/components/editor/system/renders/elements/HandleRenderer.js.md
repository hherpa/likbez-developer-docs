# HandleRenderer.js

## Описание
HandleRenderer - рендерер для handles. Соблюдает SOLID принципы.

## Экспортируемые компоненты
- `HandleRenderer` - класс рендерера для handles
- `HandleRendererComponent` - функциональный компонент для обратной совместимости

## Структура
- Класс `HandleRenderer`, наследующий `BaseRenderer`
- Метод `renderElement` для рендеринга handles
- Функциональный компонент `HandleRendererComponent` для обратной совместимости

## Взаимодействие
- Наследует от `BaseRenderer` и реализует метод `renderElement`
- Использует `Handle` и `Position` из 'reactflow' для создания handles
- Принимает элемент и контекст для рендеринга

## Зависимости
- `react` для создания компонентов
- `reactflow` для работы с handles
- `BaseRenderer` из '../core/BaseRenderer'

## Архитектура
Класс `HandleRenderer` наследует от `BaseRenderer` и реализует метод `renderElement` для рендеринга handles. Компонент создает div элемент с левым и правым handles, а также текстом между ними. В зависимости от контекста, handles могут быть реализованы как компоненты `Handle` из reactflow или как обычные div элементы. Также экспортируется функциональный компонент `HandleRendererComponent` для обратной совместимости, который создает экземпляр `HandleRenderer` и вызывает его метод `renderElement`.