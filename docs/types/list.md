# Списки

**Списки** в Python - упорядоченные изменяемые коллекции объектов произвольных типов (почти как массив, но типы могут отличаться).

## Создание списков

Чтобы использовать списки, их нужно создать. Создать список можно несколькими способами. Например, можно обработать любой итерируемый объект (например, строку) встроенной функцией `list`:

```python
>>> list('список')
['с', 'п', 'и', 'с', 'о', 'к']
```

Список можно создать и при помощи литерала:

```python
>>> s = []  # Пустой список
>>> l = ['s', 'p', ['isok'], 2]
>>> s
[]
>>> l
['s', 'p', ['isok'], 2]
```

Как видно из примера, список может содержать любое количество любых объектов (в том числе и вложенные списки), или не содержать ничего.

## Генераторы списков

И еще один способ создать список - это генераторы списков. Генератор списков - способ построить новый список, применяя выражение к каждому элементу последовательности. Генераторы списков очень похожи на цикл `for`.

```python
>>> c = [c * 3 for c in 'list']
>>> c
['lll', 'iii', 'sss', 'ttt']
```

Возможна и более сложная конструкция генератора списков:

```python
>>> c = [c * 3 for c in 'list' if c != 'i']
>>> c
['lll', 'sss', 'ttt']
>>> c = [c + d for c in 'list' if c != 'i' for d in 'spam' if d != 'a']
>>> c
['ls', 'lp', 'lm', 'ss', 'sp', 'sm', 'ts', 'tp', 'tm']
```

Но в сложных случаях лучше пользоваться обычным циклом `for` для генерации списков.

## Функции и методы списков

Для списков доступны основные встроенные функции, а также методы списков.

| Метод                            | Что делает                                                                                              |
| -------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `list.append(x)`                 | Добавляет элемент в конец списка                                                                        |
| `list.extend(L)`                 | Расширяет список `list`, добавляя в конец все элементы списка `L`                                       |
| `list.insert(i, x)`              | Вставляет на `i`-ый элемент значение `x`                                                                |
| `list.remove(x)`                 | Удаляет первый элемент в списке, имеющий значение `x`. `ValueError`, если такого элемента не существует |
| `list.pop([i])`                  | Удаляет `i`-ый элемент и возвращает его. Если индекс не указан, удаляется последний элемент             |
| `list.index(x, [start [, end]])` | Возвращает положение первого элемента со значением `x` (при этом поиск ведется от `start` до `end`)     |
| `list.count(x)`                  | Возвращает количество элементов со значением `x`                                                        |
| `list.sort([key=функция])`       | Сортирует список на основе функции                                                                      |
| `list.reverse()`                 | Разворачивает список                                                                                    |
| `list.copy()`                    | Поверхностная копия списка                                                                              |
| `list.clear()`                   | Очищает список                                                                                          |

Нужно отметить, что методы списков, в отличие от строковых методов, изменяют сам список, а потому результат выполнения не нужно записывать в эту переменную.

```python
>>> l = [1, 2, 3, 5, 7]
>>> l.sort()
>>> l
[1, 2, 3, 5, 7]
>>> l = l.sort()
>>> print(l)
None
```

И, напоследок, примеры работы со списками:

```python
>>> a = [66.25, 333, 333, 1, 1234.5]
>>> print(a.count(333), a.count(66.25), a.count('x'))
2 1 0
>>> a.insert(2, -1)
>>> a.append(333)
>>> a
[66.25, 333, -1, 333, 1, 1234.5, 333]
>>> a.index(333)
1
>>> a.remove(333)
>>> a
[66.25, -1, 333, 1, 1234.5, 333]
>>> a.reverse()
>>> a
[333, 1234.5, 1, 333, -1, 66.25]
>>> a.sort()
>>> a
[-1, 1, 66.25, 333, 333, 1234.5]
```

Изредка, для увеличения производительности, списки заменяют гораздо менее гибкими массивами (хотя в таких случаях обычно используют сторонние библиотеки, например `NumPy`).
