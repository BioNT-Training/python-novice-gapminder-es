---
title: Pandas DataFrames
teaching: 15
exercises: 15
---


::::::::::::::::::::::::::::::::::::::: objectives

- Selecciona valores individuales de un marco de datos Pandas.
- Selecciona filas enteras o columnas enteras de un marco de datos.
- Selecciona un subconjunto de filas y columnas de un marco de datos en una sola
  operación.
- Seleccionar un subconjunto de un marco de datos mediante un único criterio booleano.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo puedo hacer un análisis estadístico de datos tabulares?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Nota sobre Pandas DataFrames/Series

Un [DataFrame][pandas-dataframe] es una colección de [Series][pandas-series]; El
DataFrame es la forma en que Pandas representa una tabla, y Series es la estructura de
datos que Pandas utiliza para representar una columna.

Pandas está construido sobre la librería [Numpy][numpy], lo que en la práctica significa
que la mayoría de los métodos definidos para Numpy Arrays se aplican a Pandas
Series/DataFrames.

Lo que hace que Pandas sea tan atractivo es la potente interfaz para acceder a registros
individuales de la tabla, el manejo adecuado de los valores que faltan y las operaciones
de base de datos relacional entre DataFrames.

## Seleccionar valores

Para acceder a un valor en la posición `[i,j]` de un DataFrame, tenemos dos opciones,
dependiendo de cuál sea el significado de `i` en uso. Recuerde que un DataFrame
proporciona un *índice* como forma de identificar las filas de la tabla; una fila,
entonces, tiene una *posición* dentro de la tabla así como una *etiqueta*, que
identifica unívocamente su *entrada* en el DataFrame.

## Usar `DataFrame.iloc[..., ...]` para seleccionar valores por su posición (de entrada)

- Puede especificar la ubicación por índice numérico de forma análoga a la versión 2D de
  la selección de caracteres en cadenas.

```python
import pandas as pd
data = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
print(data.iloc[0, 0])
```

```output
1601.056136
```

## Usa `DataFrame.loc[..., ...]` para seleccionar valores por su etiqueta (de entrada).

- Puede especificar la ubicación por nombre de fila y/o columna.

```python
print(data.loc["Albania", "gdpPercap_1952"])
```

```output
1601.056136
```

## Use `:` solo para significar todas las columnas o todas las filas.

- Igual que la notación de corte habitual de Python.

```python
print(data.loc["Albania", :])
```

```output
gdpPercap_1952    1601.056136
gdpPercap_1957    1942.284244
gdpPercap_1962    2312.888958
gdpPercap_1967    2760.196931
gdpPercap_1972    3313.422188
gdpPercap_1977    3533.003910
gdpPercap_1982    3630.880722
gdpPercap_1987    3738.932735
gdpPercap_1992    2497.437901
gdpPercap_1997    3193.054604
gdpPercap_2002    4604.211737
gdpPercap_2007    5937.029526
Name: Albania, dtype: float64
```

- Obtendría el mismo resultado imprimiendo `data.loc["Albania"]` (sin un segundo
  índice).

```python
print(data.loc[:, "gdpPercap_1952"])
```

```output
country
Albania                    1601.056136
Austria                    6137.076492
Belgium                    8343.105127
⋮ ⋮ ⋮
Switzerland               14734.232750
Turkey                     1969.100980
United Kingdom             9979.508487
Name: gdpPercap_1952, dtype: float64
```

- Obtendría el mismo resultado imprimiendo `data["gdpPercap_1952"]`
- También se obtiene el mismo resultado imprimiendo `data.gdpPercap_1952` (no
  recomendado, porque se confunde fácilmente con la notación `.` para métodos)

## Selecciona múltiples columnas o filas usando `DataFrame.loc` y un slice con nombre.

```python
print(data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'])
```

