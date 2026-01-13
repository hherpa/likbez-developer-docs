# modules/ipc/ipcHandlers.js

## Описание

Центральный обработчик IPC сообщений Electron приложения Likbez. Координирует регистрацию обработчиков для различных типов сообщений между main и renderer процессами.

## Основные функции

### constructor()

Инициализирует обработчики IPC:

- Создает экземпляры DataManager и MediaManager
- Регистрирует обработчики данных, медиа, тегов и watcher'а

### setupHandlers()

Регистрирует обработчики для различных типов сообщений:

- registerDataHandlers: обработчики данных
- registerMediaHandlers: обработчики медиа
- registerTagHandlers: обработчики тегов
- registerWatcherHandlers: обработчики watcher'а

### getDataManager()

Возвращает экземпляр DataManager для использования другими модулями.

### getMediaManager()

Возвращает экземпляр MediaManager для использования другими модулями.

### cleanup()

Очищает ресурсы при завершении работы:

- Останавливает отслеживание изменений
- Удаляет все зарегистрированные обработчики IPC

## Обработчики сообщений

### Обработчики данных
- data:init - инициализация структуры данных
- data:read - чтение данных
- data:write - запись данных
- data:getNodeDirectory - получение пути к папке узла

### Обработчики медиа
- media:open - открытие медиафайла
- media:chooseAndImport - выбор и импорт медиафайла
- media:importToNode - импорт медиафайла в узел
- media:resolvePath - разрешение пути к медиафайлу
- media:getPreview - получение превью медиафайла
- media:delete - удаление медиафайла
- media:listNodeMedia - список медиафайлов узла
- media:list - список всех медиафайлов
- media:getInfo - получение информации о медиафайле
- media:getNodeMedia - получение медиафайлов узла
- media:cleanup - очистка неиспользуемых медиафайлов

### Обработчики тегов
- tags:read - чтение тегов
- tags:write - запись тегов

### Обработчики watcher'а
- watcher:start - запуск отслеживания изменений
- watcher:stop - остановка отслеживания изменений

## Импорты

- electron: модуль ipcMain для обработки IPC сообщений
- DataManager из ../dataManager: менеджер данных
- MediaManager из ../media/mediaManager: менеджер медиа
- registerDataHandlers из ./ipcDataHandlers: обработчики данных
- registerMediaHandlers из ./ipcMediaHandlers: обработчики медиа
- registerTagHandlers из ./ipcTagHandlers: обработчики тегов
- registerWatcherHandlers из ./ipcWatcherHandlers: обработчики watcher'а