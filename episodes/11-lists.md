---
title: Listas
teaching: 10
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Explica por qué los programas necesitan colecciones de valores.
- Escribe programas que creen listas planas, las indexen, las rebanen y las modifiquen
  mediante asignaciones y llamadas a métodos.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo puedo almacenar varios valores?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Una lista almacena muchos valores en una sola estructura.

- Hacer cálculos con cien variables llamadas `pressure_001`, `pressure_002`, etc., sería
  al menos tan lento como hacerlos a mano.
- Utiliza una *lista* para almacenar muchos valores juntos.
  - Entre corchetes `[...]`.
  - Valores separados por comas `,`.
- Utilice `len` para averiguar cuántos valores hay en una lista.

```python
pressures = [0.273, 0.275, 0.277, 0.275, 0.276]
print('pressures:', pressures)
print('length:', len(pressures))
```

```output
pressures: [0.273, 0.275, 0.277, 0.275, 0.276]
length: 5
```

## Utiliza el índice de un elemento para obtenerlo de una lista.

- Igual que las cadenas.

```python
print('zeroth item of pressures:', pressures[0])
print('fourth item of pressures:', pressures[4])
```

```output
zeroth item of pressures: 0.273
fourth item of pressures: 0.276
```

## Los valores de las listas se pueden reemplazar asignándoles.

- Utilice una expresión de índice a la izquierda de la asignación para reemplazar un
  valor.

```python
pressures[0] = 0.265
print('pressures is now:', pressures)
```

```output
pressures is now: [0.265, 0.275, 0.277, 0.275, 0.276]
```

## Añadir elementos a una lista la alarga.

- Utilice `list_name.append` para añadir elementos al final de una lista.

```python
primes = [2, 3, 5]
print('primes is initially:', primes)
primes.append(7)
print('primes has become:', primes)
```

```output
primes is initially: [2, 3, 5]
primes has become: [2, 3, 5, 7]
```

- `append` es un *método* de listas.
  - Como una función, pero ligada a un objeto concreto.
- Utilice `object_name.method_name` para llamar a métodos.
  - Se parece deliberadamente a la forma en que nos referimos a las cosas en una
    biblioteca.
- Conoceremos otros métodos de listas a medida que avancemos.
  - Utilice `help(list)` para una vista previa.
- `extend` es similar a `append`, pero permite combinar dos listas. Por ejemplo:

```python
teen_primes = [11, 13, 17, 19]
middle_aged_primes = [37, 41, 43, 47]
print('primes is currently:', primes)
primes.extend(teen_primes)
print('primes has now become:', primes)
primes.append(middle_aged_primes)
print('primes has finally become:', primes)
```

```output
primes is currently: [2, 3, 5, 7]
primes has now become: [2, 3, 5, 7, 11, 13, 17, 19]
primes has finally become: [2, 3, 5, 7, 11, 13, 17, 19, [37, 41, 43, 47]]
```

Tenga en cuenta que mientras `extend` mantiene la estructura "plana" de la lista, añadir
una lista a una lista significa que el último elemento en `primes` será una lista, no un
entero. Las listas pueden contener valores de cualquier tipo, por lo que son posibles
listas de listas.

## Utilice `del` para eliminar elementos de una lista por completo.

- Utilizamos `del list_name[index]` para eliminar un elemento de una lista (en el
  ejemplo, 9 no es un número primo) y así acortarla.
- `del` no es una función ni un método, sino una sentencia del lenguaje.

```python
primes = [2, 3, 5, 7, 9]
print('primes before removing last item:', primes)
del primes[4]
print('primes after removing last item:', primes)
```

```output
primes before removing last item: [2, 3, 5, 7, 9]
primes after removing last item: [2, 3, 5, 7]
```

## La lista vacía no contiene valores.

- Utilice `[]` solo para representar una lista que no contiene ningún valor.
  - "El cero de las listas"
- Útil como punto de partida para recoger valores (que veremos en el [próximo
  episodio](12-for-loops.md)).

## Las listas pueden contener valores de diferentes tipos.

