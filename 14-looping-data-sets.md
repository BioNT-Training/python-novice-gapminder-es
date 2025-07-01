---
title: Bucle sobre conjuntos de datos
teaching: 5
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Ser capaz de leer y escribir expresiones globbing que coincidan con conjuntos de
  ficheros.
- Utilice glob para crear listas de ficheros.
- Escribe bucles for para realizar operaciones sobre ficheros dados sus nombres en una
  lista.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo puedo procesar muchos conjuntos de datos con un solo comando?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Utiliza un bucle `for` para procesar ficheros dada una lista de sus nombres.

- Un nombre de fichero es una cadena de caracteres.
- Y las listas pueden contener cadenas de caracteres.

```python
import pandas as pd
for filename in ['data/gapminder_gdp_africa.csv', 'data/gapminder_gdp_asia.csv']:
    data = pd.read_csv(filename, index_col='country')
    print(filename, data.min())
```

```output
data/gapminder_gdp_africa.csv gdpPercap_1952    298.846212
gdpPercap_1957    335.997115
gdpPercap_1962    355.203227
gdpPercap_1967    412.977514
⋮ ⋮ ⋮
gdpPercap_1997    312.188423
gdpPercap_2002    241.165877
gdpPercap_2007    277.551859
dtype: float64
data/gapminder_gdp_asia.csv gdpPercap_1952    331
gdpPercap_1957    350
gdpPercap_1962    388
gdpPercap_1967    349
⋮ ⋮ ⋮
gdpPercap_1997    415
gdpPercap_2002    611
gdpPercap_2007    944
dtype: float64
```

## Use [`glob.glob`](https://docs.python.org/3/library/glob.html#glob.glob) para encontrar conjuntos de ficheros cuyos nombres coincidan con un patrón.

- En Unix, el término "globbing" significa "buscar un conjunto de ficheros con un
  patrón".
- Los patrones más comunes son:
  - `*` significa "coincide con cero o más caracteres"
  - `?` significa "coincide exactamente con un carácter"
