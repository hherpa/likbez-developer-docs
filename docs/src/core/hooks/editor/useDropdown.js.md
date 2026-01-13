# useDropdown

Хук для общей логики работы dropdown компонентов.

## Описание

Инкапсулирует общее поведение dropdown компонентов: клик вне, клавиатура, получение выделенного текста.

## Параметры

- `options` (Object): Опции хука
  - `isOpen` (boolean): Открыт ли dropdown
  - `onClose` (Function): Функция закрытия dropdown
  - `getSelectedText` (Function, опционально): Функция получения выделенного текста
  - `onEnter` (Function, опционально): Функция для обработки Enter

## Возвращаемое значение

Объект с:
- `dropdownRef`: ref для dropdown элемента
- `hoveredItem`: состояние hover
- `setHoveredItem`: функция установки hover
- `getSelectedText`: функция получения выделенного текста

## Особенности

- Обрабатывает клик вне dropdown для закрытия
- Обрабатывает клавиши Escape и Enter
- Предоставляет утилиту для получения выделенного текста
- Поддерживает hover состояние для элементов списка

## Использование

```javascript
const { dropdownRef, hoveredItem, setHoveredItem, getSelectedText } = useDropdown({
  isOpen: isDropdownOpen,
  onClose: handleClose,
  getSelectedText: getSelectedText,
  onEnter: handleEnter
});
```