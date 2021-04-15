Стандартная библиотека
======================

Стандартная библиотека Python содержит огромное количество полезных модулей и
является частью стандартного комплекта поставки Python. Ознакомиться со 
стандартной библиотекой Python очень важно, так как множество задач можно 
решить очень быстро, если вы знакомы с возможностями этих библиотек.

Рассмотрим некоторые наиболее часто используемые модули этой библиотеки. 
Детальное описание всех модулей стандартной библиотеки Python можно найти в
`разделе "Library Reference" <http://docs.python.org/py3k/library/index.html>`_ 
документации, входящей в комплект поставки Python.

Давайте изучим несколько полезных модулей.

.. admonition :: Примечание

  Если темы в настоящей главе покажутся вам слишком сложными, вы можете её 
  пропустить. Однако я настоятельно рекомендую вернуться к этой главе, когда
  вы будете чувствовать себя более уверенно с Python.


Модуль sys
----------

Модуль ``sys`` содержит функциональность, характерную для системы. Так мы 
видели, что список ``sys.argv`` содержит аргументы командной строки.

Предположим, нам нужно узнать версию используемой команды Python с тем, чтобы,
к примеру, убедиться в том, что мы используем как минимум версию 3. Модуль 
``sys`` предоставляет такую возможность.

.. sourcecode:: python

  >>> import sys
  >>> sys.version_info
  (3, 0, 0, 'beta', 2)
  >>> sys.version_info[0] >= 3
  True

**Как это работает:**

  Модуль ``sys`` содержит кортеж ``version_info``, который хранит информацию о
  версии. Первый элемент этого кортежа обозначает старшую версию. Мы можем
  использовать его, например, для того, чтобы убедиться, что программа будет
  выполняться только в Python 3.0:

Сохраните как ``versioncheck.py``:

.. sourcecode:: python

  import sys, warnings
  if sys.version_info[0] < 3:
      warnings.warn("Для выполнения этой программы необходима как минимум \
                     версия Python 3.0",
            RuntimeWarning)
  else:
      print('Нормальное продолжение')


**Вывод:**

::

  $ python2.7 versioncheck.py
  versioncheck.py:6: Для выполнения этой программы необходима как минимум версия Python 3.0
    RuntimeWarning)

  $ python3 versioncheck.py
  Нормальное продолжение


**Как это работает:**

  Мы используем один из модулей стандартной библиотеки, который называется
  ``warnings`` и служит для отображения предупреждений пользователю. Если
  версия Python менее 3, мы показываем соответствующее предупреждение.


Модуль logging
--------------

Представьте ситуацию, когда необходимо сохранить некоторые отладочные или другие
важные сообщения где-нибудь, чтобы иметь возможность позже проверить, отработала
ли программа, как ожидалось. Как мы "сохраним где-нибудь" эти сообщения? Сделать
это можно при помощи модуля ``logging``.

Сохраните как ``use_logging.py``:

.. sourcecode:: python

  import os, platform, logging

  if platform.platform().startswith('Windows'):
      logging_file = os.path.join(os.getenv('HOMEDRIVE'), \
                                  os.getenv('HOMEPATH'), \
				  'test.log')
  else:
      logging_file = os.path.join(os.getenv('HOME'), 'test.log')

  print("Сохраняем лог в", logging_file)

  logging.basicConfig(
      level=logging.DEBUG,
      format='%(asctime)s : %(levelname)s : %(message)s',
      filename = logging_file,
      filemode = 'w',
  )

  logging.debug("Начало программы")
  logging.info("Какие-то действия")
  logging.warning("Программа умирает")


**Вывод:**

::

  $ python3 use_logging.py
  Сохраняем лог в C:\Users\swaroop\test.log

Если открыть файл ``test.log``, он будет выглядеть примерно так:

::

  2012-10-26 16:52:41,457 : DEBUG : Начало программы
  2012-10-26 16:52:41,474 : INFO : Какие-то действия
  2012-10-26 16:52:41,475 : WARNING : Программа умирает

**Как это работает:**

  Мы использовали три модуля из стандартной библиотеки: модуль ``os`` для 
  взаимодействия с операционной системой, модуль ``platform`` для получения 
  информации о платформе (т.е. операционной системе) и модуль ``logging`` для
  сохранения лога\ [1]_.

  Прежде всего, при помощи строки, возвращаемой функцией ``platform.platform()``
  мы проверяем, какая операционная система используется (для более подробной 
  информации см. ``import platform; help(platform)``). Если это Windows, то мы
  определяем диск, содержащий домашний каталог, путь к домашнему каталогу на нём
  и имя файла, в котором хотим сохранить информацию. Сложив все эти три части, 
  мы получаем полный путь к файлу. Для других платформ нам нужно знать только
  путь к домашнему каталогу пользователя, и мы получим полный путь к файлу.

  При помощи функции ``os.path.join()`` мы объединяем три части пути к файлу
  вместе. Мы используем эту функцию вместо простого объединения строк для того,
  чтобы гарантировать, что полный путь к файлу записан в формате, ожидаемом
  операционной системой.

  Далее мы конфигурируем модуль ``logging`` таким образом, чтобы он записывал
  все сообщения в определённом формате в указанный файл.

  Наконец, мы можем выводить сообщения, предназначенные для отладки, 
  информирования, предупреждения и даже критические сообщения. После выполнения
  программы можно просмотреть этот файл и узнать, что происходило в программе, 
  хотя пользователю, запустившему программу, ничего не было показано.

