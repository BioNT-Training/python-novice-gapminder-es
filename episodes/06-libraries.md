---
title: Librerías
teaching: 10
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Explicar qué son las librerías de software y por qué los programadores las crean y
  utilizan.
- Escribir programas que importen y utilicen módulos de la librería estándar de
  Python.
- Buscar y leer documentación de la librería estándar de forma interactiva (en el
  intérprete) y en línea.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo puedo utilizar software que ha escrito otra gente?
- ¿Cómo puedo averiguar qué hace ese programa?

::::::::::::::::::::::::::::::::::::::::::::::::::

## La mayor parte de la potencia de un lenguaje de programación está en sus librerías.

- Una *librería* es una colección de ficheros (llamados *módulos*) que contienen
  funciones para ser usadas por otros programas.
  - También puede contener valores de datos (por ejemplo, constantes numéricas) y otras
    cosas.
  - Se supone que los contenidos de la librería están relacionados, pero no hay forma
    de hacer cumplir esto.
- La [librería estándar][stdlib] de Python es un extenso conjunto de módulos que
  vienen con el propio Python.
- Muchas librerías adicionales están disponibles en [PyPI][pypi] (the Python Package
  Index).
- Veremos más adelante cómo escribir nuevas librerías.

::::::::::::::::::::::::::::::::::::::::: callout

## librerías y módulos

Una librería es una colección de módulos, pero a menudo los términos se usan
indistintamente, especialmente porque muchas librerías sólo consisten en un único
módulo, así que no te preocupes si los mezclas.


::::::::::::::::::::::::::::::::::::::::::::::::::

## Un programa debe importar un módulo de librería antes de usarlo.

- Utilice `import` para cargar un módulo de librería en la memoria de un programa.
- Luego refiérase a cosas del módulo como `module_name.thing_name`.
  - Python usa `.` para significar "parte de".
- Usando `math`, uno de los módulos de la librería estándar:

```python
import math

print('pi is', math.pi)
print('cos(pi) is', math.cos(math.pi))
```

```output
pi is 3.141592653589793
cos(pi) is -1.0
```

- Tienes que referirte a cada elemento con el nombre del módulo.
  - `math.cos(pi)` no funciona: la referencia a `pi` no "hereda" de algún modo la
    referencia de la función a `math`.

## Utilice `help` para conocer el contenido de un módulo de librería.

- Funciona igual que la ayuda para una función.

```python
help(math)
```

```output
Help on module math:

NAME
    math

MODULE REFERENCE
    http://docs.python.org/3/library/math

    The following documentation is automatically generated from the Python
    source files.  It may be incomplete, incorrect or include features that
    are considered implementation detail and may vary between Python
    implementations.  When in doubt, consult the module reference at the
    location listed above.

DESCRIPTION
    This module is always available.  It provides access to the
    mathematical functions defined by the C standard.

FUNCTIONS
    acos(x, /)
        Return the arc cosine (measured in radians) of x.
⋮ ⋮ ⋮
```

## Importar elementos específicos de un módulo de librería para acortar programas.

- Utilice `from ... import ...` para cargar sólo elementos específicos de un módulo de
  librería.
- Luego refiérase a ellos directamente sin el nombre de la librería como prefijo.

```python
from math import cos, pi

print('cos(pi) is', cos(pi))
```

```output
cos(pi) is -1.0
```

## Crear un alias para un módulo de librería al importarlo para acortar programas.

- Utilice `import ... as ...` para dar un *alias* corto a una librería al importarla.
- A continuación, haga referencia a los elementos de la librería utilizando ese nombre
  abreviado.

```python
import math as m

print('cos(pi) is', m.cos(m.pi))
```

```output
cos(pi) is -1.0
```

- Comúnmente utilizado para librerías de uso frecuente o con nombres largos.
  - Por ejemplo, la librería de ploteo `matplotlib` a menudo tiene el alias `mpl`.
- Pero puede hacer que los programas sean más difíciles de entender, ya que los lectores
  deben aprender los alias de su programa.

::::::::::::::::::::::::::::::::::::::: challenge

## Explorando el Módulo de Matemáticas

1. ¿Qué función del módulo `math` puedes usar para calcular una raíz cuadrada *sin* usar
   `sqrt`?
