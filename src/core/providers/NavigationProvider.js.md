# NavigationProvider.js

## Обзор

React Context провайдер для управления состоянием навигации между уровнями приложения. Использует хук `useNavigation` для получения состояния навигации.

## Назначение

NavigationProvider отвечает за:
- Предоставление контекста состояния навигации
- Централизованное управление стеком навигации и уровнями
- Обеспечение доступа к состоянию навигации в компонентах

## Контекст

### NavigationContext
React Context, который предоставляет доступ к значению хука `useNavigation`:
- `navStack` - стек навигации (массив идентификаторов уровней)
- `setNavStack` - функция для установки стека навигации
- `subLevels` - данные подуровней (объект с узлами и связями для каждого уровня)
- `setSubLevels` - функция для установки данных подуровней
- `currentLevel` - идентификатор текущего уровня
- `setCurrentLevel` - функция для установки текущего уровня
- `getCurrentKey` - функция для получения ключа текущего уровня
- `onNodeDoubleClick` - обработчик двойного клика по узлу
- `onNodeEdit` - обработчик редактирования узла
- `onBack` - обработчик возврата назад
- `canNavigate` - функция проверки возможности навигации

### useNavigationContext()
Пользовательский хук для получения значения контекста:
```javascript
const { 
  navStack, setNavStack, 
  subLevels, setSubLevels, 
  currentLevel, setCurrentLevel 
} = useNavigationContext();
```

!> При использовании хука вне провайдера будет выброшена ошибка "useNavigationContext must be used within NavigationProvider"

## Структура компонента

### NavigationProvider
Основной компонент-провайдер, который:
1. Использует хук `useNavigation` для получения состояния навигации
2. Предоставляет значение контекста через NavigationContext.Provider

## Хуки

### useNavigation
Хук, импортируемый из `../hooks/navigation/useNavigation`, который предоставляет:
- Состояние стека навигации и функции для управления им
- Состояние подуровней и функции для управления ими
- Состояние текущего уровня и функции для управления им
- Обработчики событий навигации (onNodeDoubleClick, onBack, onNodeEdit)

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
import { useNavigationContext } from '../providers/NavigationProvider';

const MyComponent = () => {
  const { currentLevel, setCurrentLevel, onBack } = useNavigationContext();
  // ... логика компонента
};
```

## Зависимости

- React (createContext, useContext)
- `useNavigation` хук из `../hooks/navigation/useNavigation`

## Принципы работы

1. **Инкапсуляция состояния** - состояние навигации управляется через хук
2. **Контекстное предоставление** - значение доступно через React Context
3. **Типобезопасность** - проверка использования хука внутри провайдера
4. **Интеграция** - использует хуки из навигационных хуков

## Особенности реализации

!> Зависимость от `useNavigation` хука создает связь с навигационными хуками
!> Состояние `subLevels` хранит данные всех уровней, что может повлиять на производительность при большом количестве данных