```output
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy           8243.582340    10022.401310    12269.273780
Montenegro      4649.593785     5907.850937     7778.414017
Netherlands    12790.849560    15363.251360    18794.745670
Norway         13450.401510    16361.876470    18965.055510
Poland          5338.752143     6557.152776     8006.506993
```

En el código anterior, descubrimos que **el troceado utilizando `loc` es inclusivo en
ambos extremos**, lo que difiere del **troceado utilizando `iloc`**, donde el troceado
indica todo hasta el índice final, pero sin incluirlo.

## El resultado del corte puede utilizarse en operaciones posteriores.

- Normalmente no se imprime sólo un trozo.
- Todos los operadores estadísticos que funcionan en marcos de datos enteros funcionan
  de la misma manera en cortes.
- Por ejemplo, calcular el máximo de una porción.

```python
print(data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'].max())
```

```output
gdpPercap_1962    13450.40151
gdpPercap_1967    16361.87647
gdpPercap_1972    18965.05551
dtype: float64
```

```python
print(data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'].min())
```

```output
gdpPercap_1962    4649.593785
gdpPercap_1967    5907.850937
gdpPercap_1972    7778.414017
dtype: float64
```

## Utiliza comparaciones para seleccionar datos en función de su valor.

- La comparación se aplica elemento por elemento.
- Devuelve un marco de datos de forma similar de `True` y `False`.

```python
# Use a subset of data to keep output readable.
subset = data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972']
print('Subset of data:\n', subset)

# Which values were greater than 10000 ?
print('\nWhere are values large?\n', subset > 10000)
```

```output
Subset of data:
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy           8243.582340    10022.401310    12269.273780
Montenegro      4649.593785     5907.850937     7778.414017
Netherlands    12790.849560    15363.251360    18794.745670
Norway         13450.401510    16361.876470    18965.055510
Poland          5338.752143     6557.152776     8006.506993

Where are values large?
            gdpPercap_1962 gdpPercap_1967 gdpPercap_1972
country
Italy                False           True           True
Montenegro           False          False          False
Netherlands           True           True           True
Norway                True           True           True
Poland               False          False          False
```

## Seleccionar valores o NaN usando una máscara booleana.

- Un marco lleno de booleanos a veces se llama *máscara* por cómo se puede usar.

```python
mask = subset > 10000
print(subset[mask])
```

```output
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy                   NaN     10022.40131     12269.27378
Montenegro              NaN             NaN             NaN
Netherlands     12790.84956     15363.25136     18794.74567
Norway          13450.40151     16361.87647     18965.05551
Poland                  NaN             NaN             NaN
```

- Obtiene el valor donde la máscara es verdadera, y NaN (Not a Number) donde es falsa.
- Útil porque los NaNs son ignorados por operaciones como max, min, promedio, etc.

```python
print(subset[subset > 10000].describe())
```

```output
       gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
count        2.000000        3.000000        3.000000
mean     13120.625535    13915.843047    16676.358320
std        466.373656     3408.589070     3817.597015
min      12790.849560    10022.401310    12269.273780
25%      12955.737547    12692.826335    15532.009725
50%      13120.625535    15363.251360    18794.745670
75%      13285.513523    15862.563915    18879.900590
max      13450.401510    16361.876470    18965.055510
```

## Agrupar por: split-apply-combine

::::::::::::::::::::::::::::::::::::: instructor

Los alumnos suelen tener dificultades en este punto, ya que muchos no trabajan con datos
y conceptos financieros, por lo que les resulta difícil entender los conceptos del
ejemplo. Sin embargo, el mayor problema es la línea que genera la puntuación de la
riqueza:
* Utiliza la conversión implícita entre valores booleanos y flotantes que no se ha
  tratado en el curso hasta ahora.
* Es necesario explicar claramente el argumento axis=1.

:::::::::::::::::::::::::::::::::::::::::::::::::

Los métodos de vectorización y las operaciones de agrupación de Pandas son
características que proporcionan a los usuarios mucha flexibilidad para analizar sus
datos.

