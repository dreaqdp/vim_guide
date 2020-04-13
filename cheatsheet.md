# VIM workshop

## Basic

Basic modes:

* Normal: default mode, se vuelve a él con `ESC`
* Insert: escribir
* Visual: seleccionar

Cómo puedo guardar? 
`ESC :w`

Cómo puedo salir?
`ESC :q`

Y guardar y salir?
`ESC :wq`

## Normal mode
Las letras tienen asignadas diferentes funcionalidades, no escribir como tal.

### Desplazamiento

* `k`, `j`: subir, bajar una línea
* `h`, `l`: un carácter a la izquierda, derecha
* `0`, `$`: inicio, final de la línea
* `gg`, `G`: principio, final del documento
* `{`, `}`: saltar de línea en blanco a línea en blanco (bloques de código), hacia arriba, abajo
* `w`: desplazarte a la siguiente palabra, situa el cursor al principio de esta
* `e`: desplazarte al final de la palabra en la que estaba el cursor
* `b`: desplazarte a la palabra anterior, situa el cursor al principio de esta
* `f` + char: ir hasta la primera ocurrencia del carácter, situa el cursor encima del char
* `t` + char: ir hasta la primera ocurencia del carácter, situa el cursos un carácter antes del char especificado
* `:` + número línea: ir al número de línea indicado

Todos estos comandos pueden combinarse con números para indicar que se relace la acción X veces. 

 EX: `4w` desplaza 4 palabras


## Insert mode
Es el modo de escritura. Hay diversas formas de entrar:

* `i`: el cursor se situa en la posición que estaba
* `a`: el cursor se situa un carácter a la derecha de donde estaba
* `I`: el cursor se situa al inicio de la línea, ignorando espacio en blanco
* `A`: el cursor se situa al final de la línea
* `o`: inserta una nueva línea en blanco debajo
* `O`: inserta una nueva línea en blanco arriba

## Reemplazar
Sin necesidad de entrar en modo insert, eliminar y escribir. Puedes reemplazar:

* `r` + char: reemplaza el carácter donde está el cursor por el char indicado, luego vuelve a normal mode
* `R` + chars: reemplaza los carácter a partir de donde está el cursor

## Visual mode
Modo para seleccionar el texto/código:

* `v` (+ desplazamiento): selección "típica"\* 
* `V` (+ desplazamiento): selección de una línea\*
* `ctrl` + `v` (+ desplazamiento): selección en bloque\*

\* puedes seleccionar más con el desplazamiento

### Combinaciones
Se puede combinar la selección hecha con otros comandos, como `d` (ver sección de eliminar), `y` (ver sección de copiar).

Una combinación que permite insertar en diversar líneas a la vez el mismo contenido es: `ctrl` + `v` + desplazamiento (selección en bloque) + `I` +  texto + `ESC`. Al apretar `ESC` aparecerá el texto escrito en todas las líneas seleccionadas en el bloque.


## Eliminar
Para eliminar se utiliza `d`. Lo eliminado se almacena en el mismo registro interno que `y` (ver sección Copiar y Pegar).

Puede combinarse con desplazamiento y selección. Por ejemplo: 

* `d3w` elimina 4 palabras
* `Vjd` elimina la selección de 2 líneas

Para eliminar una línea rápido existe el comando: `dd`.

### Eliminar + insert
Después de eliminar puedes querer entrar en Insert mode, para evitar hacer `di` podemos utilizar `c`.

`c` se utiliza de la misma manera que `d`.

`s` equivale a `cl`.

`S` equivale a `cc`.

## Copiar y pegar
### Copiar
Se copia mediante `y` (yank):

* selección + `y`: copia la selección
* `y` + desplazamiento: copia el desplazamiento indicado
* `yy`: copia una línea

### Pegar
Mediante `p` (paste):

* `p`: pega en la línea de debajo del cursor
* `P`: pega en la línea de encima del cursor

Se puede pegar tanto lo copiado mediante `y` como lo eliminado (`d`, `c`, `s`...)

### Ctrl + c, ctrl + v funciona?
Con `y` y `p` se copia y pega lo copiado en registros internos de VIM. Para poder pegar algo copiado fuera de VIM, en otro programa se tiene que estar en modo Insert.

* `i` + `ctrl + shift + v`

## Buscar

* `/` + patrón: búsqueda case sensitive
* `/\c` + patrón: búsqueda no case sensitive

Una vez buscado el patrón, para navegar por las coincidencias:

* `n`: siguente coincidencia
* `N`: coincidencia anterior

También se pueden utilizar los siguentes comandos que no requieren de escribir el patrón, puesto que buscan la palabra sobre la que esté el cursor:

* `#`: búsqueda de coincidencias previas
* `*`: búsqueda de coincidencias anteriores

Añadir que estos dos últimos comandos guardan la palabra en el registro de búsqueda. Esto significa que se puede cambiar el cursor de palabra y seguir buscando la palabra, patrón anterior mediante `n` y `N`.

### Buscar y substituir
Utilizar la siguente regex: `:%s/patrón_buscar/patrón_substituir/gci`

* `%`: aplicar la regex a todo el documento
* `g`: buscar en la línea
* `c`: pedir confirmación para cada substitución
* `i`: hacer la búsqueda case insensitive

## Deshacer y rehacer

* `u`: undo (ctrl + z en otros editores)
* `ctrl` + `r`: redo

## Otros comandos útiles
Incrementar y decrementar números, va a buscar la primera ocurrencia de números de la línea:

* `ctrl` + `a`: incrementa
* `ctrl` + `x`: decrementa

Ir al man (manual) de la syscall, comando de bash:
* `K`: busca el man de la palabra donde está el cursor

Concatenación de líneas:
* `J`: concatena la línea en la que está el cursor con la de abajo

Otras opciones al salir/guardar:
* `:q!`: salir sin aplicar los cambios no guardados
* `:` + `w`/`q` + `a`: `a` aplica guardar y/o salir a todos los ficheros abiertos

### Identación
* `<`: identa a la izquierda 
* `>`: identa a la derecha
* `gg=G`: autoidenta todo el código

### Macros
1. `q` + tecla: empezar a grabar una macro en la tecla indicada.
2. comandos
3. `q`: acabar de grabar la macro
4. `@` + letra: aplicar la macro

## Visualización de varios ficheros
### Pestañas
* `:tabe ` + nombre fichero: abre el fichero en otra pestaña
* `gt`: desplazarse a la pestaña de la derecha
* `gT`: desplazarse a la pestaña de la izquierda
* num\_tab + `gt`: desplazarse a la pestaña num\_tab, la primera correponde al 1.

Se puede abrir VIM directamente con los ficheros en pestañas diferentes:
* `vim -p ` + ficheros

### División de la pantalla
* `:sp` + fichero: abrir el fichero dividiendo la consola horizontalmente
* `:vsp` + fichero: abrir el fichero dividiendo la consola verticalmente
* `ctrl` + `w` + `j`/`k`/`h`/`l`: cambiar la vista activa

Se pueden combinar las pestañas con la división de la pantalla. La división de los ficheros será local a la pestana. Es decir, en cada pestaña se puede tener una división diferente.


