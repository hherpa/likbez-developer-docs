# useNavigation.js

## Обзор

Пользовательский React хук для управления навигацией между уровнями приложения. Обеспечивает управление стеком навигации, подуровнями и текущим уровнем.

## Назначение

useNavigation отвечает за:
- Управление стеком навигации (историей переходов)
- Управление данными подуровней (узлы и связи)
- Управление текущим уровнем навигации
- Обработку навигации между уровнями
- Интеграцию с редактором узлов

## Зависимости

Хук использует следующие модули и хуки:
- `useState` из React - для управления состоянием
- `useNodeEditor` из `../editor/useNodeEditor` - для интеграции с редактором

## Возвращаемое значение

Хук возвращает объект со следующими свойствами:

### Состояние навигации
- `navStack` - массив идентификаторов уровней в стеке навигации
- `setNavStack` - функция для установки стека навигации
- `subLevels` - объект с данными подуровней (узлы и связи)
- `setSubLevels` - функция для установки данных подуровней
- `currentLevel` - идентификатор текущего уровня
- `setCurrentLevel` - функция для установки текущего уровня

### Функции управления
- `getCurrentKey` - функция для получения ключа текущего уровня
- `onNodeDoubleClick` - обработчик двойного клика по узлу для навигации
- `onNodeEdit` - обработчик редактирования узла
- `onBack` - обработчик возврата назад
- `canNavigate` - функция проверки возможности навигации

## Логика работы

### Инициализация состояния
Хук инициализирует начальное состояние:
```javascript
const [navStack, setNavStack] = useState([]);
const [subLevels, setSubLevels] = useState({});
const [currentLevel, setCurrentLevel] = useState('root_0');
```

!> Жестко закодированное значение 'root_0' для начального уровня

### onNodeEdit
Функция для открытия редактора узла:
```javascript
const onNodeEdit = (node, openEditorCallback) => {
  if (!node?.id || !openEditorCallback) return;
  openEditorCallback(node);
};
```

### onNodeDoubleClick
Функция для навигации к подуровню узла:
```javascript
const onNodeDoubleClick = (_evt, node, setNodes, setEdges, currentLevelOpt) => {
  // ... логика навигации
};
```

#### Определение следующего уровня
Для корневого уровня:
```javascript
if (levelNow === 'root_0') {
  nextLevel = `${node.id}_1`;
}
```

Для подуровней:
```javascript
const match = levelNow.match(/^(.*)_([0-9]+)$/);
if (match) {
  const currentDepth = parseInt(match[2], 10);
  const nextDepth = isNaN(currentDepth) ? 1 : currentDepth + 1;
  nextLevel = `${node.id}_${nextDepth}`;
}
```

!> Жестко закодированная логика формирования идентификаторов уровней

#### Обновление состояния
Функция обновляет стек навигации и текущий уровень:
```javascript
setNavStack((st) => [...st, levelNow]);
setCurrentLevel(nextLevel);
```

#### Создание нового уровня
Если уровень не существует:
```javascript
setSubLevels((prev) => prev[nextLevel] ? prev : { ...prev, [nextLevel]: { nodes: [], edges: [] } });
```

### onBack
Функция для возврата к предыдущему уровню:
```javascript
const onBack = (setNodes, setEdges) => {
  // ... логика возврата
};
```

#### Обновление состояния
Функция возвращает последний уровень из стека:
```javascript
setNavStack((st) => {
  if (!st.length) return st;
  const last = st[st.length - 1];
  setCurrentLevel(last);
  // ... загрузка данных уровня
  return st.slice(0, -1);
});
```

## Использование

Хук используется в NavigationProvider:
```javascript
const value = useNavigation();
```

Также используется напрямую в компонентах для управления навигацией:
```javascript
const { 
  navStack, setNavStack,
  subLevels, setSubLevels,
  currentLevel, setCurrentLevel,
  onNodeDoubleClick,
  onBack
} = useNavigation();
```

## Интеграция с другими хуками

### useNodeEditor
Используется для интеграции с редактором узлов:
```javascript
import { useNodeEditor } from '../editor/useNodeEditor';
```

## Принципы работы

1. **Централизация** - вся логика навигации в одном хуке
2. **Состояние** - управление всеми аспектами навигации через состояние
3. **Интеграция** - интеграция с редактором узлов
4. **Гибкость** - поддержка различных сценариев навигации

## Особенности реализации

!> Жестко закодированное значение 'root_0' для начального уровня может потребовать изменения
!> Жестко закодированная логика формирования идентификаторов уровней может быть не гибкой
!> Отсутствует валидация идентификаторов уровней
!> Использование регулярных выражений для парсинга идентификаторов может быть неэффективным
!> Отсутствует обработка ошибок при навигации