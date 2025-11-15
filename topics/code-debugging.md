
# Отладка кода

## Описание

**Отладка кода (дебаггинг)** — это систематический процесс поиска, анализа и исправления ошибок (багов) в программном обеспечении. Ошибки могут варьироваться от синтаксических проблем, которые легко обнаруживаются компилятором, до сложных логических ошибок, которые проявляются только при определённых условиях выполнения программы. Отладка — это неотъемлемая часть разработки, и овладение её техниками критически важно для создания надёжного и качественного кода[1][2][3].

Правильная отладка требует комбинации различных подходов: использование специализированных отладчиков (debuggers), логирование событий, обработка исключений, и модульное тестирование. В 2025 году, с развитием IDE и инструментов автоматизации, отладка стала более доступной и эффективной, но основные принципы остаются неизменными.

## Уровень

Основы

## Классификация ошибок

Прежде чем приступить к отладке, необходимо понимать различные типы ошибок, которые могут возникнуть в программе[4][5][6]:

### Синтаксические ошибки (Compile-time errors)

**Синтаксические ошибки** возникают при нарушении правил языка программирования. Они обнаруживаются компилятором на этапе компиляции и представляют собой самые лёгкие ошибки для исправления[4][5]:

- Несоответствие числа открывающих и закрывающих скобок
- Отсутствие точки с запятой в конце оператора
- Неправильное использование ключевых слов
- Попытка использования несуществующего объекта или метода
- Пропуск необходимого типа при объявлении переменной

Пример синтаксической ошибки в Java:

```java
// Синтаксическая ошибка: отсутствует точка с запятой
int x = 10  // Error: ';' expected

// Синтаксическая ошибка: неправильный синтаксис цикла
for (int i = 0 i < 10; i++) // Error: ':' expected
```

### Ошибки выполнения (Runtime errors)

**Ошибки выполнения** не нарушают синтаксис языка, но приводят к ошибочным операциям во время работы программы. Они обнаруживаются только при запуске программы при определённых условиях[4][5]:

- Деление на ноль
- Доступ к несуществующему элементу массива (IndexOutOfBoundsException)
- Попытка обращения к методу null-объекта (NullPointerException)
- Недостаточно памяти для выполнения операции (OutOfMemoryError)
- Попытка открыть несуществующий файл (FileNotFoundException)

Пример ошибки выполнения в Python:

```python
# Ошибка выполнения: деление на ноль
x = 10
y = 0
result = x / y  # ZeroDivisionError: division by zero

# Ошибка выполнения: индекс за границами массива
numbers = [1, 2, 3]
print(numbers[5])  # IndexError: list index out of range
```

### Логические ошибки (Алгоритмические ошибки)

**Логические ошибки** — это ошибки в алгоритме программы. При верных исходных данных и внешне безошибочной работе программа производит неверные результаты. Это самый коварный тип ошибок, так как пользователь может получить неправильный результат, считая его корректным[4][5]:

- Неправильная логика условия
- Ошибка в вычислениях
- Бесконечные циклы
- Неправильный порядок операций

Пример логической ошибки в C++:

```cpp
// Логическая ошибка: условие всегда истинно
int age = 25;
if (age > 0 || age < 100) {  // Всегда true, бесполезное условие
    cout << "Valid age" << endl;
}

// Логическая ошибка: неправильный расчёт
double average = (a + b + c) / 3;  // Должно быть: (a + b + c) / 3.0
```

## Методы отладки

### Метод 1: Вывод отладочной информации

**Самый простой и старейший метод отладки** — добавление операторов вывода в критические точки программы для отслеживания значений переменных и потока выполнения[1][3]:

```python
def calculate_discount(price, discount_percent):
    print(f"DEBUG: price = {price}")  # Выводим исходные значения
    print(f"DEBUG: discount_percent = {discount_percent}")
    
    discount = price * discount_percent / 100
    print(f"DEBUG: discount = {discount}")
    
    final_price = price - discount
    print(f"DEBUG: final_price = {final_price}")
    
    return final_price
```

Преимущества этого метода:
- Простота реализации
- Доступность в любой среде
- Не требует дополнительных инструментов

Недостатки:
- Много кода для удаления после отладки
- Загромождает логику программы
- Непрактично для больших приложений

### Метод 2: Логирование