Por ejemplo, supongamos que queremos tener una visión más clara de cómo se dividen los
países europeos según su PIB.

1. Podemos echar un vistazo dividiendo los países en dos grupos durante los años
   estudiados, los que presentaron un PIB *superior* a la media europea y los que
   tuvieron un PIB *inferior*.
2. A continuación, estimamos una *puntuación de riqueza* basada en los valores
   históricos (de 1962 a 2007), en la que tenemos en cuenta cuántas veces ha participado
   un país en los grupos de PIB *más bajo* o *más alto

```python
mask_higher = data > data.mean()
wealth_score = mask_higher.aggregate('sum', axis=1) / len(data.columns)
print(wealth_score)
```

```output
country
Albania                   0.000000
Austria                   1.000000
Belgium                   1.000000
Bosnia and Herzegovina    0.000000
Bulgaria                  0.000000
Croatia                   0.000000
Czech Republic            0.500000
Denmark                   1.000000
Finland                   1.000000
France                    1.000000
Germany                   1.000000
Greece                    0.333333
Hungary                   0.000000
Iceland                   1.000000
Ireland                   0.333333
Italy                     0.500000
Montenegro                0.000000
Netherlands               1.000000
Norway                    1.000000
Poland                    0.000000
Portugal                  0.000000
Romania                   0.000000
Serbia                    0.000000
Slovak Republic           0.000000
Slovenia                  0.333333
Spain                     0.333333
Sweden                    1.000000
Switzerland               1.000000
Turkey                    0.000000
United Kingdom            1.000000
dtype: float64
```

Por último, para cada grupo de la tabla `wealth_score`, sumamos su contribución
(financiera) a lo largo de los años encuestados utilizando métodos encadenados:

```python
print(data.groupby(wealth_score).sum())
```

```output
          gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  gdpPercap_1967  \
0.000000    36916.854200    46110.918793    56850.065437    71324.848786   
0.333333    16790.046878    20942.456800    25744.935321    33567.667670   
0.500000    11807.544405    14505.000150    18380.449470    21421.846200   
1.000000   104317.277560   127332.008735   149989.154201   178000.350040   

          gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  gdpPercap_1987  \
0.000000    88569.346898   104459.358438   113553.768507   119649.599409   
0.333333    45277.839976    53860.456750    59679.634020    64436.912960   
0.500000    25377.727380    29056.145370    31914.712050    35517.678220   
1.000000   215162.343140   241143.412730   263388.781960   296825.131210   

          gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  gdpPercap_2007  
0.000000    92380.047256   103772.937598   118590.929863   149577.357928  
0.333333    67918.093220    80876.051580   102086.795210   122803.729520  
0.500000    36310.666080    40723.538700    45564.308390    51403.028210  
1.000000   315238.235970   346930.926170   385109.939210   427850.333420
```

::::::::::::::::::::::::::::::::::::::: challenge

## Selección de valores individuales

Suponga que ha importado Pandas a su cuaderno y que ha cargado los datos del PIB de
Gapminder para Europa:

```python
import pandas as pd

data_europe = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
```

Escribe una expresión para hallar el PIB per cápita de Serbia en 2007.

::::::::::::::: solution

## Solución

La selección puede hacerse utilizando las etiquetas tanto de la fila ("Serbia") como de
la columna ("gdpPercap\_2007"):

```python
print(data_europe.loc['Serbia', 'gdpPercap_2007'])
```

La salida es

```output
9786.534714
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Extensión del corte

1. ¿Las dos sentencias siguientes producen la misma salida?
2. En base a esto, ¿qué regla gobierna lo que se incluye (o no) en los cortes numéricos
   y los cortes con nombre en Pandas?

```python
print(data_europe.iloc[0:2, 0:2])
print(data_europe.loc['Albania':'Belgium', 'gdpPercap_1952':'gdpPercap_1962'])
```

::::::::::::::: solution

## Solución

¡No, no producen la misma salida! La salida de la primera sentencia es

```output
        gdpPercap_1952  gdpPercap_1957
