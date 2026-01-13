# ElectronProvider.js

## Обзор

React Context провайдер для интеграции с Electron API. Предоставляет доступ к Electron API в компонентах приложения через React Context.

## Назначение

ElectronProvider отвечает за:
- Предоставление доступа к Electron API через React Context
- Обработку случаев, когда приложение работает вне Electron окружения
- Централизованное управление доступом к Electron функциям

## Контекст

### ElectronContext
React Context, который предоставляет доступ к Electron API:
- В браузерной среде: пустой объект `{}`
- В Electron среде: `window.electronAPI` или пустой объект если API недоступен

### useElectron()
Пользовательский хук для получения Electron API:
```javascript
const electronAPI = useElectron();
```

!> При использовании в браузерной среде будет возвращен пустой объект

## Структура компонента

### ElectronProvider
Основной компонент-провайдер, который:
1. Использует `useMemo` для мемоизации значения API
2. Проверяет доступность `window.electronAPI`
3. Предоставляет значение контекста через ElectronContext.Provider

## Мемоизация

Используется `useMemo` для оптимизации производительности:
```javascript
const api = useMemo(() => (typeof window !== 'undefined' ? window.electronAPI || {} : {}), []);
```

!> Значение мемоизируется и не будет пересоздаваться при каждом рендере

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

Для доступа к Electron API в компонентах:
```javascript
import { useElectron } from '../providers/ElectronProvider';

const MyComponent = () => {
  const electronAPI = useElectron();
  
  const handleSave = async () => {
    if (electronAPI.saveData) {
      await electronAPI.saveData(data);
    }
  };
};
```

## Зависимости

- React (createContext, useContext, useMemo)
- `window.electronAPI` - глобальный объект Electron API

## Принципы работы

1. **Безопасность окружения** - проверка наличия window перед доступом к electronAPI
2. **Гибкость** - работает как в Electron, так и в браузерной среде
3. **Производительность** - мемоизация значения API
4. **Простота** - минимальная логика, только предоставление API

## Особенности реализации

!> Жестко закодированная проверка `typeof window !== 'undefined'` может потребовать изменения при использовании SSR

!> Возврат пустого объекта в случае отсутствия electronAPI может скрыть ошибки интеграции