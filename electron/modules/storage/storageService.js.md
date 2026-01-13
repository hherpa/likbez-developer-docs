# modules/storage/storageService.js

## Описание

Сервис хранения данных Electron приложения Likbez. Предоставляет унифицированный интерфейс для работы с файловой системой и JSON данными.

## Основные функции

### constructor()

Инициализирует сервис хранения:

- Получает ссылки на модули fs, fsp, path
- Использует утилиты FileUtils и JsonUtils

### getDataRoot()

Получает путь к корневой директории данных:

- Делегирует вызов FileUtils.getDataRoot()

### ensureDir(dirPath)

Создает директорию рекурсивно:

- Делегирует вызов FileUtils.ensureDir()

### fileExists(filePath)

Проверяет существование файла:

- Делегирует вызов FileUtils.fileExists()

### writeJson(filePath, data)

Записывает данные в JSON файл:

- Делегирует вызов JsonUtils.writeJson()

### readJson(filePath, fallback)

Читает данные из JSON файла:

- Делегирует вызов JsonUtils.readJson()

### writeFile(filePath, content, encoding)

Записывает содержимое в файл:

- Создает директорию при необходимости
- Записывает содержимое в файл с указанной кодировкой

### readFile(filePath, encoding)

Читает содержимое файла:

- Читает файл с указанной кодировкой

### rename(oldPath, newPath)

Переименовывает файл или директорию:

- Вызывает fs.promises.rename

### readdir(dirPath, opts)

Сканирует содержимое директории:

- Вызывает fs.promises.readdir с опциями

### stat(filePath)

Получает статистику файла:

- Вызывает fs.promises.stat

### rm(dirPath, opts)

Удаляет файл или директорию:

- Вызывает fs.promises.rm с опциями

### copyFile(src, dst)

Копирует файл:

- Вызывает fs.promises.copyFile

### unlink(filePath)

Удаляет файл:

- Вызывает fs.promises.unlink

## Особенности реализации

### Синглтон
Сервис реализован как синглтон - экспортируется уже созданный экземпляр класса.

### Делегирование
Большинство операций делегируются утилитам FileUtils и JsonUtils для переиспользования кода.

## Импорты

- fs: модуль для работы с файловой системой
- fsp: промисы для работы с файловой системой
- path: модуль для работы с путями файловой системы
- FileUtils, JsonUtils из ../utils: утилиты для работы с файлами и JSON