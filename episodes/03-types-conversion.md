---
title: Tipos de datos y conversión de tipos
teaching: 10
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Explica las principales diferencias entre los números enteros y los de coma flotante.
- Explica las principales diferencias entre números y cadenas de caracteres.
- Utiliza funciones incorporadas para convertir entre enteros, números de coma flotante
  y cadenas.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Qué tipo de datos almacenan los programas?
- ¿Cómo puedo convertir un tipo en otro?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Cada valor tiene un tipo.

- Cada valor en un programa tiene un tipo específico.
- Número entero (`int`): representa números enteros positivos o negativos como 3 o -512.
- Número en coma flotante (`float`): representa números reales como 3.14159 o -2.5.
- Cadena de caracteres (normalmente llamada "string", `str`): texto.
  - Escrita entre comillas simples o dobles (siempre que coincidan).
  - Las comillas no se imprimen cuando se muestra la cadena.

## Utilice la función incorporada `type` para encontrar el tipo de un valor.

- Utilice la función incorporada `type` para averiguar qué tipo tiene un valor.
- También funciona con variables.
  - Pero recuerda: el *valor* tiene el tipo --- la *variable* es sólo una etiqueta.

```python
print(type(52))
```

```output
<class 'int'>
```

```python
fitness = 'average'
print(type(fitness))
```

```output
<class 'str'>
```

## Los tipos controlan qué operaciones (o métodos) pueden realizarse sobre un valor dado.

- El tipo de un valor determina lo que el programa puede hacer con él.

```python
print(5 - 3)
```

```output
2
```

```python
print('hello' - 'h')
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-2-67f5626a1e07> in <module>()
----> 1 print('hello' - 'h')

TypeError: unsupported operand type(s) for -: 'str' and 'str'
```

## Puede utilizar los operadores "+" y "\*" en cadenas.

- "Sumar" cadenas de caracteres las concatena.

```python
full_name = 'Ahmed' + ' ' + 'Walsh'
print(full_name)
```

```output
Ahmed Walsh
```

- Al multiplicar una cadena de caracteres por un número entero *N* se crea una nueva
  cadena que consiste en esa cadena de caracteres repetida *N* veces.
  - Dado que la multiplicación es una suma repetida.

```python
separator = '=' * 10
print(separator)
```

```output
==========
```

## Las cadenas tienen una longitud (pero los números no).

- La función incorporada `len` cuenta el número de caracteres de una cadena.

```python
print(len(full_name))
```

```output
11
```

- Pero los números no tienen longitud (ni siquiera cero).

```python
print(len(52))
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-3-f769e8e8097d> in <module>()
----> 1 print(len(52))

TypeError: object of type 'int' has no len()
```

## Debe convertir números en cadenas o viceversa cuando opera con ellos. {#convertir-números-y-cadenas}

- No puede sumar números y cadenas.

```python
print(1 + '2')
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-4-fe4f54a023c6> in <module>()
----> 1 print(1 + '2')

TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

- No está permitido porque es ambiguo: ¿debería `1 + '2'` ser `3` o `'12'`?
- Algunos tipos pueden convertirse en otros utilizando el nombre del tipo como función.

```python
print(1 + int('2'))
print(str(1) + '2')
```

```output
3
12
```

## Puede mezclar enteros y flotantes libremente en las operaciones.

- Los números enteros y los de coma flotante pueden mezclarse en aritmética.
  - Python 3 convierte automáticamente enteros a flotantes cuando es necesario.

```python
print('half is', 1 / 2.0)
print('three squared is', 3.0 ** 2)
```

```output
half is 0.5
three squared is 9.0
```

## Las variables sólo cambian de valor cuando se les asigna algo.

- Si hacemos que una celda de una hoja de cálculo dependa de otra, y actualizamos esta
  última, la primera se actualiza automáticamente.
- Esto **no** ocurre en los lenguajes de programación.

```python
variable_one = 1
variable_two = 5 * variable_one
variable_one = 2
print('first is', variable_one, 'and second is', variable_two)
```

```output
first is 2 and second is 5
```

- El ordenador lee el valor de `variable_one` al hacer la multiplicación, crea un nuevo
  valor y se lo asigna a `variable_two`.
- Después, el valor de `variable_two` se fija al nuevo valor y *no depende de
  `variable_one`* por lo que su valor no cambia automáticamente cuando cambia
  `variable_one`.

::::::::::::::::::::::::::::::::::::::: challenge

## Fracciones

¿Qué tipo de valor es 3.4? ¿Cómo puedes averiguarlo?

::::::::::::::: solution

## Solución

Es un número de coma flotante (a menudo abreviado "float"). Se puede averiguar
utilizando la función incorporada `type()`.

```python
print(type(3.4))
```

```output
<class 'float'>
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Conversión automática de tipos

