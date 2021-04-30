# Функции

В этой статье я планирую рассказать о функциях, именных и анонимных, инструкциях `def`, `return` и `lambda`, обязательных и необязательных аргументах функции, функциях с произвольным числом аргументов.

## Именные функции, инструкция def

**Функция** в Python - объект, принимающий аргументы и возвращающий значение. Обычно функция определяется с помощью инструкции `def`.

Определим простейшую функцию:

```python
def add(x, y):
    return x + y
```

Инструкция `return` говорит, что нужно вернуть значение. В нашем случае функция возвращает сумму `x` и `y`.

Теперь мы ее можем вызвать:

```python
>>> add(1, 10)
11
>>> add('abc', 'def')
'abcdef'
```

Функция может быть любой сложности и возвращать любые объекты (списки, кортежи, и даже функции!):

```python
>>> def newfunc(n):
...     def myfunc(x):
...         return x + n
...     return myfunc
...
>>> new = newfunc(100)  # new - это функция
>>> new(200)
300
```

Функция может и не заканчиваться инструкцией `return`, при этом функция вернет значение `None`:

```python
>>> def func():
...     pass
...
>>> print(func())
None
```

## Аргументы функции

Функция может принимать произвольное количество аргументов или не принимать их вовсе. Также распространены функции с произвольным числом аргументов, функции с позиционными и именованными аргументами, обязательными и необязательными.

```python
>>> def func(a, b, c=2): # c - необязательный аргумент
...     return a + b + c
...
>>> func(1, 2)  # a = 1, b = 2, c = 2 (по умолчанию)
5
>>> func(1, 2, 3)  # a = 1, b = 2, c = 3
6
>>> func(a=1, b=3)  # a = 1, b = 3, c = 2
6
>>> func(a=3, c=6)  # a = 3, c = 6, b не определен
Traceback (most recent call last):
  File "", line 1, in
    func(a=3, c=6)
TypeError: func() takes at least 2 arguments (2 given)
```

Функция также может принимать переменное количество позиционных аргументов, тогда перед именем ставится `*`:

```python
>>> def func(*args):
...     return args
...
>>> func(1, 2, 3, 'abc')
(1, 2, 3, 'abc')
>>> func()
()
>>> func(1)
(1,)
```

Как видно из примера, `args` - это [кортеж](tuple.md) из всех переданных аргументов функции, и с переменной можно работать также, как и с кортежем.

Функция может принимать и произвольное число именованных аргументов, тогда перед именем ставится `**`:

```python
>>> def func(**kwargs):
...     return kwargs
...
>>> func(a=1, b=2, c=3)
{'a': 1, 'c': 3, 'b': 2}
>>> func()
{}
>>> func(a='python')
{'a': 'python'}
```

В переменной `kwargs` у нас хранится [словарь](dict.md), с которым мы, опять-таки, можем делать все, что нам заблагорассудится.

## Анонимные функции, инструкция lambda

Анонимные функции могут содержать лишь одно выражение, но и выполняются они быстрее. Анонимные функции создаются с помощью инструкции `lambda`. Кроме этого, их не обязательно присваивать переменной, как делали мы инструкцией `def func()`:

```python
>>> func = lambda x, y: x + y
>>> func(1, 2)
3
>>> func('a', 'b')
'ab'
>>> (lambda x, y: x + y)(1, 2)
3
>>> (lambda x, y: x + y)('a', 'b')
'ab'
```

lambda-функции, в отличие от обычной, не требуется инструкция `return`, а в остальном, ведет себя точно так же:

```python
>>> func = lambda *args: args
>>> func(1, 2, 3, 4)
(1, 2, 3, 4)
```

## Встроенные функции, выполняющие преобразование типов

`bool(x)`
: преобразование к типу `bool`, использующая стандартную процедуру проверки истинности. Если `х` является ложным или опущен, возвращает значение `False`, в противном случае она возвращает `True`.

`bytearray([источник [, кодировка [ошибки]]])`
: преобразование к [`bytearray`](byte.md). Bytearray - изменяемая последовательность целых чисел в диапазоне `0≤X<256`. Вызванная без аргументов, возвращает пустой массив байт.

`bytes([источник [, кодировка [ошибки]]])`
: возвращает объект типа [`bytes`](byte.md), который является неизменяемой последовательностью целых чисел в диапазоне `0≤X<256`. Аргументы конструктора интерпретируются как для `bytearray()`.

`complex([real[, imag]])`
: преобразование к [комплексному числу](number.md).

`dict([object])`
: преобразование к [словарю](dict.md).

`float([X])`
: преобразование к [числу с плавающей точкой](number.md). Если аргумент не указан, возвращается `0.0`.

`frozenset([последовательность])`
: возвращает неизменяемое [множество](set.md).

`int([object], [основание системы счисления])`
: преобразование к [целому числу](number.md).

`list([object])`
: создает [список](list.md).

`memoryview([object])`
: создает объект `memoryview`.

`object()`
: возвращает безликий объект, являющийся базовым для всех объектов.

