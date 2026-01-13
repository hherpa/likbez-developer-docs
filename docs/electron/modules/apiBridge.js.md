# modules/apiBridge.js

## Описание

Мост API для безопасного взаимодействия между main и renderer процессами Electron приложения Likbez. Предоставляет типизированный интерфейс для всех операций с данными, медиа и файловой системой.

## Основные функции

### setupAPI()

Настраивает API через Context Bridge, предоставляя renderer процессу безопасный доступ к функциям main процесса. Включает методы для:

- Основных операций с данными (initData, readData, writeData, getNodeDirectory)
- Управления тегами (readTags, writeTags)
- Медиа операций (openMedia, chooseAndImportMedia, importMediaToNode, resolveMediaPath, getMediaPreview, deleteMedia, listNodeMedia, listMediaFiles, getMediaInfo, getNodeMedia, cleanupUnusedMedia)
- File watcher (startWatcher, stopWatcher, onWatcherChange, removeWatcherListener)
- Утилит (validateDataStructure, validateFilePath, sanitizeDirName)

### invoke(channel, ...args)

Безопасный вызов IPC с обработкой ошибок. Обеспечивает надежное взаимодействие между процессами с логированием ошибок.

### validateDataStructure(data)

Валидация структуры данных для обеспечения целостности информации в приложении.

### validateFilePath(filePath)

Валидация пути к файлу для предотвращения path traversal атак.

### sanitizeDirName(name)

Санитизация имени директории для обеспечения совместимости с файловой системой.

### getAPIInfo()

Получение информации о доступных методах API, включая версию и список доступных методов.

## Безопасность

APIBridge обеспечивает безопасность приложения путем:

- Использования Context Bridge для изоляции контекстов
- Валидации всех входных данных
- Предотвращения path traversal атак
- Санитизации имен файлов и директорий

## Импорты

- electron: модули contextBridge и ipcRenderer для взаимодействия между процессами