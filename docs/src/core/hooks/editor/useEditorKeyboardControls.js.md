# useEditorKeyboardControls

Хук для управления горячими клавишами редактора.

## Описание

Отвечает только за обработку клавиатурных событий в редакторе. Соблюдает принцип Single Responsibility Principle (SRP).

## Параметры

- `isOpen` (boolean): Открыт ли редактор
- `onSave` (Function): Функция сохранения
- `onCancel` (Function): Функция отмены
- `showConfirmDialog` (boolean): Показан ли диалог подтверждения
- `onCancelClose` (Function): Функция отмены закрытия

## Возвращаемое значение

Объект с:
- `handleKeyDown`: Обработчик события keydown

## Особенности

- Обрабатывает Ctrl+S (Cmd+S) для сохранения
- Обрабатывает Escape для отмены/закрытия
- Автоматически добавляет/удаляет обработчик событий при открытии/закрытии редактора
- Поддерживает диалог подтверждения при закрытии с несохраненными изменениями

## Использование

```javascript
const { handleKeyDown } = useEditorKeyboardControls({
  isOpen: isEditorOpen,
  onSave: handleSave,
  onCancel: handleCancel,
  showConfirmDialog: showConfirmDialog,
  onCancelClose: handleCancelClose
});

// В компоненте:
useEffect(() => {
  if (isOpen) {
    document.addEventListener('keydown', handleKeyDown);
    return () => document.removeEventListener('keydown', handleKeyDown);
  }
}, [isOpen, handleKeyDown]);
```