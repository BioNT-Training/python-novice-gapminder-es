---
title: Condicionales
teaching: 10
exercises: 15
---


::::::::::::::::::::::::::::::::::::::: objectives

- Escribir correctamente programas que utilicen sentencias if y else y expresiones
  booleanas sencillas (sin operadores lógicos).
- Rastrea la ejecución de condicionales no anidadas y condicionales dentro de bucles.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo pueden los programas hacer cosas diferentes para datos diferentes?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Usar sentencias `if` para controlar si un bloque de código se ejecuta o no.

- Una sentencia `if` (más propiamente llamada sentencia *condicional*) controla si un
  bloque de código se ejecuta o no.
- La estructura es similar a una sentencia `for`:
  - La primera línea se abre con `if` y termina con dos puntos
  - El cuerpo que contiene una o más sentencias tiene sangría (normalmente de 4
    espacios)

```python
mass = 3.54
if mass > 3.0:
    print(mass, 'is large')

mass = 2.07
if mass > 3.0:
    print (mass, 'is large')
```

```output
3.54 is large
```

## Los condicionales se usan a menudo dentro de bucles.

- No tiene mucho sentido usar una condicional cuando conocemos el valor (como arriba).
- Pero útil cuando tenemos una colección que procesar.

```python
masses = [3.54, 2.07, 9.22, 1.86, 1.71]
for m in masses:
    if m > 3.0:
        print(m, 'is large')
```

```output
3.54 is large
9.22 is large
```

## Use `else` para ejecutar un bloque de código cuando una condición `if` es *no* verdadera.

- `else` puede utilizarse después de `if`.
- Nos permite especificar una alternativa a ejecutar cuando la rama `if` no está tomada.

```python
masses = [3.54, 2.07, 9.22, 1.86, 1.71]
for m in masses:
    if m > 3.0:
        print(m, 'is large')
    else:
        print(m, 'is small')
```

```output
3.54 is large
2.07 is small
9.22 is large
1.86 is small
1.71 is small
```

## Utilice `elif` para especificar pruebas adicionales.

- Puede proporcionar varias opciones alternativas, cada una con su propia prueba.
- Utilice `elif` (abreviatura de "else if") y una condición para especificarlas.
- Siempre asociado a un `if`.
- Debe ir antes de `else` (que es el "catch all").

```python
masses = [3.54, 2.07, 9.22, 1.86, 1.71]
for m in masses:
    if m > 9.0:
        print(m, 'is HUGE')
    elif m > 3.0:
        print(m, 'is large')
    else:
        print(m, 'is small')
```

```output
3.54 is large
2.07 is small
9.22 is HUGE
1.86 is small
1.71 is small
```

## Las condiciones se prueban una vez, en orden.

- Python recorre las ramas de la condicional en orden, probando cada una a su vez.
- El orden es importante.

```python
grade = 85
if grade >= 90:
    print('grade is A')
elif grade >= 80:
    print('grade is B')
elif grade >= 70:
    print('grade is C')
```

```output
grade is B
```

- *No* vuelve atrás automáticamente y reevalúa si los valores cambian.

```python
velocity = 10.0
if velocity > 20.0:
    print('moving too fast')
else:
    print('adjusting velocity')
    velocity = 50.0
```

```output
adjusting velocity
```

- Utiliza a menudo condicionales en un bucle para "evolucionar" los valores de las
  variables.

```python
velocity = 10.0
for i in range(5): # execute the loop 5 times
    print(i, ':', velocity)
    if velocity > 20.0:
        print('moving too fast')
        velocity = velocity - 5.0
    else:
        print('moving too slow')
        velocity = velocity + 10.0
print('final velocity:', velocity)
```

```output
0 : 10.0
moving too slow
1 : 20.0
moving too slow
2 : 30.0
moving too fast
3 : 25.0
moving too fast
4 : 20.0
moving too slow
final velocity: 30.0
```

## Crear una tabla con los valores de las variables para seguir la ejecución de un programa.

<table>
  <tr>   <td><strong>i</strong></td>   <td>0</td>   <td>.</td>   <td>1</td>   <td>.</td>   <td>2</td>   <td>.</td>   <td>3</td>   <td>.</td>   <td>4</td>   <td>.</td>
  </tr>
  <tr>   <td><strong>velocity</strong></td>   <td>10.0</td>   <td>20.0</td>   <td>.</td>   <td>30.0</td>   <td>.</td>   <td>25.0</td>   <td>.</td>   <td>20.0</td>   <td>.</td>   <td>30.0</td>
  </tr>
</table>

- El programa debe tener una sentencia `print` *fuera* del cuerpo del bucle para mostrar
  el valor final de `velocity`, ya que su valor se actualiza en la última iteración del
  bucle.

::::::::::::::::::::::::::::::::::::::::: callout

## Relaciones compuestas usando `and`, `or` y paréntesis

A menudo, se desea que alguna combinación de cosas sea verdadera. Puede combinar
relaciones dentro de una condicional utilizando `and` y `or`. Siguiendo con el ejemplo
anterior, supongamos que tenemos