- Una lista puede contener números, cadenas y cualquier otra cosa.

```python
goals = [1, 'Create lists.', 2, 'Extract items from lists.', 3, 'Modify lists.']
```

## Las cadenas de caracteres pueden indexarse como listas.

- Obtiene caracteres individuales de una cadena de caracteres utilizando índices entre
  corchetes.

```python
element = 'carbon'
print('zeroth character:', element[0])
print('third character:', element[3])
```

```output
zeroth character: c
third character: b
```

## Las cadenas de caracteres son inmutables.

- No se pueden cambiar los caracteres de una cadena una vez creada.
  - *Inmutable*: no se puede modificar después de la creación.
  - Por el contrario, las listas son *mutables*: pueden modificarse in situ.
- Python considera la cadena como un único valor con partes, no como una colección de
  valores.

```python
element[0] = 'C'
```

```error
TypeError: 'str' object does not support item assignment
```

- Tanto las listas como las cadenas de caracteres son *colecciones*.

## Indexar más allá del final de la colección es un error.

- Python reporta un `IndexError` si intentamos acceder a un valor que no existe.
  - Esto es un tipo de [error de ejecución](04-built-in.md).
  - No puede detectarse al analizar el código porque el índice podría calcularse a
    partir de los datos.

```python
print('99th element of element is:', element[99])
```

```output
IndexError: string index out of range
```

::::::::::::::::::::::::::::::::::::::: challenge

## Rellene los espacios en blanco

Rellena los espacios en blanco para que el programa de abajo produzca la salida
mostrada.

```python
values = ____
values.____(1)
values.____(3)
values.____(5)
print('first time:', values)
values = values[____]
print('second time:', values)
```

```output
first time: [1, 3, 5]
second time: [3, 5]
```

::::::::::::::: solution

## Solución

```python
values = []
values.append(1)
values.append(3)
values.append(5)
print('first time:', values)
values = values[1:]
print('second time:', values)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## ¿Qué tamaño tiene una rebanada?

Si `start` y `stop` son enteros no negativos, ¿cuánto mide la lista
`values[start:stop]`?

::::::::::::::: solution

## Solución

La lista `values[start:stop]` tiene hasta `stop - start` elementos. Por ejemplo,
`values[1:4]` tiene los 3 elementos `values[1]`, `values[2]`, y `values[3]`. ¿Por qué
"hasta"? Como vimos en el [episodio 2](02-variables.md), si `stop` es mayor que la
longitud total de la lista `values`, seguiremos obteniendo una lista, pero será más
corta de lo esperado.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## De cadenas a listas y viceversa

Dado esto:

```python
print('string to list:', list('tin'))
print('list to string:', ''.join(['g', 'o', 'l', 'd']))
```

```output
string to list: ['t', 'i', 'n']
list to string: gold
```

1. ¿Qué hace `list('some string')`?
2. ¿Qué genera `'-'.join(['x', 'y', 'z'])`?

::::::::::::::: solution

## Solución

1. [`list('some string')`](https://docs.python.org/3/library/stdtypes.html#list)
   convierte una cadena en una lista que contiene todos sus caracteres.
2. [`join`](https://docs.python.org/3/library/stdtypes.html#str.join) devuelve una
   cadena que es la *concatenación* de cada elemento de cadena de la lista y añade el
   separador entre cada elemento de la lista. El resultado es `x-y-z`. El separador
   entre los elementos es la cadena que proporciona este método.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Trabajar con el final

¿Qué imprime el siguiente programa?

```python
element = 'helium'
print(element[-1])
```

1. ¿Cómo interpreta Python un índice negativo?
2. Si una lista o cadena tiene N elementos, ¿cuál es el índice más negativo que se puede
   utilizar con seguridad con ella, y qué lugar representa ese índice?
3. Si `values` es una lista, ¿qué hace `del values[-1]`?
4. ¿Cómo puedes mostrar todos los elementos menos el último sin cambiar `values`?
   (Sugerencia: tendrás que combinar el troceado y la indexación negativa)

::::::::::::::: solution

## Solución

El programa imprime `m`.

1. Python interpreta un índice negativo como que empieza por el final (en lugar de
   empezar por el principio). El último elemento es `-1`.
2. El último índice que se puede utilizar con seguridad con una lista de N elementos es
   el elemento `-N`, que representa el primer elemento.
3. `del values[-1]` elimina el último elemento de la lista.
4. `values[:-1]`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Recorriendo una lista

¿Qué imprime el siguiente programa?

```python
element = 'fluorine'
print(element[::2])
print(element[::-1])
```

1. Si escribimos un slice como `low:high:stride`, ¿qué hace `stride`?
2. ¿Qué expresión seleccionaría todos los elementos pares de una colección?

::::::::::::::: solution

## Solución

El programa imprime

```python
furn
eniroulf
```

1. `stride` es el tamaño de paso de la rebanada.
2. El corte `1::2` selecciona todos los elementos pares de una colección: comienza con
   el elemento `1` (que es el segundo elemento, ya que la indexación comienza en `0`),
   sigue hasta el final (ya que no se da `end`), y utiliza un tamaño de paso de `2` (es
   decir, selecciona cada dos elementos).

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Límites de corte

¿Qué imprime el siguiente programa?

```python
element = 'lithium'
print(element[0:20])
print(element[-1:3])
```

::::::::::::::: solution

## Solución

```output
lithium

