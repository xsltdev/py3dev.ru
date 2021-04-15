Дополнительно
=============

К настоящему моменту мы уже рассмотрели большую часть того, что вам придётся
использовать при работе с Python. В этой главе мы охватим некоторые 
дополнительные аспекты, которые помогут отшлифовать ваши знания.


Передача кортежей
-----------------

Хотелось ли вам когда-нибудь, чтобы функция возвращала не один результат, а два?
Это возможно. Всё, что для этого нужно, -- использовать кортеж.

.. sourcecode:: python

  >>> def get_error_details():
  ...     return (2, 'описание ошибки No2')
  ...
  >>> errnum, errstr = get_error_details()
  >>> errnum
  2
  >>> errstr
  'описание ошибки No2'


Обратите внимание, что использование выражения "``a, b = <некоторое 
выражение>``" интерпретирует результат как кортеж из двух значений.

Чтобы интерпретировать результат как "``(a, <всё остальное>)``", нужно просто 
поставить звёздочку, как это делалось для параметров функций:

.. sourcecode:: python

  >>> a, *b = [1, 2, 3, 4]
  >>> a
  1
  >>> b
  [2, 3, 4]

Это также подразумевает, что поменять местами два значения в Python быстрее 
всего можно так:

.. sourcecode:: python

  >>> a = 5; b = 8
  >>> a, b = b, a
  >>> a, b
  (8, 5)


Специальные методы
------------------

Есть ряд методов, играющих особую роль для классов. Например, ``__init__`` и 
``__del__``.

Специальные методы служат для того, чтобы имитировать поведение встроенных типов
данных. Например, всё, что потребуется для использования операции индексирования
``x[индекс]`` применительно к своему классу (в таком виде, как это делалось для 
списков и кортежей), это реализовать метод ``__getitem__()``. Кстати, именно 
этот метод Python использует для самого класса ``list``!

Некоторые полезные специальные методы перечислены в таблице ниже. Все другие
методы можно посмотреть в `документации <http://docs.python.org/py3k/reference/datamodel.html#specialnames>`_.

+------------------------+-----------------------------------------------------+
|          Имя           |                       Описание                      |
+------------------------+-----------------------------------------------------+
| __init__(self, ...)    | Этот метод вызывается прямо перед тем, как вновь    |
|                        | созданный объект возвращается для использования.    |
+------------------------+-----------------------------------------------------+
| __del__(self)          | Вызывается перед уничтожением объекта               |
+------------------------+-----------------------------------------------------+
| __str__(self)          | Вызывается при использовании функции ``print`` или  |
|                        | ``str()``.                                          |
+------------------------+-----------------------------------------------------+
| __lt__(self, other)    | Вызывается, когда используется оператор "меньше"    |
|                        | (<). Существуют и аналогичные методы для всех       |
|                        | операторов (+, >, и т.д.)                           |
+------------------------+-----------------------------------------------------+
| __getitem__(self, key) | Вызывается при использовании оператора              |
|                        | индексирования ``x[индекс]``                        |
+------------------------+-----------------------------------------------------+
| __len__(self)          | Вызывается при обращении к встроенной функции       |
|                        | ``len()`` для объекта-последовательности.           |
+------------------------+-----------------------------------------------------+


Блоки в одно выражение
----------------------

Мы неоднократно говорили, что каждый блок команд отделяется от других своим
собственным уровнем отступа. Однако, существует и исключение. Если блок команд 
содержит только одно выражение, его можно указывать в одной строке с условным 
оператором или, скажем, оператором цикла. Рассмотрим это на примере:


.. sourcecode:: python

  >>> flag = True
  >>> if flag: print('Да')
  Да

Обратите внимание, что единственный оператор расположен в той же строке, а не
отдельным блоком. Этот способ может подкупить тем, что якобы "сокращает" 
программу, но я настоятельно рекомендую избегать его во всех случаях, кроме 
проверки ошибок. Прежде всего, потому что гораздо легче добавлять команды, 
когда уже есть необходимый уровень отступа.


Lambda-формы
------------