```python
mass     = [ 3.54,  2.07,  9.22,  1.86,  1.71]
velocity = [10.00, 20.00, 30.00, 25.00, 20.00]

i = 0
for i in range(5):
    if mass[i] > 5 and velocity[i] > 20:
        print("Fast heavy object.  Duck!")
    elif mass[i] > 2 and mass[i] <= 5 and velocity[i] <= 20:
        print("Normal traffic")
    elif mass[i] <= 2 and velocity[i] <= 20:
        print("Slow light object.  Ignore it")
    else:
        print("Whoa!  Something is up with the data.  Check it")
```

Al igual que con la aritmética, puede y debe utilizar paréntesis siempre que exista una
posible ambigüedad. Una buena regla general es usar *siempre* paréntesis cuando se
mezclan `and` y `or` en la misma condición. Es decir, en lugar de

```python
if mass[i] <= 2 or mass[i] >= 5 and velocity[i] > 20:
```

escribe uno de estos:

```python
if (mass[i] <= 2 or mass[i] >= 5) and velocity[i] > 20:
if mass[i] <= 2 or (mass[i] >= 5 and velocity[i] > 20):
```

para que quede perfectamente claro para un lector (y para Python) lo que realmente
quieres decir.


::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Rastreando Ejecución

¿Qué imprime este programa?

```python
pressure = 71.9
if pressure > 50.0:
    pressure = 25.0
elif pressure <= 50.0:
    pressure = 0.0
print(pressure)
```

::::::::::::::: solution

## Solución

```output
25.0
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Recorte de Valores

Rellena los espacios en blanco para que este programa cree una nueva lista que contenga
ceros donde los valores de la lista original eran negativos y unos donde los valores de
la lista original eran positivos.

```python
original = [-1.5, 0.2, 0.4, 0.0, -1.3, 0.4]
result = ____
for value in original:
    if ____:
        result.append(0)
    else:
        ____
print(result)
```

```output
[0, 1, 1, 1, 0, 1]
```

::::::::::::::: solution

## Solución

```python
original = [-1.5, 0.2, 0.4, 0.0, -1.3, 0.4]
result = []
for value in original:
    if value < 0.0:
        result.append(0)
    else:
        result.append(1)
print(result)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Procesamiento de ficheros pequeños

Modifica este programa para que sólo procese ficheros con menos de 50 registros.

```python
import glob
import pandas as pd
for filename in glob.glob('data/*.csv'):
    contents = pd.read_csv(filename)
    ____:
        print(filename, len(contents))
```

::::::::::::::: solution

## Solución

```python
import glob
import pandas as pd
for filename in glob.glob('data/*.csv'):
    contents = pd.read_csv(filename)
    if len(contents) < 50:
        print(filename, len(contents))
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Inicializando

Modifica este programa para que encuentre los valores mayor y menor de la lista sin
importar el rango de valores original.

```python
values = [...some test data...]
smallest, largest = None, None
for v in values:
    if ____:
        smallest, largest = v, v
    ____:
        smallest = min(____, v)
        largest = max(____, v)
print(smallest, largest)
```

¿Cuáles son las ventajas y desventajas de utilizar este método para hallar el rango de
los datos?

::::::::::::::: solution

## Solución

```python
values = [-2,1,65,78,-54,-24,100]
smallest, largest = None, None
for v in values:
    if smallest is None and largest is None:
        smallest, largest = v, v
    else:
        smallest = min(smallest, v)
        largest = max(largest, v)
print(smallest, largest)
```

Si escribiste `== None` en lugar de `is None`, también funciona, pero los programadores
de Python siempre escriben `is None` debido a la forma especial en que `None` funciona
en el lenguaje.

Se puede argumentar que una ventaja de utilizar este método sería hacer el código más
legible. Sin embargo, una desventaja es que este código no es eficiente porque dentro de
cada iteración de la declaración del bucle `for`, hay dos bucles más que se ejecutan
sobre dos números cada uno (las funciones `min` y `max`). Sería más eficiente iterar
sobre cada número una sola vez:

```python
values = [-2,1,65,78,-54,-24,100]
smallest, largest = None, None
for v in values:
    if smallest is None or v < smallest:
        smallest = v
    if largest is None or v > largest:
        largest = v
print(smallest, largest)
```

Ahora tenemos un bucle, pero cuatro pruebas de comparación. Hay dos formas de mejorarlo:
o bien utilizar menos comparaciones en cada iteración, o bien utilizar dos bucles que
contengan cada uno sólo una prueba de comparación. La solución más sencilla suele ser la
mejor:

```python
values = [-2,1,65,78,-54,-24,100]
smallest = min(values)
largest = max(values)
print(smallest, largest)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Utilice sentencias `if` para controlar si se ejecuta o no un bloque de código.
- Los condicionales se usan a menudo dentro de bucles.
- Utilice `else` para ejecutar un bloque de código cuando una condición `if` es *no*
  verdadera.
- Utilice `elif` para especificar pruebas adicionales.
- Las condiciones se prueban una vez, en orden.
- Crea una tabla con los valores de las variables para seguir la ejecución de un
  programa.

::::::::::::::::::::::::::::::::::::::::::::::::::