- La librería estándar de Python contiene el módulo
  [`glob`](https://docs.python.org/3/library/glob.html) para proporcionar la
  funcionalidad de coincidencia de patrones
- El módulo [`glob`](https://docs.python.org/3/library/glob.html) contiene una función
  también llamada `glob` para encontrar patrones de ficheros
- Por ejemplo, `glob.glob('*.txt')` coincide con todos los ficheros del directorio
  actual cuyos nombres terminen en `.txt`.
- El resultado es una lista (posiblemente vacía) de cadenas de caracteres.

```python
import glob
print('all csv files in data directory:', glob.glob('data/*.csv'))
```

```output
all csv files in data directory: ['data/gapminder_all.csv', 'data/gapminder_gdp_africa.csv', \
'data/gapminder_gdp_americas.csv', 'data/gapminder_gdp_asia.csv', 'data/gapminder_gdp_europe.csv', \
'data/gapminder_gdp_oceania.csv']
```

```python
print('all PDB files:', glob.glob('*.pdb'))
```

```output
all PDB files: []
```

## Utilice `glob` y `for` para procesar lotes de ficheros.

- Ayuda mucho si los ficheros se nombran y almacenan de forma sistemática y consistente
  para que los patrones simples encuentren los datos correctos.

```python
for filename in glob.glob('data/gapminder_*.csv'):
    data = pd.read_csv(filename)
    print(filename, data['gdpPercap_1952'].min())
```

```output
data/gapminder_all.csv 298.8462121
data/gapminder_gdp_africa.csv 298.8462121
data/gapminder_gdp_americas.csv 1397.717137
data/gapminder_gdp_asia.csv 331.0
data/gapminder_gdp_europe.csv 973.5331948
data/gapminder_gdp_oceania.csv 10039.59564
```

- Incluye todos los datos, así como los datos por región.
- Utilice un patrón más específico en los ejercicios para excluir todo el conjunto de
  datos.
- Pero tenga en cuenta que el mínimo de todo el conjunto de datos es también el mínimo
  de uno de los conjuntos de datos, lo que es una buena comprobación de la corrección.

::::::::::::::::::::::::::::::::::::::: challenge

## Determinación de coincidencias

¿Cuál de estos ficheros *no* coincide con la expresión `glob.glob('data/*as*.csv')`?

1. `data/gapminder_gdp_africa.csv`
2. `data/gapminder_gdp_americas.csv`
3. `data/gapminder_gdp_asia.csv`

::::::::::::::: solution

## Solución

1 no coincide con el glob.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Tamaño mínimo de fichero

Modifica este programa para que imprima el número de registros del fichero que menos
registros tenga.

```python
import glob
import pandas as pd
fewest = ____
for filename in glob.glob('data/*.csv'):
    dataframe = pd.____(filename)
    fewest = min(____, dataframe.shape[0])
print('smallest file has', fewest, 'records')
```

Tenga en cuenta que el método [`DataFrame.shape()`][shape-method] devuelve una tupla con
el número de filas y columnas del marco de datos.

::::::::::::::: solution

## Solución

```python
import glob
import pandas as pd
fewest = float('Inf')
for filename in glob.glob('data/*.csv'):
    dataframe = pd.read_csv(filename)
    fewest = min(fewest, dataframe.shape[0])
print('smallest file has', fewest, 'records')
```

Puede que hayas elegido inicializar la variable `fewest` con un número mayor que los
números con los que estás tratando, pero eso podría traerte problemas si reutilizas el
código con números mayores. Python te permite usar infinito positivo, que funcionará sin
importar lo grandes que sean tus números. ¿Qué otras cadenas especiales reconoce la
función [`float`][float-function]?



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Comparación de datos

Escribe un programa que lea los conjuntos de datos regionales y represente el PIB per
cápita medio de cada región a lo largo del tiempo en un único gráfico. Pandas emitirá un
error si encuentra columnas no numéricas en el cálculo de un marco de datos, por lo que
es posible que tenga que filtrar esas columnas o decirle a pandas que las ignore.


::::::::::::::: solution

## Solución

Esta solución construye una leyenda útil utilizando el método [string `split`
method][split-method] para extraer el `region` de la ruta
'data/gapminder\_gdp\_a\_specific\_region.csv'.

```python
import glob
import pandas as pd
import matplotlib.pyplot as plt
fig, ax = plt.subplots(1,1)
for filename in glob.glob('data/gapminder_gdp*.csv'):
    dataframe = pd.read_csv(filename)
   # extraer <región> del nombre de archivo, que se espera en el formato 'data/gapminder_gdp_<region>.csv'  
   # dividiremos la cadena utilizando el método split y `_` como separador,  
   # recuperaremos la última cadena de la lista que devuelve split (`<region>.csv`),  
   # y luego eliminaremos la extensión `.csv` de esa cadena.  
   # NOTA: el módulo pathlib, que se cubre en el siguiente apartado, también ofrece  
  # abstracciones convenientes para trabajar con rutas del sistema de archivos y podría resolver esto también:
    # from pathlib import Path
    # region = Path(filename).stem.split('_')[-1]
    region = filename.split('_')[-1][:-4]
    # exreae los años de las columnas del dataframe
    headings = dataframe.columns[1:]
    years = headings.str.split('_').str.get(1)
    # pandas tira errores cuando se encuentra con columnas no-numŕeicas en la computación de un dataframe
    # pero podemos decir a pandas que los ignore con el parámetro 'numeric_only`
    dataframe.mean(numeric_only=True).plot(ax=ax, label=region)
    # NOTA: otra manera de hacer esto es seleccionar solo las columnas con gdp en su nombre utilizando el método de filtraje
    # dataframe.filter(like="gdp").mean().plot(ax=ax, label=region)
# set the title and labels
ax.set_title('GDP Per Capita for Regions Over Time')
ax.set_xticks(range(len(years)))
ax.set_xticklabels(years)
ax.set_xlabel('Year')
plt.tight_layout()
plt.legend()
plt.show()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Tratamiento de rutas de ficheros

El módulo [`pathlib`][pathlib-module] proporciona abstracciones útiles para la
manipulación de ficheros y rutas, como devolver el nombre de un fichero sin la
extensión. Esto es muy útil cuando se realiza un bucle sobre archivos y directorios. En
el siguiente ejemplo, creamos un objeto `Path` e inspeccionamos sus atributos.

```python
from pathlib import Path

p = Path("data/gapminder_gdp_africa.csv")
print(p.parent)
print(p.stem)
print(p.suffix)
```

```output
data
gapminder_gdp_africa
.csv
```

**Pista:** Comprueba todos los atributos y métodos disponibles en el objeto `Path` con
la función `dir()`.


::::::::::::::::::::::::::::::::::::::::::::::::::

[shape-method]:
https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.shape.html
[float-function]: https://docs.python.org/3/library/functions.html#float
[split-method]: https://docs.python.org/3/library/stdtypes.html#str.split
[pathlib-module]: https://docs.python.org/3/library/pathlib.html


:::::::::::::::::::::::::::::::::::::::: keypoints

- Utiliza un bucle `for` para procesar ficheros a partir de una lista de nombres.
- Utilice `glob.glob` para encontrar conjuntos de ficheros cuyos nombres coincidan con
  un patrón.
- Utilice `glob` y `for` para procesar lotes de ficheros.

::::::::::::::::::::::::::::::::::::::::::::::::::



