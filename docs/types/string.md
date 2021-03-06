# Строки

**Строки** в Python - упорядоченные последовательности символов, используемые для хранения и представления текстовой информации, поэтому с помощью строк можно работать со всем, что может быть представлено в текстовой форме.

## Литералы строк

Работа со строками в Python очень удобна. Существует несколько литералов строк, которые мы сейчас и рассмотрим.

### Строки в апострофах и в кавычках

```python
S = 'spam"s'
S = "spam's"
```

Строки в апострофах и в кавычках - одно и то же. Причина наличия двух вариантов в том, чтобы позволить вставлять в литералы строк символы кавычек или апострофов, не используя экранирование.

### Служебные символы

Экранированные последовательности позволяют вставить символы, которые сложно ввести с клавиатуры.

| Экранированная последовательность | Назначение                                          |
| --------------------------------- | --------------------------------------------------- |
| `\n`                              | Перевод строки                                      |
| `\a`                              | Звонок                                              |
| `\b`                              | Забой                                               |
| `\f`                              | Перевод страницы                                    |
| `\r`                              | Возврат каретки                                     |
| `\t`                              | Горизонтальная табуляция                            |
| `\v`                              | Вертикальная табуляция                              |
| `\N{id}`                          | Идентификатор ID базы данных Юникода                |
| `\uhhhh`                          | 16-битовый символ Юникода в 16-ричном представлении |
| `\Uhhhh…`                         | 32-битовый символ Юникода в 32-ричном представлении |
| `\xhh`                            | 16-ричное значение символа                          |
| `\ooo`                            | 8-ричное значение символа                           |
| `\0`                              | Символ `Null` (не является признаком конца строки)  |

### "Сырые" строки

Если перед открывающей кавычкой стоит символ `r` (в любом регистре), то механизм экранирования отключается.

```python
S = r'C:\newt.txt'
```

Но, несмотря на назначение, "сырая" строка не может заканчиваться символом обратного слэша. Пути решения:

```python
S = r'\n\n\\'[:-1]
S = r'\n\n' + '\\'
S = '\\n\\n'
```

### Строки в тройных апострофах или кавычках

Главное достоинство строк в тройных кавычках в том, что их можно использовать для записи многострочных блоков текста. Внутри такой строки возможно присутствие кавычек и апострофов, главное, чтобы не было трех кавычек подряд.

```python
>>> c = '''это очень большая
... строка, многострочный
... блок текста'''
>>> c
'это очень большая\nстрока, многострочный\nблок текста'
>>> print(c)
это очень большая
строка, многострочный
блок текста
```

## Функции и методы строк

### Конкатенация (сложение)

```python
>>> S1 = 'spam'
>>> S2 = 'eggs'
>>> print(S1 + S2)
'spameggs'
```

### Дублирование строки

```python
>>> print('spam' * 3)
spamspamspam
```

### Длина строки (функция len)

```python
>>> len('spam')
4
```

### Доступ по индексу

```python
>>> S = 'spam'
>>> S[0]
's'
>>> S[2]
'a'
>>> S[-2]
'a'
```

Как видно из примера, в Python возможен и доступ по отрицательному индексу, при этом отсчет идет от конца строки.

### Извлечение среза

Оператор извлечения среза: `[X:Y]`. `X` – начало среза, а `Y` – окончание;

символ с номером `Y` в срез не входит. По умолчанию первый индекс равен `0`, а второй - длине строки.

```python
>>> s = 'spameggs'
>>> s[3:5]
'me'
>>> s[2:-2]
'ameg'
>>> s[:6]
'spameg'
>>> s[1:]
'pameggs'
>>> s[:]
'spameggs'
```

Кроме того, можно задать шаг, с которым нужно извлекать срез.

```python
>>> s[::-1]
'sggemaps'
>>> s[3:5:-1]
''
>>> s[2::2]
'aeg'
```

### Другие функции и методы строк

При вызове методов необходимо помнить, что строки в Python относятся к категории неизменяемых последовательностей, то есть все функции и методы могут лишь создавать новую строку.

```python
>>> s = 'spam'
>>> s[1] = 'b'
Traceback (most recent call last):
  File "", line 1, in
    s[1] = 'b'
TypeError: 'str' object does not support item assignment
>>> s = s[0] + 'b' + s[2:]
>>> s
'sbam'
```

