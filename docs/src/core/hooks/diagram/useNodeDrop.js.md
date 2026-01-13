# useNodeDrop.js

## Обзор

Пользовательский React хук для обработки drag & drop узлов на холст ReactFlow. Обрабатывает события перетаскивания и создает новые узлы с соответствующими данными.

## Назначение

useNodeDrop отвечает за:
- Обработку событий drag over на холсте ReactFlow
- Обработку событий drop для создания новых узлов
- Создание контента узлов в markdown формате
- Позиционирование узлов на холсте

## Зависимости

Хук использует следующие модули и хуки:
- `useCallback` из React - для мемоизации обработчиков событий
- `createTemplate` из `../../../components/editor/system/parser/core/NodeFactory` - для создания шаблонов контента
- `rfInstance` - инстанс ReactFlow для проецирования координат
- `setNodes` - функция для добавления узлов

## Возвращаемое значение

Хук возвращает объект с двумя свойствами:

### onDragOver
Функция-обработчик события drag over:
```javascript
const onDragOver = useCallback((event) => {
  event.preventDefault();
  if (event.dataTransfer) {
    event.dataTransfer.dropEffect = 'move';
  }
}, []);
```

!> Используется мемоизация для оптимизации производительности

### onDrop
Функция-обработчик события drop:
```javascript
const onDrop = useCallback((event) => {
  // ... логика создания узла
}, [rfInstance, setNodes]);
```

!> Используется мемоизация с зависимостями от rfInstance и setNodes

## Логика работы

### Обработка drag over
Функция предотвращает поведение по умолчанию и устанавливает эффект перетаскивания:
```javascript
event.preventDefault();
event.dataTransfer.dropEffect = 'move';
```

### Обработка drop
Функция выполняет следующие шаги:

1. **Получение данных** из dataTransfer:
```javascript
const raw = event.dataTransfer.getData('application/reactflow');
const payload = JSON.parse(raw || '{}');
```

2. **Определение типа узла** (всегда 'base'):
```javascript
const type = 'base';
```

3. **Извлечение дополнительных данных**:
```javascript
const extra = payload.payload || {};
```

4. **Проекция координат** на холст ReactFlow:
```javascript
const position = rfInstance && rfInstance.project
  ? rfInstance.project({ 
      x: event.clientX - bounds.left, 
      y: event.clientY - bounds.top 
    })
  : { 
      x: event.clientX - bounds.left, 
      y: event.clientY - bounds.top 
    };
```

!> Жестко закодированная проекция координат может потребовать изменения при изменении структуры данных

5. **Создание идентификатора** узла:
```javascript
const id = `n-${Date.now()}`;
```

!> Использование Date.now() может привести к коллизиям при быстром создании узлов

6. **Создание контента** в markdown формате:
```javascript
const content = createTemplate({
  title: extra.title || 'Новый узел',
  text: extra.text || 'Описание узла...',
  tag: extra.tag || '',
  symbols: extra.symbol || '',
  latex: extra.latex || '',
  images: extra.image ? [extra.image] : []
});
```

7. **Создание данных узла**:
```javascript
const data = { 
  content,
  title: extra.title || 'Новый узел',
  ...extra 
};
```

8. **Добавление узла** в состояние:
```javascript
setNodes((nds) => nds.concat({ id, type, position, data }));
```

## Использование

Хук используется в основном компоненте App.js:
```javascript
const { onDragOver, onDrop } = useNodeDrop(rfInstance, currentLevel, setNodes);
```

Обработчики передаются в компонент ReactFlow:
```jsx
<ReactFlow
  onDragOver={onDragOver}
  onDrop={onDrop}
  // ... другие props
/>
```

## Интеграция с другими модулями

### createTemplate
Используется для создания шаблонов контента:
```javascript
import { createTemplate } from '../../../components/editor/system/parser/core/NodeFactory';
```

### NodeFactory
Используется для создания структурированного контента узлов в markdown формате.

## Принципы работы

1. **Интеграция** - использует существующие модули для создания контента
2. **Оптимизация** - использование useCallback для предотвращения лишних созданий функций
3. **Гибкость** - поддержка различных типов данных при перетаскивании
4. **Совместимость** - работает с различными версиями ReactFlow

## Особенности реализации

!> Жестко закодированное значение `type = 'base'` может ограничивать гибкость создания узлов
!> Использование `Date.now()` для генерации идентификаторов может привести к коллизиям
!> Отсутствует обработка ошибок при парсинге данных перетаскивания
!> Жестко закодированная структура контента узла может потребовать изменения при изменении формата данных