**Логирование** — это более структурированный подход к отслеживанию событий в программе. В отличие от простого вывода, логи могут быть разных уровней и записываться в файлы или системы мониторинга[7][8][9]:

#### Уровни логирования

Все стандартные логирующие библиотеки используют иерархию уровней логирования[7][8][9]:

| Уровень | Назначение | Пример использования |
|---------|-----------|---------------------|
| **TRACE** | Наиболее детальная информация | Вход/выход из функции, значения локальных переменных |
| **DEBUG** | Подробная техническая информация для отладки | Значения переменных, состояние объектов |
| **INFO** | Общие информационные сообщения | Запуск приложения, инициализация сервиса, ключевые события |
| **WARN** | Предупреждения о потенциальных проблемах | Устаревшие API, недостаток памяти, нестандартные условия |
| **ERROR** | Ошибки, требующие внимания | Исключения, ошибки подключения к БД, invalid данные |
| **FATAL/CRITICAL** | Критические ошибки, при которых приложение может упасть | Out of memory, stack overflow, невозможность загрузить конфигурацию |

#### Примеры логирования на Python

```python
import logging

# Базовая настройка логирования
logging.basicConfig(
    level=logging.DEBUG,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    filename='app.log'
)

logger = logging.getLogger(__name__)

def process_data(data):
    logger.debug(f"Starting processing with data: {data}")
    
    try:
        if not isinstance(data, dict):
            logger.warning(f"Expected dict, got {type(data)}")
            return None
        
        result = data['value'] / data['divisor']
        logger.info(f"Successfully processed data: {result}")
        return result
        
    except KeyError as e:
        logger.error(f"Missing key: {e}")
        raise
    except ZeroDivisionError:
        logger.critical("Division by zero detected!")
        raise
    except Exception as e:
        logger.error(f"Unexpected error: {e}")
        raise
```

#### Логирование в Go с уровнями

Go по умолчанию не поддерживает уровни логирования в стандартной библиотеке, но можно реализовать их вручную или использовать сторонние библиотеки[7]:

```go
package main

import (
    "log"
    "os"
    "fmt"
)

type LogLevel int

const (
    DEBUG LogLevel = iota
    INFO
    WARN
    ERROR
    FATAL
)

var logLevel = INFO

func Log(level LogLevel, msg string) {
    if level < logLevel {
        return
    }
    
    prefix := ""
    switch level {
    case DEBUG:
        prefix = "DEBUG"
    case INFO:
        prefix = "INFO"
    case WARN:
        prefix = "WARN"
    case ERROR:
        prefix = "ERROR"
    case FATAL:
        prefix = "FATAL"
    }
    
    log.Printf("[%s] %s", prefix, msg)
    if level == FATAL {
        os.Exit(1)
    }
}

func main() {
    Log(DEBUG, "Загрузка конфигурации")
    Log(INFO, "Сервер запущен по адресу localhost:8080")
    Log(WARN, "Память заканчивается")
    Log(ERROR, "Соединение с БД потеряно")
}
```

Популярные логирующие библиотеки[7]:
- **Logrus** (Go) — структурированное логирование с уровнями
- **Zap** (Go) — быстрое и структурированное логирование
- **Zerolog** (Go) — лёгкое логирование с JSON выводом
- **logging** (Python) — встроенная библиотека Python
- **Winston** (Node.js) — гибкое логирование для JavaScript

### Метод 3: Отладчики (Debuggers)

**Отладчик (debugger)** — это специализированный инструмент, который позволяет выполнять программу пошагово, приостанавливать её в определённых местах, и инспектировать значения переменных в реальном времени[1][2][10][3]:

#### Основные возможности отладчика

- **Точки останова (breakpoints)** — программа останавливается в определённых строках кода
- **Пошаговое выполнение** — выполнение программы строка за строкой
- **Анализ переменных** — просмотр текущих значений всех переменных
- **Просмотр стека вызовов** — отслеживание цепочки вызванных функций
- **Условные точки останова** — остановка только при выполнении определённого условия

#### GDB (GNU Debugger)

**GDB** — универсальный отладчик для C, C++, Java, Python и других языков. Работает из командной строки[10][11][12]:

