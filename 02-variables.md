---
title: Variables y asignación
teaching: 10
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Escribe programas que asignen valores escalares a variables y realicen cálculos con
  esos valores.
- Trazar correctamente cambios de valor en programas que usan asignación escalar.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo puedo almacenar datos en los programas?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Usa variables para almacenar valores.

- **Variables** son nombres para valores.

- Nombres de variables

  - **sólo** puede contener letras, dígitos y el guión bajo `_` (típicamente usado para
    separar palabras en nombres largos de variables)
  - no puede empezar por un dígito
  - son **sensibles a mayúsculas** (edad, Age y AGE son tres variables diferentes)

- El nombre también debe ser significativo para que usted u otro programador sepa lo que
  es

- Los nombres de variables que empiezan con guiones bajos como `__alistairs_real_age`
  tienen un significado especial, así que no lo haremos hasta que entendamos la
  convención.

- En Python el símbolo `=` asigna el valor de la derecha al nombre de la izquierda.

- La variable se crea cuando se le asigna un valor.

- Aquí, Python asigna una edad a la variable `age` y un nombre entre comillas a la
  variable `first_name`.

  ```python
  age = 42
  first_name = 'Ahmed'
  ```

## Usa `print` para mostrar valores.

- Python tiene una función integrada llamada `print` que imprime cosas como texto.
- Llama a la función (es decir, dile a Python que la ejecute) utilizando su nombre.
- Proporcione valores a la función (es decir, las cosas a imprimir) entre paréntesis.
- Para añadir una cadena a la impresión, encierre la cadena entre comillas simples o
  dobles.
- Los valores pasados a la función se llaman **argumentos**

```python
print(first_name, 'is', age, 'years old')
```

```output
Ahmed is 42 years old
```

- `print` pone automáticamente un espacio entre los elementos para separarlos.
- Y se envuelve en una nueva línea al final.

## Las variables deben ser creadas antes de ser usadas.

- Si una variable aún no existe, o si el nombre está mal escrito, Python informa de un
  error. (A diferencia de algunos lenguajes, que "adivinan" un valor por defecto)

```python
print(last_name)
```

```error
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-1-c1fbb4e96102> in <module>()
----> 1 print(last_name)

NameError: name 'last_name' is not defined
```