..
  Модули urllib и json
  --------------------
  
  How much fun would it be if we could write our own program that will get search 
  results from the web? Let us explore that now.
  
  This can be achieved using a few modules. First is the ``urllib`` module that 
  we can use to fetch any webpage from the internet. We will make use of Yahoo! 
  Search to get the search results and luckily they can give us the results in a 
  format called JSON which is easy for us to parse because of the built-in 
  ``json`` module in the standard library.
  
  ; TODO
  : This program doesn't work yet which [http://bugs.python.org/issue3763 seems to be a bug in Python 3.0 beta 2].
  
  ..sourcecode :: python
  
    #!/usr/bin/python
    # Filename: yahoo_search.py
    
    import sys
    if sys.version_info[0] != 3:
        sys.exit('This program needs Python 3.0')
    
    import json
    import urllib, urllib.parse, urllib.request, urllib.response
    
    # Get your own APP ID at http://developer.yahoo.com/wsregapp/
      YAHOO_APP_ID = 'jl22psvV34HELWhdfUJbfDQzlJ2B57KFS_qs4I8D0Wz5U5_yCI1Awv8.lBSfPhwr'
      SEARCH_BASE = 'http://search.yahooapis.com/WebSearchService/V1/webSearch'
    
    class YahooSearchError(Exception):
        pass
    
    # Taken from http://developer.yahoo.com/python/python-json.html
    def search(query, results=20, start=1, **kwargs):
        kwargs.update({
                      'appid': YAHOO_APP_ID,
                      'query': query,
                    'results': results,
                      'start': start,
                     'output': 'json'
                     })
        url = SEARCH_BASE + '?' + urllib.parse.urlencode(kwargs)
        result = json.load(urllib.request.urlopen(url))
        if 'Error' in result:
            raise YahooSearchError(result['Error'])
        return result['ResultSet']

      query = input('What do you want to search for? ')
    for result in search(query)['Result']:
        print("{0} : {1}".format(result['Title'], result['Url']))


    
    Output:
    
    ; TODO
    
    How It Works:
    
    We can get the search results from a particular website by giving the text we are searching for in a particular format. We have to specify many options which we combine using ``key1=value1&key2=value2`` format which is handled by the ``urllib.parse.urlencode()`` function.
    
    So for example, open [http://search.yahooapis.com/WebSearchService/V1/webSearch?query=byte+of+python&appid=jl22psvV34HELWhdfUJbfDQzlJ2B57KFS_qs4I8D0Wz5U5_yCI1Awv8.lBSfPhwr&results=20&start=1&output=json this link in your web browser] and you will see 20 results, starting from the first result, for the words "byte of python", and we are asking for the output in JSON format.
    
    We make a connection to this URL using the ``urllib.request.urlopen()`` function and pass that file handle to ``json.load()`` which will read the content and simultaneously convert it to a Python object. We then loop through these results and display it to the end-user.
    


Серия "Модуль недели"
---------------------

В стандартной библиотеке можно найти ещё много полезного. Например, 
`отладка <http://docs.python.org/py3k/library/pdb.html>`_, 
`обработка параметров командной строки 
<http://docs.python.org/py3k/library/argparse.html>`_, 
`регулярные выражения 
<http://docs.python.org/py3k/library/re.html>`_ и так далее.

Лучший способ дальнейшего изучения стандартной библиотеки -- читать 
замечательную серию Дуга Хелмана `"Модуль недели" 
<http://www.doughellmann.com/projects/PyMOTW/>`_ или официальную `документацию
Python <http://docs.python.org/py3k/>`_.



Резюме
------

Мы изучили лишь некоторые возможности некоторых модулей стандартной библиотеки 
Python. Я настоятельно рекомендую просмотреть `документацию по стандартной
библиотеке Python <http://docs.python.org/py3k/library/index.html>`_, чтобы
увидеть все доступные модули.

Далее мы обратимся к некоторым аспектам, которые сделают вашу экскурсию по 
Python более "завершённой".



Примечания
----------

.. [1] log -- *англ.* "журнал", "вести журнал" (*прим.перев.*)