Поэтому все строковые методы возвращают новую строку, которую потом следует присвоить переменной.

| Функция или метод                                    | Назначение                                                                                                                                                                                                      |
| ---------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `S = 'str'; S = "str"; S = '''str'''; S = """str"""` | Литералы строк                                                                                                                                                                                                  |
| `S = "s\np\ta\nbbb"`                                 | Экранированные последовательности                                                                                                                                                                               |
| `S = r"C:\temp\new"`                                 | Неформатированные строки (подавляют экранирование)                                                                                                                                                              |
| `S = b"byte"`                                        | Строка байтов                                                                                                                                                                                                   |
| `S1 + S2`                                            | Конкатенация (сложение строк)                                                                                                                                                                                   |
| `S1 * 3`                                             | Повторение строки                                                                                                                                                                                               |
| `S[i]`                                               | Обращение по индексу                                                                                                                                                                                            |
| `S[i:j:step]`                                        | Извлечение среза                                                                                                                                                                                                |
| `len(S)`                                             | Длина строки                                                                                                                                                                                                    |
| `S.find(str, [start],[end])`                         | Поиск подстроки в строке. Возвращает номер первого вхождения или `-1`                                                                                                                                           |
| `S.rfind(str, [start],[end])`                        | Поиск подстроки в строке. Возвращает номер последнего вхождения или `-1`                                                                                                                                        |
| `S.index(str, [start],[end])`                        | Поиск подстроки в строке. Возвращает номер первого вхождения или вызывает `ValueError`                                                                                                                          |
| `S.rindex(str, [start],[end])`                       | Поиск подстроки в строке. Возвращает номер последнего вхождения или вызывает `ValueError`                                                                                                                       |
| `S.replace(шаблон, замена[, maxcount])`              | Замена шаблона на замену. `maxcount` ограничивает количество замен                                                                                                                                              |
| `S.split(символ)`                                    | Разбиение строки по разделителю                                                                                                                                                                                 |
| `S.isdigit()`                                        | Состоит ли строка из цифр                                                                                                                                                                                       |
| `S.isalpha()`                                        | Состоит ли строка из букв                                                                                                                                                                                       |
| `S.isalnum()`                                        | Состоит ли строка из цифр или букв                                                                                                                                                                              |
| `S.islower()`                                        | Состоит ли строка из символов в нижнем регистре                                                                                                                                                                 |
| `S.isupper()`                                        | Состоит ли строка из символов в верхнем регистре                                                                                                                                                                |
| `S.isspace()`                                        | Состоит ли строка из неотображаемых символов (пробел, символ перевода страницы (`\f`), "новая строка" (`\n`), "перевод каретки" (`\r`), "горизонтальная табуляция" (`\t`) и "вертикальная табуляция" (`\v`))    |
| `S.istitle()`                                        | Начинаются ли слова в строке с заглавной буквы                                                                                                                                                                  |
| `S.upper()`                                          | Преобразование строки к верхнему регистру                                                                                                                                                                       |
| `S.lower()`                                          | Преобразование строки к нижнему регистру                                                                                                                                                                        |
| `S.startswith(str)`                                  | Начинается ли строка `S` с шаблона `str`                                                                                                                                                                        |
| `S.endswith(str)`                                    | Заканчивается ли строка `S` шаблоном `str`                                                                                                                                                                      |
| `S.join(список)`                                     | Сборка строки из списка с разделителем `S`                                                                                                                                                                      |
| `ord(символ)`                                        | Символ в его код ASCII                                                                                                                                                                                          |
| `chr(число)`                                         | Код ASCII в символ                                                                                                                                                                                              |
| `S.capitalize()`                                     | Переводит первый символ строки в верхний регистр, а все остальные в нижний                                                                                                                                      |
| `S.center(width, [fill])`                            | Возвращает отцентрованную строку, по краям которой стоит символ `fill` (пробел по умолчанию)                                                                                                                    |
| `S.count(str, [start],[end])`                        | Возвращает количество непересекающихся вхождений подстроки в диапазоне `[начало, конец]` (`0` и длина строки по умолчанию)                                                                                      |
| `S.expandtabs([tabsize])`                            | Возвращает копию строки, в которой все символы табуляции заменяются одним или несколькими пробелами, в зависимости от текущего столбца. Если `TabSize` не указан, размер табуляции полагается равным 8 пробелам |
| `S.lstrip([chars])`                                  | Удаление пробельных символов в начале строки                                                                                                                                                                    |
| `S.rstrip([chars])`                                  | Удаление пробельных символов в конце строки                                                                                                                                                                     |
| `S.strip([chars])`                                   | Удаление пробельных символов в начале и в конце строки                                                                                                                                                          |
| `S.partition(шаблон)`                                | Возвращает кортеж, содержащий часть перед первым шаблоном, сам шаблон, и часть после шаблона. Если шаблон не найден, возвращается кортеж, содержащий саму строку, а затем две пустых строки                     |
| `S.rpartition(sep)`                                  | Возвращает кортеж, содержащий часть перед последним шаблоном, сам шаблон, и часть после шаблона. Если шаблон не найден, возвращается кортеж, содержащий две пустых строки, а затем саму строку                  |
| `S.swapcase()`                                       | Переводит символы нижнего регистра в верхний, а верхнего – в нижний                                                                                                                                             |
| `S.title()`                                          | Первую букву каждого слова переводит в верхний регистр, а все остальные в нижний                                                                                                                                |
| `S.zfill(width)`                                     | Делает длину строки не меньшей `width`, по необходимости заполняя первые символы нулями                                                                                                                         |
| `S.ljust(width, fillchar=" ")`                       | Делает длину строки не меньшей `width`, по необходимости заполняя последние символы символом `fillchar`                                                                                                         |
| `S.rjust(width, fillchar=" ")`                       | Делает длину строки не меньшей `width`, по необходимости заполняя первые символы символом `fillchar`                                                                                                            |
| `S.format(*args, **kwargs)`                          | Форматирование строки                                                                                                                                                                                           |

