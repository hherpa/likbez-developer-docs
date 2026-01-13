# useImageUpload

Хук для обработки drag&drop изображений в редактор.

## Описание

Сохраняет изображения в папку data/ и возвращает относительные пути.

## Параметры

Нет параметров.

## Возвращаемое значение

Объект с:
- `isUploading`: Состояние загрузки
- `uploadProgress`: Прогресс загрузки (0-100)
- `uploadImage`: Функция загрузки одного изображения
- `uploadMultipleImages`: Функция загрузки нескольких изображений
- `handleDrop`: Обработчик события drop
- `handleFileSelect`: Обработчик выбора файла
- `isImageFile`: Проверка, является ли файл изображением
- `getImageDimensions`: Получение размеров изображения
- `createImagePreview`: Создание превью изображения

## Особенности

- Загружает изображения в папку data/ через Electron API
- Поддерживает fallback для веб-версии (blob URL)
- Обрабатывает drag&drop и выбор файлов через input
- Проверяет, что файлы являются изображениями
- Получает размеры изображений
- Создает превью изображений
- Отслеживает состояние загрузки и прогресс

## Использование

```javascript
const {
  isUploading,
  uploadProgress,
  uploadImage,
  handleDrop,
  handleFileSelect
} = useImageUpload();

// В JSX:
<div 
  onDrop={handleDrop}
  onDragOver={(e) => e.preventDefault()}
>
  <input 
    type="file" 
    accept="image/*" 
    onChange={handleFileSelect} 
    multiple 
  />
  {isUploading && (
    <div>Загрузка... {uploadProgress}%</div>
  )}
</div>
```