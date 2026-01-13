# useNodeEditor

Хук для управления состоянием редактора узлов.

## Описание

Заменяет старую систему двойного клика и форм редактирования.

## Параметры

Нет параметров.

## Возвращаемое значение

Объект с:
- `isEditorOpen`: Состояние открытости редактора
- `editingNode`: Узел для редактирования
- `openEditor`: Функция открытия редактора
- `closeEditor`: Функция закрытия редактора
- `saveNode`: Функция сохранения узла
- `isNodeBeingEdited`: Функция проверки, редактируется ли конкретный узел

## Особенности

- Управляет состоянием модального окна редактора узлов
- Обрабатывает открытие/закрытие редактора
- Сохраняет изменения узла через переданный callback
- Проверяет, редактируется ли конкретный узел
- Интегрируется с системой управления узлами

## Использование

```javascript
const {
  isEditorOpen,
  editingNode,
  openEditor,
  closeEditor,
  saveNode,
  isNodeBeingEdited
} = useNodeEditor();

// Открытие редактора:
const handleNodeDoubleClick = (node) => {
  openEditor(node);
};

// Сохранение узла:
const handleSave = (nodeId, nodeData) => {
  saveNode(nodeId, nodeData, updateNodeCallback);
};

// Проверка, редактируется ли узел:
const isEditing = isNodeBeingEdited(nodeId);
```