country                                
Albania     1601.056136     1942.284244
Austria     6137.076492     8842.598030
```

La segunda sentencia da:

```output
        gdpPercap_1952  gdpPercap_1957  gdpPercap_1962
country                                                
Albania     1601.056136     1942.284244     2312.888958
Austria     6137.076492     8842.598030    10750.721110
Belgium     8343.105127     9714.960623    10991.206760
```

Claramente, la segunda sentencia produce una columna y una fila adicionales en
comparación con la primera sentencia.  
¿Qué conclusión podemos sacar? Vemos que un corte numérico, 0:2, *omite* el índice final
(es decir, el índice 2) en el rango proporcionado, mientras que un corte con nombre,
'gdpPercap\_1952':'gdpPercap\_1962', *incluye* el elemento final.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Reconstruyendo Datos

Explica qué hace cada línea del siguiente programa corto: ¿qué hay en `first`, `second`,
etc.?

```python
first = pd.read_csv('data/gapminder_all.csv', index_col='country')
second = first[first['continent'] == 'Americas']
third = second.drop('Puerto Rico')
fourth = third.drop('continent', axis = 1)
fourth.to_csv('result.csv')
```

::::::::::::::: solution

## Solución

Repasemos este trozo de código línea por línea.

```python
first = pd.read_csv('data/gapminder_all.csv', index_col='country')
```

Esta línea carga el conjunto de datos que contiene los datos del PIB de todos los países
en un marco de datos llamado `first`. El parámetro `index_col='country'` selecciona la
columna que se utilizará como etiquetas de fila en el marco de datos.

```python
second = first[first['continent'] == 'Americas']
```

Esta línea realiza una selección: sólo se extraen las filas de `first` cuya columna
"continente" coincida con "Américas". Observe cómo la expresión booleana dentro de los
corchetes, `first['continent'] == 'Americas'`, se utiliza para seleccionar sólo aquellas
filas en las que la expresión es verdadera. Intente imprimir esta expresión ¿Puede
imprimir también sus elementos individuales Verdadero/Falso? (pista: asigna primero la
expresión a una variable)

```python
third = second.drop('Puerto Rico')
```

Como sugiere la sintaxis, esta línea elimina la fila de `second` donde la etiqueta es
'Puerto Rico'. El marco de datos resultante `third` tiene una fila menos que el marco de
datos original `second`.

```python
fourth = third.drop('continent', axis = 1)
```

Volvemos a aplicar la función drop, pero en este caso no eliminamos una fila, sino una
columna entera. Para ello, tenemos que especificar también el parámetro `axis` (queremos
eliminar la segunda columna que tiene el índice 1).

```python
fourth.to_csv('result.csv')
```

El paso final es escribir los datos con los que hemos estado trabajando en un fichero
csv. Pandas hace esto fácil con la función `to_csv()`. El único argumento requerido para
la función es el nombre del fichero. Ten en cuenta que el fichero se escribirá en el
directorio desde el que iniciaste la sesión de Jupyter o Python.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Selección de índices

Explica en términos sencillos lo que hacen `idxmin` y `idxmax` en el breve programa que
aparece a continuación. ¿Cuándo utilizarías estos métodos?

```python
data = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
print(data.idxmin())
print(data.idxmax())
```

::::::::::::::: solution

## Solución

Para cada columna de `data`, `idxmin` devolverá el valor del índice correspondiente al
mínimo de cada columna; `idxmax` hará lo mismo para el valor máximo de cada columna.

Puede utilizar estas funciones siempre que desee obtener el índice de fila del valor
mínimo/máximo y no el valor mínimo/máximo real.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Practica con la selección

Supongamos que se ha importado Pandas y se han cargado los datos de PIB de Gapminder
para Europa. Escriba una expresión para seleccionar cada uno de los siguientes
elementos:

1. PIB per cápita de todos los países en 1982.
2. PIB per cápita de Dinamarca para todos los años.
3. PIB per cápita de todos los países para los años *después* de 1985.
4. PIB per cápita de cada país en 2007 como múltiplo del PIB per cápita de ese país en
   1952.

::::::::::::::: solution

## Solución

1:

```python
data['gdpPercap_1982']
```

2:

```python
data.loc['Denmark',:]
```

3:

```python
data.loc[:,'gdpPercap_1985':]
```

Pandas es lo suficientemente inteligente como para reconocer el número al final de la
etiqueta de la columna y no le da un error, aunque en realidad no exista ninguna columna
llamada `gdpPercap_1985`. Esto es útil si más tarde se añaden nuevas columnas al fichero
CSV.

4:

```python
data['gdpPercap_2007']/data['gdpPercap_1952']
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Muchas formas de acceso

