# useEditorTabs

Хук для управления состоянием вкладок редактора.

## Описание

Отвечает только за управление активной вкладкой. Соблюдает принцип Single Responsibility Principle (SRP).

## Параметры

- `defaultTab` (string): Идентификатор вкладки по умолчанию (по умолчанию 'edit')

## Возвращаемое значение

Объект с:
- `activeTab`: Идентификатор активной вкладки
- `setActiveTab`: Функция установки активной вкладки
- `handleTabChange`: Функция изменения активной вкладки

## Особенности

- Управляет состоянием активной вкладки редактора
- Предоставляет удобные методы для переключения между вкладками
- Поддерживает начальное состояние

## Использование

```javascript
const { activeTab, setActiveTab, handleTabChange } = useEditorTabs('edit');

// В JSX:
<TabButton 
  active={activeTab === 'edit'} 
  onClick={() => handleTabChange('edit')}
>
  Редактирование
</TabButton>
<TabButton 
  active={activeTab === 'settings'} 
  onClick={() => handleTabChange('settings')}
>
  Настройки
</TabButton>
```