```bash
# Компиляция с отладочной информацией
gcc -g -o my_program my_program.c

# Запуск программы в GDB
gdb ./my_program

# Основные команды GDB
(gdb) break main              # Установить точку останова на функцию main
(gdb) break my_file.c:10      # Установить точку останова на строку 10
(gdb) break func if i == 5    # Условная точка останова
(gdb) run                      # Запустить программу
(gdb) step                     # Пошаговое выполнение (заходит в функции)
(gdb) next                     # Переход на следующую строку (не заходит в функции)
(gdb) continue                 # Продолжить выполнение
(gdb) print variable_name      # Вывести значение переменной
(gdb) print *pointer           # Вывести значение, на которое указывает указатель
(gdb) backtrace                # Показать стек вызовов
(gdb) info breakpoints         # Список всех точек останова
(gdb) disable 1                # Отключить точку останова номер 1
(gdb) delete 1                 # Удалить точку останова номер 1
(gdb) quit                     # Выход из GDB
```

#### Visual Studio Debugger

**Visual Studio Debugger** — встроенный отладчик в Visual Studio, поддерживает множество языков[13]:

- Щёлкните левой кнопкой мыши слева от строки кода для установления точки останова
- Нажмите F5 для запуска в режиме отладки
- Используйте горячие клавиши: F10 (next), F11 (step), Shift+F11 (выход из функции)
- В окне Variables инспектируйте значения переменных
- Используйте Watch для отслеживания выражений

#### Типы точек останова

| Тип | Описание | Применение |
|-----|---------|-----------|
| **Простая точка останова** | Останавливает выполнение в определённой строке | Базовая отладка |
| **Условная точка останова** | Остаётся только если выражение истинно | Отладка циклов, сложные условия |
| **Точка останова по счётчику** | Срабатывает после N итераций | Отладка цикла, срабатывающего после определённого числа повторений |
| **Точка останова данных (Data breakpoint)** | Останавливает программу при изменении переменной | Поиск неожиданных изменений переменных |
| **Зависимая точка останова** | Активируется только если сначала была достигнута другая точка | Сложная отладка многопоточности |
| **Временная точка останова** | Удаляется после первого срабатывания | Разовая проверка |

## Обработка исключений

**Обработка исключений** — это механизм для перехвата и обработки ошибок выполнения, предотвращая аварийное завершение программы[14][15][16]:

### Конструкция try-except (Python)

```python
try:
    # Код, который может вызвать исключение
    a = int(input("Введите первое число: "))
    b = int(input("Введите второе число: "))
    result = a / b
    
except ValueError:
    # Обработка ошибки преобразования типа
    print("Пожалуйста, вводите только числа")
    
except ZeroDivisionError:
    # Обработка деления на ноль
    print("На ноль делить нельзя")
    
except Exception as e:
    # Обработка всех остальных исключений
    print(f"Произошла ошибка: {e}")
    
else:
    # Выполняется если исключений не было
    print(f"Результат деления: {result}")
    
finally:
    # Выполняется всегда
    print("Программа завершена")
```

### Try-catch в Java

```java
try {
    String[] fruits = {"Яблоко", "Банан"};
    System.out.println(fruits[5]);  // IndexOutOfBoundsException
    
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Ошибка: индекс за границами массива");
    e.printStackTrace();
    
} catch (NullPointerException e) {
    System.out.println("Ошибка: null-указатель");
    
} finally {
    System.out.println("Блок finally выполнен");
}
```

### Try-catch в C++

```cpp
#include <iostream>
#include <stdexcept>
using namespace std;

try {
    int x = 10;
    int y = 0;
    
    if (y == 0) {
        throw invalid_argument("Делитель не может быть нулём");
    }
    
    int result = x / y;
    cout << "Результат: " << result << endl;
    
} catch (invalid_argument& e) {
    cout << "Ошибка аргумента: " << e.what() << endl;
    
} catch (exception& e) {
    cout << "Неизвестная ошибка: " << e.what() << endl;
    
} catch (...) {
    cout << "Неожиданная ошибка неизвестного типа" << endl;
}
```

### Лучшие практики обработки исключений

- **Ловите специфические исключения**: Не используйте везде `catch (Exception)`, ловите конкретные типы ошибок
- **Логируйте ошибки**: Всегда записывайте информацию об исключении в логи
- **Не подавляйте исключения**: Пустой catch-блок скрывает проблемы
- **Используйте finally для очистки ресурсов**: Закрытие файлов, соединений и других ресурсов
- **Создавайте пользовательские исключения**: Для специфических ошибок вашего приложения
- **Не используйте исключения для управления потоком**: Исключения предназначены для обработки ошибок, не для нормального управления потоком

