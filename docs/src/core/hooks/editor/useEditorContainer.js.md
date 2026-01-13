# useEditorContainer

Хук для координации работы редактора узлов.

## Описание

Отвечает за управление состоянием, навигацией, модальными окнами и горячими клавишами редактора узлов.

## Параметры

- `isOpen` (boolean): Открыт ли редактор
- `node` (Object): Узел для редактирования
- `onClose` (Function): Функция закрытия редактора
- `onSave` (Function): Функция сохранения изменений
- `currentLevel` (string): Текущий уровень навигации

## Возвращаемое значение

Объект с:
- `editorData`: Состояние данных редактора
- `canNavigateToNext`: Возможность перехода на следующий уровень
- `nextLevel`: Следующий уровень навигации
- `handleSave`: Обработчик сохранения
- `showConfirmDialog`: Состояние диалога подтверждения
- `handleCancel`: Обработчик отмены
- `handleConfirmClose`: Обработчик подтверждения закрытия
- `handleCancelClose`: Обработчик отмены закрытия
- `handleContentManagerData`: Callback для получения данных
- `handleHasChangesChange`: Callback для обновления состояния изменений

## Особенности

- Интеграция с системой навигации по уровням
- Управление состоянием модального окна редактора
- Обработка горячих клавиш (Ctrl+S для сохранения, Escape для отмены)
- Координация с EditorContentManager для получения данных
- Извлечение заголовка из контента при сохранении
- Поддержка диалога подтверждения при наличии несохраненных изменений

## Использование

```javascript
const {
  editorData,
  canNavigateToNext,
  nextLevel,
  handleSave,
  showConfirmDialog,
  handleCancel,
  handleConfirmClose,
  handleCancelClose,
  handleContentManagerData,
  handleHasChangesChange
} = useEditorContainer({
  isOpen: isEditorOpen,
  node: editingNode,
  onClose: handleClose,
  onSave: handleSave,
  currentLevel: currentLevel
});
```