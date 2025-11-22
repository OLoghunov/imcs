# IMCS - Image/data Compression using Compressed Sensing

Дипломная работа: Инженерная реализация формата сжатия данных `.imcs` на основе алгоритма compressed sensing.

## Описание проекта

IMCS (Image/data Compression using Compressed Sensing) - это формат сжатия данных, основанный на теории сжатого восприятия (compressed sensing). Проект включает в себя реализацию кодера и декодера для сжатия и восстановления данных.

### Основные компоненты

- **Encoder (Кодер)**: Сжимает данные используя алгоритмы compressed sensing
- **Decoder (Декодер)**: Восстанавливает данные из сжатого формата
- **Utils**: Вспомогательные функции для работы с измерительными матрицами и метриками

## Установка

### 1. Создание виртуального окружения

```bash
python3 -m venv venv
```

### 2. Активация виртуального окружения

На macOS/Linux:
```bash
source venv/bin/activate
```

На Windows:
```bash
venv\Scripts\activate
```

### 3. Установка зависимостей

```bash
pip install -r requirements.txt
pip install -e .
```

Или используя Makefile:
```bash
make install
```

## Структура проекта

```
imcs/
├── imcs/                  # Основной пакет
│   ├── __init__.py       # Инициализация пакета
│   ├── encoder.py        # Реализация кодера
│   ├── decoder.py        # Реализация декодера
│   └── utils.py          # Вспомогательные функции
├── test_imcs/             # Тесты
│   ├── conftest.py       # Fixtures
│   ├── test_encoder.py   # Тесты encoder
│   ├── test_decoder.py   # Тесты decoder
│   └── test_utils.py     # Тесты utils
├── venv/                  # Виртуальное окружение
├── main.py               # Точка входа в приложение
├── requirements.txt      # Зависимости проекта
├── setup.py              # Конфигурация пакета
├── pytest.ini            # Конфигурация pytest
├── Makefile              # Команды для разработки
└── README.md             # Этот файл
```

## Использование

### Запуск основного приложения

```bash
python main.py
```

### Пример использования кодера

```python
from imcs import IMCSEncoder
import numpy as np

# Создание кодера
encoder = IMCSEncoder(compression_ratio=0.5, sparsity_basis='dct')

# Сжатие данных
data = np.random.rand(100)
compressed = encoder.encode(data)
```

### Пример использования декодера

```python
from imcs import IMCSDecoder

# Создание декодера
decoder = IMCSDecoder(reconstruction_algorithm='omp')

# Восстановление данных
reconstructed = decoder.decode(compressed)
```

## Тестирование

Проект использует pytest для тестирования. Все тесты находятся в директории `test_imcs/`.

### Запуск всех тестов

```bash
pytest
```

Или:
```bash
make test
```

### Запуск тестов с фильтрацией по названию/модулю

Используя pytest напрямую:
```bash
# Запуск тестов, содержащих "encoder" в названии
pytest -k encoder

# Запуск тестов из конкретного модуля
pytest test_imcs/test_encoder.py             # Все тесты encoder
pytest test_imcs/test_decoder.py             # Все тесты decoder
pytest test_imcs/test_utils.py               # Все тесты utils

# Запуск конкретного теста
pytest test_imcs/test_encoder.py::test_encoder_initialization

# Запуск конкретного параметризованного теста
pytest test_imcs/test_encoder.py::test_encoder_initialization[0.5-dct]
```

Используя Makefile:
```bash
# Запуск тестов с фильтром
make test-filter FILTER=encoder

# Запуск тестов декодера
make test-filter FILTER=decoder

# Запуск тестов утилит
make test-filter FILTER=utils

# Запуск тестов по части названия
make test-filter FILTER=initialization
```

## Разработка

### Форматирование кода

```bash
# Форматирование с помощью black
make format

# Или напрямую
black imcs test_imcs
```

### Проверка кода (linting)

```bash
# Запуск flake8
make lint

# Или напрямую
flake8 imcs test_imcs
```

### Деактивация виртуального окружения

```bash
deactivate
```

## Зависимости

### Основные
- `numpy` - работа с массивами и математические операции
- `scipy` - научные вычисления и оптимизация

### Тестирование
- `pytest` - фреймворк для тестирования
- `pytest-cov` - покрытие кода тестами

### Разработка
- `black` - форматирование кода
- `flake8` - проверка стиля кода
- `mypy` - статическая проверка типов

## Roadmap

- [ ] Реализация базового кодера
- [ ] Реализация базового декодера
- [ ] Реализация генерации измерительных матриц
- [ ] Реализация алгоритмов восстановления
- [ ] Определение формата файла .imcs
- [ ] Реализация работы с файлами
- [ ] Добавление метрик качества сжатия
- [ ] Оптимизация производительности
- [ ] Документация API
- [ ] Примеры использования

## Автор

Oleg Y. Logunov

## Лицензия

MIT License