Existen al menos dos formas de acceder a un valor o a un segmento de un DataFrame: por
nombre o por índice. Sin embargo, existen muchas otras. Por ejemplo, se puede acceder a
una sola columna o fila como un objeto `DataFrame` o `Series`.

Sugiere distintas formas de realizar las siguientes operaciones en un DataFrame:

1. Accede a una sola columna
2. Accede a una única fila
3. Accede a un elemento individual del DataFrame
4. Accede a varias columnas
5. Accede a varias filas
6. Accede a un subconjunto de filas y columnas específicas
7. Accede a un subconjunto de rangos de filas y columnas

::::::::::::::: solution

## Solución

1\. Accede a una sola columna:

```python
# by name
data["col_name"]   # as a Series
data[["col_name"]] # as a DataFrame

# by name using .loc
data.T.loc["col_name"]  # as a Series
data.T.loc[["col_name"]].T  # as a DataFrame

# Dot notation (Series)
data.col_name

# by index (iloc)
data.iloc[:, col_index]   # as a Series
data.iloc[:, [col_index]] # as a DataFrame

# using a mask
data.T[data.T.index == "col_name"].T
```

2\. Accede a una única fila:

```python
# by name using .loc
data.loc["row_name"] # as a Series
data.loc[["row_name"]] # as a DataFrame

# by name
data.T["row_name"] # as a Series
data.T[["row_name"]].T # as a DataFrame

# by index
data.iloc[row_index]   # as a Series
data.iloc[[row_index]]   # as a DataFrame

# using mask
data[data.index == "row_name"]
```

3\. Accede a un elemento individual del DataFrame:

```python
# by column/row names
data["column_name"]["row_name"]         # as a Series

data[["col_name"]].loc["row_name"]  # as a Series
data[["col_name"]].loc[["row_name"]]  # as a DataFrame

data.loc["row_name"]["col_name"]  # as a value
data.loc[["row_name"]]["col_name"]  # as a Series
data.loc[["row_name"]][["col_name"]]  # as a DataFrame

data.loc["row_name", "col_name"]  # as a value
data.loc[["row_name"], "col_name"]  # as a Series. Preserves index. Column name is moved to `.name`.
data.loc["row_name", ["col_name"]]  # as a Series. Index is moved to `.name.` Sets index to column name.
data.loc[["row_name"], ["col_name"]]  # as a DataFrame (preserves original index and column name)

# by column/row names: Dot notation
data.col_name.row_name

# by column/row indices
data.iloc[row_index, col_index] # as a value
data.iloc[[row_index], col_index] # as a Series. Preserves index. Column name is moved to `.name`
data.iloc[row_index, [col_index]] # as a Series. Index is moved to `.name.` Sets index to column name.
data.iloc[[row_index], [col_index]] # as a DataFrame (preserves original index and column name)

# column name + row index
data["col_name"][row_index]
data.col_name[row_index]
data["col_name"].iloc[row_index]

# column index + row name
data.iloc[:, [col_index]].loc["row_name"]  # as a Series
data.iloc[:, [col_index]].loc[["row_name"]]  # as a DataFrame

# using masks
data[data.index == "row_name"].T[data.T.index == "col_name"].T
```