2. Dado que la librería contiene esta función, ¿por qué existe `sqrt`?

::::::::::::::: solution

## Solución

1. Usando `help(math)` vemos que tenemos `pow(x,y)` además de `sqrt(x)`, así que
   podríamos usar `pow(x, 0.5)` para encontrar una raíz cuadrada.

2. La función `sqrt(x)` es posiblemente más legible que `pow(x, 0.5)` cuando se
   implementan ecuaciones. La legibilidad es una piedra angular de la buena
   programación, por lo que tiene sentido proporcionar una función especial para este
   caso común específico.

Además, el diseño de la librería `math` de Python tiene su origen en el estándar C,
que incluye tanto `sqrt(x)` como `pow(x,y)`, por lo que un poco de la historia de la
programación se muestra en los nombres de las funciones de Python.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Localizando el Módulo Correcto

Desea seleccionar un carácter aleatorio de una cadena:

```python
bases = 'ACTTGCTTGAC'
```

1. ¿Qué módulo de [librería estándar][stdlib] podría ayudarle?
2. ¿Qué función seleccionarías de ese módulo? ¿Existen alternativas?
3. Intenta escribir un programa que utilice la función.

::::::::::::::: solution

## Solución

El [módulo aleatorio][randommod] parece que podría ayudar.

