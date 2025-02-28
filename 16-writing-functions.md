---
title: Funciones de escritura
teaching: 10
exercises: 15
---


::::::::::::::::::::::::::::::::::::::: objectives

- Explica e identifica la diferencia entre definición de función y llamada a función.
- Escribe una función que tome un número pequeño y fijo de argumentos y produzca un
  único resultado.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo puedo crear mis propias funciones?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Descomponer los programas en funciones para facilitar su comprensión.

- Los seres humanos sólo pueden mantener unos pocos elementos en la memoria de trabajo a
  la vez.
- Comprender ideas más grandes/más complicadas entendiendo y combinando piezas.
  - Componentes de una máquina.
  - Lemas para demostrar teoremas.
- Las funciones tienen el mismo propósito en los programas.
  - *Encapsular* la complejidad para que podamos tratarla como una única "cosa".
- También permite *reutilizar*.
  - Escribir una vez, usar muchas veces.

## Define una función usando `def` con un nombre, parámetros y un bloque de código.

- Comienza la definición de una nueva función con `def`.
- Seguido del nombre de la función.
  - Debe obedecer las mismas reglas que los nombres de variables.
- Entonces *parámetros* entre paréntesis.
  - Paréntesis vacíos si la función no toma ninguna entrada.
  - Lo discutiremos en detalle dentro de un momento.
- Entonces dos puntos.
- A continuación, un bloque de código con sangría.

```python
def print_greeting():
    print('Hello!')
    print('The weather is nice today.')
    print('Right?')
```

## Definir una función no la ejecuta.

- Definir una función no la ejecuta.
  - Como asignar un valor a una variable.
- Debe llamar a la función para ejecutar el código que contiene.

```python
print_greeting()
```

```output
Hello!
```

## Los argumentos de una llamada a función se corresponden con sus parámetros definidos.

- Las funciones son más útiles cuando pueden operar sobre diferentes datos.
- Especifica *parámetros* al definir una función.
  - Se convierten en variables cuando se ejecuta la función.
  - Se asignan los argumentos en la llamada (es decir, los valores pasados a la
    función).
  - Si no nombras los argumentos cuando los usas en la llamada, los argumentos se
    emparejarán con los parámetros en el orden en que los parámetros están definidos en
    la función.

```python
def print_date(year, month, day):
    joined = str(year) + '/' + str(month) + '/' + str(day)
    print(joined)

print_date(1871, 3, 19)
```

```output
1871/3/19
```

O bien, podemos nombrar los argumentos cuando llamamos a la función, lo que nos permite
especificarlos en cualquier orden y añade claridad al sitio de llamada; de lo contrario,
mientras uno está leyendo el código podría olvidar si el segundo argumento es el mes o
el día, por ejemplo.

```python
print_date(month=3, day=19, year=1871)
```

```output
1871/3/19
```

