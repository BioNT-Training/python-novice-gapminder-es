---
title: Funciones incorporadas y ayuda
teaching: 15
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Explica el propósito de las funciones.
- Llama correctamente a las funciones incorporadas de Python.
- Anida correctamente las llamadas a funciones incorporadas.
- Utilice la ayuda para mostrar la documentación de las funciones incorporadas.
- Describir correctamente las situaciones en las que se producen SyntaxError y
  NameError.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo puedo utilizar las funciones incorporadas?
- ¿Cómo puedo averiguar lo que hacen?
- ¿Qué tipo de errores pueden ocurrir en los programas?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Usa comentarios para añadir documentación a los programas.

```python
# This sentence isn't executed by Python.
adjustment = 0.5   # Neither is this - anything after '#' is ignored.
```

## Una función puede tomar cero o más argumentos.

- Ya hemos visto algunas funciones --- ahora echemos un vistazo más de cerca.
- Un *argumento* es un valor que se pasa a una función.
- `len` toma exactamente uno.
- `int`, `str`, y `float` crean un nuevo valor a partir de uno existente.
- `print` toma cero o más.
- `print` sin argumentos imprime una línea en blanco.
  - Siempre se deben usar paréntesis, incluso si están vacíos, para que Python sepa que
    se está llamando a una función.

```python
print('before')
print()
print('after')
```

```output
before

after
```

## Cada función devuelve algo.

- Cada llamada a una función produce algún resultado.
- Si la función no tiene un resultado útil que devolver, normalmente devuelve el valor
  especial `None`.`None` es un objeto de Python que se sustituye cuando no hay ningún
  valor.

```python
result = print('example')
print('result of print is', result)
```

```output
example
result of print is None
```

## Las funciones incorporadas más utilizadas son `max`, `min`, y `round`.

- Utilice `max` para encontrar el mayor valor de uno o más valores.
- Usa `min` para encontrar el más pequeño.
- Ambos funcionan tanto con cadenas de caracteres como con números.
  - "Mayor" y "menor" utilizan (0-9, A-Z, a-z) para comparar letras.

```python
print(max(1, 2, 3))
print(min('a', 'A', '0'))
```

```output
3
0
```

## Puede que las funciones sólo funcionen para ciertos (combinaciones de) argumentos.

- `max` y `min` deben tener al menos un argumento.
  - "Mayor del conjunto vacío" es una pregunta sin sentido.
- Y se les debe dar cosas que puedan ser comparadas significativamente.

```python
print(max(1, 'a'))
```

```error
TypeError                                 Traceback (most recent call last)
<ipython-input-52-3f049acf3762> in <module>
----> 1 print(max(1, 'a'))

TypeError: '>' not supported between instances of 'str' and 'int'
```

## Las funciones pueden tener valores por defecto para algunos argumentos.

- `round` redondeará un número de coma flotante.
- Por defecto, redondea a cero decimales.

```python
round(3.712)
```

```output
4
```

- Podemos especificar el número de decimales que queremos.

```python
round(3.712, 1)
```

```output
3.7
```

## Las funciones adjuntas a objetos se llaman métodos

- Las funciones toman otra forma que será común en los episodios de pandas.
- Los métodos tienen paréntesis como las funciones, pero van después de la variable.
- Algunos métodos se utilizan para operaciones internas de Python, y están marcados con
  doble subrayado.

```python
my_string = 'Hello world!'  # creation of a string object 

print(len(my_string))       # the len function takes a string as an argument and returns the length of the string

print(my_string.swapcase()) # calling the swapcase method on the my_string object

print(my_string.__len__())  # calling the internal __len__ method on the my_string object, used by len(my_string)

```

```output
12
hELLO WORLD!
12
```

- Incluso puede verlos encadenados. Funcionan de izquierda a derecha.

```python
print(my_string.isupper())          # Not all the letters are uppercase
print(my_string.upper())            # This capitalizes all the letters

print(my_string.upper().isupper())  # Now all the letters are uppercase
```

```output
False
HELLO WORLD
True
```

## Use la función incorporada `help` para obtener ayuda de una función.

- Cada función incorporada tiene documentación en línea.

```python
help(round)
```

```output
Help on built-in function round in module builtins:

round(number, ndigits=None)
    Round a number to a given precision in decimal digits.

    The return value is an integer if ndigits is omitted or None.  Otherwise
    the return value has the same type as the number.  ndigits may be negative.
```

## El Jupyter Notebook tiene dos formas de obtener ayuda.

- Opción 1: Coloque el cursor cerca del lugar donde se invoca la función en una celda
  (es decir, el nombre de la función o sus parámetros),
  - Mantén pulsado <kbd>Shift</kbd> y pulsa <kbd>Tab</kbd>.
  - Haga esto varias veces para ampliar la información devuelta.
- Opción 2: Escribe el nombre de la función en una celda con un signo de interrogación
  detrás. A continuación, ejecute la celda.

## Python informa de un error de sintaxis cuando no puede entender el código fuente de un programa.

- Ni siquiera intentará ejecutar el programa si no puede ser analizado.

```python
# Forgot to close the quote marks around the string.
name = 'Feng
```

```error
  File "<ipython-input-56-f42768451d55>", line 2
    name = 'Feng
                ^
SyntaxError: EOL while scanning string literal
```

```python
# An extra '=' in the assignment.
age = = 52
```

```error
  File "<ipython-input-57-ccc3df3cf902>", line 2
    age = = 52
          ^
SyntaxError: invalid syntax
```