¿Qué tipo de valor es 3,25 + 4?

::::::::::::::: solution

## Solución

Es un float: los enteros se convierten automáticamente en floats cuando es
necesario.

```python
result = 3.25 + 4
print(result, 'is', type(result))
```

```output
7.25 is <class 'float'>
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Elija un tipo

¿Qué tipo de valor (entero, número de coma flotante o cadena de caracteres) utilizarías
para representar cada uno de los siguientes elementos? Intenta dar más de una buena
respuesta para cada problema. Por ejemplo, en # 1, ¿cuándo tendría más sentido contar
los días con una variable de coma flotante que con un número entero?

1. Número de días transcurridos desde el inicio del año.
2. Tiempo transcurrido desde el inicio del año hasta ahora en días.
3. Número de serie de un equipo de laboratorio.
4. Edad de una muestra de laboratorio
5. Población actual de una ciudad.
6. Población media de una ciudad a lo largo del tiempo.

::::::::::::::: solution

## Solución

Las respuestas a las preguntas son:

1. Número entero, ya que el número de días estaría comprendido entre 1 y 365.
2. coma flotante, ya que se requieren días fraccionarios
3. Cadena de caracteres si el número de serie contiene letras y números, en caso
   contrario entero si el número de serie consta sólo de números
4. ¡Esto variará! ¿Cómo se define la edad de un espécimen? ¿días enteros desde la
   recogida (entero)? ¿fecha y hora (cadena)?
5. Elija coma flotante para representar la población como grandes agregados (por
   ejemplo, millones), o enteros para representar la población en unidades de
   individuos.
6. Número en coma flotante, ya que es probable que un promedio tenga una parte
   fraccionaria.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Tipos de división

En Python 3, el operador `//` realiza la división de enteros (números enteros), el
operador `/` realiza la división de coma flotante, y el operador `%` (o *modulo*)
calcula y devuelve el resto de la división de enteros:

```python
print('5 // 3:', 5 // 3)
print('5 / 3:', 5 / 3)
print('5 % 3:', 5 % 3)
```

```output
5 // 3: 1
5 / 3: 1.6666666666666667
5 % 3: 2
```

Si `num_subjects` es el número de sujetos que participan en un estudio, y
`num_per_survey` es el número que puede participar en una sola encuesta, escriba una
expresión que calcule el número de encuestas necesarias para llegar a todos una sola
vez.

::::::::::::::: solution

## Solución

Queremos el número mínimo de encuestas que llega a todos una vez, que es el valor
redondeado de `num_subjects/ num_per_survey`. Esto equivale a realizar una división por
el suelo con `//` y sumarle 1. Antes de la división hay que restar 1 al número de
sujetos para el caso en que `num_subjects` sea divisible por `num_per_survey`.

```python
num_subjects = 600
num_per_survey = 42
num_surveys = (num_subjects - 1) // num_per_survey + 1

print(num_subjects, 'subjects,', num_per_survey, 'per survey:', num_surveys)
```

