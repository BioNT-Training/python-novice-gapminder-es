---
title: Bucles For
teaching: 10
exercises: 15
---


::::::::::::::::::::::::::::::::::::::: objectives

- Explica para qué se usan normalmente los bucles for.
- Traza la ejecución de un bucle simple (no anidado) e indica correctamente los valores
  de las variables en cada iteración.
- Escriba bucles for que utilicen el patrón Acumulador para agregar valores.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo puedo hacer que un programa haga muchas cosas?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Un *bucle for* ejecuta órdenes una vez por cada valor de una colección.

- Hacer cálculos sobre los valores de una lista uno a uno es tan doloroso como trabajar
  con `pressure_001`, `pressure_002`, etc.
- Un *bucle for* le dice a Python que ejecute algunas sentencias una vez por cada valor
  de una lista, una cadena de caracteres o alguna otra colección.
- "para cada cosa en este grupo, haz estas operaciones"

```python
for number in [2, 3, 5]:
    print(number)
```

- Este bucle `for` es equivalente a:

```python
print(2)
print(3)
print(5)
```

- Y la salida del bucle `for` es:

```output
2
3
5
```

## Un bucle `for` se compone de una colección, una variable de bucle y un cuerpo.

```python
for number in [2, 3, 5]:
    print(number)
```

- La colección, `[2, 3, 5]`, es sobre la que se está ejecutando el bucle.
- El cuerpo, `print(number)`, especifica qué hacer para cada valor de la colección.
- La variable de bucle, `number`, es la que cambia en cada *iteración* del bucle.
  - Lo "actual".

## La primera línea del bucle `for` debe terminar con dos puntos, y el cuerpo debe tener sangría.

- Los dos puntos al final de la primera línea indican el inicio de un *bloque* de
  sentencias.
- Python usa sangría en lugar de `{}` o `begin`/`end` para mostrar *anidamiento*.
  - Cualquier sangría consistente es legal, pero casi todo el mundo utiliza cuatro
    espacios.

```python
for number in [2, 3, 5]:
print(number)
```

```error
IndentationError: expected an indented block
```

- La sangría siempre tiene sentido en Python.

```python
firstName = "Jon"
  lastName = "Smith"
```

```error
  File "<ipython-input-7-f65f2962bf9c>", line 2
    lastName = "Smith"
    ^
IndentationError: unexpected indent
```

- Este error puede solucionarse eliminando los espacios sobrantes al principio de la
  segunda línea.

## Las variables de bucle pueden llamarse como se quiera.

- Como todas las variables, las variables de bucle son:
  - Creado a petición.
  - Sin sentido: sus nombres pueden ser cualquier cosa.

```python
for kitten in [2, 3, 5]:
    print(kitten)
```

## El cuerpo de un bucle puede contener muchas sentencias.

- Pero ningún bucle debe tener más de unas pocas líneas.
- Difícil para los seres humanos mantener en mente grandes trozos de código.

```python
primes = [2, 3, 5]
for p in primes:
    squared = p ** 2
    cubed = p ** 3
    print(p, squared, cubed)
```

```output
2 4 8
3 9 27
5 25 125
```

## Use `range` para iterar sobre una secuencia de números.

