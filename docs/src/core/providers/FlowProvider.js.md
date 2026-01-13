# FlowProvider.js

## Обзор

React Context провайдер для управления состоянием диаграммы узлов. Использует хук `useNodeEdges` из компонентов диаграммы для получения состояния узлов и связей.

## Назначение

FlowProvider отвечает за:
- Предоставление контекста состояния диаграммы (узлы и связи)
- Централизованное управление состоянием ReactFlow
- Обеспечение доступа к состоянию диаграммы в компонентах

## Контекст

### FlowContext
React Context, который предоставляет доступ к значению хука `useNodeEdges`:
- `nodes` - массив узлов диаграммы
- `setNodes` - функция для установки узлов
- `edges` - массив связей диаграммы
- `setEdges` - функция для установки связей
- `onNodesChange` - обработчик изменений узлов
- `onEdgesChange` - обработчик изменений связей
- `onConnect` - обработчик создания связей

### useFlowContext()
Пользовательский хук для получения значения контекста:
```javascript
const { nodes, setNodes, edges, setEdges } = useFlowContext();
```

!> При использовании хука вне провайдера будет выброшена ошибка "useFlowContext must be used within FlowProvider"

## Структура компонента

### FlowProvider
Основной компонент-провайдер, который:
1. Использует хук `useNodeEdges` для получения состояния диаграммы
2. Предоставляет значение контекста через FlowContext.Provider

## Хуки

### useNodeEdges
Хук, импортируемый из `../../components/diagram/node`, который предоставляет:
- Состояние узлов и функции для управления ими
- Состояние связей и функции для управления ими
- Обработчики событий ReactFlow (onNodesChange, onEdgesChange, onConnect)

## Использование

Провайдер используется в основном компоненте App.js:
```jsx
<ElectronProvider>
  <AppProvider>
    <FlowProvider>
      <NavigationProvider>
        <AppShell />
      </NavigationProvider>
    </FlowProvider>
  </AppProvider>
</ElectronProvider>
```

Для доступа к контексту в компонентах:
```javascript
import { useFlowContext } from '../providers/FlowProvider';

const MyComponent = () => {
  const { nodes, setNodes, edges, setEdges } = useFlowContext();
  // ... логика компонента
};
```

## Зависимости

- React (createContext, useContext)
- `useNodeEdges` хук из `../../components/diagram/node`

## Принципы работы

1. **Инкапсуляция состояния** - состояние диаграммы управляется через хук
2. **Контекстное предоставление** - значение доступно через React Context
3. **Типобезопасность** - проверка использования хука внутри провайдера
4. **Интеграция** - использует хуки из компонентов диаграммы

## Особенности реализации

!> Зависимость от `useNodeEdges` хука создает связь с компонентами диаграммы