Ключевое слово ``lambda`` используется для создания функций и возврата их 
значения во время выполнения программы. ``lambda`` принимает параметр, за 
которым следует одно выражение, которое становится телом функции, а значение 
этого выражения возвращается новой функцией.

**Пример:** (сохраните как ``lambda.py``)

.. sourcecode:: python

  points = [ { 'x' : 2, 'y' : 3 }, { 'x' : 4, 'y' : 1 } ]
  points.sort(key=lambda i : i['y'])
  print(points)

**Вывод:**

::

    $ python3 lambda.py
    [{'x': 4, 'y': 1}, {'x': 2, 'y': 3}]


**Как это работает:**

  Обратите внимание на то, что метод ``sort`` класса ``list`` может принимать
  параметр ``key``, определяющий способ сортировки списка (обычно мы думаем
  только о сортировке по возрастанию или по убыванию). В данном случае мы хотим
  провести сортировку по собственному принципу, для чего нам необходимо написать
  соответствующую функцию. Но вместо того, чтобы создавать отдельный блок 
  ``def`` для описания функции, которая будет использоваться только в этом 
  месте, мы применяем лямбда-выражение.



Генераторы списков
------------------

.. List Comprehension

Генераторы списков служат для создания новых списков на основе существующих. 
Представьте, что имеется список чисел, на основе которого требуется получить 
новый список, состоящий из всех чисел, умноженных на 2, но только при условии,
что само число больше 2. Генераторы списков подходят для таких задач как нельзя 
лучше.

**Пример:** (сохраните как ``list_comprehension.py``)

.. sourcecode:: python

  listone = [2, 3, 4]
  listtwo = [2*i for i in listone if i > 2]
  print(listtwo)

**Вывод:**

::

  $ python3 list_comprehension.py
  [6, 8]

**Как это работает:**

  В этом примере мы создаём новый список, указав операцию, которую необходимо
  произвести (``2 * i``), когда выполняется некоторое условие (``if i > 2``).
  Обратите внимание, что исходный список при этом не изменяется.

Преимущество использования генераторов списков состоит в том, что это заметно
сокращает объёмы стандартного кода, необходимого для циклической обработки 
каждого элемента списка и сохранения его в новом списке.


Передача кортежей и словарей в функции
--------------------------------------

Для получения параметров, переданных функции, в виде кортежа или словаря, 
существуют специальные приставки "``*``" или "``**``" соответственно. Это 
особенно полезно в случаях, когда функция может принимать переменное число 
параметров.

.. sourcecode:: python

  >>> def powersum(power, *args):
  ...     '''Возвращает сумму аргументов, возведённых в указанную степень.'''
  ...     total = 0
  ...     for i in args:
  ...         total += pow(i, power)
  ...     return total
  ...
  >>> powersum(2, 3, 4)
  25

  >>> powersum(2, 10)
  100

Поскольку перед переменной ``args`` указана приставка "``*``", все 
дополнительные аргументы, переданные функции, сохранятся в ``args`` в виде 
кортежа. В случае использования приставки "``**``" все дополнительные параметры 
будут рассматриваться как пары ключ/значение в словаре.



exec и eval
-----------

Функция ``exec`` служит для выполнения команд Python, содержащихся в строке или
файле, в отличие от самого текста программы. Например, во время выполнения 
программы можно сформировать строку, содержащую текст программы на Python, и 
запустить его при помощи ``exec``:

.. sourcecode:: python

  >>> exec('print("Здравствуй, Мир!")')
  Здравствуй, Мир!

Аналогично, функция ``eval`` позволяет вычислять корректные выражения Python, 
содержащиеся в строке. Вот простой пример.

.. sourcecode:: python

  >>> eval('2*3')
  6



Оператор assert
---------------

Оператор ``assert`` существует для того, чтобы указать, что нечто является 
истиной. Например, если требуется гарантировать, что в списке будет хотя бы 
один элемент, и вызвать ошибку, если это не так, то оператор ``assert`` 
идеально подойдёт для такой задачи. Когда заявленное выражение ложно, 
вызывается ошибка ``AssertionError``. Метод ``pop()`` возвращает последний
элемент списка, одновременно удаляя его оттуда.