## Модульное тестирование (Unit Testing)

**Модульное тестирование** — это автоматическое тестирование отдельных компонентов (функций, методов, классов) программы для проверки их корректности[17][18][19]:

### Unittest в Python

```python
import unittest

def add(a, b):
    return a + b

def divide(a, b):
    if b == 0:
        raise ValueError("Делитель не может быть нулём")
    return a / b

class TestMathOperations(unittest.TestCase):
    
    def test_add_positive(self):
        """Тест сложения положительных чисел"""
        self.assertEqual(add(2, 3), 5)
    
    def test_add_negative(self):
        """Тест сложения отрицательных чисел"""
        self.assertEqual(add(-1, -1), -2)
    
    def test_divide_success(self):
        """Тест успешного деления"""
        self.assertEqual(divide(10, 2), 5.0)
    
    def test_divide_by_zero(self):
        """Тест деления на ноль"""
        with self.assertRaises(ValueError):
            divide(10, 0)
    
    def test_divide_result_type(self):
        """Тест типа результата"""
        result = divide(5, 2)
        self.assertIsInstance(result, float)

if __name__ == '__main__':
    unittest.main()
```

### Методы проверки в unittest

| Метод | Описание | Пример |
|-------|---------|--------|
| `assertEqual(a, b)` | Проверка равенства | `self.assertEqual(add(2, 3), 5)` |
| `assertNotEqual(a, b)` | Проверка неравенства | `self.assertNotEqual(x, y)` |
| `assertTrue(x)` | Проверка истинности | `self.assertTrue(is_valid)` |
| `assertFalse(x)` | Проверка ложности | `self.assertFalse(is_empty)` |
| `assertIsNone(x)` | Проверка на None | `self.assertIsNone(result)` |
| `assertIn(a, b)` | Проверка вхождения | `self.assertIn("ERROR", log)` |
| `assertRaises(exception)` | Проверка исключения | `self.assertRaises(ValueError, divide, 1, 0)` |
| `assertIsInstance(a, b)` | Проверка типа | `self.assertIsInstance(result, int)` |

### Pytest в Python

```python
import pytest

def square_root(x):
    if x < 0:
        raise ValueError("Cannot compute square root of negative number")
    return x ** 0.5

def test_square_root_positive():
    assert square_root(4) == 2.0

def test_square_root_zero():
    assert square_root(0) == 0.0

def test_square_root_negative():
    with pytest.raises(ValueError):
        square_root(-1)

# Параметризованный тест
@pytest.mark.parametrize("x,expected", [
    (4, 2.0),
    (9, 3.0),
    (16, 4.0),
])
def test_square_root_parametrized(x, expected):
    assert square_root(x) == expected
```

## Практические примеры

### Пример 1: Отладка с print

```python
def calculate_factorial(n):
    print(f"DEBUG: calculating factorial of {n}")
    result = 1
    
    for i in range(1, n + 1):
        print(f"DEBUG: i = {i}, result before = {result}")
        result *= i
        print(f"DEBUG: result after = {result}")
    
    return result

print(calculate_factorial(5))
```

### Пример 2: Обработка исключений

```python
def read_numbers_from_file(filename):
    numbers = []
    try:
        with open(filename, 'r') as file:
            for line in file:
                try:
                    number = int(line.strip())
                    numbers.append(number)
                except ValueError:
                    print(f"Ошибка: '{line.strip()}' не является числом")
    
    except FileNotFoundError:
        print(f"Ошибка: файл '{filename}' не найден")
    
    except Exception as e:
        print(f"Неожиданная ошибка: {e}")
    
    finally:
        print("Завершена работа с файлом")
    
    return numbers

# Использование
result = read_numbers_from_file("numbers.txt")
print(f"Прочитано чисел: {len(result)}")
```

### Пример 3: Логирование

