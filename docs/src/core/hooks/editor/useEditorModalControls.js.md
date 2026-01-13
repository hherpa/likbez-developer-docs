# useEditorModalControls

Хук для управления состоянием модального окна редактора.

## Описание

Отвечает только за управление состоянием модального окна и диалогов подтверждения. Соблюдает принцип Single Responsibility Principle (SRP).

## Параметры

Нет параметров.

## Возвращаемое значение

Объект с:
- `showConfirmDialog`: Состояние диалога подтверждения
- `handleCancel`: Обработчик отмены
- `handleConfirmClose`: Обработчик подтверждения закрытия
- `handleCancelClose`: Обработчик отмены закрытия

## Особенности

- Управляет состоянием диалога подтверждения при закрытии с несохраненными изменениями
- Предоставляет обработчики для различных сценариев закрытия модального окна
- Интегрируется с системой управления редактором

## Использование

```javascript
const {
  showConfirmDialog,
  handleCancel,
  handleConfirmClose,
  handleCancelClose
} = useEditorModalControls();

// Пример использования в обработчике отмены:
const handleCancelClick = () => {
  handleCancel(hasUnsavedChanges, onClose);
};

// Пример использования в диалоге подтверждения:
const handleConfirm = () => {
  handleConfirmClose(onClose);
};

const handleCancelDialog = () => {
  handleCancelClose();
};
```