.. sourcecode:: python

  >>> mylist = ['item']
  >>> assert len(mylist) >= 1
  >>> mylist.pop()
  'item'
  >>> mylist
  []
  >>> assert len(mylist) >= 1
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  AssertionError



Тем не менее, оператор ``assert`` следует использовать благоразумно. В 
большинстве случаев гораздо лучше "отлавливать" исключения и либо решать 
соответствующую проблему автоматически, либо выдавать пользователю сообщение об 
ошибке и завершать работу программы.



Функция repr
------------

Функция ``repr`` используется для получения канонического строкового
представления объекта. Любопытно, что в большинстве случаев 
``eval(repr(object)) == object``.

.. sourcecode:: python

  >>> i = []
  >>> i.append('item')
  >>> repr(i)
  "['item']"
  >>> eval(repr(i))
  ['item']
  >>> eval(repr(i)) == i
  True


По большому счёту, функция ``repr`` служит для получения печатаемого 
представления объекта. Определив метод ``__repr__`` в собственном классе, можно
указать, что он будет возвращать по вызову функции ``repr``.


Управляющие последовательности
------------------------------

Попробуйте ответить на вопрос: Как указать строку, содержащую одинарную кавычку 
(``'``)? Например, строку "``What's your name?``". Её ведь нельзя записать 
просто как "``'What's your name?'``", потому что тогда Python не сможет 
определить, где начало строки, и где конец. В таком случае придётся каким-то 
образом указать, что данная одинарная кавычка не обозначает конца строки. Это 
можно сделать при помощи так называемой *управляющей последовательности*. 
Укажите одинарную кавычку как ``\'`` -- через обратную косую черту. Теперь наша 
строка будет выглядеть так: ``'What\'s your name?'``.

Другой способ записи такой специфической строки -- ``"What's your name?"``, т.е.
с использованием двойных кавычек. Аналогично следует использовать управляющую 
последовательность для вставки двойной кавычки в строку, ограниченную двойными 
кавычками. Сама же обратная наклонная черта указывается управляющей 
последовательностью ``\\``.

А как записать двустрочную строку? Один из вариантов нам уже знаком -- заключить
строку в тройные кавычки, как было показано :ref:`ранее <triple-quotes>`. Но
есть и другой -- использовать управляющую последовательность для символа 
перевода строки ``\n``. Например: "``Это первая строка\nЭто вторая строка``". 
Полезно знать ещё одну управляющую последовательность -- табуляцию (``\t``). 
Управляющих последовательностей существует намного больше, но здесь упомянуты 
только наиболее важные.

Следует отметить, что одинарная наклонная черта в конце строки лишь указывает 
на то, что продолжение идёт строкой ниже, но не вставляет перевода строки. 
Например:

.. sourcecode:: python

    "Это первое предложение. \
    Это второе предложение."

эквивалентно записи ``"Это первое предложение. Это второе предложение."``.


Необрабатываемые строки
-----------------------

Для записи строки, в которой не будет проводиться никакой специальной обработки,
как, например, управляющих последовательностей, перед строкой указывается 
приставка "``r``" или "``R``"\ [1]_. Например, 
``r"Перевод строки обозначается \n"``.

.. admonition:: Замечание для пользователей регулярных выражений

    Для работы с регулярными выражениями всегда используйте необрабатываемые 
    строки. В противном случае вас ждёт много возни с обратными косыми 
    чёрточками. Например, обратные ссылки можно обозначать как ``'\\1'`` или 
    ``r'\1'``.

Резюме
------

Итак, в настоящей главе мы рассмотрели некоторые дополнительные возможности 
Python, хотя по-прежнему, не охватили всего. Тем не менее, к настоящему 
моменту мы уже прошли почти всё, что вам когда-либо понадобится использовать на
практике. Этого вполне достаточно для начала работы над любыми программами.

Далее мы обсудим, как продолжать исследовать Python.


Примечания
----------
.. [1] "r" -- *от англ.* "raw" -- "сырой, необработанный" (*прим. перев.*)