```python
import logging
import traceback

# Настройка логирования
logging.basicConfig(
    level=logging.DEBUG,
    format='%(asctime)s - %(levelname)s - %(message)s',
    handlers=[
        logging.FileHandler('app.log'),
        logging.StreamHandler()
    ]
)

logger = logging.getLogger(__name__)

def process_transaction(transaction_id, amount):
    logger.info(f"Starting transaction {transaction_id} for amount {amount}")
    
    try:
        if amount <= 0:
            logger.warning(f"Suspicious transaction: amount is {amount}")
            raise ValueError("Amount must be positive")
        
        # Имитация обработки
        logger.debug(f"Validating transaction {transaction_id}")
        
        logger.info(f"Transaction {transaction_id} completed successfully")
        return True
    
    except ValueError as e:
        logger.error(f"Invalid transaction {transaction_id}: {e}")
        return False
    
    except Exception as e:
        logger.critical(f"Unexpected error in transaction {transaction_id}: {e}")
        logger.debug(traceback.format_exc())
        return False

# Использование
process_transaction("TRX001", 100)
process_transaction("TRX002", -50)  # Ошибка
```

### Пример 4: Модульные тесты

```python
import unittest

def find_max(numbers):
    if not numbers:
        raise ValueError("List cannot be empty")
    return max(numbers)

class TestFindMax(unittest.TestCase):
    
    def test_max_positive_numbers(self):
        self.assertEqual(find_max([1, 5, 3]), 5)
    
    def test_max_negative_numbers(self):
        self.assertEqual(find_max([-10, -5, -20]), -5)
    
    def test_max_single_number(self):
        self.assertEqual(find_max([42]), 42)
    
    def test_max_empty_list(self):
        with self.assertRaises(ValueError):
            find_max([])

if __name__ == '__main__':
    unittest.main()
```

## Примеры использования

### Использование отладчиков

- Установка точек останова для приостановки выполнения в критических местах
- Пошаговое прохождение кода для отслеживания логики выполнения
- Инспекция переменных в реальном времени для выявления неожиданных значений
- Анализ стека вызовов для понимания последовательности выполнения функций

### Логирование для отслеживания выполнения

- Запись информации о входе и выходе из функций
- Логирование ключевых переменных и промежуточных результатов
- Использование разных уровней логирования для разной информации
- Сохранение логов в файлы для последующего анализа

### Обработка исключений с try-except блоками

- Перехват ожидаемых ошибок (файл не найден, неверный ввод пользователя)
- Предотвращение аварийного завершения программы
- Информирование пользователя об ошибке
- Очистка ресурсов в блоке finally

## Ресурсы для изучения

### Документация отладчиков