4\. Accede a varias columnas:

```python
# by name
data[["col1", "col2", "col3"]]
data.loc[:, ["col1", "col2", "col3"]]

# by index
data.iloc[:, [col1_index, col2_index, col3_index]]
```

5\. Accede a varias filas

```python
# by name
data.loc[["row1", "row2", "row3"]]

# by index
data.iloc[[row1_index, row2_index, row3_index]]
```

6\. Accede a un subconjunto de filas y columnas específicas

```python
# by names
data.loc[["row1", "row2", "row3"], ["col1", "col2", "col3"]]

# by indices
data.iloc[[row1_index, row2_index, row3_index], [col1_index, col2_index, col3_index]]

# column names + row indices
data[["col1", "col2", "col3"]].iloc[[row1_index, row2_index, row3_index]]

# column indices + row names
data.iloc[:, [col1_index, col2_index, col3_index]].loc[["row1", "row2", "row3"]]
```

7\. Accede a un subconjunto de rangos de filas y columnas

```python
# by name
data.loc["row1":"row2", "col1":"col2"]

# by index
data.iloc[row1_index:row2_index, col1_index:col2_index]

# column names + row indices
data.loc[:, "col1_name":"col2_name"].iloc[row1_index:row2_index]

# column indices + row names
data.iloc[:, col1_index:col2_index].loc["row1":"row2"]
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Explorar los métodos disponibles utilizando la función `dir()`

Python incluye una función `dir()` que se puede utilizar para mostrar todos los métodos
disponibles (funciones) que están incorporados en un objeto de datos. En el Episodio 4,
utilizamos algunos métodos con una cadena. Pero podemos ver muchos más disponibles
usando `dir()`:

```python
my_string = 'Hello world!'   # creation of a string object 
dir(my_string)
```

Este comando devuelve:

```python
['__add__',
...
'__subclasshook__',
'capitalize',
'casefold',
'center',
...
'upper',
'zfill']
```

Puede utilizar `help()` o <kbd>Shift</kbd>\+<kbd>Tab</kbd> para obtener más información
sobre lo que hacen estos métodos.

Supongamos que se ha importado Pandas y se han cargado los datos del PIB de Gapminder
para Europa como `data`. A continuación, utilice `dir()` para encontrar la función que
imprime la mediana del PIB per cápita en todos los países europeos para cada año en que
la información está disponible.

::::::::::::::: solution

## Solución

Entre muchas opciones, `dir()` lista la función `median()` como una posibilidad. Por lo
tanto

```python
data.median()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Interpretación

Las fronteras de Polonia han sido estables desde 1945, pero cambiaron varias veces en
los años anteriores. ¿Cómo gestionaría esta situación si estuviera creando una tabla del
PIB per cápita de Polonia para todo el siglo XX?


::::::::::::::::::::::::::::::::::::::::::::::::::

[pandas-dataframe]:
https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html
[pandas-series]:
https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html
[numpy]: https://www.numpy.org/


:::::::::::::::::::::::::::::::::::::::: keypoints

- Usa `DataFrame.iloc[..., ...]` para seleccionar valores por posición entera.
- Use `:` solo para significar todas las columnas o todas las filas.
- Selecciona múltiples columnas o filas usando `DataFrame.loc` y una rebanada con
  nombre.
- El resultado del corte puede usarse en operaciones posteriores.
- Utiliza comparaciones para seleccionar datos en función de su valor.
- Selecciona valores o NaN usando una máscara booleana.

::::::::::::::::::::::::::::::::::::::::::::::::::



