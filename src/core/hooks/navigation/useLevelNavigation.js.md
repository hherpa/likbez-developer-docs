# useLevelNavigation.js

## Обзор

Пользовательский React хук для управления навигацией между уровнями настроек приложения. Интегрируется с настройками уровней и позволяет переходить между различными уровнями глубины узлов.

## Назначение

useLevelNavigation отвечает за:
- Определение текущего уровня настроек на основе навигации
- Проверку возможности перехода на следующий уровень
- Получение информации о следующем уровне
- Переход на следующий уровень с созданием или загрузкой данных

## Зависимости

Хук использует следующие модули и хуки:
- `useCallback` из React - для мемоизации функций
- `useSettings` из `../../../components/settings/SettingsProvider` - для получения настроек уровней
- Параметры контекста навигации:
  - `currentLevel` - текущий уровень навигации
  - `editingNode` - редактируемый узел
  - `subLevels` - данные подуровней
  - `setCurrentLevel` - функция установки текущего уровня
  - `setNavStack` - функция управления стеком навигации
  - `setSubLevels` - функция управления данными подуровней
  - `setNodes` - функция установки узлов
  - `setEdges` - функция установки связей

## Возвращаемое значение

Хук возвращает объект со следующими свойствами:

### getCurrentSettingsLevel
Функция для определения текущего уровня настроек:
```javascript
const getCurrentSettingsLevel = useCallback(() => {
  // ... логика определения уровня
}, [currentLevel, levels]);
```

!> Используется мемоизация для оптимизации производительности

### canNavigateToNext
Свойство, указывающее возможность перехода на следующий уровень:
```javascript
canNavigateToNext: canNavigateToNext()
```

!> Вычисляется сразу при вызове хука

### getNextLevel
Свойство, содержащее информацию о следующем уровне:
```javascript
getNextLevel: getNextLevel()
```

!> Вычисляется сразу при вызове хука

### navigateToNextLevel
Функция для перехода на следующий уровень:
```javascript
const navigateToNextLevel = useCallback((nextLevelId, currentNode = editingNode) => {
  // ... логика перехода
}, [editingNode, currentLevel, subLevels, setCurrentLevel, setNavStack, setSubLevels, setNodes, setEdges]);
```

## Логика работы

### Определение текущего уровня настроек
Функция анализирует текущий уровень навигации:
```javascript
if (currentLevel === 'root_0') {
  return levels[0]?.id || 'level1';
}

// Для уровней вида nodeId_depth определяем уровень по глубине
const match = currentLevel.match(/^.*_([0-9]+)$/);
if (match) {
  const depth = parseInt(match[1], 10);
  const levelIndex = Math.min(depth, levels.length - 1);
  return levels[levelIndex]?.id || 'level1';
}
```

!> Жестко закодированная логика определения уровней по глубине

### Проверка возможности перехода
Функция проверяет, можно ли перейти на следующий уровень:
```javascript
const canNavigateToNext = useCallback(() => {
  const currentSettingsLevelId = getCurrentSettingsLevel();
  const currentLevelIndex = levels.findIndex(level => level.id === currentSettingsLevelId);
  return currentLevelIndex >= 0 && currentLevelIndex < levels.length - 1;
}, [getCurrentSettingsLevel, levels]);
```

### Получение следующего уровня
Функция возвращает информацию о следующем уровне:
```javascript
const getNextLevel = useCallback(() => {
  const currentSettingsLevelId = getCurrentSettingsLevel();
  const currentLevelIndex = levels.findIndex(level => level.id === currentSettingsLevelId);
  if (currentLevelIndex >= 0 && currentLevelIndex < levels.length - 1) {
    return levels[currentLevelIndex + 1];
  }
  return null;
}, [getCurrentSettingsLevel, levels]);
```

### Переход на следующий уровень
Функция выполняет переход на указанный уровень:

1. **Определение уровня навигации**:
```javascript
if (nextLevelId === 'level1') {
  targetNavigationLevel = 'root_0';
} else {
  const depth = levelNumber - 1;
  targetNavigationLevel = `${currentNode.id}_${depth}`;
}
```

!> Жестко закодированное сопоставление уровней настроек и уровней навигации

2. **Обновление стека навигации**:
```javascript
setNavStack(prev => [...prev, currentLevel]);
```

3. **Переход на уровень**:
```javascript
setCurrentLevel(targetNavigationLevel);
```

4. **Создание или загрузка уровня**:
```javascript
if (!subLevels[targetNavigationLevel]) {
  // Создание нового уровня
  setSubLevels(prev => ({
    ...prev,
    [targetNavigationLevel]: { nodes: [], edges: [] }
  }));
  setNodes([]);
  setEdges([]);
} else {
  // Загрузка существующего уровня
  const levelData = subLevels[targetNavigationLevel];
  setNodes(levelData.nodes || []);
  setEdges(levelData.edges || []);
}
```

## Использование

Хук используется в основном компоненте App.js:
```javascript
const { 
  getCurrentSettingsLevel,
  canNavigateToNext,
  getNextLevel,
  navigateToNextLevel
} = useLevelNavigation({
  currentLevel,
  editingNode,
  subLevels,
  setCurrentLevel,
  setNavStack,
  setSubLevels,
  setNodes,
  setEdges
});
```

## Интеграция с другими модулями

### useSettings
Используется для получения настроек уровней:
```javascript
import { useSettings } from '../../../components/settings/SettingsProvider';
const { levels } = useSettings();
```

## Принципы работы

1. **Интеграция** - тесная интеграция с настройками уровней
2. **Оптимизация** - использование useCallback для предотвращения лишних созданий функций
3. **Гибкость** - поддержка различных сценариев перехода между уровнями
4. **Совместимость** - совместимость с существующей системой уровней

## Особенности реализации

!> Жестко закодированное сопоставление уровней настроек и уровней навигации может быть не гибким
!> Использование регулярных выражений для парсинга идентификаторов уровней может быть неэффективным
!> Отсутствует валидация идентификаторов уровней
!> Жестко закодированное значение 'level1' как fallback уровень
!> Отсутствует обработка ошибок при переходе между уровнями