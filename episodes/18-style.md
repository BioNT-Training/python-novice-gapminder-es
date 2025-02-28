---
title: Estilo de programación
teaching: 15
exercises: 15
---


::::::::::::::::::::::::::::::::::::::: objectives

- Proporcione justificaciones sólidas para las reglas básicas de estilo de codificación.
- Refactorice programas de una página para hacerlos más legibles y justifique los
  cambios.
- Utiliza los estándares de codificación de la comunidad Python (PEP-8).

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo puedo hacer mis programas más legibles?
- ¿Cómo formatean su código la mayoría de los programadores?
- ¿Cómo pueden los programas comprobar su propio funcionamiento?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Estilo de codificación

Un estilo de codificación consistente ayuda a otros (incluyendo a nuestros futuros yoes)
a leer y entender el código más fácilmente. El código se lee mucho más a menudo de lo
que se escribe, y como dice el [Zen of
Python](https://www.python.org/dev/peps/pep-0020), "La legibilidad cuenta". Python
propuso un estilo estándar a través de una de sus primeras Propuestas de Mejora de
Python (PEP), [PEP8](https://www.python.org/dev/peps/pep-0008).

Algunos puntos que vale la pena destacar:

- documente su código y asegúrese de que las suposiciones, algoritmos internos, entradas
  esperadas, salidas esperadas, etc., están claros
- use nombres de variables claros y semánticamente significativos
- use espacios en blanco, *no* tabuladores, para sangrar las líneas (los tabuladores
  pueden causar problemas en diferentes editores de texto, sistemas operativos y
  sistemas de control de versiones)

## Siga el estilo estándar de Python en su código.

- [PEP8](https://www.python.org/dev/peps/pep-0008): una guía de estilo para Python que
  trata temas como el nombre de las variables, la sangría del código, la estructura de
  las sentencias `import`, etc. Adherirse a PEP8 hace que sea más fácil para otros
  desarrolladores de Python leer y entender tu código, y comprender cómo deben ser sus
  contribuciones.
- Para comprobar que tu código cumple con PEP8, puedes utilizar la [aplicación
  pycodestyle](https://pypi.org/project/pycodestyle/) y herramientas como el
  [formateador de código negro](https://github.com/psf/black) pueden formatear
  automáticamente tu código para que se ajuste a PEP8 y pycodestyle (también existe un
  formateador para cuadernos Jupyter
  [nb\_black](https://github.com/dnanhkhoa/nb_black)).
- Algunos grupos y organizaciones siguen diferentes guías de estilo además de PEP8. Por
  ejemplo, la [guía de estilo de Google sobre
  Python](https://google.github.io/styleguide/pyguide.html) hace recomendaciones
  ligeramente diferentes. Google escribió una aplicación que puede ayudarte a formatear
  tu código en su estilo o en PEP8 llamada [yapf](https://github.com/google/yapf/).
- Con respecto al estilo de codificación, la clave es la *consistencia*. Elige un estilo
  para tu proyecto, ya sea PEP8, el estilo de Google o cualquier otro, y haz todo lo
  posible para asegurarte de que tú y cualquier otra persona con la que colabores os
  atenéis a él. La coherencia dentro de un proyecto suele tener más impacto que el
  estilo concreto utilizado. Un estilo coherente hará que tu software sea más fácil de
  leer y entender para los demás y para tu futuro yo.

## Utilice aserciones para comprobar errores internos.

Las aserciones son un método sencillo pero potente para asegurarse de que el contexto en
el que se ejecuta el código es el esperado.

```python
def calc_bulk_density(mass, volume):
    '''Return dry bulk density = powder mass / powder volume.'''
    assert volume > 0
    return mass / volume
```

Si la aserción es `False`, el intérprete de Python lanza una excepción en tiempo de
ejecución `AssertionError`. El código fuente de la expresión que falló se mostrará como
parte del mensaje de error. Para ignorar las aserciones en su código ejecute el
intérprete con la opción '-O' (optimizar). Las aserciones deben contener sólo
comprobaciones simples y nunca cambiar el estado del programa. Por ejemplo, una aserción
nunca debe contener una asignación.

## Utiliza docstrings para proporcionar ayuda integrada.

Si lo primero en una función es una cadena de caracteres que no está asignada
directamente a una variable, Python la adjunta a la función, accesible a través de la
función de ayuda incorporada. Esta cadena que proporciona documentación también se
conoce como *docstring*.

```python
def average(values):
    "Return average of values, or None if no values are supplied."

    if len(values) == 0:
        return None
    return sum(values) / len(values)

help(average)
```

```output
Help on function average in module __main__:

average(values)
    Return average of values, or None if no values are supplied.
```

::::::::::::::::::::::::::::::::::::::::: callout

## Cadenas multilínea

Utilice a menudo *cadenas multilínea* para la documentación. Éstas empiezan y terminan
con tres caracteres de comillas (simples o dobles) y terminan con tres caracteres
coincidentes.

```python
"""This string spans
multiple lines.

Blank lines are allowed."""
```

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## ¿Qué se mostrará?

Resalta las líneas en el código de abajo que estarán disponibles como ayuda en línea.
¿Hay líneas que deberían estar disponibles, pero no lo estarán? ¿Alguna línea producirá
un error de sintaxis o un error de ejecución?

```python
"Find maximum edit distance between multiple sequences."
# This finds the maximum distance between all sequences.

def overall_max(sequences):
    '''Determine overall maximum edit distance.'''

    highest = 0
    for left in sequences:
        for right in sequences:
            '''Avoid checking sequence against itself.'''
            if left != right:
                this = edit_distance(left, right)
                highest = max(highest, this)

    # Report.
    return highest
```

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Documenta Esto

Utiliza comentarios para describir y ayudar a otros a entender secciones potencialmente
poco intuitivas o líneas individuales de código. Son especialmente útiles para quien
pueda necesitar entender y editar su código en el futuro, incluido usted mismo.

Use docstrings para documentar las entradas aceptables y las salidas esperadas de un
método o clase, su propósito, suposiciones y comportamiento previsto. Los docstrings se
muestran cuando un usuario invoca el método incorporado `help` en su método o clase.

Convierte el comentario de la siguiente función en un docstring y comprueba que `help`
lo muestra correctamente.

```python
def middle(a, b, c):
    # Return the middle value of three.
    # Assumes the values can actually be compared.
    values = [a, b, c]
    values.sort()
    return values[1]
```

::::::::::::::: solution

## Solución

```python
def middle(a, b, c):
    '''Return the middle value of three.
    Assumes the values can actually be compared.'''
    values = [a, b, c]
    values.sort()
    return values[1]
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Limpiar este código

1. Lee este breve programa e intenta predecir lo que hace.
2. Ejecútalo: ¿cómo de precisa fue tu predicción?
3. Refactoriza el programa para hacerlo más legible. Recuerda ejecutarlo después de cada
   cambio para asegurarte de que su comportamiento no ha cambiado.
4. Compara tu reescritura con la de tu vecino. ¿Qué has hecho igual? ¿Qué hiciste
   diferente y por qué?

```python
n = 10
s = 'et cetera'
print(s)
i = 0
while i < n:
    # print('at', j)
    new = ''
    for j in range(len(s)):
        left = j-1
        right = (j+1)%len(s)
        if s[left]==s[right]: new = new + '-'
        else: new = new + '*'
    s=''.join(new)
    print(s)
    i += 1
```

::::::::::::::: solution

## Solución

He aquí una solución.

```python
def string_machine(input_string, iterations):
    """
    Takes input_string and generates a new string with -'s and *'s
    corresponding to characters that have identical adjacent characters
    or not, respectively.  Iterates through this procedure with the resultant
    strings for the supplied number of iterations.
    """
    print(input_string)
    input_string_length = len(input_string)
    old = input_string
    for i in range(iterations):
        new = ''
        # iterate through characters in previous string
        for j in range(input_string_length):
            left = j-1
            right = (j+1) % input_string_length  # ensure right index wraps around
            if old[left] == old[right]:
                new = new + '-'
            else:
                new = new + '*'
        print(new)
        # store new string as old
        old = new     

string_machine('et cetera', 10)
```

```output
et cetera
*****-***
----*-*--
---*---*-
--*-*-*-*
**-------
***-----*
--**---**
*****-***
----*-*--
---*---*-
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Siga el estilo estándar de Python en su código.
- Utilice docstrings para proporcionar ayuda integrada.

::::::::::::::::::::::::::::::::::::::::::::::::::



