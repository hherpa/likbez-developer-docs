# TagManager.js

## Описание
TagManager - класс для управления тегами категорий. Отвечает за создание, переименование, получение и применение тегов к узлам. Обновлен для работы с markdown синтаксисом.

## Экспортируемые компоненты
- `TagManager` - основной класс управления тегами

## Структура
- `constructor(categoryTags, updateCategoryTag, setNodes, subLevels)` - инициализация менеджера тегов
- `updateLocalTags(newCategoryTags)` - обновление локальных тегов
- `updateSubLevels(newSubLevels)` - обновление подуровней
- `renameTag(tagId, newName)` - переименование тега
- `createTag(newTag, color, idOverride)` - создание нового тега
- `getExistingTags()` - получение существующих тегов
- `getLocalTags()` - получение локальных тегов
- `getTagByValue(tagValue)` - получение тега по значению
- `getColorForTag(tagValue)` - получение цвета тега
- `getCategoryTagForNode(nodeId)` - получение тега категории по id узла
- `applyTagToNode(nodeId, tagValue)` - применение тега к узлу
- `updateTagColor(tagId, color)` - обновление цвета тега
- `getTagCounts(node)` - подсчет тегов на следующем уровне категории
- `handleTagCreateAndApply(nodeId, newTag, getNodeFn, isCategoryNodeFn)` - создание и применение тега к узлу категории
- `validateAndSaveTag(values, currentNode, isCategoryNode, options)` - валидация тега и сохранение

## Взаимодействия
- Работает с локальным хранилищем тегов (`localTags`)
- Взаимодействует с функцией обновления тегов категории (`updateCategoryTag`)
- Обновляет узлы через `setNodes`
- Использует `subLevels` для подсчета тегов
- Использует вспомогательные функции из `TagCounts.js` и `TagApplier.js`

## Зависимости
- `./TagCounts.js` - для подсчета тегов
- `./TagApplier.js` - для применения тегов к узлам

## Архитектура
TagManager реализует паттерн управления состоянием тегов с возможностью:
1. Создания и переименования тегов
2. Применения тегов к узлам
3. Обновления цвета тегов
4. Подсчета количества тегов
5. Валидации тегов перед сохранением
6. Работы как с обычными узлами, так и с узлами категорий

Класс инкапсулирует всю логику работы с тегами, обеспечивая согласованность данных между различными частями приложения.