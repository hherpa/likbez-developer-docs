# Editor Hooks

Коллекция React хуков для управления редактором узлов в приложении Likbez.

## Основные хуки

- [useDropdown](../src/core/hooks/editor/useDropdown.js.md) - общий хук для работы с dropdown компонентами
- [useEditorContainer](../src/core/hooks/editor/useEditorContainer.js.md) - координация работы редактора узлов
- [useEditorKeyboardControls](../src/core/hooks/editor/useEditorKeyboardControls.js.md) - управление горячими клавишами редактора
- [useEditorModalControls](../src/core/hooks/editor/useEditorModalControls.js.md) - управление состоянием модального окна редактора
- [useEditorNodeWidth](../src/core/hooks/editor/useEditorNodeWidth.js.md) - управление шириной узла редактора
- [useEditorPreview](../src/core/hooks/editor/useEditorPreview.js.md) - управление состоянием предпросмотра редактора
- [useEditorTabs](../src/core/hooks/editor/useEditorTabs.js.md) - управление состоянием вкладок редактора
- [useFloatingToolbar](../src/core/hooks/editor/useFloatingToolbar.js.md) - координация между textarea и FloatingToolbar
- [useImageUpload](../src/core/hooks/editor/useImageUpload.js.md) - обработка drag&drop изображений в редактор
- [useNodeEditor](../src/core/hooks/editor/useNodeEditor.js.md) - управление состоянием редактора узлов
- [usePreviewMode](../src/core/hooks/editor/usePreviewMode.js.md) - управление режимом превью редактора
- [useSyntaxHighlight](../src/core/hooks/editor/useSyntaxHighlight.js.md) - управление подсветкой синтаксиса
- [useTextarea](../src/core/hooks/editor/useTextarea.js.md) - управление textarea элементом
- [useTextareaView](../src/core/hooks/editor/useTextareaView.js.md) - управление видимостью textarea

## Поддиректории

### Preview

Хуки для управления редактированием элементов в режиме предпросмотра:

- [useBackspaceKeyHandler](../src/core/hooks/editor/preview/useBackspaceKeyHandler.js.md) - обработка нажатия клавиши Backspace
- [useEditableElement](../src/core/hooks/editor/preview/useEditableElement.js.md) - главный хук для редактируемого элемента
- [useEditingFocus](../src/core/hooks/editor/preview/useEditingFocus.js.md) - управление фокусом при редактировании
- [useEditValue](../src/core/hooks/editor/preview/useEditValue.js.md) - управление значением редактирования
- [useEnterKeyHandler](../src/core/hooks/editor/preview/useEnterKeyHandler.js.md) - обработка нажатия клавиши Enter
- [useTextExtraction](../src/core/hooks/editor/preview/useTextExtraction.js.md) - извлечение текста из contentEditable
- [useToolbarSelection](../src/core/hooks/editor/preview/useToolbarSelection.js.md) - управление видимостью тулбара при выделении

### Toolbar

Хуки для управления плавающим тулбаром:

- [useDropdownManager](../src/core/hooks/editor/toolbar/useDropdownManager.js.md) - управление состоянием dropdown
- [useToolbarAnimation](../src/core/hooks/editor/toolbar/useToolbarAnimation.js.md) - управление анимацией тулбара
- [useToolbarPosition](../src/core/hooks/editor/toolbar/useToolbarPosition.js.md) - управление позиционированием тулбара