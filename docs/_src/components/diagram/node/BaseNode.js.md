# BaseNode

## 1. Назначение компонента

BaseNode - главный компонент узла диаграммы с разделенной ответственностью, реализующий архитектуру с четким разделением обязанностей между различными классами:

- `BaseNodeConfig` - отвечает за конфигурацию и настройки узла
- `BaseNodeStyles` - отвечает за стили и CSS
### Main Component: BaseNode
```javascript
export const BaseNode = React.memo(({ 
  data, 

## 2. Основные функции и методы

### Основной компонент BaseNode
- **Мемоизация экземпляров классов**: Создает экземпляры `BaseNodeStyles` и `NodeRenderer` один раз с помощью `useMemo`
- **Мемоизация результата рендеринга**: Использует `useMemo` для оптимизации рендеринга
- **Рендеринг узла**: Делегирует рендеринг экземпляру `NodeRenderer`

### BaseNodeWrapper
- **Интеграция с темой**: Использует хук `useTheme` для получения текущей темы
- **Передача темы**: Передает параметр `darkMode` в основной компонент `BaseNode`

### Вспомогательные хуки
- **useBaseNodeConfig**: Хук для получения конфигурации узла с мемоизацией

## 3. Входные параметры (props)

### BaseNode
| Параметр | Тип | По умолчанию | Описание |
|---------|-----|-------------|----------|
| data | Object | undefined | Данные узла |
| selected | boolean | false | Выбран ли узел |
| darkMode | boolean | false | Темная тема |
| nodeProps | Object | {} | Дополнительные свойства узла |
| config | BaseNodeConfig | defaultConfig | Конфигурация узла |

### BaseNodeWrapper
Принимает все пропсы, которые передаются в `BaseNode`, а также:
- Получает тему через хук `useTheme`

## 4. Возвращаемые значения

Компонент возвращает React-элемент, представляющий узел диаграммы, который включает:
- Контейнер узла со стилями
- Handles (если они включены и нет кастомных handles)
- Заголовок узла
- Основной контент узла
- Футер узла (если включен)

## 5. Взаимодействие с другими компонентами

### Зависимости
- **React**: Основной фреймворк
- **reactflow**: Библиотека для создания диаграмм
- **useTheme**: Хук для получения темы приложения
- **BaseNodeConfig**: Конфигурация узла
- **NodeRenderer**: Рендерер узла
- **BaseNodeStyles**: Стили узла

### Используемые компоненты
- **Handle** из reactflow: Для создания точек соединения
- **BaseNodeConfig**: Для конфигурации узла
- **BaseNodeStyles**: Для стилей узла
- **NodeRenderer**: Для рендеринга узла
- **BaseNodeHandles**: Для логики handles

## 6. Используемые хуки и зависимости

### React хуки
- **useMemo**: Для мемоизации экземпляров классов и результата рендеринга
- **useTheme**: Для получения текущей темы приложения

### Внешние зависимости
- **react**: Основной фреймворк
- **reactflow**: Библиотека для создания диаграмм
- **BaseNodeConfig**: Конфигурация узла
- **BaseNodeStyles**: Стили узла
- **BaseNodeHandles**: Логика handles
- **NodeRenderer**: Рендерер узла
- **ContentRenderer**: Рендерер контента
- **parseMarkdownContent**: Парсер markdown контента

## 7. Архитектура

Компонент следует принципам SOLID:

1. **SRP (Single Responsibility Principle)**: Каждый класс имеет одну ответственность
2. **OCP (Open/Closed Principle)**: Легко расширяется новыми типами узлов
3. **LSP (Liskov Substitution Principle)**: Работает с любыми конфигурациями узлов
4. **ISP (Interface Segregation Principle)**: Только необходимые методы для рендеринга узла
5. **DIP (Dependency Inversion Principle)**: Зависит от абстракций (ContentRenderer, парсер)

## 8. Структура файлов

```
src/components/diagram/node/
├── BaseNode.js          # Основной компонент
├── BaseNodeConfig.js    # Конфигурация узла
├── BaseNodeStyles.js    # Стили узла
├── BaseNodeHandles.js   # Логика handles
├── BaseNodeEdges.js     # Логика рёбер (не рассмотрен)
└── index.js            # Экспорты
```