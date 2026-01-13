# useDataPersistence.js

## Обзор

Пользовательский React хук для автоматического сохранения и загрузки данных приложения. Обеспечивает синхронизацию состояния приложения с файловой системой через Electron API.

## Назначение

useDataPersistence отвечает за:
- Автоматическую загрузку данных при инициализации приложения
- Автоматическое сохранение данных при изменениях
- Синхронизацию данных между уровнями навигации
- Управление состоянием инициализации

## Зависимости

Хук использует следующие модули и хуки:
- `useEffect` из React - для управления побочными эффектами
- `useRef` из React - для хранения ссылок на состояние
- `useElectron` из `../../providers/ElectronProvider` - для доступа к Electron API

## Параметры

Хук принимает объект со следующими свойствами:
- `subLevels` - данные подуровней
- `navStack` - стек навигации
- `categoryTags` - теги категорий
- `setSubLevels` - функция установки данных подуровней
- `setNavStack` - функция установки стека навигации
- `setCategoryTags` - функция установки тегов категорий
- `setNodes` - функция установки узлов
- `setEdges` - функция установки связей

## Возвращаемое значение

Хук возвращает объект со следующими свойствами:

### Состояние инициализации
- `isInitialized` - булево значение, указывающее завершена ли инициализация

## Логика работы

### Загрузка данных
Хук загружает данные при первом запуске:
```javascript
useEffect(() => {
  if (!electronAPI?.readData || isInitialized.current) return;
  
  const loadData = async () => {
    try {
      // Инициализация данных
      if (electronAPI.initData) {
        await electronAPI.initData(null);
      }
      
      // Чтение данных
      const data = await electronAPI.readData();
      
      // Обновление состояния
      if (data && data.subLevels && Object.keys(data.subLevels).length > 0) {
        setSubLevels(data.subLevels);
        const rootLevel = data.subLevels['root_0'] || { nodes: [], edges: [] };
        setNodes(rootLevel.nodes || []);
        setEdges(rootLevel.edges || []);
      }
      
      // Загрузка тегов
      if (data?.categoryTags) {
        setCategoryTags(data.categoryTags);
      }
      
      // Загрузка стека навигации
      if (data?.navStack && setNavStack) {
        setNavStack(data.navStack);
      }
      
      isInitialized.current = true;
    } catch (error) {
      console.error('Error loading data:', error);
      isInitialized.current = true;
    }
  };
  
  loadData();
}, [electronAPI, setSubLevels, setNavStack, setCategoryTags, setNodes, setEdges]);
```

!> Жестко закодированное значение 'root_0' для корневого уровня
!> Отсутствует обработка ошибок при инициализации данных

### Автоматическое сохранение
Хук автоматически сохраняет данные при изменениях:
```javascript
useEffect(() => {
  if (!electronAPI?.writeData || !isInitialized.current) return;
  
  // Не сохранять если subLevels пустые
  if (!subLevels || Object.keys(subLevels).length === 0) return;
  
  // Очистить предыдущий таймаут
  if (saveTimeoutRef.current) {
    clearTimeout(saveTimeoutRef.current);
  }
  
  // Сохранить с задержкой (дебаунс 1 секунда)
  saveTimeoutRef.current = setTimeout(async () => {
    try {
      isSaving.current = true;
      
      await electronAPI.writeData({
        navStack: navStack || [],
        subLevels: subLevels,
        categoryTags: categoryTags,
      });
      
      isSaving.current = false;
    } catch (error) {
      console.error('Error saving data:', error);
      isSaving.current = false;
    }
  }, 1000);
  
  return () => {
    if (saveTimeoutRef.current) {
      clearTimeout(saveTimeoutRef.current);
    }
  };
}, [subLevels, navStack, categoryTags, electronAPI]);
```

!> Используется дебаунс для предотвращения частых сохранений
!> Жестко закодированная задержка 1000 мс
!> Отсутствует обработка ошибок при сохранении данных

### Сохранение перед закрытием
Хук сохраняет данные перед закрытием окна:
```javascript
useEffect(() => {
  if (!electronAPI?.writeData || !isInitialized.current) return;
  
  const handleBeforeUnload = async (e) => {
    e.preventDefault();
    try {
      // Не сохранять если subLevels пустые
      if (!subLevels || Object.keys(subLevels).length === 0) return;
      
      await electronAPI.writeData({
        navStack: navStack || [],
        subLevels: subLevels,
        categoryTags: categoryTags,
      });
    } catch (error) {
      console.error('Error saving data before exit:', error);
    }
  };
  
  window.addEventListener('beforeunload', handleBeforeUnload);
  
  return () => {
    window.removeEventListener('beforeunload', handleBeforeUnload);
  };
}, [subLevels, navStack, categoryTags, electronAPI]);
```

## Использование

Хук используется в основном компоненте App.js:
```javascript
const { isInitialized } = useDataPersistence({ 
  subLevels,
  navStack,
  categoryTags, 
  setSubLevels,
  setNavStack,
  setCategoryTags,
  setNodes,
  setEdges 
});
```

## Интеграция с другими компонентами

### useElectron
Используется для доступа к Electron API:
```javascript
import { useElectron } from '../../providers/ElectronProvider';
const electronAPI = useElectron();
```

## Принципы работы

1. **Автоматизация** - автоматическая загрузка и сохранение данных
2. **Оптимизация** - использование дебаунса для предотвращения частых сохранений
3. **Безопасность** - проверка инициализации перед выполнением операций
4. **Надежность** - обработка ошибок при загрузке и сохранении данных

## Особенности реализации

!> File watcher отключен - создает конфликты при одновременном редактировании
!> Жестко закодированное значение 'root_0' для корневого уровня
!> Используется дебаунс с фиксированной задержкой 1000 мс
!> Отсутствует прогрессивное сохранение (сохранение только измененных данных)
!> Не предусмотрена обработка конфликтов при одновременном редактировании
!> Отсутствует валидация сохраняемых данных