## Форматирование строк

Иногда (а точнее, довольно часто) возникают ситуации, когда нужно сделать строку, подставив в неё некоторые данные, полученные в процессе выполнения программы (пользовательский ввод, данные из файлов и т. д.). Подстановку данных можно сделать с помощью форматирования строк. Форматирование можно сделать с помощью оператора `%`, либо с помощью метода `format`.

Если для подстановки требуется только один аргумент, то значение - сам аргумент:

```python
>>> 'Hello, {}!'.format('Vasya')
'Hello, Vasya!'
```

А если несколько, то значениями будут являться все аргументы со строками подстановки (обычных или именованных):

```python
>>> '{0}, {1}, {2}'.format('a', 'b', 'c')
'a, b, c'
>>> '{}, {}, {}'.format('a', 'b', 'c')
'a, b, c'
>>> '{2}, {1}, {0}'.format('a', 'b', 'c')
'c, b, a'
>>> '{2}, {1}, {0}'.format(*'abc')
'c, b, a'
>>> '{0}{1}{0}'.format('abra', 'cad')
'abracadabra'
>>> 'Coordinates: {latitude}, {longitude}'.format(latitude='37.24N', longitude='-115.81W')
'Coordinates: 37.24N, -115.81W'
>>> coord = {'latitude': '37.24N', 'longitude': '-115.81W'}
>>> 'Coordinates: {latitude}, {longitude}'.format(**coord)
'Coordinates: 37.24N, -115.81W'
```

Однако метод `format` умеет большее. Вот его синтаксис:

```
поле замены     ::=  "{" [имя поля] ["!" преобразование] [":" спецификация] "}"
имя поля        ::=  arg_name ("." имя атрибута | "[" индекс "]")*
преобразование  ::=  "r" (внутреннее представление) | "s" (человеческое представление)
спецификация    ::=  см. ниже
```

Например:

```python
>>> "Units destroyed: {players[0]}".format(players = [1, 2, 3])
'Units destroyed: 1'
>>> "Units destroyed: {players[0]!r}".format(players = ['1', '2', '3'])
"Units destroyed: '1'"
```

Теперь спецификация формата:

```
спецификация ::=  [[fill]align][sign][#][0][width][,][.precision][type]
заполнитель  ::=  символ кроме '{' или '}'
выравнивание ::=  "<" | ">" | "=" | "^"
знак         ::=  "+" | "-" | " "
ширина       ::=  integer
точность     ::=  integer
тип          ::=  "b" | "c" | "d" | "e" | "E" | "f" | "F" | "g" | "G" |
                  "n" | "o" | "s" | "x" | "X" | "%"
```

Выравнивание производится при помощи символа-заполнителя. Доступны следующие варианты выравнивания:

| Флаг | Значение                                                                               |
| ---- | -------------------------------------------------------------------------------------- |
| `<`  | Символы-заполнители будут справа (выравнивание объекта по левому краю) (по умолчанию). |
| `>`  | выравнивание объекта по правому краю.                                                  |
| `=`  | Заполнитель будет после знака, но перед цифрами. Работает только с числовыми типами.   |
| `^`  | Выравнивание по центру.                                                                |

Опция "знак" используется только для чисел и может принимать следующие значения:

| Флаг     | Значение                                         |
| -------- | ------------------------------------------------ |
| `+`      | Знак должен быть использован для всех чисел.     |
| `-`      | `-` для отрицательных, ничего для положительных. |
| `Пробел` | `-` для отрицательных, пробел для положительных. |

Поле "тип" может принимать следующие значения:

| Тип           | Значение                                                                                                                               |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `d`, `i`, `u` | Десятичное число.                                                                                                                      |
| `o`           | Число в восьмеричной системе счисления.                                                                                                |
| `x`           | Число в шестнадцатеричной системе счисления (буквы в нижнем регистре).                                                                 |
| `X`           | Число в шестнадцатеричной системе счисления (буквы в верхнем регистре).                                                                |
| `e`           | Число с плавающей точкой с экспонентой (экспонента в нижнем регистре).                                                                 |
| `E`           | Число с плавающей точкой с экспонентой (экспонента в верхнем регистре).                                                                |
| `f`, `F`      | Число с плавающей точкой (обычный формат).                                                                                             |
| `g`           | Число с плавающей точкой. с экспонентой (экспонента в нижнем регистре), если она меньше, чем `-4` или точности, иначе обычный формат.  |
| `G`           | Число с плавающей точкой. с экспонентой (экспонента в верхнем регистре), если она меньше, чем `-4` или точности, иначе обычный формат. |
| `c`           | Символ (строка из одного символа или число - код символа).                                                                             |
| `s`           | Строка.                                                                                                                                |
| `%`           | Число умножается на `100`, отображается число с плавающей точкой, а за ним знак `%`.                                                   |

И напоследок, несколько примеров:

```python
>>> coord = (3, 5)
>>> 'X: {0[0]};  Y: {0[1]}'.format(coord)
'X: 3;  Y: 5'
>>> "repr() shows quotes: {!r}; str() doesn't: {!s}".format('test1', 'test2')
"repr() shows quotes: 'test1'; str() doesn't: test2"
>>> '{:<30}'.format('left aligned')
'left aligned                  '
>>> '{:>30}'.format('right aligned')
'                 right aligned'
>>> '{:^30}'.format('centered')
'           centered           '
>>> '{:*^30}'.format('centered')  # use '*' as a fill char
'***********centered***********'
>>> '{:+f}; {:+f}'.format(3.14, -3.14)  # show it always
'+3.140000; -3.140000'
>>> '{: f}; {: f}'.format(3.14, -3.14)  # show a space for positive numbers
' 3.140000; -3.140000'
>>> '{:-f}; {:-f}'.format(3.14, -3.14)  # show only the minus -- same as '{:f}; {:f}'
'3.140000; -3.140000'
>>> # format also supports binary numbers
>>> "int: {0:d};  hex: {0:x};  oct: {0:o};  bin: {0:b}".format(42)
'int: 42;  hex: 2a;  oct: 52;  bin: 101010'
>>> # with 0x, 0o, or 0b as prefix:
>>> "int: {0:d};  hex: {0:#x};  oct: {0:#o};  bin: {0:#b}".format(42)
'int: 42;  hex: 0x2a;  oct: 0o52;  bin: 0b101010'
>>> points = 19.5
>>> total = 22
>>> 'Correct answers: {:.2%}'.format(points/total)
'Correct answers: 88.64%'
```