La cadena tiene 11 caracteres, cada uno con un índice posicional de 0 a 10. Podría
utilizar las funciones
[`random.randrange`](https://docs.python.org/3/library/random.html#random.randrange) o
[`random.randint`](https://docs.python.org/3/library/random.html#random.randint) para
obtener un número entero aleatorio entre 0 y 10, y luego seleccionar el carácter `bases`
en ese índice:

```python
from random import randrange

random_index = randrange(len(bases))
print(bases[random_index])
```

o de forma más compacta:

```python
from random import randrange

print(bases[randrange(len(bases))])
```

¿Quizás haya encontrado la función
[`random.sample`](https://docs.python.org/3/library/random.html#random.sample)? Permite
escribir un poco menos, pero puede ser un poco más difícil de entender con sólo leerla:

```python
from random import sample

print(sample(bases, 1)[0])
```

Tenga en cuenta que esta función devuelve una lista de valores. Aprenderemos sobre
listas en el [episodio 11](11-lists.md).

La solución más simple y corta es la función
[`random.choice`](https://docs.python.org/3/library/random.html#random.choice) que hace
exactamente lo que queremos:

```python
from random import choice

print(choice(bases))
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Ejemplo de Programación de Rompecabezas (Problema de Parson)

Reorganice las siguientes sentencias para que se imprima una base de ADN aleatoria y su
índice en la cadena. Puede que no se necesiten todas las sentencias. Siéntete libre de
usar/añadir variables intermedias.

```python
bases="ACTTGCTTGAC"
import math
import random
___ = random.randrange(n_bases)
___ = len(bases)
print("random base ", bases[___], "base index", ___)
```

::::::::::::::: solution

## Solución

```python
import math 
import random
bases = "ACTTGCTTGAC" 
n_bases = len(bases)
idx = random.randrange(n_bases)
print("random base", bases[idx], "base index", idx)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## ¿Cuándo está disponible la ayuda?

Cuando un colega tuyo teclea `help(math)`, Python informa de un error:

```error
NameError: name 'math' is not defined
```

¿Qué se le ha olvidado hacer a tu colega?

::::::::::::::: solution

## Solución

Importación del módulo math (`import math`)



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Importar con alias

1. Rellena los espacios en blanco para que el programa de abajo imprima `90.0`.
2. Reescribe el programa para que use `import` *sin* `as`.
3. ¿Qué forma te parece más fácil de leer?

```python
import math as m
angle = ____.degrees(____.pi / 2)
print(____)
```

::::::::::::::: solution

## Solución

```python
import math as m
angle = m.degrees(m.pi / 2)
print(angle)
```

puede escribirse como

```python
import math
angle = math.degrees(math.pi / 2)
print(angle)
```

Como acabas de escribir el código y estás familiarizado con él, puede que encuentres la
primera versión más fácil de leer. Pero cuando se trata de leer un enorme trozo de
código escrito por otra persona, o cuando se vuelve al propio trozo enorme de código
después de varios meses, los nombres no abreviados suelen ser más fáciles, excepto
cuando hay convenciones claras de abreviación.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## ¡Hay Muchas Formas De Importar Librerías!

Empareja las siguientes sentencias de impresión con las llamadas a librería
apropiadas.

Comandos de impresión:

1. `print("sin(pi/2) =", sin(pi/2))`
2. `print("sin(pi/2) =", m.sin(m.pi/2))`
3. `print("sin(pi/2) =", math.sin(math.pi/2))`

Llamadas a librerías:

1. `from math import sin, pi`
2. `import math`
3. `import math as m`
4. `from math import *`

::::::::::::::: solution

## Solución

1. Llamadas a las librerías 1 y 4. Para referirse directamente a `sin` y `pi` sin el
   nombre de la librería como prefijo, es necesario utilizar la sentencia `from ...
   import ...`. Mientras que la llamada a librería 1 importa específicamente las dos
   funciones `sin` y `pi`, la llamada a librería 4 importa todas las funciones del
   módulo `math`.
2. Llamada a la librería 3. Aquí se hace referencia a `sin` y `pi` con un nombre de
   librería abreviado `m` en lugar de `math`. La llamada a librería 3 hace
   exactamente eso utilizando la sintaxis `import ... as ...` - crea un alias para
   `math` con el nombre abreviado `m`.
3. Llamada a la librería 2. Aquí se hace referencia a `sin` y `pi` con el nombre de
   librería normal `math`, por lo que basta con la llamada normal `import ...`.

**Nota:** aunque la llamada a librería 4 funciona, importar todos los nombres de un
módulo usando una importación comodín [no es recomendable][pep8-imports] ya que hace que
no quede claro qué nombres del módulo se usan en el código. En general, es mejor hacer
las importaciones tan específicas como sea posible y sólo importar lo que el código
utiliza. En la llamada a librería 1, la sentencia `import` nos dice explícitamente que
la función `sin` es importada del módulo `math`, pero la llamada a librería 4 no
transmite esta información.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Importar elementos específicos

1. Rellena los espacios en blanco para que el programa de abajo imprima `90.0`.
2. ¿Encuentra esta versión más fácil de leer que las anteriores?
3. ¿Por qué *los programadores no* usarían siempre esta forma de `import`?

```python
____ math import ____, ____
angle = degrees(pi / 2)
print(angle)
```

::::::::::::::: solution

## Solución

```python
from math import degrees, pi
angle = degrees(pi / 2)
print(angle)
```

Lo más probable es que encuentres esta versión más fácil de leer ya que es menos densa.
La principal razón para no utilizar esta forma de importación es evitar conflictos de
nombres. Por ejemplo, no importaría `degrees` de esta forma si también quisiera usar el
nombre `degrees` para una variable o función propia. O si también importaras una función
llamada `degrees` de otra librería.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Lectura de mensajes de error

1. Lee el siguiente código e intenta identificar cuáles son los errores sin ejecutarlo.
2. Ejecuta el código y lee el mensaje de error. ¿Qué tipo de error es?

```python
from math import log
log(0)
```

::::::::::::::: solution

## Solución

```output
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-1-d72e1d780bab> in <module>
      1 from math import log
----> 2 log(0)

ValueError: math domain error
```

1. El logaritmo de `x` sólo está definido para `x > 0`, por lo que 0 queda fuera del
   dominio de la función.
2. Aparece un error de tipo `ValueError`, indicando que la función recibió un valor de
   argumento inapropiado. El mensaje adicional "error de dominio matemático" aclara cuál
   es el problema.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

[stdlib]: https://docs.python.org/3/library/
[pypi]: https://pypi.python.org/pypi/
[randommod]: https://docs.python.org/3/library/random.html
[pep8-imports]: https://pep8.org/#imports


:::::::::::::::::::::::::::::::::::::::: keypoints

- La mayor parte de la potencia de un lenguaje de programación está en sus librerías.
- Un programa debe importar un módulo de librería para poder utilizarlo.
- Utilice `help` para conocer el contenido de un módulo de librería.
- Importa elementos específicos de una librería para acortar programas.
- Crea un alias para una librería al importarla para acortar programas.

::::::::::::::::::::::::::::::::::::::::::::::::::