- Vía [Twitter](https://twitter.com/minisciencegirl/status/693486088963272705): `()`
  contiene los ingredientes de la función mientras que el cuerpo contiene la receta.

## Las funciones pueden devolver un resultado a su invocador usando `return`.

- Utiliza `return ...` para devolver un valor al llamante.
- Puede aparecer en cualquier parte de la función.
- Pero las funciones son más fáciles de entender si aparece `return`:
  - Al principio para tratar casos especiales.
  - Al final, con un resultado final.

```python
def average(values):
    if len(values) == 0:
        return None
    return sum(values) / len(values)
```

```python
a = average([1, 3, 4])
print('average of actual values:', a)
```

```output
average of actual values: 2.6666666666666665
```

```python
print('average of empty list:', average([]))
```

```output
average of empty list: None
```

- Recuerda: [toda función devuelve algo](04-built-in.md).
- Una función que no explícitamente `return` un valor devuelve automáticamente `None`.

```python
result = print_date(1871, 3, 19)
print('result of call is:', result)
```

```output
1871/3/19
result of call is: None
```

::::::::::::::::::::::::::::::::::::::: challenge

## Identificación de errores de sintaxis

1. Lee el siguiente código e intenta identificar cuáles son los errores *sin*
   ejecutarlo.
2. Ejecuta el código y lee el mensaje de error. ¿Es un `SyntaxError` o un
   `IndentationError`?
3. Corrige el error.
4. Repite los pasos 2 y 3 hasta que hayas corregido todos los errores.

```python
def another_function
  print("Syntax errors are annoying.")
   print("But at least python tells us about them!")
  print("So they are usually not too hard to fix.")
```

::::::::::::::: solution

## Solución

```python
def another_function():
  print("Syntax errors are annoying.")
  print("But at least Python tells us about them!")
  print("So they are usually not too hard to fix.")
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Definición y uso

¿Qué imprime el siguiente programa?

```python
def report(pressure):
    print('pressure is', pressure)

print('calling', report, 22.5)
```

::::::::::::::: solution

## Solución

```output
calling <function report at 0x7fd128ff1bf8> 22.5
```

Una llamada a una función siempre necesita paréntesis, de lo contrario se obtiene la
dirección de memoria del objeto de la función. Por lo tanto, si quisiéramos llamar a la
función llamada informe, y darle el valor 22.5 para informar, podríamos tener nuestra
llamada a la función de la siguiente manera

```python
print("calling")
report(22.5)
```

```output
calling
pressure is 22.5
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Orden de operaciones

1. ¿Qué falla en este ejemplo?

  ```python
  result = print_time(11, 37, 59)

  def print_time(hour, minute, second):
     time_string = str(hour) + ':' + str(minute) + ':' + str(second)
     print(time_string)
  ```

2. Después de solucionar el problema anterior, explica por qué ejecutar este código de
   ejemplo:

  ```python
  result = print_time(11, 37, 59)
  print('result of call is:', result)
  ```

da esta salida:

  ```output
  11:37:59
  result of call is: None
  ```

3. ¿Por qué el resultado de la llamada es `None`?

::::::::::::::: solution

## Solución

1. El problema con el ejemplo es que la función `print_time()` se define *después* de
   hacer la llamada a la función. Python no sabe cómo resolver el nombre `print_time` ya
   que no se ha definido todavía y lanzará un `NameError` por ejemplo, `NameError: name
   'print_time' is not defined`

2. La primera línea de salida `11:37:59` es impresa por la primera línea de código,
   `result = print_time(11, 37, 59)` que vincula el valor devuelto por la invocación
   `print_time` a la variable `result`. La segunda línea es de la segunda llamada de
   impresión para imprimir el contenido de la variable `result`.

3. `print_time()` no devuelve explícitamente `return` un valor, por lo que devuelve
   automáticamente `None`.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Encapsulación

Rellena los espacios en blanco para crear una función que tome un único nombre de
fichero como argumento, cargue los datos en el fichero nombrado por el argumento y
devuelva el valor mínimo en esos datos.

```python
import pandas as pd

def min_in_data(____):
    data = ____
    return ____
```

::::::::::::::: solution

## Solución

```python
import pandas as pd

def min_in_data(filename):
    data = pd.read_csv(filename)
    return data.min()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Hallar el Primer

Rellena los espacios en blanco para crear una función que tome una lista de números como
argumento y devuelva el primer valor negativo de la lista. ¿Qué hace la función si la
lista está vacía? ¿Y si la lista no tiene números negativos?

```python
def first_negative(values):
    for v in ____:
        if ____:
            return ____
```

::::::::::::::: solution

## Solución

```python
def first_negative(values):
    for v in values:
        if v < 0:
            return v
```

Si a esta función se le pasa una lista vacía o una lista con todos los valores
positivos, devuelve `None`:

```python
my_list = []
print(first_negative(my_list))
```

```output
None
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Llamado por su nombre

Anteriormente vimos esta función:

```python
def print_date(year, month, day):
    joined = str(year) + '/' + str(month) + '/' + str(day)
    print(joined)
```

Vimos que podemos llamar a la función usando *nombres de argumentos*, así:

```python
print_date(day=1, month=2, year=2003)
```

1. ¿Qué imprime `print_date(day=1, month=2, year=2003)`?
2. ¿Cuándo has visto una llamada a una función como ésta?
3. ¿Cuándo y por qué es útil llamar así a las funciones?

::::::::::::::: solution

## Solución

1. `2003/2/1`
2. Vimos ejemplos de uso de *argumentos con nombre* al trabajar con la librería pandas.
   Por ejemplo, cuando se lee un conjunto de datos usando `data =
   pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')`, el último
   argumento `index_col` es un argumento con nombre.
3. El uso de argumentos con nombre puede hacer que el código sea más legible, ya que uno
   puede ver en la llamada a la función qué nombre tienen los diferentes argumentos
   dentro de la función. También puede reducir las posibilidades de pasar argumentos en
   el orden incorrecto, ya que al utilizar argumentos con nombre el orden no importa.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Encapsulación de un bloque If/Print

El siguiente código se ejecutará en una impresora de etiquetas para huevos de gallina.
Una balanza digital informará de la masa de un huevo de gallina (en gramos) al ordenador
y éste imprimirá una etiqueta.

```python
import random
for i in range(10):

    # simulating the mass of a chicken egg
    # the (random) mass will be 70 +/- 20 grams
    mass = 70 + 20.0 * (2.0 * random.random() - 1.0)

    print(mass)

    # egg sizing machinery prints a label
    if mass >= 85:
        print("jumbo")
    elif mass >= 70:
        print("large")
    elif mass < 70 and mass >= 55:
        print("medium")
    else:
        print("small")
```

El bloque if que clasifica los huevos podría ser útil en otras situaciones, así que para
evitar repetirlo, podríamos plegarlo en una función, `get_egg_label()`. Revisando el
programa para usar la función tendríamos esto:

```python
# revised version
import random
for i in range(10):

    # simulating the mass of a chicken egg
    # the (random) mass will be 70 +/- 20 grams
    mass = 70 + 20.0 * (2.0 * random.random() - 1.0)

    print(mass, get_egg_label(mass))

```

1. Cree una definición de función para `get_egg_label()` que funcione con el programa
   revisado anteriormente. Tenga en cuenta que el valor de retorno de la función
   `get_egg_label()` será importante. La salida de ejemplo del programa anterior sería
   `71.23 large`.
2. Un huevo sucio puede tener una masa superior a 90 gramos, y un huevo estropeado o
   roto probablemente tendrá una masa inferior a 50 gramos. Modifique su función
   `get_egg_label()` para tener en cuenta estas condiciones de error. Un ejemplo de
   salida podría ser `25 too light, probably spoiled`.

::::::::::::::: solution

## Solución

```python
def get_egg_label(mass):
    # egg sizing machinery prints a label
    egg_label = "Unlabelled"
    if mass >= 90:
        egg_label = "warning: egg might be dirty"
    elif mass >= 85:
        egg_label = "jumbo"
    elif mass >= 70:
        egg_label = "large"
    elif mass < 70 and mass >= 55:
        egg_label = "medium"
    elif mass < 50:
        egg_label = "too light, probably spoiled"
    else:
        egg_label = "small"
    return egg_label
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Análisis encapsulado de datos

Supongamos que se ha ejecutado el siguiente código:

```python
import pandas as pd

data_asia = pd.read_csv('data/gapminder_gdp_asia.csv', index_col=0)
japan = data_asia.loc['Japan']
```

1. Complete los enunciados siguientes para obtener el PIB medio de Japón en los años
   indicados para la década de 1980.

  ```python
  year = 1983
  gdp_decade = 'gdpPercap_' + str(year // ____)
  avg = (japan.loc[gdp_decade + ___] + japan.loc[gdp_decade + ___]) / 2
  ```

2. Abstrae el código anterior en una única función.

  ```python
  def avg_gdp_in_decade(country, continent, year):
      data_countries = pd.read_csv('data/gapminder_gdp_'+___+'.csv',delimiter=',',index_col=0)
      ____
      ____
      ____
      return avg
  ```

3. ¿Cómo generalizaría esta función si no supiera de antemano qué años concretos
   aparecen como columnas en los datos? Por ejemplo, ¿qué pasaría si también tuviéramos
   datos de los años que terminan en 1 y 9 para cada década? (Sugerencia: utilice las
   columnas para filtrar las que corresponden a la década, en lugar de enumerarlas en el
   código)

::::::::::::::: solution

## Solución

1. El PIB medio de Japón a lo largo de los años reportados para la década de 1980 se
   calcula con:

  ```python
  year = 1983
  gdp_decade = 'gdpPercap_' + str(year // 10)
  avg = (japan.loc[gdp_decade + '2'] + japan.loc[gdp_decade + '7']) / 2
  ```

2. Que se codifica como una función es:

  ```python
  def avg_gdp_in_decade(country, continent, year):
      data_countries = pd.read_csv('data/gapminder_gdp_' + continent + '.csv', index_col=0)
      c = data_countries.loc[country]
      gdp_decade = 'gdpPercap_' + str(year // 10)
      avg = (c.loc[gdp_decade + '2'] + c.loc[gdp_decade + '7'])/2
      return avg
  ```

3. Para obtener la media de los años relevantes, necesitamos hacer un bucle sobre ellos:

  ```python
  def avg_gdp_in_decade(country, continent, year):
      data_countries = pd.read_csv('data/gapminder_gdp_' + continent + '.csv', index_col=0)
      c = data_countries.loc[country]
      gdp_decade = 'gdpPercap_' + str(year // 10)
      total = 0.0
      num_years = 0
      for yr_header in c.index: # c's index contains reported years
          if yr_header.startswith(gdp_decade):
              total = total + c.loc[yr_header]
              num_years = num_years + 1
      return total/num_years
  ```

La función se puede llamar ahora por:

```python
avg_gdp_in_decade('Japan','asia',1983)
```

```output
20880.023800000003
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Simulación de un sistema dinámico

En matemáticas, un [sistema dinámico](https://en.wikipedia.org/wiki/Dynamical_system) es
un sistema en el que una función describe la dependencia temporal de un punto en un
espacio geométrico. Un ejemplo canónico de sistema dinámico es el [mapa
logístico](https://en.wikipedia.org/wiki/Logistic_map), un modelo de crecimiento que
calcula una nueva densidad de población (entre 0 y 1) a partir de la densidad actual. En
el modelo, el tiempo toma valores discretos 0, 1, 2, ...

1. Definir una función llamada `logistic_map` que toma dos entradas: `x`, que representa
   la población actual (en el momento `t`), y un parámetro `r = 1`. Esta función debe
   devolver un valor que representa el estado del sistema (población) en el momento `t +
   1`, utilizando la función de mapeo:

`f(t+1) = r * f(t) * [1 - f(t)]`

2. Utilizando un bucle `for` o `while`, itere la función `logistic_map` definida en la
   parte 1, partiendo de una población inicial de 0.5, durante un periodo de tiempo
   `t_final = 10`. Almacena los resultados intermedios en una lista, de forma que al
   finalizar el bucle hayas acumulado una secuencia de valores que representen el estado
   del mapa logístico en los tiempos `t = [0,1,...,t_final]` (11 valores en total).
   Imprima esta lista para ver la evolución de la población.

3. Encapsule la lógica de su bucle en una función llamada `iterate` que toma la
   población inicial como primera entrada, el parámetro `t_final` como segunda entrada y
   el parámetro `r` como tercera entrada. La función debe devolver la lista de valores
   que representan el estado del mapa logístico en los tiempos `t = [0,1,...,t_final]`.
   Ejecute esta función para los periodos `t_final = 100` y `1000` e imprima algunos de
   los valores. ¿La población tiende hacia un estado estacionario?

::::::::::::::: solution

## Solución

1. 
  ```python
  def logistic_map(x, r):
      return r * x * (1 - x)
  ```

2. 
  ```python
  initial_population = 0.5
  t_final = 10
  r = 1.0
  population = [initial_population]

  for t in range(t_final):
      population.append( logistic_map(population[t], r) )
  ```

3. 
  ```python
  def iterate(initial_population, t_final, r):
      population = [initial_population]
      for t in range(t_final):
          population.append( logistic_map(population[t], r) )
      return population

  for period in (10, 100, 1000):
      population = iterate(0.5, period, 1)
      print(population[-1])
  ```

  ```output
  0.06945089389714401
  0.009395779870614648
  0.0009913908614406382
  ```

La población parece acercarse a cero.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Uso de funciones con condicionales en Pandas

Las funciones a menudo contienen condicionales. He aquí un breve ejemplo que indicará en
qué cuartil se encuentra el argumento basándose en los valores codificados a mano para
los puntos de corte de los cuartiles.

```python
def calculate_life_quartile(exp):
    if exp < 58.41:
        # This observation is in the first quartile
        return 1
    elif exp >= 58.41 and exp < 67.05:
        # This observation is in the second quartile
       return 2
    elif exp >= 67.05 and exp < 71.70:
        # This observation is in the third quartile
       return 3
    elif exp >= 71.70:
        # This observation is in the fourth quartile
       return 4
    else:
        # This observation has bad data
       return None

calculate_life_quartile(62.5)
```

```output
2
```

Esa función se usaría típicamente dentro de un bucle `for`, pero Pandas tiene una forma
diferente y más eficiente de hacer lo mismo, y es *aplicando* una función a un marco de
datos o a una porción de un marco de datos. He aquí un ejemplo, utilizando la definición
anterior.

```python
data = pd.read_csv('data/gapminder_all.csv')
data['life_qrtl'] = data['lifeExp_1952'].apply(calculate_life_quartile)
```

Hay muchas cosas en esa segunda línea, así que vayamos por partes. En el lado derecho de
la `=` empezamos con `data['lifeExp']`, que es la columna en el marco de datos llamado
`data` etiquetado `lifExp`. Utilizamos el `apply()` para hacer lo que dice, aplicar el
`calculate_life_quartile` al valor de esta columna para cada fila en el marco de datos.


::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Descomponer los programas en funciones para facilitar su comprensión.
- Define una función usando `def` con un nombre, parámetros y un bloque de código.
- Definir una función no la ejecuta.
- Los argumentos de una llamada a una función coinciden con sus parámetros definidos.
- Las funciones pueden devolver un resultado a su invocador utilizando `return`.

::::::::::::::::::::::::::::::::::::::::::::::::::



