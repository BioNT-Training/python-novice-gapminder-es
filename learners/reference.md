---
title: Referencia
---


## Referencia

## [Ejecutar y Salir](episodes/01-run-quit.md)

- Los ficheros Python tienen la extensión `.py`.
- Puede escribirse en un fichero de texto o en un [Jupyter Notebook][jupyter].
  - Los cuadernos Jupyter tienen la extensión `.ipynb`
  - Los cuadernos Jupyter se pueden abrir desde
    [Anaconda](https://docs.continuum.io/anaconda/install) o a través de la línea de
    comandos introduciendo `$ jupyter notebook`
    - Markdown y HTML están permitidos en las celdas markdown para documentar código.

## [Variables y Asignación](episodes/02-variables.md)

- Las variables se almacenan utilizando `=`.
  - Las cadenas se definen entre comillas `'...'`.
  - Los números enteros y de coma flotante se definen sin comillas.
- Las variables pueden contener letras, dígitos y guiones bajos `_`.
  - No puede empezar por un dígito.
  - Se deben evitar las variables que empiecen por guión bajo.
- Utilice `print(...)` para mostrar los valores como texto.
- Puede usar indexación en cadenas.
  - La indexación comienza en 0.
  - La posición se indica entre corchetes `[position]` a continuación del nombre de la
    variable.
  - Toma un trozo usando `[start:stop]`. Esto hace una copia de parte de la cadena
    original.
    - `start` es el índice del primer elemento.
    - `stop` es el índice del elemento después del último elemento deseado.
- Utilice `len(...)` para encontrar la longitud de una variable o cadena.

## [Tipos de datos y conversión de tipos](episodes/03-types-conversion.md)

- Cada valor tiene un tipo. Esto controla lo que se puede hacer con él.
  - `int` representa un entero
  - `float` representa un número en coma flotante.
  - `str` representa una cadena.
- Para determinar el tipo de una variable, utilice la función incorporada `type(...)`,
  incluyendo el nombre de la variable entre paréntesis.
- Modificación de cadenas:
  - Usa `+` para concatenar cadenas.
  - Usa `*` para repetir una cadena.
  - Los números y las cadenas no pueden sumarse entre sí.
    - Convierte cadena a entero: `int(...)`.
    - Convierte entero a cadena: `str(...)`.

## [Funciones incorporadas y ayuda](episodes/04-built-in.md)

- Para añadir un comentario, coloque `#` antes de lo que no desea que se ejecute.
- Funciones incorporadas de uso común:
  - `min()` encuentra el valor más pequeño.
  - `max()` encuentra el valor más grande.
  - `round()` redondea un número en coma flotante.
  - `help()` muestra la documentación de la función entre paréntesis.
    - Otras formas de obtener ayuda incluyen mantener pulsado `shift` y pulsar `tab` en
      Jupyter Notebooks.

## [Bibliotecas](episodes/06-libraries.md)

- Importación de una librería:
  - Usa `import ...` para cargar una librería.
  - Se refiere a esta librería usando `module_name.thing_name`.
    - `.` indica 'parte de'.
- Para importar un elemento específico de una biblioteca: `from ... import ...`
- Para importar una librería usando un alias: `import ... as ...`
- Importación de la librería matemática: `import math`
  - Ejemplo de referencia a un elemento con el nombre del módulo: `math.cos(math.pi)`.
- Importación de la librería de ploteo como alias: `import matplotlib as mpl`

## [Lectura de datos tabulares en DataFrames](episodes/07-reading-tabular.md)

- Utiliza la librería pandas para hacer estadísticas sobre datos tabulares. Cargar con
  `import pandas as pd`.
  - Para leer en un csv: `pd.read_csv()`, incluyendo el nombre de la ruta entre
    paréntesis.
    - Para especificar que los valores de una columna deben usarse como encabezados de
      fila: `pd.read_csv('path', index_col='column name')`, donde ruta y nombre de
      columna deben sustituirse por los valores correspondientes.
- Para obtener más información sobre un DataFrame, utilice `DataFrame.info`,
  sustituyendo `DataFrame` por el nombre de la variable de su DataFrame.
- Utilice `DataFrame.columns` para ver los nombres de las columnas.
- Usa `DataFrame.T` para transponer un DataFrame.
- Utilice `DataFrame.describe` para obtener estadísticas de resumen sobre sus datos.

## [Pandas DataFrames](episodes/08-data-frames.md)

- Seleccionar datos usando `[i,j]`
  - Para seleccionar por posición de entrada: `DataFrame.iloc[..., ...]`
    - Incluye todo excepto el índice final.
  - Para seleccionar por etiqueta de entrada: `DataFrame.loc[..., ...]`
    - Puede seleccionar múltiples filas o columnas listando etiquetas.
    - Esto incluye ambos extremos.
  - Utilice `:` para seleccionar todas las filas o columnas.
- También puede seleccionar datos basados en valores usando `True` y `False`. Se trata
  de una máscara booleana.
  - `mask = subset > 10000`
  - Podemos usar esto para seleccionar valores.
- Para usar una operación select-apply-combine usamos `data.apply(lambda x: x >
  x.mean())` donde `mean()` puede ser cualquier operación que el usuario quiera que se
  aplique a x.

## [Plotting](episodes/09-plotting.md)

- La librería de ploteo más utilizada es `matplotlib`.
  - Normalmente se importa usando `import matplotlib.pyplot as plt`.
  - Para representar gráficamente utilizamos el comando `plt.plot(time, position)`.
  - Para crear una leyenda utilice `plt.legend(['label1', 'label2'], loc='upper left')`
    - También puede definir etiquetas dentro de las sentencias de trazado utilizando
      `plt.plot(time, position, label='label')`. Para que aparezca la leyenda, utilice
      `plt.legend()`
  - Para etiquetar los ejes x e y se utilizan `plt.xlabel('label')` y
    `plt.ylabel('label')`.
- Los DataFrames de Pandas se pueden usar para trazar usando `DataFrame.plot()`.
  Cualquier operación que se pueda utilizar en un DataFrame se puede aplicar al trazar.
  - Para trazar un gráfico de barras `data.plot(kind='bar')`

```python
import matplotlib.puplot as plot
plt.plot(time, position, label='label')
plt.xlabel('x axis label')
plt.ylabel('y axis label')
plt.legend()
```

## [Listas](episodios/11-listas.md)

- Definidas dentro de `[...]` y separadas por `,`.
  - Se puede crear una lista vacía utilizando `[]`.
- Puede usar `len(...)` para determinar cuántos valores hay en una lista.
- Se puede indexar igual que en lecciones anteriores.
  - La indexación se puede utilizar para reasignar valores `list_name[0] = newvalue`.
- Para añadir un elemento a una lista utilice `list_name.append()`, con el elemento a
  añadir entre paréntesis.
- Para combinar dos listas utilice `list_name_1.extend(list_name_2)`.
- Para eliminar un elemento de una lista utilice `del list_name[index]`.

## [Bucles For](episodes/12-for-loops.md)

- Comienza un bucle for con `for number in [1, 2, 3]:`, con las siguientes líneas
  sangradas.
  - `[1, 2, 3]` se considera la colección.
  - `number` es la variable de bucle.
  - La acción que sigue a la colección es el cuerpo.
- Para iterar sobre una secuencia de números usa `range(start, end)`

```python
for number in range(0,5):
    print(number)
```

## [Condicionales](episodios/13-condicionales.md)

- Definida de forma similar a un bucle, utilizando `if variable conditional value:`.
  - Por ejemplo, `if variable > 5:`.
- Utilice `elif:` para pruebas adicionales.
- Utilice `else:` para cuando la sentencia if no sea verdadera.
- Puede combinar más de una condicional usando `and` o `or`.
- A menudo se utiliza en combinación con bucles for.
- Condiciones que se pueden utilizar:
  - `==` igual a.
  - `>=` mayor o igual que.
  - `<=` menor o igual que.
  - `>` mayor que.
  - `<` menor que.

```python
for m in [3, 6, 7, 2, 8]:
    if m > 5:
        print(m, 'is large')
    elif m == 5:
        print(m, 'is 5')
    else:
        print(m, 'is small')
```

## [Looping Over Data Sets](episodes/14-looping-data-sets.md)

- Utiliza un bucle for: `for filename in [file1, file2]:`
- Para encontrar un conjunto de ficheros usando un patrón use `glob.glob`
  - Debe importarse primero usando `import glob`.
  - `*` indica "coincide con cero o más caracteres"
  - `?` indica "coincide exactamente con un carácter"
    - Por ejemplo: `glob.glob(*.txt)` encontrará todos los ficheros que terminen en
      `.txt` en el directorio actual.
- Combínalas escribiendo un bucle usando: `for filename in glob.glob(*.txt):`

```python
for filename in glob.glob(*.txt):
  data = pd.read_csv(filename)
```

## [Funciones de escritura](episodes/16-writing-functions.md)

- Define una función usando `def function_name(parameters):`. Sustituya `parameters` por
  las variables a utilizar cuando se ejecute la función.
- Se ejecuta usando `function_name(parameters)`.
- Para devolver un resultado a la persona que llama utiliza `return ...` en la función.

```python
def add_numbers(a, b):
    result = a + b
    return result

add_numbers(1, 4)
```

## [Ámbito de la variable](episodes/17-scope.md)

- Una variable local se define en una función y sólo puede verse y usarse dentro de esa
  función.
- Una variable global se define fuera de una función y se puede ver o utilizar en
  cualquier lugar después de su definición.

## [Estilo de Programación](episodes/18-style.md)

- Documenta tu código.
- Utilice nombres de variables claros y significativos.
- Sigue [la guía de estilo PEP8](https://www.python.org/dev/peps/pep-0008) cuando
  configures tu código.
- Utiliza aserciones para comprobar errores internos.
- Utiliza docstrings para proporcionar ayuda.

## Glosario

Argumentos : Valores que se pasan a las funciones.

Matriz : Un contenedor que contiene elementos del mismo tipo.

Booleano : Un objeto compuesto por `True` y `False`. xYZ.1

DataFrame : La forma en que Pandas representa una tabla; una colección de series.

Elemento : Elemento de una lista o matriz. Para una cadena, son los caracteres
individuales.

Función : Un bloque de código que puede ser llamado y reutilizado en otro lugar.

Variable global : Una variable definida fuera de una función que puede ser usada en
cualquier lugar.

Índice : La posición de un elemento dado.

Jupyter Notebook : Entorno de codificación interactivo que permite una combinación de
código y markdown.

Biblioteca : Una colección de ficheros que contienen funciones usadas por otros
programas.

Variable Local : Una variable definida dentro de una función que sólo puede ser usada
dentro de esa función.

Máscara : Un objeto booleano utilizado para seleccionar datos de otro objeto.

Método : Una acción ligada a un objeto en particular. Se llama utilizando
`object.method`. xYZ.1:: MÉTODO

Módulos : Los archivos de una biblioteca que contienen funciones utilizadas por otros
programas.

Parámetros : Variables utilizadas al ejecutar una función.

Serie : Una estructura de datos Pandas para representar una columna.

Subcadena : Parte de una cadena.

Variables : Nombres de valores.