- **GDB Manual** (https://sourceware.org/gdb/documentation/) — официальная документация GNU Debugger
- **Visual Studio Debugger Documentation** (https://learn.microsoft.com/en-us/visualstudio/debugger/) — подробные инструкции для Visual Studio
- **LLDB Documentation** (https://lldb.llvm.org/) — отладчик для macOS и Linux
- **Python Debugger (pdb)** (https://docs.python.org/3/library/pdb.html) — встроенный отладчик Python

### Рекомендуемые книги

- **"Debugging: The 9 Indispensable Rules for Finding Even the Most Elusive Software and Hardware Problems"** (David J. Agans) — классическая книга о техниках отладки
- **"The Pragmatic Programmer"** (David Thomas, Andrew Hunt) — включает главы об отладке и тестировании
- **"Code Complete"** (Steve McConnell) — раздел о методах отладки и поиске ошибок
- **"Effective Python"** (Brett Slatkin) — включает рекомендации по логированию и отладке

### Инструменты и платформы

- **IDE встроенные отладчики**: PyCharm, Visual Studio Code, Visual Studio, Xcode
- **Логирующие библиотеки**: logging (Python), Log4j (Java), Logrus (Go), Winston (Node.js)
- **Тестирование**: pytest, unittest (Python), JUnit (Java), NUnit (.NET)
- **Профилирование**: cProfile (Python), Valgrind (C/C++), Java Flight Recorder (Java)
- **Статический анализ**: SonarQube, Pylint, ESLint

### Видеоматериалы

- Туториалы по использованию GDB, Visual Studio Debugger и других инструментов
- Лекции по практикам отладки и тестирования
- Демонстрации использования loggers и обработки исключений
- Примеры применения отладчиков в реальных проектах

## Методы поиска ошибок

### Метод индукции

Тщательный анализ симптомов ошибки. Начните с наблюдений: неправильные результаты, зависания, сообщения об ошибках. На их основании выдвигайте гипотезы и проверяйте их поочередно[3]:

1. Наблюдайте проявления ошибки
2. Выдвигайте гипотезы о причинах
3. Проверяйте каждую гипотезу
4. Сужайте область поиска

### Метод обратного прослеживания

Начните с точки, где обнаружена ошибка, и отследите причину в обратном направлении[3]:

1. Найдите точку вывода неправильного результата
2. Выдвигайте гипотезы о значениях переменных, приведших к ошибке
3. Переходите к предыдущей точке
4. Повторяйте до обнаружения источника ошибки

### Метод divide and conquer

Разделите программу на части и проверяйте их независимо:

1. Разбейте программу на логические блоки
2. Проверьте каждый блок отдельно
3. Найдите блок с ошибкой
4. Разбейте блок на части и повторите

## Заключение

Отладка кода — это критический навык для разработчика, требующий терпения, логического мышления и систематического подхода. В 2025 году инструменты отладки стали намного более мощными и удобными, но основные принципы остаются неизменными: использование логирования, отладчиков, обработки исключений и модульного тестирования. Комбинация этих методов позволяет эффективно находить и исправлять ошибки, обеспечивая качество и надёжность программного обеспечения. Практика и опыт помогают разработчикам быстрее диагностировать проблемы и писать более устойчивый код.

Цитаты:
[1] Исправление ошибок в коде: от классических методов до ... https://developers.sber.ru/help/gigachat-api/correcting-errors-in-code
[2] Отладка кода: методы, инструменты и руководство по ... https://stoneforest.ru/look/allabout/marketing/otladka-koda-metody-instrumenty-i-rukovodstvo-po-poisku-oshibok-v-programme/
[3] Дебаггинг: описание, особенности, методы реализации https://otus.ru/journal/debagging-opisanie-osobennosti-metody-realizacii/
[4] Классификация ошибок https://studfile.net/preview/9036283/page:3/
[5] Ошибки - 1.4.2. Типы ошибок https://tat67183862.narod.ru/oschibki1.htm
[6] Классификация ошибок https://ofim.oscsbras.ru/~eugene/docums/Delphi/d7_beg/Glava%2013/Index2.htm
[7] Настройка уровней логирования log levels в Go https://purpleschool.ru/knowledge-base/article/log-levels
[8] Логирование: описание, механизмы, особенности https://otus.ru/journal/logirovanie-opisanie-mehanizmy-osobennosti/
[9] Настройка уровней логирования - JSP & Servlets https://javarush.com/quests/lectures/questservlets.level05.lecture03
[10] Как найти ошибку в коде с использованием отладчиков https://foxminded.ua/ru/kak-najti-oshibku-v-kode/
[11] GDB. Точки останова (breakpoints) https://www.youtube.com/watch?v=rsNHrHEHJkE
[12] Отладка с помощью GDB - Остановка и продолжение ... https://www.opennet.ru/docs/RUS/gdb/gdb_6.html
[13] Использование правильного типа точки останова https://learn.microsoft.com/ru-ru/visualstudio/debugger/using-breakpoints?view=vs-2022
[14] Работа с исключениями try/except/else/finally https://pyneng.readthedocs.io/ru/latest/book/06_control_structures/exceptions.html
[15] Как обрабатывать исключения в Python: try, except, else, ... https://sky.pro/media/ispolzovanie-try-except-else-v-python-horoshaya-praktika-ili-net/
[16] 5.3. Модель исключений Python. Try, except, else, finally. ... https://education.yandex.ru/handbook/python/article/model-isklyuchenij-python-try-except-else-finally-moduli
[17] Python unittest — пример юнит-теста и руководство https://arenda-server.cloud/blog/python-unittest-primer-junit-testa-i-rukovodstvo/
[18] Тестирование на Python: unittest и pytest https://qarocks.ru/python-testing-unittest-pytest/
[19] Учимся тестировать на Python: unittest и pytest https://tproger.ru/articles/testiruem-na-python-unittest-i-pytest-instrukcija-dlja-nachinajushhih
[20] Точки останова данных в Visual Studio Code https://learn.microsoft.com/ru-ru/shows/pure-virtual-cpp-2022/data-breakpoints-in-visual-studio-code