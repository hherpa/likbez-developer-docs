# useFileExplorerNavigation.js

## Обзор

Пользовательский React хук для навигации к узлам из File Explorer. Централизует логику определения уровня и навигации к узлу, интегрируя различные контексты и хуки.

## Назначение

useFileExplorerNavigation отвечает за:
- Определение уровня, на котором находится узел
- Навигацию к узлу с переходом на нужный уровень при необходимости
- Анимацию перехода к узлу на диаграмме

## Зависимости

Хук использует следующие контексты и хуки:
- `useNavigationContext` из `../../providers` - для управления навигацией
- `useFlowContext` из `../../providers` - для управления узлами и связями
- `useUI` из `../navigation/useUI` - для получения инстанса ReactFlow
- `useNodeNavigation` из `../diagram/useNodeNavigation` - для анимации к узлу
- `useCallback` из React - для мемоизации функции навигации

## Возвращаемое значение

Хук возвращает объект с одним свойством:

### handleFileExplorerNavigate
Функция для навигации к узлу из File Explorer:
```javascript
const handleFileExplorerNavigate = useCallback((node) => {
  // ... логика навигации
}, [currentLevel, navigateToNode, setCurrentLevel, subLevels, setNodes, setEdges]);
```

Функция принимает:
- `node` - объект узла для навигации

!> Используется мемоизация для оптимизации производительности

## Логика работы

### Определение уровня
Функция определяет уровень, на котором находится узел:
```javascript
if (!node.parentId) {
  // Корневой узел - переходим на root_0
  targetLevel = 'root_0';
} else {
  // Дочерний узел - переходим на уровень родителя
  targetLevel = `${node.parentId}_${node.depth}`;
}
```

!> Жестко закодированная логика формирования идентификаторов уровней

### Навигация без смены уровня
Если уже на нужном уровне, просто анимирует к узлу:
```javascript
if (targetLevel === currentLevel) {
  setTimeout(() => navigateToNode(node), 100);
  return;
}
```

!> Используется setTimeout для задержки анимации

### Навигация со сменой уровня
Если нужно сменить уровень:
```javascript
setCurrentLevel(targetLevel);
const levelData = subLevels[targetLevel] || { nodes: [], edges: [] };
setNodes(levelData.nodes || []);
setEdges(levelData.edges || []);

// Анимация к узлу после смены уровня
setTimeout(() => navigateToNode(node), 300);
```

## Использование

Хук используется в основном компоненте App.js:
```javascript
const { handleFileExplorerNavigate } = useFileExplorerNavigation();
```

Функция передается в компонент боковой панели:
```jsx
<Sidebar 
  onNodeNavigate={handleFileExplorerNavigate}
  // ... другие props
/>
```

## Интеграция с другими хуками

### useNodeNavigation
Используется для анимации к узлу:
```javascript
const { navigateToNode } = useNodeNavigation(rfInstance);
```

### useNavigationContext
Используется для управления навигацией:
```javascript
const { currentLevel, setCurrentLevel, subLevels } = useNavigationContext();
```

### useFlowContext
Используется для управления узлами и связями:
```javascript
const { setNodes, setEdges } = useFlowContext();
```

### useUI
Используется для получения инстанса ReactFlow:
```javascript
const { rfInstance } = useUI();
```

## Принципы работы

1. **Централизация** - вся логика навигации из File Explorer в одном месте
2. **Интеграция** - использует существующие хуки для основной логики
3. **Оптимизация** - использование useCallback для предотвращения лишних созданий функций
4. **Плавность** - использование setTimeout для плавной анимации

## Особенности реализации

!> Жестко закодированная логика формирования идентификаторов уровней может потребовать изменения при изменении структуры данных
!> Использование setTimeout для задержек анимации может быть нестабильным
!> Отсутствует обработка ошибок при навигации