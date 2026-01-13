# useDropdownManager

Управление состоянием dropdown.

## Описание

Отвечает ТОЛЬКО за управление состоянием всех dropdown в тулбаре.

## Параметры

- `isVisible` (boolean): Видимость тулбара
- `toolbarRef` (React.RefObject): ref тулбара

## Возвращаемое значение

Объект с:
- `showNotionDropdown`: Состояние dropdown Notion
- `setShowNotionDropdown`: Функция установки состояния dropdown Notion
- `showColorDropdown`: Состояние dropdown цвета
- `setShowColorDropdown`: Функция установки состояния dropdown цвета
- `showBgColorDropdown`: Состояние dropdown фона
- `setShowBgColorDropdown`: Функция установки состояния dropdown фона
- `closeAllDropdowns`: Функция закрытия всех dropdown

## Особенности

- Управляет состоянием всех dropdown в тулбаре
- Закрывает все dropdown при изменении видимости тулбара
- Обрабатывает клик вне dropdown для закрытия
- Предоставляет функцию закрытия всех dropdown

## Использование

```javascript
const {
  showNotionDropdown,
  setShowNotionDropdown,
  showColorDropdown,
  setShowColorDropdown,
  showBgColorDropdown,
  setShowBgColorDropdown,
  closeAllDropdowns
} = useDropdownManager(isVisible, toolbarRef);

// В JSX:
<NotionDropdown 
  show={showNotionDropdown} 
  onClose={() => setShowNotionDropdown(false)} 
/>
<ColorDropdown 
  show={showColorDropdown} 
  onClose={() => setShowColorDropdown(false)} 
/>
<BgColorDropdown 
  show={showBgColorDropdown} 
  onClose={() => setShowBgColorDropdown(false)} 
/>
```