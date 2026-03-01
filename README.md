# Hadoop MapReduce Streaming Demo (HDFS + Python mappers/reducers)

Учебный проект/ноутбук демонстрирует полный цикл batch-обработки данных в Hadoop:
загрузка датасетов в HDFS → выполнение MapReduce задач через Hadoop Streaming (Python) → чтение результатов из HDFS.

## Что реализовано

### 1) Работа с HDFS (CLI)
- Создание директорий в HDFS
- Загрузка файлов в HDFS (`hdfs dfs -put`)
- Проверка наличия данных, просмотр первых строк (`hdfs dfs -cat | head`)
- Работа с рекурсивным листингом и проверкой размеров

### 2) MapReduce задачи (Hadoop Streaming + Python)
#### 2.1 WordCount (Shakespeare)
- Подсчет частот слов в тексте
- Условие: считать только слова длиной > 4 символов
- Реализация: `mapper.py` эмитит `(word, 1)`, `reducer.py` суммирует

#### 2.2 Максимальный доход компании по стране
Данные: `country;company;date;income`
- Группировка по `(country, company)`
- Поиск максимального `income` внутри группы
- Реализация: `mapper.py` → ключ `country+company`, `reducer.py` → max()

#### 2.3 Top-5 самых посещаемых сайтов по каждой дате (2 MR-job’а)
Данные: `url;timestamp`
- Job 1: считает посещения для `(url, date)`
- Job 2: делает top-5 по каждой `date` (используются настройки сортировки/партиционирования ключей в shuffle)

## Технологии
- Hadoop / HDFS / YARN
- Hadoop Streaming (`hadoop-streaming-*.jar`)
- Python 3 (mapper/reducer)
- Bash-команды (запуск джоб)
- Jupyter Notebook (как единый сценарий Run All)