- La función incorporada
  [`range`](https://docs.python.org/3/library/stdtypes.html#range) produce una secuencia
  de números.
  - *No* una lista: los números se producen bajo demanda para hacer más eficiente el
    bucle sobre rangos grandes.
- `range(N)` son los números 0..N-1
  - Exactamente los índices legales de una lista o cadena de caracteres de longitud N

```python
print('a range is not a list: range(0, 3)')
for number in range(0, 3):
    print(number)
```

```output
a range is not a list: range(0, 3)
0
1
2
```

## El patrón Acumulador convierte muchos valores en uno.

- Un patrón común en los programas es:
  1. Inicializa una variable *acumulador* a cero, la cadena vacía o la lista vacía.
  2. Actualiza la variable con valores de una colección.

```python
# Sum the first 10 integers.
total = 0
for number in range(10):
   total = total + (number + 1)
print(total)
```

```output
55
```

- Lee `total = total + (number + 1)` como:
  - Suma 1 al valor actual de la variable de bucle `number`.
  - Añádelo al valor actual de la variable acumuladora `total`.
  - Asigna esto a `total`, reemplazando el valor actual.
- Tenemos que añadir `number + 1` porque `range` produce 0..9, no 1..10.

::::::::::::::::::::::::::::::::::::::: challenge

## Clasificación de errores

¿Un error de sangría es un error de sintaxis o de ejecución?

::::::::::::::: solution

## Solución

Un IndentationError es un error de sintaxis. Los programas con errores de sintaxis no
pueden iniciarse. Un programa con un error de ejecución se iniciará pero se lanzará un
error bajo ciertas condiciones.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Seguimiento de la ejecución

Crea una tabla que muestre los números de las líneas que se ejecutan cuando se ejecuta
este programa, y los valores de las variables después de ejecutar cada línea.

```python
total = 0
for char in "tin":
    total = total + 1
```

::::::::::::::: solution

## Solución

| Line no | Variables            |
| ------- | -------------------- |
| 1       | total = 0            |
| 2       | total = 0 char = 't' |
| 3       | total = 1 char = 't' |
| 2       | total = 1 char = 'i' |
| 3       | total = 2 char = 'i' |
| 2       | total = 2 char = 'n' |
| 3       | total = 3 char = 'n' |

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Invertir una cadena

Rellena los espacios en blanco del siguiente programa para que imprima "nit" (la inversa
de la cadena de caracteres original "tin").

```python
original = "tin"
result = ____
for char in original:
    result = ____
print(result)
```

::::::::::::::: solution

## Solución

```python
original = "tin"
result = ""
for char in original:
    result = char + result
print(result)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Practica Acumulando

Rellene los espacios en blanco en cada uno de los programas siguientes para obtener el
resultado indicado.

```python
# Total length of the strings in the list: ["red", "green", "blue"] => 12
total = 0
for word in ["red", "green", "blue"]:
    ____ = ____ + len(word)
print(total)
```

::::::::::::::: solution

## Solución

```python
total = 0
for word in ["red", "green", "blue"]:
    total = total + len(word)
print(total)
```

:::::::::::::::::::::::::

```python
# List of word lengths: ["red", "green", "blue"] => [3, 5, 4]
lengths = ____
for word in ["red", "green", "blue"]:
    lengths.____(____)
print(lengths)
```

::::::::::::::: solution

## Solución

```python
lengths = []
for word in ["red", "green", "blue"]:
    lengths.append(len(word))
print(lengths)
```

:::::::::::::::::::::::::

```python
# Concatenate all words: ["red", "green", "blue"] => "redgreenblue"
words = ["red", "green", "blue"]
result = ____
for ____ in ____:
    ____
print(result)
```

::::::::::::::: solution

## Solución

```python
words = ["red", "green", "blue"]
result = ""
for word in words:
    result = result + word
print(result)
```

:::::::::::::::::::::::::

**Crea un acrónimo:** A partir de la lista `["red", "green", "blue"]`, crea el acrónimo
`"RGB"` usando un bucle for.

**Pista:** Puede que necesites usar un método de cadena para formatear correctamente el
acrónimo.

::::::::::::::: solution

## Solución

```python
acronym = ""
for word in ["red", "green", "blue"]:
    acronym = acronym + word[0].upper()
print(acronym)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Suma Acumulada

Reordena y aplica la sangría adecuada a las líneas de código siguientes para que
impriman una lista con la suma acumulada de datos. El resultado debe ser `[1, 3, 5,
10]`.

```python
cumulative.append(total)
for number in data:
cumulative = []
total = total + number
total = 0
print(cumulative)
data = [1,2,2,5]
```

::::::::::::::: solution

## Solución

```python
total = 0
data = [1,2,2,5]
cumulative = []
for number in data:
    total = total + number
    cumulative.append(total)
print(cumulative)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Identificación de errores de nombres de variables

1. Lee el siguiente código e intenta identificar cuáles son los errores *sin*
   ejecutarlo.
2. Ejecuta el código y lee el mensaje de error. ¿Qué tipo de `NameError` crees que es?
   ¿Es una cadena sin comillas, una variable mal escrita, o una variable que debería
   haber sido definida pero no lo fue?
3. Corrige el error.
4. Repita los pasos 2 y 3, hasta que haya corregido todos los errores.

```python
for number in range(10):
    # use a if the number is a multiple of 3, otherwise use b
    if (Number % 3) == 0:
        message = message + a
    else:
        message = message + "b"
print(message)
```

::::::::::::::: solution

## Solución

- Los nombres de variables en Python distinguen entre mayúsculas y minúsculas: `number`
  y `Number` se refieren a variables diferentes.
- La variable `message` debe inicializarse como una cadena vacía.
- Queremos añadir la cadena `"a"` a `message`, no la variable indefinida `a`.

```python
message = ""
for number in range(10):
    # use a if the number is a multiple of 3, otherwise use b
    if (number % 3) == 0:
        message = message + "a"
    else:
        message = message + "b"
print(message)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Identificación de errores de posición

1. Lee el siguiente código e intenta identificar cuáles son los errores *sin*
   ejecutarlo.
2. Ejecuta el código y lee el mensaje de error. ¿Qué tipo de error es?
3. Corrige el error.

```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
print('My favorite season is ', seasons[4])
```

::::::::::::::: solution

## Solución

Esta lista tiene 4 elementos y el índice para acceder al último elemento de la lista es
`3`.

```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
print('My favorite season is ', seasons[3])
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Un *bucle for* ejecuta órdenes una vez por cada valor de una colección.
- Un bucle `for` se compone de una colección, una variable de bucle y un cuerpo.
- La primera línea del bucle `for` debe terminar con dos puntos, y el cuerpo debe tener
  sangría.
- La sangría siempre tiene sentido en Python.
- Las variables de bucle pueden llamarse como se quiera (pero se recomienda
  encarecidamente dar un nombre significativo a la variable de bucle).
- El cuerpo de un bucle puede contener muchas sentencias.
- Utilice `range` para iterar sobre una secuencia de números.
- El patrón Acumulador convierte muchos valores en uno.

::::::::::::::::::::::::::::::::::::::::::::::::::