```

La primera sentencia imprime toda la cadena, ya que la rebanada va más allá de la
longitud total de la cadena. La segunda sentencia devuelve una cadena vacía, ya que el
trozo se sale de los límites de la cadena.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Ordenar y Clasificar

¿Qué imprimen estos dos programas? En términos sencillos, explique la diferencia entre
`sorted(letters)` y `letters.sort()`.

```python
# Program A
letters = list('gold')
result = sorted(letters)
print('letters is', letters, 'and result is', result)
```

```python
# Program B
letters = list('gold')
result = letters.sort()
print('letters is', letters, 'and result is', result)
```

::::::::::::::: solution

## Solución

El programa A imprime

```output
letters is ['g', 'o', 'l', 'd'] and result is ['d', 'g', 'l', 'o']
```

El programa B imprime

```output
letters is ['d', 'g', 'l', 'o'] and result is None
```

`sorted(letters)` devuelve una copia ordenada de la lista `letters` (la lista original
`letters` permanece inalterada), mientras que `letters.sort()` ordena la lista `letters`
en su lugar y no devuelve nada.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Copiar (o no)

¿Qué imprimen estos dos programas? En términos sencillos, explique la diferencia entre
`new = old` y `new = old[:]`.

```python
# Program A
old = list('gold')
new = old      # simple assignment
new[0] = 'D'
print('new is', new, 'and old is', old)
```

```python
# Program B
old = list('gold')
new = old[:]   # assigning a slice
new[0] = 'D'
print('new is', new, 'and old is', old)
```

::::::::::::::: solution

## Solución

El programa A imprime

```output
new is ['D', 'o', 'l', 'd'] and old is ['D', 'o', 'l', 'd']
```

El programa B imprime

```output
new is ['D', 'o', 'l', 'd'] and old is ['g', 'o', 'l', 'd']
```

`new = old` hace que `new` sea una referencia a la lista `old`; `new` y `old` apuntan al
mismo objeto.

`new = old[:]` sin embargo crea un nuevo objeto lista `new` que contiene todos los
elementos de la lista `old`; `new` y `old` son objetos diferentes.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Una lista almacena muchos valores en una única estructura.
- Utiliza el índice de un elemento para obtenerlo de una lista.
- Los valores de las listas pueden sustituirse asignándoles.
- Añadir elementos a una lista la alarga.
- Utilice `del` para eliminar elementos de una lista por completo.
- La lista vacía no contiene valores.
- Las listas pueden contener valores de distintos tipos.
- Las cadenas de caracteres pueden indexarse como listas.
- Las cadenas de caracteres son inmutables.
- Indexar más allá del final de la colección es un error.

::::::::::::::::::::::::::::::::::::::::::::::::::



