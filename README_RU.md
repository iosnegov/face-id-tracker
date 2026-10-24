# Face ID Tracker: Распознавание лиц в реальном времени с аппаратным ускорением CUDA

*Конвейер распознавания лиц в реальном времени, полностью настроенный в изолированном Conda-окружении для простой установки, воспроизводимости и переносимости.*

## Доступная документация / Available Documentation

- [English Documentation](README.md) (current document / текущий документ)
- [Документация на русском языке](README_RU.md)

## Структура проекта

```
face-id-tracker/
├── .env.example    # Шаблон конфигурации
├── SBOMs/          # Метаданные зависимостей
├── app/            # Исходный код приложения
└── photos/         # Фотографии для работы
```

## Инструкция по установке и запуску

### I. Предварительные требования

| Компонент | Требование |
| :--- | :--- |
| **Менеджер пакетов** | [`Micromamba`](https://github.com/mamba-org/mamba) |
| **Операционная система** | GNU/Linux-система |
| **Архитектура** | `x86_64` |
| **Аппаратное обеспечение** | Видеокарта NVIDIA с драйвером, поддерживающим CUDA >= 11.8 |
| **Инструменты разработки** *(Опционально)* | [`conda-lock`](https://github.com/conda/conda-lock) и [`pip-licenses`](https://github.com/raimon49/pip-licenses) |

> **Примечание:**  
> Это не строгие требования, а базовое окружение, в котором код гарантированно работает «из коробки». Возможны альтернативные настройки, но они могут потребовать ручной конфигурации.

### II. Клонирование репозитория

```bash
git clone https://github.com/snegoviol/face-id-tracker.git
cd face-id-tracker
```

### III. Создание и активация виртуальной среды

```bash
micromamba env create -p ./.venv -f SBOMs/conda-linux-64-lock.yml
micromamba activate ./.venv
```

### IV. Подготовка данных

В директорию `photos` вы можете добавить любые фотографии. Имя файла будет использоваться как имя человека при распознавании.  
В качестве демонстрации вы можете скачать фотографии с сайта [Pexels Free Stock Photos](https://www.pexels.com/).  
Например: [Man in brown polo shirt by Simon Robben from Pexels](https://www.pexels.com/photo/man-in-brown-polo-shirt-614810/).

### V. Настройка конфигурации через `.env`

1. Создайте файл `.env` из шаблона:

    ```bash
    cp .env.example .env
    ```

2. Отредактируйте `.env` в любом текстовом редакторе (например, `nano`, `VSCode`):

    ```bash
    nano .env
    ```

3. Настройте параметры: файл разделен на секции — измените значения в соответствии с вашими задачами. Например:

    ```bash
    # === MODEL CONFIGURATION ===
    FACE_RECOGNITION_MODEL=hog
    FACE_DISTANCE_THRESHOLD=0.6

    # === DISPLAY SETTINGS ===
    CAMERA_INDEX=0
    CAMERA_WIDTH=1280
    CAMERA_HEIGHT=720
    RESIZE_FACTOR=2

    FONT=FONT_HERSHEY_COMPLEX
    COLOR_KNOWN=0,255,0
    COLOR_UNKNOWN=0,0,255
    COLOR_INFO=255,0,0

    # === PATH CONFIGURATION ===
    PHOTOS_DIR=photos

    # === LOCALIZATION SETTINGS ===
    UNKNOWN_PERSON_LABEL=Unknown
    TIMEZONE_OFFSET=0
    TIMEZONE_LABEL=UTC
    ```

### VI. Запуск приложения

```bash
python -m app.main
```

## Лицензия

Каждый файл в этом репозитории распространяется под лицензией [MIT No Attribution License](LICENSE.txt).