- La última línea de un mensaje de error suele ser la más informativa.
- Veremos los mensajes de error en detalle [más
  adelante](17-scope.md#reading-error-messages).

::::::::::::::::::::::::::::::::::::::::: callout

## Las variables persisten entre celdas

Ten en cuenta que lo importante en un cuaderno Jupyter es el *orden* de ejecución de las
celdas, no el orden en que aparecen. Python recordará *todo* el código que se ejecutó
previamente, incluyendo cualquier variable que hayas definido, independientemente del
orden en el cuaderno. Por lo tanto, si defines variables más abajo en el cuaderno y
luego (re)ejecutas celdas más arriba, las definidas más abajo seguirán presentes. Como
ejemplo, cree dos celdas con el siguiente contenido, en este orden:

```python
print(myval)
```

```python
myval = 1
```

Si ejecutas esto en orden, la primera celda dará un error. Sin embargo, si ejecutas la
primera celda *después* de la segunda se imprimirá `1`. Para evitar confusiones, puede
ser útil utilizar la opción `Kernel` -> `Restart & Run All` que limpia el intérprete y
ejecuta todo desde cero de arriba a abajo.


::::::::::::::::::::::::::::::::::::::::::::::::::

## Las variables pueden usarse en cálculos.

- Podemos usar variables en cálculos como si fueran valores.
  - Recuerda, asignamos el valor `42` a `age` hace unas líneas.

```python
age = age + 3
print('Age in three years:', age)
```

```output
Age in three years: 45
```

## Usa un índice para obtener un único carácter de una cadena.

- Los caracteres (letras, números, etc.) de una cadena están ordenados. Por ejemplo, la
  cadena `'AB'` no es lo mismo que `'BA'`. Debido a este orden, podemos tratar la cadena
  como una lista de caracteres.
- A cada posición en la cadena (primera, segunda, etc.) se le asigna un número. Este
  número se llama **índice** o a veces subíndice.
- Los índices se numeran desde 0.
- Usa el índice de la posición entre corchetes para obtener el carácter en esa posición.

[Una línea de código Python, print(nombre_del_átomo[0]), demuestra que el uso del índice
cero mostrará sólo la letra inicial, en este caso "h" de
helio](fig/2_indexing.svg){alt='Explica la indexación imprimiendo subconjuntos de la
cadena'}

```python
atom_name = 'helium'
print(atom_name[0])
```

```output
h
```

## Usa un slice para obtener una subcadena.

- Una parte de una cadena se llama **subcadena**. Una subcadena puede ser tan corta como
  un solo carácter.
- Un elemento de una lista se llama elemento. Cuando tratamos una cadena como si fuera
  una lista, los elementos de la cadena son sus caracteres individuales.
- Un slice es una parte de una cadena (o, más generalmente, una parte de cualquier cosa
  parecida a una lista).
- Tomamos una porción con la notación `[start:stop]`, donde `start` es el índice entero
  del primer elemento que queremos y `stop` es el índice entero del elemento *justo
  después* del último elemento que queremos.
- La diferencia entre `stop` y `start` es la longitud de la porción.
- Tomar un slice no cambia el contenido de la cadena original. En su lugar, al tomar una
  porción se devuelve una copia de parte de la cadena original.

```python
atom_name = 'sodium'
print(atom_name[0:3])
```

```output
sod
```

## Usa la función `len` para encontrar la longitud de una cadena.

```python
print(len('helium'))
```

```output
6
```

- Las funciones anidadas se evalúan de dentro a fuera, como en matemáticas.

## Python distingue entre mayúsculas y minúsculas.

- Python piensa que las mayúsculas y minúsculas son diferentes, por lo que `Name` y
  `name` son variables diferentes.
- Hay convenciones para usar mayúsculas al principio de los nombres de las variables,
  así que por ahora usaremos minúsculas.

## Usa nombres de variables con sentido.

- A Python no le importa cómo llames a las variables siempre que cumplan las reglas
  (caracteres alfanuméricos y guión bajo).

```python
flabadab = 42
ewr_422_yY = 'Ahmed'
print(ewr_422_yY, 'is', flabadab, 'years old')
```

- Utiliza nombres de variables significativos para ayudar a otras personas a entender lo
  que hace el programa.
- La "otra persona" más importante es tu futuro yo.

::::::::::::::::::::::::::::::::::::::: challenge

## Intercambiando Valores

Rellena la tabla con los valores de las variables de este programa *después* de ejecutar
cada sentencia.

```python
# Command  # Value of x   # Value of y   # Value of swap #
x = 1.0    #              #              #               #
y = 3.0    #              #              #               #
swap = x   #              #              #               #
x = y      #              #              #               #
y = swap   #              #              #               #
```

::::::::::::::: solution

## Solución

```output
# Command  # Value of x   # Value of y   # Value of swap #
x = 1.0    # 1.0          # not defined  # not defined   #
y = 3.0    # 1.0          # 3.0          # not defined   #
swap = x   # 1.0          # 3.0          # 1.0           #
x = y      # 3.0          # 3.0          # 1.0           #
y = swap   # 3.0          # 1.0          # 1.0           #
```

Estas tres líneas intercambian los valores en `x` y `y` usando la variable `swap` para
almacenamiento temporal. Este es un lenguaje de programación bastante común.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Predicción de valores

¿Cuál es el valor final de `position` en el programa? (Intenta predecir el valor sin
ejecutar el programa, luego comprueba tu predicción)

```python
initial = 'left'
position = initial
initial = 'right'
```

::::::::::::::: solution

## Solución

```python
print(position)
```

```output
left
```

A la variable `initial` se le asigna el valor `'left'`. En la segunda línea, la variable
`position` también recibe el valor `'left'`. En la tercera línea, la variable `initial`
recibe el valor `'right'`, pero la variable `position` conserva su valor de cadena
`'left'`.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Desafío

Si asignas `a = 123`, ¿qué pasa si intentas obtener el segundo dígito de `a` mediante
`a[1]`?

::::::::::::::: solution

## Solución

Los números no son cadenas o secuencias y Python dará un error si intentas realizar una
operación de índice en un número. En la [próxima lección sobre tipos y conversión de
tipos](03-tipos-conversion.md) aprenderemos más sobre tipos y cómo convertir entre
diferentes tipos. Si quieres el enésimo dígito de un número puedes convertirlo en una
cadena utilizando la función incorporada `str` y luego realizar una operación de índice
sobre esa cadena.

```python
a = 123
print(a[1])
```

```error
TypeError: 'int' object is not subscriptable
```

```python
a = str(123)
print(a[1])
```

```output
2
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Elegir un Nombre

¿Qué nombre de variable es mejor, `m`, `min` o `minutes`? Pista: piensa qué código
preferirías heredar de alguien que va a dejar el laboratorio:

1. `ts = m * 60 + s`
2. `tot_sec = min * 60 + sec`
3. `total_seconds = minutes * 60 + seconds`

::::::::::::::: solution

## Solución

`minutes` es mejor porque `min` puede significar algo como "mínimo" (y en realidad es
una función incorporada en Python que veremos más adelante).



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Práctica de rebanado

¿Qué imprime el siguiente programa?

```python
atom_name = 'carbon'
print('atom_name[1:3] is:', atom_name[1:3])
```

::::::::::::::: solution

## Solución

```output
atom_name[1:3] is: ar
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Conceptos de rebanado

Dada la siguiente cadena:

```python
species_name = "Acacia buxifolia"
```

¿Qué devolverían estas expresiones?

1. `species_name[2:8]`
2. `species_name[11:]` (sin valor después de los dos puntos)
3. `species_name[:4]` (sin valor antes de los dos puntos)
4. `species_name[:]` (sólo dos puntos)
5. `species_name[11:-3]`
6. `species_name[-5:-3]`
7. ¿Qué pasa cuando eliges un valor `stop` que está fuera de rango? (por ejemplo, prueba
   con `species_name[0:20]` o `species_name[:103]`)

::::::::::::::: solution

## Soluciones

1. `species_name[2:8]` devuelve la subcadena `'acia b'`
2. `species_name[11:]` devuelve la subcadena `'folia'`, desde la posición 11 hasta el
   final
3. `species_name[:4]` devuelve la subcadena `'Acac'`, desde el inicio hasta la posición
   4, pero sin incluirla
4. `species_name[:]` devuelve la cadena completa `'Acacia buxifolia'`
5. `species_name[11:-3]` devuelve la subcadena `'fo'`, desde la posición 11 hasta la
   antepenúltima posición
6. `species_name[-5:-3]` también devuelve la subcadena `'fo'`, desde la quinta última
   posición hasta la antepenúltima
7. Si una parte de la porción está fuera del rango, la operación no falla.
   `species_name[0:20]` da el mismo resultado que `species_name[0:]`, y
   `species_name[:103]` da el mismo resultado que `species_name[:]`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Utiliza variables para almacenar valores.
- Usa `print` para mostrar valores.
- Las variables persisten entre celdas.
- Las variables deben crearse antes de usarse.
- Las variables pueden usarse en cálculos.
- Utiliza un índice para obtener un único carácter de una cadena.
- Usa un slice para obtener una subcadena.
- Usa la función `len` para encontrar la longitud de una cadena.
- Python distingue entre mayúsculas y minúsculas.
- Usa nombres de variables con sentido.

::::::::::::::::::::::::::::::::::::::::::::::::::