- Fíjate mejor en el mensaje de error:

```python
print("hello world"
```

```error
  File "<ipython-input-6-d1cc229bf815>", line 1
    print ("hello world"
                        ^
SyntaxError: unexpected EOF while parsing
```

- El mensaje indica un problema en la primera línea de la entrada ("línea 1").
  - En este caso la sección "ipython-input" del nombre del archivo nos indica que
    estamos trabajando con entrada en IPython, el intérprete de Python utilizado por el
    Jupyter Notebook.
- La parte `-6-` del nombre del archivo indica que el error se produjo en la celda 6 de
  nuestro Cuaderno.
- A continuación se muestra la línea de código problemática, indicando el problema con
  un puntero `^`.

## Python informa de un error de ejecución cuando algo va mal mientras se ejecuta un programa. {#error en tiempo de ejecución}

```python
age = 53
remaining = 100 - aege # mis-spelled 'age'
```

```error
NameError                                 Traceback (most recent call last)
<ipython-input-59-1214fb6c55fc> in <module>
      1 age = 53
----> 2 remaining = 100 - aege # mis-spelled 'age'

NameError: name 'aege' is not defined
```

- Corrige los errores de sintaxis leyendo el código fuente y los errores de ejecución
  rastreando la ejecución del programa.

::::::::::::::::::::::::::::::::::::::: challenge

## Qué ocurre cuando

1. Explica en términos sencillos el orden de las operaciones en el siguiente programa:
   cuándo se produce la suma, cuándo la resta, cuándo se llama a cada función, etc.
2. ¿Cuál es el valor final de `radiance`?

```python
radiance = 1.0
radiance = max(2.1, 2.0 + min(radiance, 1.1 * radiance - 0.5))
```

::::::::::::::: solution

## Solución

1. Orden de las operaciones:
  1. `1.1 * radiance = 1.1`
  2. `1.1 - 0.5 = 0.6`
  3. `min(radiance, 0.6) = 0.6`
  4. `2.0 + 0.6 = 2.6`
  5. `max(2.1, 2.6) = 2.6`
2. Al final, `radiance = 2.6`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Encuentra la Diferencia

1. Predice lo que imprimirá cada una de las sentencias `print` del siguiente programa.
2. ¿Se ejecuta `max(len(rich), poor)` o produce un mensaje de error? Si se ejecuta,
   ¿tiene algún sentido su resultado?

```python
easy_string = "abc"
print(max(easy_string))
rich = "gold"
poor = "tin"
print(max(rich, poor))
print(max(len(rich), len(poor)))
```

::::::::::::::: solution

## Solución

```python
print(max(easy_string))
```

```output
c
```

```python
print(max(rich, poor))
```

```output
tin
```

```python
print(max(len(rich), len(poor)))
```

```output
4
```

`max(len(rich), poor)` lanza un TypeError. Esto se convierte en `max(4, 'tin')` y como
discutimos anteriormente una cadena y un entero no pueden ser comparados
significativamente.

```error 
TypeError                                 Traceback (most recent call last)
<ipython-input-65-bc82ad05177a> in <module>
----> 1 max(len(rich), poor)

TypeError: '>' not supported between instances of 'str' and 'int'
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## ¿Por qué no?

¿Por qué `max` y `min` no devuelven `None` cuando se llaman sin argumentos?

::::::::::::::: solution

## Solución

`max` y `min` devuelven TypeErrors en este caso porque no se suministró el número
correcto de parámetros. Si sólo devolviera `None`, el error sería mucho más difícil de
rastrear, ya que probablemente se almacenaría en una variable y se utilizaría más
adelante en el programa, sólo para lanzar probablemente un error en tiempo de ejecución.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Último carácter de una cadena

Si Python empieza a contar desde cero, y `len` devuelve el número de caracteres de una
cadena, ¿qué expresión índice obtendrá el último carácter de la cadena `name`? (Nota:
veremos una forma más sencilla de hacer esto en un episodio posterior)

::::::::::::::: solution

## Solución

`name[len(name) - 1]`



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## ¡Explora la documentación de Python!

La [documentación oficial de Python](https://docs.python.org/3/) es posiblemente la
fuente de información más completa sobre el lenguaje. Está disponible en diferentes
idiomas y contiene muchos recursos útiles. La [página de funciones
incorporadas](https://docs.python.org/3/library/functions.html) contiene un catálogo de
todas estas funciones, incluyendo las que hemos cubierto en esta lección. Algunas de
ellas son más avanzadas e innecesarias por el momento, pero otras son muy sencillas y
útiles.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Utiliza comentarios para añadir documentación a los programas.
- Una función puede tomar cero o más argumentos.
- Las funciones incorporadas más utilizadas son `max`, `min` y `round`.
- Puede que las funciones sólo funcionen para ciertos (combinaciones de) argumentos.
- Las funciones pueden tener valores por defecto para algunos argumentos.
- Utilice la función incorporada `help` para obtener ayuda sobre una función.
- El Jupyter Notebook tiene dos formas de obtener ayuda.
- Toda función devuelve algo.
- Python informa de un error de sintaxis cuando no puede entender el código fuente de un
  programa.
- Python informa de un error de ejecución cuando algo va mal mientras se ejecuta un
  programa.
- Corrige los errores de sintaxis leyendo el código fuente, y los errores de ejecución
  rastreando la ejecución del programa.

::::::::::::::::::::::::::::::::::::::::::::::::::



