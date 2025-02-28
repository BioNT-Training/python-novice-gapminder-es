---
title: Lectura de datos tabulares en DataFrames
teaching: 10
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Importa la biblioteca Pandas.
- Utiliza Pandas para cargar un simple conjunto de datos CSV.
- Obtiene información básica sobre un Pandas DataFrame.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo puedo leer datos tabulares?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Utiliza la librería Pandas para realizar estadísticas sobre datos tabulares.

- [Pandas](https://pandas.pydata.org/) es una biblioteca de Python ampliamente utilizada
  para estadísticas, en particular sobre datos tabulares.
- Toma prestadas muchas características de los marcos de datos de R.
  - Una tabla bidimensional cuyas columnas tienen nombres y potencialmente tienen
    diferentes tipos de datos.
- Cargar Pandas con `import pandas as pd`. El alias `pd` se utiliza comúnmente para
  referirse a la biblioteca Pandas en código.
- Leer un fichero de datos de valores separados por comas (CSV) con `pd.read_csv`.
  - Argumento es el nombre del fichero a leer.
  - Devuelve un marco de datos que se puede asignar a una variable

```python
import pandas as pd

data_oceania = pd.read_csv('data/gapminder_gdp_oceania.csv')
print(data_oceania)
```

```output
       country  gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  \
0    Australia     10039.59564     10949.64959     12217.22686
1  New Zealand     10556.57566     12247.39532     13175.67800

   gdpPercap_1967  gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  \
0     14526.12465     16788.62948     18334.19751     19477.00928
1     14463.91893     16046.03728     16233.71770     17632.41040

   gdpPercap_1987  gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  \
0     21888.88903     23424.76683     26997.93657     30687.75473
1     19007.19129     18363.32494     21050.41377     23189.80135

   gdpPercap_2007
0     34435.36744
1     25185.00911
```

- Las columnas de un marco de datos son las variables observadas y las filas son las
  observaciones.
- Pandas utiliza la barra invertida `\` para mostrar las líneas envueltas cuando la
  salida es demasiado ancha para caber en la pantalla.
- El uso de nombres descriptivos para los marcos de datos nos ayuda a distinguir entre
  varios marcos de datos para que no sobrescribamos accidentalmente un marco de datos o
  leamos de uno equivocado.

::::::::::::::::::::::::::::::::::::::::: callout

## Archivo no encontrado

Nuestras lecciones almacenan sus ficheros de datos en un subdirectorio `data`, por lo
que la ruta al fichero es `data/gapminder_gdp_oceania.csv`. Si olvida incluir `data/`, o
si lo incluye pero su copia del fichero está en otro lugar, obtendrá un [error de
ejecución](04-built-in.md) que termina con una línea como esta:

```error
FileNotFoundError: [Errno 2] No such file or directory: 'data/gapminder_gdp_oceania.csv'
```

::::::::::::::::::::::::::::::::::::::::::::::::::

## Utilice `index_col` para especificar que los valores de una columna deben utilizarse como encabezamientos de fila.

- Los títulos de las filas son números (0 y 1 en este caso).
- Realmente quiero indexar por país.
- Para ello, pase el nombre de la columna a `read_csv` como parámetro `index_col`.
- Al nombrar el marco de datos `data_oceania_country` nos indica qué región incluyen los
  datos (`oceania`) y cómo están indexados (`country`).

```python
data_oceania_country = pd.read_csv('data/gapminder_gdp_oceania.csv', index_col='country')
print(data_oceania_country)
```

```output
             gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  gdpPercap_1967  \
country
Australia       10039.59564     10949.64959     12217.22686     14526.12465
New Zealand     10556.57566     12247.39532     13175.67800     14463.91893

             gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  gdpPercap_1987  \
country
Australia       16788.62948     18334.19751     19477.00928     21888.88903
New Zealand     16046.03728     16233.71770     17632.41040     19007.19129

             gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  gdpPercap_2007
country
Australia       23424.76683     26997.93657     30687.75473     34435.36744
New Zealand     18363.32494     21050.41377     23189.80135     25185.00911
```

## Utilice el método `DataFrame.info()` para obtener más información sobre un marco de datos.

```python
data_oceania_country.info()
```

```output
<class 'pandas.core.frame.DataFrame'>
Index: 2 entries, Australia to New Zealand
Data columns (total 12 columns):
gdpPercap_1952    2 non-null float64
gdpPercap_1957    2 non-null float64
gdpPercap_1962    2 non-null float64
gdpPercap_1967    2 non-null float64
gdpPercap_1972    2 non-null float64
gdpPercap_1977    2 non-null float64
gdpPercap_1982    2 non-null float64
gdpPercap_1987    2 non-null float64
gdpPercap_1992    2 non-null float64
gdpPercap_1997    2 non-null float64
gdpPercap_2002    2 non-null float64
gdpPercap_2007    2 non-null float64
dtypes: float64(12)
memory usage: 208.0+ bytes
```

- Se trata de un `DataFrame`
- Dos filas llamadas `'Australia'` y `'New Zealand'`
- Doce columnas, cada una de las cuales tiene dos valores reales en coma flotante de 64
  bits.
  - Más adelante hablaremos de los valores nulos, que se utilizan para representar las
    observaciones que faltan.
- Utiliza 208 bytes de memoria.

## La variable `DataFrame.columns` almacena información sobre las columnas del marco de datos.

- Nótese que se trata de datos, *no* de un método. (No tiene paréntesis)
  - Como `math.pi`.
  - Así que no use `()` para intentar llamarlo.
- Llamada *variable miembro*, o simplemente *miembro*.

```python
print(data_oceania_country.columns)
```

```output
Index(['gdpPercap_1952', 'gdpPercap_1957', 'gdpPercap_1962', 'gdpPercap_1967',
       'gdpPercap_1972', 'gdpPercap_1977', 'gdpPercap_1982', 'gdpPercap_1987',
       'gdpPercap_1992', 'gdpPercap_1997', 'gdpPercap_2002', 'gdpPercap_2007'],
      dtype='object')
```

## Utilice `DataFrame.T` para transponer un marco de datos.

- A veces se desea tratar las columnas como filas y viceversa.
- Transponer (escrito `.T`) no copia los datos, sólo cambia la visión que el programa
  tiene de ellos.
- Al igual que `columns`, es una variable miembro.

```python
print(data_oceania_country.T)
```

```output
country           Australia  New Zealand
gdpPercap_1952  10039.59564  10556.57566
gdpPercap_1957  10949.64959  12247.39532
gdpPercap_1962  12217.22686  13175.67800
gdpPercap_1967  14526.12465  14463.91893
gdpPercap_1972  16788.62948  16046.03728
gdpPercap_1977  18334.19751  16233.71770
gdpPercap_1982  19477.00928  17632.41040
gdpPercap_1987  21888.88903  19007.19129
gdpPercap_1992  23424.76683  18363.32494
gdpPercap_1997  26997.93657  21050.41377
gdpPercap_2002  30687.75473  23189.80135
gdpPercap_2007  34435.36744  25185.00911
```

## Utilice `DataFrame.describe()` para obtener estadísticas resumidas sobre los datos.

`DataFrame.describe()` obtiene las estadísticas de resumen sólo de las columnas que
tienen datos numéricos. Todas las demás columnas se ignoran, a menos que se utilice el
argumento `include='all'`.

```python
print(data_oceania_country.describe())
```

```output
       gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  gdpPercap_1967  \
count        2.000000        2.000000        2.000000        2.000000
mean     10298.085650    11598.522455    12696.452430    14495.021790
std        365.560078      917.644806      677.727301       43.986086
min      10039.595640    10949.649590    12217.226860    14463.918930
25%      10168.840645    11274.086022    12456.839645    14479.470360
50%      10298.085650    11598.522455    12696.452430    14495.021790
75%      10427.330655    11922.958888    12936.065215    14510.573220
max      10556.575660    12247.395320    13175.678000    14526.124650

       gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  gdpPercap_1987  \
count         2.00000        2.000000        2.000000        2.000000
mean      16417.33338    17283.957605    18554.709840    20448.040160
std         525.09198     1485.263517     1304.328377     2037.668013
min       16046.03728    16233.717700    17632.410400    19007.191290
25%       16231.68533    16758.837652    18093.560120    19727.615725
50%       16417.33338    17283.957605    18554.709840    20448.040160
75%       16602.98143    17809.077557    19015.859560    21168.464595
max       16788.62948    18334.197510    19477.009280    21888.889030

       gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  gdpPercap_2007
count        2.000000        2.000000        2.000000        2.000000
mean     20894.045885    24024.175170    26938.778040    29810.188275
std       3578.979883     4205.533703     5301.853680     6540.991104
min      18363.324940    21050.413770    23189.801350    25185.009110
25%      19628.685413    22537.294470    25064.289695    27497.598692
50%      20894.045885    24024.175170    26938.778040    29810.188275
75%      22159.406358    25511.055870    28813.266385    32122.777857
max      23424.766830    26997.936570    30687.754730    34435.367440
```

- No es especialmente útil con sólo dos registros, pero sí cuando hay miles.

::::::::::::::::::::::::::::::::::::::: challenge

## Lectura de otros datos

Leer los datos de `gapminder_gdp_americas.csv` (que deben estar en el mismo directorio
que `gapminder_gdp_oceania.csv`) en una variable llamada `data_americas` y mostrar sus
estadísticas de resumen.

::::::::::::::: solution

## Solución

Para leer un CSV, utilizamos `pd.read_csv` y le pasamos el nombre de fichero
`'data/gapminder_gdp_americas.csv'`. También volvemos a pasar el nombre de columna
`'country'` al parámetro `index_col` para indexar por países. Las estadísticas resumidas
pueden visualizarse con el método `DataFrame.describe()`.

```python
data_americas = pd.read_csv('data/gapminder_gdp_americas.csv', index_col='country')
data_americas.describe()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Inspección de datos

Después de leer los datos de América, utiliza `help(data_americas.head)` y
`help(data_americas.tail)` para averiguar qué hacen `DataFrame.head` y `DataFrame.tail`.

1. ¿Qué llamada al método mostrará las tres primeras filas de estos datos?
2. ¿Qué método mostrará las tres últimas columnas de estos datos? (Sugerencia: es
   posible que tengas que cambiar la vista de los datos)

::::::::::::::: solution

## Solución

1. Podemos ver las cinco primeras filas de `data_americas` ejecutando
   `data_americas.head()` que nos permite ver el principio del DataFrame. Podemos
   especificar el número de filas que deseamos ver especificando el parámetro `n` en
   nuestra llamada a `data_americas.head()`. Para ver las tres primeras filas, ejecute:

  ```python
  data_americas.head(n=3)
  ```

  ```output
            continent  gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  \
  country
  Argentina  Americas     5911.315053     6856.856212     7133.166023
  Bolivia    Americas     2677.326347     2127.686326     2180.972546
  Brazil     Americas     2108.944355     2487.365989     3336.585802

            gdpPercap_1967  gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  \
  country
  Argentina     8052.953021     9443.038526    10079.026740     8997.897412
  Bolivia       2586.886053     2980.331339     3548.097832     3156.510452
  Brazil        3429.864357     4985.711467     6660.118654     7030.835878

             gdpPercap_1987  gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  \
  country
  Argentina     9139.671389     9308.418710    10967.281950     8797.640716
  Bolivia       2753.691490     2961.699694     3326.143191     3413.262690
  Brazil        7807.095818     6950.283021     7957.980824     8131.212843

             gdpPercap_2007
  country
  Argentina    12779.379640
  Bolivia       3822.137084
  Brazil        9065.800825
  ```

2. Para consultar las tres últimas filas de `data_americas`, utilizaríamos el comando,
   `americas.tail(n=3)`, análogo a `head()` utilizado anteriormente. Sin embargo, aquí
   queremos ver las tres últimas columnas, así que tenemos que cambiar la vista y
   utilizar `tail()`. Para ello, creamos un nuevo DataFrame en el que se intercambian
   filas y columnas:

  ```python
  americas_flipped = data_americas.T
  ```

Podemos ver las tres últimas columnas de `americas` viendo las tres últimas filas de
`americas_flipped`:

  ```python
  americas_flipped.tail(n=3)
  ```

  ```output
  country        Argentina  Bolivia   Brazil   Canada    Chile Colombia  \
  gdpPercap_1997   10967.3  3326.14  7957.98  28954.9  10118.1  6117.36
  gdpPercap_2002   8797.64  3413.26  8131.21    33329  10778.8  5755.26
  gdpPercap_2007   12779.4  3822.14   9065.8  36319.2  13171.6  7006.58

  country        Costa Rica     Cuba Dominican Republic  Ecuador    ...     \
  gdpPercap_1997    6677.05  5431.99             3614.1  7429.46    ...
  gdpPercap_2002    7723.45  6340.65            4563.81  5773.04    ...
  gdpPercap_2007    9645.06   8948.1            6025.37  6873.26    ...

  country          Mexico Nicaragua   Panama Paraguay     Peru Puerto Rico  \
  gdpPercap_1997   9767.3   2253.02  7113.69   4247.4  5838.35     16999.4
  gdpPercap_2002  10742.4   2474.55  7356.03  3783.67  5909.02     18855.6
  gdpPercap_2007  11977.6   2749.32  9809.19  4172.84  7408.91     19328.7

  country        Trinidad and Tobago United States  Uruguay Venezuela
  gdpPercap_1997             8792.57       35767.4  9230.24   10165.5
  gdpPercap_2002             11460.6       39097.1     7727   8605.05
  gdpPercap_2007             18008.5       42951.7  10611.5   11415.8
  ```

Muestra los datos que deseamos, pero es posible que prefiramos mostrar tres columnas en
lugar de tres filas, por lo que podemos darle la vuelta:

  ```python
  americas_flipped.tail(n=3).T    
  ```

**Nota:** podríamos haber hecho lo anterior en una sola línea de código "encadenando"
los comandos:

  ```python
  data_americas.T.tail(n=3).T
  ```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Lectura de ficheros en otros directorios

Los datos de su proyecto actual están almacenados en un archivo llamado `microbes.csv`,
que se encuentra en una carpeta llamada `field_data`. Usted está haciendo el análisis en
un cuaderno llamado `analysis.ipynb` en una carpeta hermana llamada `thesis`:

```output
your_home_directory
+-- field_data/
|   +-- microbes.csv
+-- thesis/
    +-- analysis.ipynb
```

¿Qué valor(es) debe pasar a `read_csv` para leer `microbes.csv` en `analysis.ipynb`?

::::::::::::::: solution

## Solución

Necesitamos especificar la ruta al fichero de interés en la llamada a `pd.read_csv`.
Primero tenemos que "saltar" fuera de la carpeta `thesis` utilizando '../' y luego a la
carpeta `field_data` utilizando `data_campo/'. A continuación, podemos especificar el
nombre de archivo `microbes.csv. El resultado es el siguiente:

```python
data_microbes = pd.read_csv('../field_data/microbes.csv')
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Datos de escritura

Además de la función `read_csv` para leer datos de un fichero, Pandas proporciona una
función `to_csv` para escribir dataframes en ficheros. Aplicando lo que has aprendido
sobre la lectura de archivos, escribe uno de tus dataframes en un archivo llamado
`processed.csv`. Puedes utilizar `help` para obtener información sobre cómo utilizar
`to_csv`.

::::::::::::::: solution

## Solución

Para escribir el DataFrame `data_americas` en un fichero llamado `processed.csv`,
ejecute el siguiente comando:

```python
data_americas.to_csv('processed.csv')
```

Para obtener ayuda sobre `read_csv` o `to_csv`, puede ejecutar, por ejemplo:

```python
help(data_americas.to_csv)
help(pd.read_csv)
```

Observe que `help(to_csv)` o `help(pd.to_csv)` dan error Esto se debe a que `to_csv` no
es una función global de Pandas, sino una función miembro de DataFrames. Esto significa
que sólo se puede llamar en una instancia de un DataFrame, por ejemplo,
`data_americas.to_csv` o `data_oceania.to_csv`



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Utiliza la librería Pandas para obtener estadísticas básicas a partir de datos
  tabulares.
- Utilice `index_col` para especificar que los valores de una columna deben utilizarse
  como encabezamientos de fila.
- Utilice `DataFrame.info` para obtener más información sobre un marco de datos.
- La variable `DataFrame.columns` almacena información sobre las columnas del marco de
  datos.
- Utilice `DataFrame.T` para transponer un marco de datos.
- Utilice `DataFrame.describe` para obtener estadísticas resumidas sobre los datos.

::::::::::::::::::::::::::::::::::::::::::::::::::



