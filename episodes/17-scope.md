---
title: Ámbito de una variable
teaching: 10
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Identifica las variables locales y globales.
- Identifica parámetros como variables locales.
- Lee un traceback y determina el archivo, función y número de línea en el que ocurrió
  el error, el tipo de error y el mensaje de error.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo funcionan realmente las llamadas a funciones?
- ¿Cómo puedo determinar dónde se han producido los errores?

::::::::::::::::::::::::::::::::::::::::::::::::::

## El ámbito de una variable es la parte de un programa que puede 'ver' esa variable.

- Hay un número limitado de nombres sensatos para las variables.
- La gente que usa funciones no debería tener que preocuparse de qué nombres de
  variables usó el autor de la función.
- La gente que escribe funciones no debería preocuparse por los nombres de las variables
  que usa el invocador de la función.
- La parte de un programa en la que una variable es visible se llama su *ámbito*.

```python
pressure = 103.9

def adjust(t):
    temperature = t * 1.43 / pressure
    return temperature
```

- `pressure` es una *variable global*.
  - Definida fuera de cualquier función particular.
  - Visible en todas partes.
- `t` y `temperature` son *variables locales* en `adjust`.
  - Definida en la función.
  - No visible en el programa principal.
  - Recuerda: un parámetro de función es una variable a la que se le asigna
    automáticamente un valor cuando se llama a la función.

```python
print('adjusted:', adjust(0.9))
print('temperature after call:', temperature)
```

```output
adjusted: 0.01238691049085659
```

```error
Traceback (most recent call last):
  File "/Users/swcarpentry/foo.py", line 8, in <module>
    print('temperature after call:', temperature)
NameError: name 'temperature' is not defined
```

::::::::::::::::::::::::::::::::::::::: challenge

## Uso de variables locales y globales

Rastrea los valores de todas las variables de este programa mientras se ejecuta.
(Utiliza '---' como valor de las variables antes y después de que existan)

```python
limit = 100

def clip(value):
    return min(max(0.0, value), limit)

value = -22.5
print(clip(value))
```

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Lectura de mensajes de error

Lee el traceback de abajo, e identifica lo siguiente:

1. ¿Cuántos niveles tiene el traceback?
2. ¿Cuál es el nombre del fichero donde se ha producido el error?
3. ¿Cuál es el nombre de la función en la que se ha producido el error?
4. ¿En qué número de línea de esta función se produjo el error?
5. ¿Cuál es el tipo de error?
6. ¿Cuál es el mensaje de error?

```error
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-2-e4c4cbafeeb5> in <module>()
      1 import errors_02
----> 2 errors_02.print_friday_message()

/Users/ghopper/thesis/code/errors_02.py in print_friday_message()
     13
     14 def print_friday_message():
---> 15     print_message("Friday")

/Users/ghopper/thesis/code/errors_02.py in print_message(day)
      9         "sunday": "Aw, the weekend is almost over."
     10     }
---> 11     print(messages[day])
     12
     13

KeyError: 'Friday'
```

::::::::::::::: solution

## Solución

1. Tres niveles.
2. `errors_02.py`
3. `print_message`
4. Línea 11
5. `KeyError`. Estos errores se producen cuando intentamos buscar una clave que no
   existe (normalmente en una estructura de datos como un diccionario). Podemos
   encontrar más información sobre `KeyError` y otras excepciones incorporadas en los
   [Python docs](https://docs.python.org/3/library/exceptions.html#KeyError).
6. `KeyError: 'Friday'`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- El ámbito de una variable es la parte de un programa que puede 'ver' esa variable.

::::::::::::::::::::::::::::::::::::::::::::::::::



