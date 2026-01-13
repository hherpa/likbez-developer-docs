# AppProvider.js

## Обзор

React Context провайдер для управления глобальным состоянием приложения, в частности тегами категорий. Оборачивает приложение в SettingsProvider для интеграции с настройками.

## Назначение

AppProvider отвечает за:
- Управление состоянием тегов категорий через хук `useApp`
- Предоставление контекста для доступа к тегам категорий в компонентах
- Интеграцию с SettingsProvider для централизованного управления настройками

## Контекст

### AppContext
React Context, который предоставляет доступ к значению хука `useApp`:
- `categoryTags` - объект с тегами категорий
- `setCategoryTags` - функция для установки тегов категорий
- `updateCategoryTag` - функция для обновления отдельного тега

### useAppContext()
Пользовательский хук для получения значения контекста:
```javascript
const { categoryTags, setCategoryTags, updateCategoryTag } = useAppContext();
```

!> При использовании хука вне провайдера будет выброшена ошибка "useAppContext must be used within AppProvider"

## Структура компонента

### AppProvider
Основной компонент-провайдер, который:
1. Использует хук `useApp` для получения состояния тегов
2. Оборачивает дочерние элементы в SettingsProvider
3. Предоставляет значение контекста через AppContext.Provider

## Хуки

### useApp
Хук, импортируемый из `../hooks/storage/useApp`, который предоставляет:
- `categoryTags` - состояние тегов категорий
- `setCategoryTags` - функция для установки тегов
- `updateCategoryTag` - функция для обновления отдельного тега

## Использование

Провайдер используется в основном компоненте App.js:
```jsx
<AppProvider>
  <FlowProvider>
    <NavigationProvider>
      <AppShell />
    </NavigationProvider>
  </FlowProvider>
</AppProvider>
```

Для доступа к контексту в компонентах:
```javascript
import { useAppContext } from '../providers/AppProvider';

const MyComponent = () => {
  const { categoryTags, updateCategoryTag } = useAppContext();
  // ... логика компонента
};
```

## Зависимости

- React (createContext, useContext)
- `useApp` хук из `../hooks/storage/useApp`
- `SettingsProvider` из `../../components/settings/SettingsProvider`

## Принципы работы

1. **Инкапсуляция состояния** - состояние тегов управляется через хук
2. **Контекстное предоставление** - значение доступно через React Context
3. **Интеграция с настройками** - использует SettingsProvider для централизованных настроек
4. **Типобезопасность** - проверка использования хука внутри провайдера