`range([start=0], stop, [step=1])`
: арифметическая прогрессия от `start` до `stop` с шагом `step`.

`set([object])`
: создает [множество](set.md).

`slice([start=0], stop, [step=1])`
: объект среза от `start` до `stop` с шагом `step`.

`str([object], [кодировка], [ошибки])`
: строковое представление объекта. Использует метод `__str__`.

`tuple(obj)`
: преобразование к [кортежу](tuple.md).

## Другие встроенные функции

`abs(x)`
: Возвращает абсолютную величину (модуль числа).

`all(последовательность)`
: Возвращает `True`, если все элементы истинные (или, если последовательность пуста).

`any(последовательность)`
: Возвращает `True`, если хотя бы один элемент - истина. Для пустой последовательности возвращает `False`.

`ascii(object)`
: Как `repr()`, возвращает строку, содержащую представление объекта, но заменяет не-ASCII символы на экранированные последовательности.

`bin(x)`
: Преобразование целого числа в двоичную строку.

`callable(x)`
: Возвращает `True` для объекта, поддерживающего вызов (как функции).

`chr(x)`
: Возвращает односимвольную строку, код символа которой равен `x`.

`classmethod(x)`
: Представляет указанную функцию методом класса.

`compile(source, filename, mode, flags=0, dont_inherit=False)`
: Компиляция в программный код, который впоследствии может выполниться функцией `eval` или `exec`. Строка не должна содержать символов возврата каретки или нулевые байты.

`delattr(object, name)`
: Удаляет атрибут с именем `name`.

`dir([object])`
: Список имен объекта, а если объект не указан, список имен в текущей локальной области видимости.

`divmod(a, b)`
: Возвращает частное и остаток от деления `a` на `b`.

`enumerate(iterable, start=0)`
: Возвращает итератор, при каждом проходе предоставляющем кортеж из номера и соответствующего члена последовательности.

`eval(expression, globals=None, locals=None)`
: Выполняет строку программного кода.

`exec(object[, globals[, locals]])`
: Выполняет программный код на Python.

`filter(function, iterable)`
: Возвращает итератор из тех элементов, для которых `function` возвращает истину.

`format(value[,format_spec])`
: Форматирование (обычно форматирование строки).

`getattr(object, name ,[default])`
: извлекает атрибут объекта или `default`.

`globals()`
: Словарь глобальных имен.

`hasattr(object, name)`
: Имеет ли объект атрибут с именем `name`.

`hash(x)`
: Возвращает хеш указанного объекта.

`help([object])`
: Вызов встроенной справочной системы.

`hex(х)`
: Преобразование целого числа в шестнадцатеричную строку.

`id(object)`
: Возвращает "адрес" объекта. Это целое число, которое гарантированно будет уникальным и постоянным для данного объекта в течение срока его существования.

`input([prompt])`
: Возвращает введенную пользователем строку. `Prompt` - подсказка пользователю.

`isinstance(object, ClassInfo)`
: Истина, если объект является экземпляром `ClassInfo` или его подклассом. Если объект не является объектом данного типа, функция всегда возвращает ложь.

`issubclass(класс, ClassInfo)`
: Истина, если класс является подклассом `ClassInfo`. Класс считается подклассом себя.

`iter(x)`
: Возвращает объект итератора.

`len(x)`
: Возвращает число элементов в указанном объекте.

`locals()`
: Словарь локальных имен.

`map(function, iterator)`
: Итератор, получившийся после применения к каждому элементу последовательности функции `function`.

`max(iter, [args ...] * [, key])`
: Максимальный элемент последовательности.

`min(iter, [args ...] * [, key])`
: Минимальный элемент последовательности.

`next(x)`
: Возвращает следующий элемент итератора.

`oct(х)`
: Преобразование целого числа в восьмеричную строку.

`open(file, mode='r', buffering=None, encoding=None, errors=None, newline=None, closefd=True)`
: Открывает файл и возвращает соответствующий поток.

`ord(с)`
: Код символа.

`pow(x, y[, r])`
: Аналогично `( x ** y ) % r`.

`reversed(object)`
: Итератор из развернутого объекта.

`repr(obj)`
: Представление объекта.

`print([object, ...], *, sep=" ", end='\n', file=sys.stdout)`
: Печать.

`property(fget=None, fset=None, fdel=None, doc=None)`

`round(X [, N])`
: Округление до `N` знаков после запятой.

`setattr(объект, имя, значение)`
: Устанавливает атрибут объекта.

`sorted(iterable[, key][, reverse])`
: Отсортированный список.

`staticmethod(function)`
: Статический метод для функции.

`sum(iter, start=0)`
: Сумма членов последовательности.

`super([тип [, объект или тип]])`
: Доступ к родительскому классу.

`type(object)`
: Возвращает тип объекта.

`type(name, bases, dict)`
: Возвращает новый экземпляр класса `name`.

`vars([object])`
: Словарь из атрибутов объекта. По умолчанию - словарь локальных имен.

`zip(*iters)`
: Итератор, возвращающий кортежи, состоящие из соответствующих элементов аргументов-последовательностей.