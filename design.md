---
title: Diseño de la lección
---


::::::::::::::::::::::::::::::::::::::::: callout

## Se busca ayuda

**Estamos rellenando los ejercicios [abajo](#etapa-3-plan-de-aprendizaje) para concretar
el plan de la lección. Las contribuciones (tanto en forma de pull requests con
ejercicios rellenados, como comentarios sobre ejercicios específicos, ordenación y
tiempos) son muy apreciadas.**


::::::::::::::::::::::::::::::::::::::::::::::::::

## Proceso utilizado

> El consejo de Michael Pollan si enseñara a programar en R o Python:
> 
> 1. Escribir código.
> 2. No demasiado.
> 3. La mayoría de los conjuntos.
> 
> — [Michael Koontz](https://twitter.com/_mikoontz/status/758021742078025728) {:
> .quotation}
> 

Esta lección fue desarrollada utilizando una variante reducida del proceso "Comprender
Diseñando". Las secciones principales son:

1. Suposiciones sobre audiencia, tiempo, etc. (El borrador actual también incluye
   algunas conclusiones y decisiones en esta sección - que deberían ser refactorizadas)

2. Resultados deseados: objetivos generales, evaluaciones sumativas con una granularidad
   de medio día, lo que los alumnos serán capaces de hacer, lo que los alumnos sabrán.

3. Plan de aprendizaje: cada episodio tiene un título que resume lo que se va a tratar,
   luego se estima el tiempo que se dedicará a la enseñanza y a los ejercicios, mientras
   que los ejercicios se dan en forma de viñetas.

## Etapa 1: Supuestos

- Audiencia
  - Estudiantes de posgrado en disciplinas numéricas desde cosmología a arqueología
  - Que han manipulado datos en hojas de cálculo y con herramientas interactivas como
    SAS
  - Pero *no* han programado más allá de CPD (copy-paste-despair)
- Restricciones
  - Un día completo 09:00-16:30
    - 06:15 hora de clase
    - 0:45 almuerzo
    - 0:30 total para dos pausas café
  - Los alumnos utilizan instalaciones nativas en sus propias máquinas
    - Puede usar VMs o recursos en la nube a discreción del instructor
    - Pero debe mantener la instalación local nativa como opción
  - Sin dependencia de otros módulos de Carpentry
    - En particular, no requiere conocimientos de shell o control de versiones
  - Utilizar el Jupyter Notebook
    - Auténtica herramienta utilizada por muchos instructores
    - No hay realmente una alternativa
    - Y significa que incluso la gente que ha visto un poco de Python antes
      probablemente aprenderá algo
- Ejemplo Motivador
  - Creación de gráficos 2D adecuados para su inclusión en artículos
  - Atrae a casi todo el mundo
  - Hace que la lección pueda ser utilizada tanto por Carpentries
    - Y significa que incluso la gente que ha visto un poco de Python antes
      probablemente aprenderá algo
- Datos
  - Utilizar los datos de gapminder en todo el proceso
  - Pero dividir en múltiples archivos por continente
    - Para hacer más ordenada la salida de los ejemplos (por ejemplo, usar
      Australia/Nueva Zelanda, que son sólo dos líneas)
    - Y permitir ejemplos que muestren el uso de conjuntos de datos múltiples
- Centrarse en Pandas en lugar de NumPy
  - Hace que la lección pueda ser utilizada tanto por Carpintería de Datos como por
    Carpintería de Software
  - Es probable que los principiantes genuinos quieran análisis de datos
  - Y personas con alguna experiencia previa:
    - aceptará el análisis de datos como tarea auténtica,
    - y es poco probable que se hayan encontrado con Pandas, por lo que obtendrán algo
      útil de la lección
- Los retos serán en su mayoría *no* "escribir este código desde cero"
  - Quieres muchos ejercicios cortos que se puedan terminar en el tiempo asignado
  - Así que usa MCQs, rellena los espacios en blanco, Problemas de Parsons, "retoca este
    código", etc.

## Etapa 2: Resultados deseados

### Preguntas

Cómo puedo...

- ...¿leer datos tabulares?
- ...¿trazar un único vector de valores?
- ...¿crear un gráfico de series temporales?
- ...¿crear un gráfico para cada uno de los conjuntos de datos?
- ...¿obtener datos extra de un único conjunto de datos para trazar?
- ...escribir programas que pueda leer y reutilizar en el futuro?

### Habilidades

Puedo...

- ...escribir scripts cortos usando bucles y condicionales.
- ...escribir funciones con un número fijo de parámetros que devuelvan un único
  resultado.
- ...importar bibliotecas usando alias y referirse a los contenidos de esas bibliotecas.
- ...realizar extracciones y formateos sencillos de datos utilizando Pandas.

### Conceptos

Sé...

- ...que un programa es un equipo de laboratorio que implementa un análisis
  - Necesita ser validado/calibrado antes/durante su uso
  - Hace que el análisis sea reproducible, revisable y compartible
- ...que los programas se escriben para las personas, no para los ordenadores
  - Nombres de variables con sentido
  - Modularidad para facilitar la lectura y la reutilización
  - Sin duplicación
  - Propósito y uso del documento
- ...que no hay magia: los programas que utilizan no difieren en principio de los que
  construyen
- ...cómo asignar valores a variables
- ...qué son enteros, flotantes, cadenas, arrays NumPy y dataframes Pandas
- ...cómo trazar la ejecución de un bucle `for`
- ...cómo rastrear la ejecución de sentencias `if`/`else`
- ...cómo crear e indexar listas
- ...cómo crear e indexar matrices NumPy
- ...cómo crear e indexar dataframes Pandas
- ...cómo crear gráficos de series temporales
- ...la diferencia entre definir y llamar a una función
- ...donde encontrar documentación sobre bibliotecas estándar
- ...cómo averiguar qué más ofrece Python científico

## Etapa 3: Plan de aprendizaje

### Evaluación Sumativa

- Midpoint: crea un gráfico de series temporales para cada fichero de un directorio.
- Final: extraer datos de Pandas dataframe y crear un gráfico comparativo de series
  temporales multilínea.

### [Ejecutar y salir de forma interactiva](../episodes/01-run-quit.md) (9:00)

- Enseñanza: 15 min (por problemas de configuración)
  - Inicia Jupyter Notebook, crea nuevos cuadernos y sal del cuaderno.
  - Crear celdas Markdown en un cuaderno.
  - Crear y ejecutar celdas Python en un cuaderno.
- Desafíos: 0 min (contabilizado en el tiempo de enseñanza - sin ejercicio separado)
  - Creación de listas en Markdown
  - ¿Qué aparece cuando se ponen varias expresiones en una misma celda?
  - Cambiar una celda existente de código a Markdown
  - Renderización de ecuaciones estilo LaTeX

### [Variables y Asignación](../episodios/02-variables.md) (9:15)

- Enseñanza: 10 min
  - Escribir programas que asignen valores escalares a variables y realicen cálculos con
    esos valores.
  - Trazar correctamente cambios de valor en programas que usan asignación escalar.
- Desafíos: 10 min
  - Trazar la ejecución de un código que intercambia dos valores utilizando una variable
    intermedia.
  - Predecir valores finales de variables después de varias asignaciones.
  - ¿Qué ocurre si intentas indexar un número?
  - ¿Cuál es mejor nombre de variable, `m`, `min`, o `minutes`?
  - ¿Qué producen las siguientes expresiones de troceo?

### [Tipos de datos y conversión de tipos](../episodes/03-types-conversion.md) (09:35)

- Enseñanza: 10 min
  - Explicar las diferencias clave entre números enteros y números de coma flotante.
  - Explicar las diferencias clave entre números y cadenas de caracteres.
  - Utilizar funciones incorporadas para convertir entre enteros, números de coma
    flotante y cadenas.
- Desafíos: 10 min
  - ¿Qué tipo de valor es 3.4?
  - ¿Qué tipo de valor es 3.25 + 4?
  - ¿Qué tipo de valor utilizarías para representar:
    - Número de días transcurridos desde el comienzo del año.
    - Tiempo transcurrido desde el comienzo del año.
    - Etc.
  - ¿Cómo puedes usar `//` (división entera) y `%` (módulo)?
  - ¿Qué hace `int("3.4")`?
  - Dados estos valores float, int y string, ¿qué expresiones imprimirán un resultado
    particular?
  - ¿Qué esperas que produzca `1+2j + 3`?

### [Funciones incorporadas y ayuda](../episodios/04-built-in.md) (09:55)

- Enseñanza: 15 min
  - Explicar el propósito de las funciones.
  - Llamar correctamente a funciones incorporadas de Python.
  - Anidar correctamente llamadas a funciones incorporadas.
  - Utilizar la ayuda para mostrar la documentación de las funciones incorporadas.
  - Describir correctamente situaciones en las que se producen SyntaxError y NameError.
- Desafíos: 10 min
  - Explique el orden de las operaciones en la siguiente expresión compleja.
  - ¿Qué producirá cada combinación anidada de llamadas `min` y `max`?
  - ¿Por qué `max` y `min` no devuelven `None` cuando no se les dan argumentos?
  - Dado lo que hemos visto hasta ahora, ¿qué expresión de índice obtendrá el último
    carácter de una cadena?

### [Café](../episodios/05-café.md): 15 min (10:20)

### [Bibliotecas](../episodios/06-libraries.md) (10:35)

- Enseñanza: 10 min
  - Explicar qué son las bibliotecas de software y por qué los programadores las crean y
    utilizan.
  - Escribir programas que importen y utilicen librerías de la librería estándar de
    Python.
  - Buscar y leer documentación de bibliotecas estándar de forma interactiva (en el
    intérprete) y en línea.
- Desafíos: 10 min
  - ¿Qué función de la biblioteca matemática estándar podrías usar para calcular una
    raíz cuadrada?
  - ¿Qué librería utilizarías para seleccionar un valor aleatorio a partir de datos?
  - Si `help(math)` produce un error, ¿qué ha olvidado hacer?
  - Rellene los espacios en blanco en el código de abajo para que la sentencia import y
    el programa se ejecuten.

### [Lectura de datos tabulares](../episodios/07-lectura-tabular.md) (10:55)

- Enseñanza: 10 min
  - Importa la librería Pandas.
  - Utilizar Pandas para cargar un simple conjunto de datos CSV.
  - Obtener información básica sobre un DataFrame de Pandas.
- Desafíos: 10 min
  - Leer los datos de las Américas y mostrar sus estadísticas resumidas.
  - ¿Qué hacen `.head` y `.tail`?
  - ¿Qué cadena(s) debes pasar a `read_csv` para leer archivos de otros directorios?
  - ¿Cómo puedes *escribir* datos CSV?

### [DataFrames](../episodios/08-data-frames.md) (11:15)

- Enseñanza: 15 min
  - Seleccionar valores individuales de un dataframe Pandas.
  - Selecciona filas enteras o columnas enteras de un marco de datos.
  - Seleccionar un subconjunto de filas y columnas de un marco de datos en una sola
    operación.
  - Seleccionar un subconjunto de un marco de datos mediante un único criterio booleano.
- Desafíos: 15 min
  - Escribe una expresión para encontrar el PIB Per Capita de Serbia en 2007.
  - ¿Qué regla gobierna lo que se incluye (o no) en los slices numéricos y con nombre en
    Pandas?
  - ¿Qué hace cada línea del siguiente programa corto?
  - ¿Qué hacen `idxmin` y `idxmax`?
  - Escribe expresiones para obtener el PIB per cápita de todos los países en 1982, de
    todos los países *después* de 1985, etc.
  - Teniendo en cuenta cómo han cambiado sus fronteras desde 1900, ¿qué harías si te
    pidieran que crearas una tabla del PIB per cápita de Polonia para el Siglo XX?

### [Plotting](../episodios/09-plotting.md) (11:45)

- Enseñanza: 15 min
  - Crear un gráfico de series temporales que muestre un único conjunto de datos.
  - Crear un gráfico de dispersión que muestre la relación entre dos conjuntos de datos.
- Ejercicio: 15 min
  - Rellena los espacios en blanco para trazar el PIB per cápita mínimo a lo largo del
    tiempo para los países europeos.
  - Modifique el ejemplo para crear un gráfico de dispersión del PIB per cápita en los
    países asiáticos.
  - Explique qué hace cada argumento de `plot` en el siguiente ejemplo.

### [Almuerzo](../episodios/10-almuerzo.md) (12:15): 45 min

### [Listas](../episodios/11-listas.md) (13:00)

- Enseñanza: 10 min
  - Explicar por qué los programas necesitan colecciones de valores.
  - Escribir programas que creen listas planas, las indexen, las rebanen y las
    modifiquen mediante asignaciones y llamadas a métodos.
- Desafíos: 10 min
  - Rellene los espacios en blanco para que el programa produzca la salida mostrada.
  - ¿Qué tamaño tienen los siguientes trozos?
  - ¿Qué imprimen las expresiones de índice negativo?
  - ¿Qué hace un "stride" en un slice?
  - ¿Cómo tratan los trozos los límites fuera de rango?
  - ¿Cuáles son las diferencias entre ordenar de estas dos maneras?
  - ¿Cuál es la diferencia entre `new = old` y `new = old[:]`?

### [Bucles](../episodios/12-para-bucles.md) (13:20)

- Enseñanza: 10 min
  - Explique para qué se utilizan normalmente los bucles for.
  - Trazar la ejecución de un bucle simple (no anidado) e indicar correctamente los
    valores de las variables en cada iteración.
  - Escribir bucles for que utilicen el patrón Accumulator para agregar valores.
- Desafíos: 15 min
  - ¿Un error de sangría es un error de sintaxis o un error de ejecución?
  - Traza qué líneas de este programa se ejecutan y en qué orden.
  - Rellena los espacios en blanco de este programa para que invierta una cadena.
  - Rellena los espacios en blanco en esta serie de ejemplos para practicar la
    acumulación de valores.
  - Reordenar y sangrar estas líneas para calcular la suma acumulativa de los valores de
    la lista.

### [Condicionales](13-condicionales) (15:00)

- Enseñanza: 10 min
  - Escribir correctamente programas que utilicen sentencias if y else y expresiones
    booleanas simples (sin operadores lógicos).
  - Trazar la ejecución de condicionales no anidados y condicionales dentro de bucles.
- Desafíos: 15 min
  - Traza la ejecución de esta sentencia condicional.
  - Rellene los espacios en blanco para que esta función sustituya los valores negativos
    por ceros.
  - Modifica este programa para que sólo procese ficheros con menos de 50 registros.
  - Modifica este programa para que siempre encuentre los valores mayor y menor de una
    lista sin importar cuales sean los valores de la lista.

### [Looping Over Data Sets](14-looping-data-sets) (13:45)

- Enseñanza: 5 min
  - Ser capaz de leer y escribir expresiones globbing que coincidan con conjuntos de
    ficheros.
  - Usar glob para crear listas de archivos.
  - Escribir bucles for para realizar operaciones sobre ficheros dados sus nombres en
    una lista.
- Desafíos: 10 min
  - ¿Qué nombres de fichero *no* coinciden con esta expresión glob?
  - Modifica este programa para que imprima el número de registros en el fichero más
    corto.
  - Escribe un programa que lea y trace todos los conjuntos de datos regionales.

### [Café](15-café) (14:45): 15 min

### [Funciones de escritura](16-funciones-de-escritura) (14:00)

- Enseñanza: 10 min
  - Explicar e identificar la diferencia entre definición de función y llamada a
    función.
  - Escribe una función que tome un número pequeño y fijo de argumentos y produzca un
    único resultado.
- Desafíos: 15 min
  - Este código define y llama a una función - ¿qué imprime cuando se ejecuta?
  - Explique por qué este corto programa imprime las cosas en el orden en que lo hace.
  - Llene los espacios en blanco para crear una función que encuentre el valor mínimo en
    un archivo de datos.
  - Rellena los espacios en blanco para crear una función que encuentre el primer valor
    negativo de una lista. ¿Qué hace tu función si la lista está vacía?
  - ¿Por qué a veces es útil pasar argumentos nombrando los parámetros correspondientes?
  - Rellena los espacios en blanco y convierte este corto trozo de código en una
    función.

### [Ámbito variable](17-ámbito) (14:25)

- Enseñanza: 10 min
  - Identificar variables locales y globales.
  - Identificar parámetros como variables locales.
  - Leer un rastreo y determinar el archivo, función y número de línea en el que ocurrió
    el error.
- Desafíos: 10 min
  - Rastrea los cambios en los valores de este programa, teniendo cuidado de distinguir
    los valores locales de los globales.

### [Estilo de programación](18-estilo) (15:25)

- Enseñanza: 15 min
  - ¿Cómo puedo hacer mis programas más legibles?
  - ¿Cómo formatean su código la mayoría de los programadores?
  - ¿Cómo pueden los programas comprobar su propio funcionamiento?
- Desafíos: 15 min
  - ¿Qué líneas de este código estarán disponibles como ayuda en línea?
  - Convierte los comentarios de este programa en docstrings.
  - Reescribe este corto programa para que sea más legible.

### [Wrap-Up](19-wrap) (15:55)

- Enseñanza: 20 min
  - Nombrar y localizar sitios de la comunidad científica Python para software, talleres
    y ayuda.
- Desafíos: 0 min
  - Ninguno.

### [Feedback](20-feedback) (16:15)

- Enseñanza: 0 min
- Desafíos: 15 min
  - Recopilar información

### Finish (16:30)



