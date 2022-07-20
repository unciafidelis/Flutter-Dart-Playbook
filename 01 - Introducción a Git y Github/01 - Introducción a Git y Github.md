01 - Introducción a Git y Github


## Crea una cuenta de GitHub

Entra a la página de [GitHub](https://github.com/) y completa el formulario:

**Username:** Procura utilizar el nombre de una marca o tu nombre y apellido, ya que con este serás identificado en Github.

**Correo:** **El email o correo electrónico que más utilices (de preferencia uno que te identifique profesionalmente para poderlo proveer despues)**  
**Contraseña:** Esta contraseña debe ser segura y que de preferencia no tenga relación alguna con tu persona o tu entorno, así será mas dificil de tener alguna brecha de seguridad.

Ahora procedemos a dar clic en **Sign up for GitHub** 

Confirmamos que no somos un robot (si es el caso bib bup bip).
  
Al terminar la verificación damos se mostrará una palomita verde y damos clic en **Join a Free Plan**  

## Verificar la Cuenta de Correo en GitHub

Para verificar nuestra cuenta de correo, debemos seguir estos pasos:

* Tendremos en nuestra bandeja de entrada un nuevo correo electrónico de GitHub le damos clic para abrirlo.    

* El correo es el siguiente, damos clic en **Mostrar contenido bloqueado**  

* Clic en **Verify email address**  

* Automáticamente nos abrirá una nueva ventana con el mensaje de que ha sido verificada nuestra cuenta.  
    
* En nuestra bandeja de entrada tendremos un correo con la verificación exitosa.

A continuación tendremos que seleccionar de una serie de opciones, aquellas con las que nos identifiquemos. Por ejemplo, Estudiante. 

También podremos seleccionar el nivel de experiencia que tenemos en programación de software. 
* **None**: Nunca he programado nada
* **A little**: Voy iniciando en la programación
* **A moderater amount**: Tengo un poco de experiencia previa.
* **A lot**: Tengo mucha experiencia previa.

Posteriormente, nos pregunta ¿Para qué queremos utilizar GitHub?, Podemos seleccionar hasta 3 opciones.
Entre las opciones se encuentran:

* Aprender a Programar
* Aprender Git y GitHub
* Crear un repositorio (Almacenar un projecto)

* Crear una página web con GitHub WebPages
* Para colaborar entre equipos
* Encontrar o contribuir a un proyecto open source

* Para trabajar en proyectos escolares
* Consumir el API de GitHub
* Otro

Finalmente nos pregunta acerca de nuestros intereses, igualmente podemos escribir algunos. 
Por ejemplo: Lenguajes de programación, algún Framework o Industria.   

Al dar enter nos mostrará la siguiente pantalla, informando que debemos verificar nuestra cuenta de correo.  
    
## Taller de GitHub 101 

### [Parte 1](https://www.youtube.com/watch?v=OIE9r0J1iRk)

### [Parte 2](https://www.youtube.com/watch?v=8B_qtbdlLSU)

## Git en Github con VS Code

Para utilizar git en Github existen 3 formas concretas:

* Por terminal <- Puro comanditos como hace 30 años (ew)
* Por aplicación de control de versiones, Github Desktop (Funciona pero esta aparte del entorno de desarrollo y esto es menos eficiente)
* Por aplicacion de terceros (VS Code en nuestro caso)

La forma más sencilla (que conozco) a la fecha para realizar las funciones más comunes de Git en Github es utilizando el control de versiones de VS code para implementarlas, pues ahí mismo tienes el código que vas a subir a github (Clonación de repositorios).

Para realizar una implementación de git en Github con VS Code y utilizar un control de versiones adecuado debemos:

1. Crear un repositorio nuevo en Github (Haremos el Hola Mundo que provee Github [Hello World en Github](https://docs.github.com/es/get-started/quickstart/hello-world))
2. Abrir VS Code
3. Dar Click en el Source control o control de versiones
4. Dar click en Clonar repository
5. Seleccionar Github y Autenticarse con tu usuario y contraseña
6. Seleccionar el Repositorio creado
7. Seleccionar donde se guardará localmente
8. Magia

Ahora ya tenemos clonado el repositorio que creamos en github en nuestro entorno local, van a notar que se creó una carpeta en su escritorio con el nombre de tu repositorio, ahi tienes la version del clonado que recien realizaste, NO TOQUES ESTA CARPETA la utilizaremos después.

Ya con nuestro repositorio podemos empezar a trabajar.

Para actualizar los cambios de nuestro repositorio local a nuestro repositorio en Github debemos tener en cuenta como funciona internamente en esta parte Git, para esto debemos saber que:

* Todo cambio realizado en el repositorio clonado genera un estado en el archivo modificado, creado o eliminado; este estado depende del tipo de modificación realizada en el repositorio. __A__: Archivo creado y añadido __M__: Archivo modificado y añadido __M__: Archivo modificado y no añadido __D__: Archivo eliminado __UU__: Conflicto entre ramas o branches. 

* El estado se puede ver al utilizar el comando ```git status -s``` o con el hermoso botón sync de Vscode que realiza exactamente la misma acción sobre el repositorio.

* Con click derecho sobre el archivo modificado y selecciona ``Stage Changes`` o si son varios los archivos que quieres actualizar da click derecho en la pestaña cambios o Changes y selecciona ``Stage All Changes`` puedes colocar en escenario o stage todas las modificaciones realizadas.

* Habrá cambios que no quieras actualizar así que puedes descartarlos con click derecho ``Discard Changes`` o realizar esta misma acción en terminal con el comando ``git reset`` (Pero igual insisto ya no estamos en esos años)

* Ya una vez que tengas todo en stage o escenario es momento de realizar la actualización o commit con la función ```git commit -m "Aqui va un mensaje diciendo que cambios hiciste"``` o como los campeones, dar click en el boton commit y colocar el mensaje de la actualización.

Tip ganador:

Todo mensaje debe utilizar una convención de palabras para que sea entendible para usuarios externos que puedan darle seguimiento a cada commit realizado, como propuesta esta:

## Convención de Mensajes en Commit

### Create: 
Agregar un nuevo archivo o carpeta

### Update:
Actualizar un archivo, elemento, texto o función

### Fix:
Solucionar un Issue o error lógico

### Typo:
Solucionar un error de escritura o falta de ortografía

### DELETE:
Eliminar un archivo

ejemplos:

* Create ArchivoNuevo.dart
* Update ArchivoNuevo.dart list added
* Fix ArchivoNuevo.dart naming issue solved
* Typo ArchivoNuevo.Dart misspelled Kow to Cow solved
* DELETE ArchivoNuevo.dart Not in use anymore

Usted ha hecho su primer modificación en un repositorio remoto utilizando el control de versiones de Git con Github y Vscode!




