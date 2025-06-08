---
title: Ejecutar y salir
teaching: 15
exercises: 0
---


::::::::::::::::::::::::::::::::::::::: objectives

- Inicia el servidor de JupyterLab.
- Crea un nuevo script Python.
- Crea un cuaderno Jupyter.
- Apaga el servidor de JupyterLab.
- Comprender la diferencia entre un script Python y un cuaderno Jupyter.
- Crea celdas Markdown en un cuaderno.
- Crear y ejecutar celdas de Python en un cuaderno.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Cómo puedo ejecutar programas Python?

::::::::::::::::::::::::::::::::::::::::::::::::::

Para ejecutar Python, vamos a utilizar [Jupyter Notebooks][jupyter] a través de
[JupyterLab][jupyterlab] para el resto de este taller. Los cuadernos Jupyter son comunes
en la ciencia de datos y visualización, y sirven como una experiencia conveniente para
ejecutar código Python de forma interactiva donde podemos ver y compartir fácilmente los
resultados de nuestro código Python.

Existen otras formas de editar, gestionar y ejecutar código. Los desarrolladores de
software suelen utilizar un entorno de desarrollo integrado (IDE) como
[PyCharm](https://www.jetbrains.com/pycharm/) o [Visual Studio
Code](https://code.visualstudio.com/), o editores de texto como Vim o Emacs, para crear
y editar sus programas Python. Después de editar y guardar sus programas Python puede
ejecutar esos programas dentro del propio IDE o directamente en la línea de comandos. En
cambio, los cuadernos Jupyter nos permiten ejecutar y ver los resultados de nuestro
código Python inmediatamente dentro del cuaderno.

JupyterLab tiene otras funciones muy útiles:

- Puedes escribir, editar y copiar y pegar fácilmente bloques de código.
- En pestaña completa te permite acceder fácilmente a los nombres de las cosas que estás
  utilizando y aprender más sobre ellas.
- Te permite anotar tu código con enlaces, texto de distinto tamaño, viñetas, etc. para
  hacerlo más accesible a ti y a tus colaboradores.
- Te permite mostrar figuras junto al código que las produce para contar una historia
  completa del análisis.

Cada cuaderno contiene una o más celdas que contienen código, texto o imágenes.

## Introducción a JupyterLab

JupyterLab es un servidor de aplicaciones con interfaz web de usuario del [Proyecto
Jupyter][jupyter] que permite trabajar con documentos y actividades como cuadernos
Jupyter, editores de texto, terminales e incluso componentes personalizados de forma
flexible, integrada y extensible. JupyterLab requiere un navegador razonablemente
actualizado (idealmente una versión actual de Chrome, Safari o Firefox); las versiones 9
e inferiores de Internet Explorer *no* son compatibles.

JupyterLab se incluye como parte de la distribución Anaconda Python. Si aún no has
instalado la distribución Anaconda Python, consulta [las instrucciones de
instalación](../learners/setup.md) para obtener instrucciones de instalación.

En esta lección ejecutaremos JupyterLab localmente en nuestras propias máquinas, por lo
que no será necesaria una conexión a Internet aparte de la conexión inicial para
descargar e instalar Anaconda y JupyterLab

- Inicia el servidor de JupyterLab en tu máquina
- Utiliza un navegador web para abrir una URL localhost especial que conecte con tu
  servidor JupyterLab
- El servidor de JupyterLab hace el trabajo y el navegador web muestra el resultado
- Escriba código en el navegador y vea los resultados después de que su servidor
  JupyterLab haya terminado de ejecutar su código

::::::::::::::::::::::::::::::::::::::::: callout

## ¿JupyterLab? ¿Y para los cuadernos Jupyter?

JupyterLab es la [siguiente etapa en la evolución del Jupyter
Notebook](https://jupyterlab.readthedocs.io/en/stable/getting_started/overview.html#overview).
Si tienes experiencia previa trabajando con cuadernos Jupyter, entonces tendrás una
buena idea de qué esperar de JupyterLab.

Los usuarios experimentados de Jupyter notebooks interesados en una discusión más
detallada de las similitudes y diferencias entre las interfaces de usuario de JupyterLab
y Jupyter notebook pueden encontrar más información en la [documentación de la interfaz
de usuario de JupyterLab][jupyterlab-ui].


::::::::::::::::::::::::::::::::::::::::::::::::::

## Iniciando JupyterLab

Puede iniciar el servidor JupyterLab a través de la línea de comandos o a través de una
aplicación llamada `Anaconda Navigator`. Anaconda Navigator se incluye como parte de la
distribución Anaconda Python.

### macOS - Línea de comandos

Para iniciar el servidor de JupyterLab necesitarás acceder a la línea de comandos a
través del Terminal. Hay dos formas de abrir Terminal en Mac.

1. En la carpeta Aplicaciones, abre Utilidades y haz doble clic en Terminal
2. Pulsa <kbd>Comando</kbd> + <kbd>barra espaciadora</kbd> para iniciar Spotlight.
   Escriba `Terminal` y, a continuación, haga doble clic en el resultado de la búsqueda
   o pulse <kbd>Intro</kbd>

Después de lanzar Terminal, escribe el comando para lanzar el servidor JupyterLab.

```bash
$ jupyter lab
```

### Usuarios de Windows - Línea de comandos

Para iniciar el servidor de JupyterLab necesitarás acceder al Prompt de Anaconda.

Pulsa <kbd>Tecla del logotipo de Windows</kbd> y busca `Anaconda Prompt`, haz clic en el
resultado o pulsa intro.

Después de haber lanzado Anaconda Prompt, escriba el comando:

```bash
$ jupyter lab
```

### Navegador Anaconda

Para iniciar un servidor JupyterLab desde Anaconda Navigator primero debes [iniciar
Anaconda Navigator (haz clic para obtener instrucciones detalladas en macOS, Windows y
Linux)](https://docs.anaconda.com/free/navigator/getting-started/#navigator-starting-navigator).
Puedes buscar Anaconda Navigator a través de Spotlight en macOS (<kbd>Comando</kbd> +
<kbd>barra espaciadora</kbd>), la función de búsqueda de Windows (<kbd>Tecla del
logotipo de Windows</kbd>) o abriendo un intérprete de comandos de terminal y ejecutando
el ejecutable `anaconda-navigator` desde la línea de comandos.

Después de iniciar el Navegador Anaconda, haz clic en el botón `Launch` debajo de
JupyterLab. Puede que tengas que desplazarte hacia abajo para encontrarlo.

He aquí una captura de pantalla de una página de Anaconda Navigator similar a la que
debería abrirse en macOS o Windows.

<p align='center'>
  <img alt="Anaconda Navigator landing page" src="fig/0_anaconda_navigator_landing_page.png" width="750"/>
</p>

Y aquí tienes una captura de pantalla de una página de inicio de JupyterLab que debería
ser similar a la que se abre en tu navegador web predeterminado después de iniciar el
servidor de JupyterLab en macOS o Windows.

<p align='center'>
  <img alt="JupyterLab landing page" src="fig/0_jupyterlab_landing_page.png" width="750"/>
</p>

## La interfaz de JupyterLab

JupyterLab tiene muchas características que se encuentran en los entornos de desarrollo
integrados (IDE) tradicionales, pero se centra en proporcionar bloques de construcción
flexibles para la computación interactiva y exploratoria.

La [Interfaz de JupyterLab][jupyterlab-ui] consiste en la Barra de Menú, una Barra
Lateral Izquierda colapsable, y el Área de Trabajo Principal que contiene pestañas de
documentos y actividades.

### Barra de menús

La Barra de Menús en la parte superior de JupyterLab tiene los menús de nivel superior
que exponen varias acciones disponibles en JupyterLab junto con sus atajos de teclado
(donde sea aplicable). Los siguientes menús están incluidos por defecto.

- **Archivo:** Acciones relacionadas con archivos y directorios como *Nuevo*, *Abrir*,
  *Cerrar*, *Guardar*, etc. El menú *Archivo* también incluye la acción *Apagar*
  utilizada para apagar el servidor de JupyterLab.
- **Edición:** Acciones relacionadas con la edición de documentos y otras actividades
  como *Deshacer*, *Cortar*, *Copiar*, *Pegar*, etc.
- **Ver:** Acciones que alteran la apariencia de JupyterLab.
- **Ejecutar:** Acciones para ejecutar código en diferentes actividades como cuadernos y
  consolas de código (discutidas más adelante).
- **Kernel:** Acciones para gestionar kernels. Los kernels en Jupyter se explicarán con
  más detalle a continuación.
- **Pestañas:** Una lista de los documentos y actividades abiertos en el área de trabajo
  principal.
- **Configuración:** Los ajustes comunes de JupyterLab pueden configurarse usando este
  menú. También hay una opción *Editor de Ajustes Avanzados* en el menú desplegable que
  proporciona un control más fino de los ajustes de JupyterLab y las opciones de
  configuración.
- **Ayuda:** Una lista de enlaces de ayuda de JupyterLab y del kernel.

::::::::::::::::::::::::::::::::::::::::: callout

## Núcleos

Los [docs] de
JupyterLab(https://jupyterlab.readthedocs.io/en/stable/user/documents_kernels.html)
definen los kernels como "procesos separados iniciados por el servidor que ejecuta tu
código en diferentes lenguajes y entornos de programación." Cuando abrimos un Jupyter
Notebook, se inicia un kernel - un proceso - que va a ejecutar el código. En esta
lección, utilizaremos el kernel ipython de Jupyter que nos permite ejecutar código
Python 3 de forma interactiva.

El uso de otros [kernels para otros lenguajes de programación] de Jupyter
(https://github.com/jupyter/jupyter/wiki/Jupyter-kernels) nos permitiría escribir y
ejecutar código en otros lenguajes de programación en la misma interfaz de JupyterLab,
como R, Java, Julia, Ruby, JavaScript, Fortran, etc.

::::::::::::::::::::::::::::::::::::::::::::::::::

A continuación se muestra una captura de pantalla de la Barra de Menús por defecto.

<p align='center'>   <img alt="JupyterLab Menu Bar" src="fig/0_jupyterlab_menu_bar.png" width="750"/>
</p>

### Barra lateral izquierda

La barra lateral izquierda contiene una serie de pestañas de uso común, como un
explorador de archivos (que muestra el contenido del directorio en el que se inició el
servidor JupyterLab), una lista de kernels y terminales en ejecución, la paleta de
comandos y una lista de pestañas abiertas en el área de trabajo principal. A
continuación se muestra una captura de pantalla de la barra lateral izquierda por
defecto.

<p align='center'>   <img alt="JupyterLab Left Side Bar" src="fig/0_jupyterlab_left_side_bar.png" width="250"/>
</p>

La barra lateral izquierda puede contraerse o expandirse seleccionando "Mostrar barra
lateral izquierda" en el menú Ver o haciendo clic en la pestaña de la barra lateral
activa.

### Área de trabajo principal

El área de trabajo principal de JupyterLab permite organizar los documentos (cuadernos,
archivos de texto, etc.) y otras actividades (terminales, consolas de código, etc.) en
paneles de pestañas que se pueden redimensionar o subdividir. A continuación se muestra
una captura de pantalla del Área de trabajo principal por defecto.

Si no ves la pestaña Launcher, haz clic en el signo más azul bajo los menús "Archivo" y
"Editar" y aparecerá.

<p align='center'>   <img alt="JupyterLab Main Work Area" src="fig/0_jupyterlab_main_work_area.png" width="750"/>
</p>

Arrastre una pestaña al centro de un panel de pestañas para mover la pestaña al panel.
Subdividir un panel de pestañas arrastrando una pestaña a la izquierda, derecha, parte
superior o inferior del panel. El área de trabajo tiene una única actividad actual. La
pestaña de la actividad actual está marcada con un borde superior de color (azul por
defecto).

## Creación de un script Python

- Para empezar a escribir un nuevo programa Python haz clic en el icono Archivo de Texto
  bajo la cabecera *Others* en la pestaña Lanzador del Área de Trabajo Principal.
  - También puede crear un nuevo archivo de texto sin formato seleccionando *New ->
    Textfile* en el menú *File* de la barra de menús.
- Para convertir este archivo de texto plano en un programa Python, selecciona la acción
  *Save file as* del menú *File* en la Barra de Menú y dale a tu nuevo
  archivo de texto un nombre que termine con la extensión `.py`.
  - La extensión `.py` permite a todo el mundo (incluido el sistema operativo) saber que
    este archivo de texto es un programa Python.
  - Esto es una convención, no un requisito.

## Crear un cuaderno Jupyter

Para abrir un nuevo cuaderno haz clic en el icono Python 3 bajo la cabecera *Notebook*
en la pestaña Lanzador del área de trabajo principal. También puedes crear un nuevo
cuaderno seleccionando *New -> Notebook* en el menú *File* de la Barra de Menús.

Notas adicionales sobre los cuadernos Jupyter.

- Los archivos de cuaderno tienen la extensión `.ipynb` para distinguirlos de los
  programas Python de texto plano.
- Los cuadernos pueden exportarse como scripts de Python que pueden ejecutarse desde la
  línea de comandos.

A continuación se muestra una captura de pantalla de un cuaderno Jupyter ejecutándose
dentro de JupyterLab. Si estás interesado en más detalles, consulta la [documentación
oficial del cuaderno][jupyterlab-notebook-docs].

<p align='center'>   <img alt="Example Jupyter Notebook" src="fig/0_jupyterlab_notebook_screenshot.png" width="750"/>
</p>

::::::::::::::::::::::::::::::::::::::::: callout

## Cómo se almacena

- El archivo del cuaderno se almacena en un formato llamado JSON.
- Al igual que una página web, lo que se guarda tiene un aspecto diferente de lo que se
  ve en el navegador.
- Pero este formato permite a Jupyter mezclar código fuente, texto e imágenes, todo en
  un mismo archivo.

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Organizar documentos en paneles de pestañas

En el área de trabajo principal de JupyterLab puedes organizar los documentos en paneles
de pestañas. Aquí tienes un ejemplo de la [documentación oficial][jupyterlab].

<p align='center'>   <img alt="Multi-panel JupyterLab" src="fig/0_multipanel_jupyterlab_screenshot.png" width="750"/>
</p>

En primer lugar, cree un archivo de texto, una consola Python y una ventana de terminal
y dispóngalos en tres paneles en el área de trabajo principal. A continuación, cree un
cuaderno, una ventana de terminal y un archivo de texto y dispóngalos en tres paneles en
el área de trabajo principal. Por último, crea tu propia combinación de paneles y
pestañas. ¿Qué combinación de paneles y pestañas crees que será más útil para tu flujo
de trabajo?

::::::::::::::: solution

## Solución

Después de crear las pestañas necesarias, puedes arrastrar una de las pestañas al centro
de un panel para mover la pestaña al panel; después puedes subdividir un panel de
pestañas arrastrando una pestaña a la izquierda, derecha, parte superior o inferior del
panel.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Código vs. Texto

Jupyter mezcla código y texto en diferentes tipos de bloques, llamados celdas. A menudo
utilizamos el término "código" para referirnos al "código fuente del software escrito en
un lenguaje como Python". Una "celda de código" en un Cuaderno es una celda que contiene
software; una "celda de texto" es una que contiene prosa ordinaria escrita para seres
humanos.


::::::::::::::::::::::::::::::::::::::::::::::::::

## El Cuaderno dispone de los modos Comando y Edición.

- Si pulsa <kbd>Esc</kbd> y <kbd>Return</kbd> alternativamente, el borde exterior de su
  celda de código cambiará de gris a azul.
- Estos son los modos **Command/Comando** (gris) y **Edit/Edición** (azul) de tu bloc de notas.
- El modo Comando te permite editar las características del cuaderno, y el modo Edición
  cambia el contenido de las celdas.
- En modo Comando (esc/gris),
  - La tecla <kbd>b</kbd> creará una nueva celda debajo de la celda seleccionada
    actualmente.
  - La tecla <kbd>a</kbd> hará una arriba.
  - La tecla <kbd>x</kbd> borrará la celda actual.
  - La tecla <kbd>z</kbd> deshará su última operación de celda (que podría ser una
    eliminación, creación, etc.).
- Todas las acciones se pueden realizar utilizando los menús, pero hay muchos atajos de
  teclado para agilizar las cosas.

::::::::::::::::::::::::::::::::::::::: challenge

## Comando Vs. Edición

En la página del cuaderno Jupyter, ¿estás actualmente en modo Comando o Edición?  
Cambia entre los modos. Utiliza los atajos para generar una nueva celda. Utiliza los
atajos para borrar una celda. Utiliza los atajos para deshacer la última operación de
celda realizada.

::::::::::::::: solution

## Solución

El modo Comando tiene un borde gris y el modo Edición tiene un borde azul. Utilice
<kbd>Esc</kbd> y <kbd>Return</kbd> para cambiar de un modo a otro. Necesitas estar en
modo Comando (Pulsa <kbd>Esc</kbd> si tu celda es azul). Escribe <kbd>b</kbd> o
<kbd>a</kbd>. Tienes que estar en modo Comando (Pulsa <kbd>Esc</kbd> si tu celda es
azul). Escriba <kbd>x</kbd>. Tienes que estar en modo Comando (Pulsa <kbd>Esc</kbd> si
tu celda es azul). Escriba <kbd>z</kbd>.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

### Utiliza el teclado y el ratón para seleccionar y editar celdas.

- Al pulsar la tecla <kbd>Return</kbd>, el borde se vuelve azul y se activa el modo
  Edición, que permite escribir dentro de la celda.
- Como queremos poder escribir muchas líneas de código en una sola celda, al pulsar la
  tecla <kbd>Retorno</kbd> cuando se está en modo Edición (azul) se mueve el cursor a la
  siguiente línea de la celda, igual que en un editor de texto.
- Necesitamos alguna otra forma de decirle al Notebook que queremos ejecutar lo que hay
  en la celda.
- Al pulsar conjuntamente <kbd>Mayús</kbd>\+<kbd>Retorno</kbd> se ejecutará el contenido
  de la celda.
- Observa que las teclas <kbd>Return</kbd> y <kbd>Shift</kbd> de la derecha del teclado
  están una al lado de la otra.

### El Cuaderno convertirá Markdown en documentación con una bonita impresión.

- Los cuadernos también pueden renderizar [Markdown][markdown].
  - Un sencillo formato de texto plano para escribir listas, enlaces y otras cosas que
    podrían ir en una página web.
  - Equivalentemente, un subconjunto de HTML que se parece a lo que enviarías en un
    correo electrónico a la antigua usanza.
- Convierte la celda actual en una celda Markdown entrando en el modo Comando
  (<kbd>Esc</kbd>/gris) y pulsa la tecla <kbd>M</kbd>.
- `In [ ]:` desaparecerá para mostrar que ya no es una celda de código y podrás escribir
  en Markdown.
- Convierta la celda actual en una celda de Código entrando en el modo Comando
  (<kbd>Esc</kbd>/gris) y pulse la tecla <kbd>y</kbd>.

### Markdown hace la mayor parte de lo que hace HTML.

Tabla: Mostrando algo de sintaxis markdown y su salida renderizada.

+---------------------------------------+------------------------------------------------+
| Markdown code                         | Rendered output                                |
+=======================================+================================================+
| ```                                   | <p></p>                                        |
| *   Use asterisks                     | -   Use asterisks                              |
| *   to create                         | -   to create                                  |
| *   bullet lists.                     | -   bullet lists.                              |
| ```                                   |                                                |
+---------------------------------------+------------------------------------------------+
| ```                                   | <p></p>                                        |
| 1.   Use numbers                      | 1.   Use numbers                               |
| 1.   to create                        | 2.   to create                                 |
| 1.   bullet lists.                    | 3.   numbered lists.                           |
| ```                                   |                                                |
+---------------------------------------+------------------------------------------------+
| ```                                   | <p></p>                                        |
| *  You can use indents                | - You can use indents                          |
|   *  To create sublists               |   - To create sublists                         |
|   *  of the same type                 |   - of the same type                           |
| *  Or sublists                        | - Or sublists                                  |
|   1. Of different                     |   1. Of different                              |
|   1. types                            |   2. types                                     |
| ```                                   |                                                |
+---------------------------------------+------------------------------------------------+
| ```                                   | <p></p>                                        |
| # A Level-1 Heading                   | ## A Level-1 Heading                           |
| ```                                   |                                                |
+---------------------------------------+------------------------------------------------+
| ```                                   | <p></p>                                        |
| ## A Level-2 Heading (etc.)           | ### A Level-2 Heading (etc.)                   |
| ```                                   |                                                |
+---------------------------------------+------------------------------------------------+
| ```                                   | <p></p>                                        |
| Line breaks                           | Line breaks                                    |
| don't matter.                         | don't matter.                                  |
|                                       |                                                |
| But blank lines                       | But blank lines                                |
| create new paragraphs.                | create new paragraphs.                         |
| ```                                   |                                                |
+---------------------------------------+------------------------------------------------+
| ```                                   | <p></p>                                        |
| [Links](http://software-carpentry.org)| [Links](https://software-carpentry.org)        |
| are created with `[...](...)`.        | are created with `[...](...)`.                 |
| Or use [named links][data-carp].      | Or use [named links][data_carpentry].          |
|                                       |                                                |
| [data-carp]: http://datacarpentry.org |                                                |
| ```                                   |                                                |
+---------------------------------------+------------------------------------------------+


::::::::::::::::::::::::::::::::::::::: challenge

## Creación de listas en Markdown

Crea una lista anidada en una celda Markdown de un cuaderno con el siguiente aspecto:

1. Obtener financiación.
2. Haz el trabajo.
  - Experimento de diseño.
  - Recopilar datos.
  - Analizar.
3. Escribe.
4. Publicar.

::::::::::::::: solution

## Solución

Este reto integra tanto la lista numerada como la lista con viñetas. Observe que la
lista con viñetas está sangrada 2 espacios para que esté en línea con los elementos de
la lista numerada.

```
1.  Get funding.
2.  Do work.
    *   Design experiment.
    *   Collect data.
    *   Analyze.
3.  Write up.
4.  Publish.
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Más matemáticas

¿Qué se muestra cuando se ejecuta una celda Python en un cuaderno que contiene varios
cálculos? Por ejemplo, ¿qué ocurre cuando se ejecuta esta celda?

```python
7 * 3
2 + 1
```

::::::::::::::: solution

## Solución

Python devuelve la salida del último cálculo.

```python
3
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Cambiar una celda existente de código a Markdown

¿Qué ocurre si escribes algo de Python en una celda de código y luego lo cambias a una
celda de Markdown? Por ejemplo, pon lo siguiente en una celda de código:

```python
x = 6 * 7 + 12
print(x)
```

Y luego ejecútalo con <kbd>Shift</kbd>\+<kbd>Return</kbd> para asegurarte de que
funciona como una celda de código. Ahora vuelve a la celda y usa <kbd>Esc</kbd> y luego
<kbd>m</kbd> para cambiar la celda a Markdown y "ejecútala" con
<kbd>Shift</kbd>\+<kbd>Return</kbd>. ¿Qué ha pasado y en qué puede ser útil?

::::::::::::::: solution

## Solución

El código Python se trata como texto Markdown. Las líneas aparecen como si formaran
parte de un párrafo contiguo. Esto podría ser útil para activar y desactivar
temporalmente celdas en cuadernos que se utilizan para múltiples propósitos.

```python
x = 6 * 7 + 12 print(x)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Ecuaciones

Markdown estándar (como el que estamos utilizando para estas notas) no mostrará
ecuaciones, pero Notebook sí. Crea una nueva celda Markdown e introduce lo siguiente:

```
$\sum_{i=1}^{N} 2^{-i} \approx 1$
```

(Probablemente sea más fácil copiar y pegar.) ¿Qué muestra? ¿Qué crees que hacen el
guión bajo, `_`, el circunflejo, `^`, y el símbolo del dólar, `$`?

::::::::::::::: solution

## Solución

El cuaderno muestra la ecuación tal y como se representaría a partir de la sintaxis de
ecuaciones de LaTeX. El signo del dólar, `$`, se utiliza para indicar a Markdown que el
texto intermedio es una ecuación LaTeX. Si no está familiarizado con LaTeX, el guión
bajo, `_`, se utiliza para los subíndices y el circunflejo, `^`, para los superíndices.
Un par de llaves, `{` y `}`, se utilizan para agrupar texto de forma que la expresión
`i=1` se convierta en subíndice y `N` en superíndice. Del mismo modo, `-i` está entre
llaves para que toda la expresión sea el superíndice de `2`.`\sum` y `\approx` son
comandos LaTeX para los símbolos "suma sobre" y "aproxima".



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Cerrar JupyterLab

- En la barra de menús, seleccione el menú "File" y, a continuación, elija "Shut down"
  en la parte inferior del menú desplegable. Se le pedirá que confirme que desea apagar
  el servidor JupyterLab (¡no olvide guardar su trabajo!). Haga clic en "Shut Down" para
  apagar el servidor JupyterLab.
- Para reiniciar el servidor de JupyterLab tendrás que volver a ejecutar el siguiente
  comando desde un intérprete de comandos.

```
$ jupyter lab
```

::::::::::::::::::::::::::::::::::::::: challenge

## Cerrar JupyterLab

Practica cerrando y reiniciando el servidor de JupyterLab.


::::::::::::::::::::::::::::::::::::::::::::::::::



[jupyterlab]: https://jupyterlab.readthedocs.io/en/stable/
[jupyterlab-ui]: https://jupyterlab.readthedocs.io/en/stable/user/interface.html
[jupyterlab-notebook-docs]:
https://jupyterlab.readthedocs.io/en/stable/user/notebook.html
[markdown]: https://en.wikipedia.org/wiki/Markdown
[data_carpentry]: https://datacarpentry.org


:::::::::::::::::::::::::::::::::::::::: keypoints

- Los scripts de Python son archivos de texto sin formato.
- Utiliza el Jupyter Notebook para editar y ejecutar Python.
- El Notebook dispone de los modos Command y Edition.
- Utilizar el teclado y el ratón para seleccionar y editar celdas.
- El Cuaderno convertirá Markdown en documentación con una bonita impresión.
- Markdown hace la mayor parte de lo que hace HTML.

::::::::::::::::::::::::::::::::::::::::::::::::::