```output
600 subjects, 42 per survey: 15
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Cadenas a Números

Cuando sea razonable, `float()` convertirá una cadena a un número de coma flotante, y
`int()` convertirá un número de coma flotante a un entero:

```python
print("string to float:", float("3.4"))
print("float to int:", int(3.4))
```

```output
string to float: 3.4
float to int: 3
```

Sin embargo, si la conversión no tiene sentido, aparecerá un mensaje de error.

```python
print("string to float:", float("Hello world!"))
```

```error
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-5-df3b790bf0a2> in <module>
----> 1 print("string to float:", float("Hello world!"))

ValueError: could not convert string to float: 'Hello world!'
```

Dada esta información, ¿qué esperas que haga el siguiente programa?

¿Qué hace realmente?

¿Por qué crees que hace eso?

```python
print("fractional string to int:", int("3.4"))
```

::::::::::::::: solution

## Solución

¿Qué esperas que haga este programa? No sería tan descabellado esperar que el comando
`int` de Python 3 convirtiera la cadena "3.4" a 3.4 y una conversión de tipo adicional a
3. Después de todo, Python 3 realiza muchas otras magias - ¿no es eso parte de su
encanto?

```python
int("3.4")
```

```output
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-2-ec6729dfccdc> in <module>
----> 1 int("3.4")
ValueError: invalid literal for int() with base 10: '3.4'
```

Sin embargo, Python 3 arroja un error. ¿Por qué? Para ser consistente, posiblemente. Si
le pides a Python que realice dos typecasts consecutivos, debes convertirlo
explícitamente en código.

```python
int(float("3.4"))
```

```output
3
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Aritmética con diferentes tipos

¿Cuál de las siguientes opciones devolverá el número de coma flotante `2.0`? Nota: puede
haber más de una respuesta correcta.

```python
first = 1.0
second = "1"
third = "1.1"
```

1. `first + float(second)`
2. `float(second) + float(third)`
3. `first + int(third)`
4. `first + int(float(third))`
5. `int(first) + int(float(third))`
6. `2.0 * second`

::::::::::::::: solution

## Solución

Respuesta: 1 y 4



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Números Complejos

Python proporciona números complejos, que se escriben como `1.0+2.0j`. Si `val` es un
número complejo, se puede acceder a sus partes real e imaginaria usando *notación de
puntos* como `val.real` y `val.imag`.

```python
a_complex_number = 6 + 2j
print(a_complex_number.real)
print(a_complex_number.imag)
```

```output
6.0
2.0
```

1. ¿Por qué crees que Python utiliza `j` en lugar de `i` para la parte imaginaria?
2. ¿Qué esperas que produzca `1 + 2j + 3`?
3. ¿Qué esperas que sea `4j`? ¿Y `4 j` o `4 + j`?

::::::::::::::: solution

## Solución

1. Los tratamientos matemáticos estándar suelen utilizar `i` para denotar un número
   imaginario. Sin embargo, según los informes de los medios de comunicación, se trata
   de una antigua convención establecida a partir de la ingeniería eléctrica que ahora
   presenta un área técnicamente costosa de cambiar. [Stack Overflow proporciona
   explicaciones y discusiones
   adicionales](https://stackoverflow.com/questions/24812444/why-are-complex-numbers-in-python-denoted-with-j-instead-of-i)
2. `(4+2j)`
3. `4j` y `Syntax Error: invalid syntax`. En estos últimos casos, `j` se considera una
   variable y la sentencia depende de si `j` está definida y, en caso afirmativo, de su
   valor asignado.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Cada valor tiene un tipo.
- Utilice la función incorporada `type` para encontrar el tipo de un valor.
- Los tipos controlan las operaciones que se pueden realizar con los valores.
- Las cadenas pueden sumarse y multiplicarse.
- Las cadenas tienen longitud (pero los números no).
- Debe convertir números en cadenas o viceversa cuando opera con ellos.
- Puede mezclar enteros y flotantes libremente en las operaciones.
- Las variables sólo cambian de valor cuando se les asigna algo.

::::::::::::::::::::::::::::::::::::::::::::::::::



