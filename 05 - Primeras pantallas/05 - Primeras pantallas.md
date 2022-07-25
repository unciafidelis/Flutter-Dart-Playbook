Esta es una guía para crear su primera aplicación Flutter. Si está familiarizado con el código orientado a objetos y los conceptos básicos de programación, como variables, bucles y condicionales, puede completar este tutorial. No necesita experiencia previa con Dart, móvil, escritorio o programación web.

## Lo que construirás
Implementarás una aplicación simple que genera nombres propuestos para una nueva startup. El usuario puede seleccionar y deseleccionar nombres, guardando los mejores. El código genera perezosamente 10 nombres a la vez (cool no?). A medida que el usuario se desplaza, se generan más nombres. No hay límite de hasta dónde puede desplazarse un usuario.

## ¿Que aprenderás?
* Cómo escribir una aplicación Flutter que se vea natural en iOS, Android, escritorio (Windows, por ejemplo) y la web
* Estructura básica de una aplicación Flutter
* Encontrar y usar paquetes para ampliar la funcionalidad
* Uso de hot reload para un ciclo de desarrollo más rápido
* Cómo implementar un widget con estados
* Cómo crear una lista infinita cargada perezosamente

Puede ejecutar este código utilizando cualquiera de los siguientes dispositivos:

* Un dispositivo físico (Android o iOS) conectado a su computadora y configurado en modo desarrollador
* El simulador de iOS (requiere instalar herramientas de Xcode)
* El emulador de Android (requiere configuración en Android Studio)
* Un navegador (se requiere Chrome para la depuración)
* Como aplicación de escritorio de Windows, Linux o macOS

Cada aplicación de Flutter creada también se compila para la web. En su IDE, debajo del menú desplegable de dispositivos, o en la línea de comandos usando dispositivos flutter, ahora debería ver Chrome y el servidor web en la lista. El dispositivo Chrome inicia automáticamente Chrome. El servidor web inicia un servidor que aloja la aplicación para que pueda cargarla desde cualquier navegador. Use el dispositivo Chrome durante el desarrollo para que pueda usar DevTools y el servidor web cuando quiera probar en otros navegadores. Para obtener más información, consulte Creación de una aplicación web con Flutter y Escriba su primera aplicación Flutter en la web.

Además, las aplicaciones de Flutter pueden compilarse para escritorio. Debería ver su sistema operativo listado en su IDE bajo dispositivos, por ejemplo: Windows (escritorio), o en la línea de comando usando dispositivos flutter. Para obtener más información sobre la creación de aplicaciones para escritorio, consulte Escribir una aplicación de escritorio Flutter.

## Step 1: Crear la aplicación Flutter de inicio
Cree una aplicación de Flutter simple y con plantilla, utilizando las instrucciones de Primeros pasos con su primera aplicación de Flutter. Nombra el proyecto startup_namer (en lugar de flutter_app).

Tip: si no ve "Nuevo proyecto de Flutter" como una opción en su IDE, asegúrese de tener instalados los complementos para Flutter y Dart.


En su mayoría, editará `lib/main.dart`, donde esta todo el código Dart.
You’ll mostly edit `lib/main.dart`, where the Dart code lives.

1. Reemplace el contenido de `lib/main.dart`.
Elimine todo el código de `lib/main.dart`. Reemplácelo con el siguiente código, que muestra "Hello World" en el centro de la pantalla.

`lib/main.dart`

```dart
// Copyright 2018 The Flutter team. All rights reserved.
// Use of this source code is governed by a BSD-style license that can be
// found in the LICENSE file.

import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Welcome to Flutter',
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Welcome to Flutter'),
        ),
        body: const Center(
          child: Text('Hello World'),
        ),
      ),
    );
  }
}
```
 Tip: al pegar código en su aplicación, la sangría puede torcerse. Puedes arreglar esto con las siguientes herramientas de Flutter:

* Android Studio e IntelliJ IDEA: haga clic con el botón derecho en el código y seleccione Reformatear código con dartfmt.
* Código VS: haga clic con el botón derecho y seleccione Formatear documento.
* Terminal: Ejecute el formato flutter <nombre de archivo>.
  
  
2. Ejecute la aplicación de la manera que describe su IDE. Debería ver Android, iOS, Windows, Linux, macOS o salida web, según su dispositivo.
  
Tip: La primera vez que ejecuta en un dispositivo físico, puede tardar un poco en cargarse. Luego, puede usar la hot reload para actualizaciones rápidas. Guardar también realiza una hot reload si la aplicación se está ejecutando. Cuando ejecute una aplicación directamente desde la consola usando flutter `run`, ingrese `r` para realizar una hot reload.
  
### Observaciones
  
Este ejemplo crea una Material app. El `material` es un lenguaje de diseño visual que es estándar en dispositivos móviles y en la web. Flutter ofrece un amplio conjunto de widgets de materiales. Es una buena idea tener una entrada `uses-material-design: true` en la sección flutter de tu archivo `pubspec.yaml`. Esto le permitirá utilizar más funciones de Material, como su conjunto de iconos predefinidos.
La aplicación amplía `StatelessWidget`, lo que convierte a la propia aplicación en un widget. En Flutter, casi todo es un widget, incluida la alineación, el relleno y el diseño.
El widget `Scaffold`, de la biblioteca Material, proporciona una barra de aplicación predeterminada y una propiedad de cuerpo que contiene el árbol de widgets para la pantalla de inicio. El subárbol de widgets puede ser bastante complejo.
El trabajo principal de un widget es proporcionar un método `build()` que describa cómo mostrar el widget en términos de otros widgets de nivel inferior.
El cuerpo de este ejemplo consta de un widget de `Center` que contiene un widget secundario de `Text`. El widget Center alinea su subárbol de widgets con el centro de la pantalla.
  
## Paso 2: Usa un paquete externo
  
En este paso, comenzará a usar un paquete de código abierto llamado `english_words`, que contiene algunos miles de las palabras en inglés más utilizadas, además de algunas funciones de utilidad.
  
Puede encontrar el paquete `english_words`, así como muchos otros paquetes de código abierto, en [pub.dev](https://pub.dev/).

1. Agregue el paquete `english_words` a su proyecto de la siguiente manera:
  ```
  flutter pub add english_words
  ```
El archivo `pubspec.yaml` administra los activos y las dependencias de una aplicación de Flutter. En `pubspec.yaml`, verá que se ha agregado la dependencia `english_words`.

2. Mientras visualiza el archivo `pubspec.yaml` en la vista de editor, haga clic en `Pub get`. Esto introduce el paquete en su proyecto. Debería ver lo siguiente en la consola:
 ```
 flutter pub get
 ```
Ejecutar Pub get también genera automáticamente el archivo `pubspec.lock` con una lista de todos los paquetes incluidos en el proyecto y sus números de versión.

3. In `lib/main.dart`, import the new package:
  
```dart
import 'package:english_words/english_words.dart';
import 'package:flutter/material.dart';
```
  
A medida que escribe, Android Studio le ofrece sugerencias de bibliotecas para importar. Luego, muestra la cadena de importación en gris, lo que le permite saber que la biblioteca importada no se ha utilizado (hasta ahora).

4. Use el paquete de palabras en inglés para generar el texto en lugar de usar la cadena "Hello World":

```dart
@@ -2,6 +2,7 @@
	  // Use of this source code is governed by a BSD-style license that can be
	  // found in the LICENSE file.
+ import 'package:english_words/english_words.dart';
	  import 'package:flutter/material.dart';
	  void main() {
@@ -13,14 +14,15 @@
	    @override
	    Widget build(BuildContext context) {
	+     final wordPair = WordPair.random();
	      return MaterialApp(
	        title: 'Welcome to Flutter',
	        home: Scaffold(
	          appBar: AppBar(
	            title: const Text('Welcome to Flutter'),
	          ),
	-         body: const Center(
	-           child: Text('Hello World'),
	+         body: Center(
	+           child: Text(wordPair.asPascalCase),
	          ),
	        ),
	      );
```
Si la aplicación se está ejecutando, use `hot reload` para actualizar la aplicación en ejecución. Cada vez que haga clic en recargar en caliente o guarde el proyecto, debería ver un par de palabras diferente, elegido al azar, en la aplicación en ejecución. Esto se debe a que el emparejamiento de palabras se genera dentro del método de compilación, que se ejecuta cada vez que `MaterialApp` requiere representación, o cuando se cambia la plataforma en Flutter Inspector.
  
  “Pascal case” (también conocido como “upper camel case”), significa que cada palabra de la cadena, incluida la primera, comienza con una letra mayúscula. Entonces, "uppercamelcase" se convierte en "UpperCamelCase".
  
## Paso 3: Agregue un widget con estado

`Stateless` widgets son inmutables, lo que significa que sus propiedades no pueden cambiar; todos los valores son finales.

`Stateful` los widgets mantienen un estado que puede cambiar durante la vida útil del widget. La implementación de un widget con estado requiere al menos dos clases: 1) a `StatefulWidget` clase que crea una instancia de 2) a `State` clase. los `StatefulWidget` La clase es, en sí misma, inmutable y se puede descartar y regenerar, pero la clase `State` persiste durante la vida útil del widget.

En este paso, agregará un widget con estado, `RandomWords`, que crea su clase `State`, `_RandomWordsState`. Luego usarás `RandomWords` como un elemento secundario dentro del widget sin estado existente en `MyApp`.

1. Cree el código repetitivo para un widget con estado.
En `lib/main.dart`, coloque el cursor después de todo el código, ingrese Retorno un par de veces para comenzar en una línea nueva. En su IDE, comience a escribir `stful`. El editor le pregunta si desea crear un widget `Stateful`. Pulse Retorno para aceptar. Aparece el código repetitivo para dos clases y el cursor se coloca para que ingrese el nombre de su widget con estado.

2. Ingrese `RandomWords` como el nombre de su widget.
El widget `RandomWords` hace poco más que crear su clase State.

Una vez que haya ingresado `RandomWords` como el nombre del widget con estado, el IDE actualiza automáticamente la clase State que lo acompaña, nombrándola `_RandomWordsState`. De forma predeterminada, el nombre de la clase `State` tiene un prefijo bajo. Prefijar un identificador con un guión bajo impone la privacidad en el lenguaje Dart y es una mejor práctica recomendada para objetos de estado.

El IDE también actualiza automáticamente la clase de estado para extender `State<RandomWords>`, lo que indica que está utilizando una clase de estado genérica especializada para usar con `RandomWords`. La mayor parte de la lógica de la aplicación reside aquí: mantiene el estado del widget `RandomWords`. Esta clase guarda la lista de pares de palabras generados, que crece infinitamente a medida que el usuario se desplaza y, en la parte 2 de este laboratorio, marca los pares de palabras favoritos a medida que el usuario los agrega o elimina de la lista al alternar el ícono del corazón.

Ambas clases ahora se ven de la siguiente manera:
  
```dart
  class RandomWords extends StatefulWidget {
    const RandomWords({super.key});

    @override
    State<RandomWords> createState() => _RandomWordsState();
  }

  class _RandomWordsState extends State<RandomWords> {
    @override
    Widget build(BuildContext context) {
      return Container();
    }
  }
```
3. Actualiza el método `build()` en `_RandomWordsState`:

```dart
  class _RandomWordsState extends State<RandomWords> {
    @override
    Widget build(BuildContext context) {
      final wordPair = WordPair.random();
      return Text(wordPair.asPascalCase);
    }
  }
```

4. Elimine el código de generación de palabras de `MyApp` realizando los cambios que se muestran en la siguiente diferencia:

```dart
   @override
	    Widget build(BuildContext context) {
	-     final wordPair = WordPair.random();
	      return MaterialApp(
	        title: 'Welcome to Flutter',
	        home: Scaffold(
	          appBar: AppBar(
	            title: const Text('Welcome to Flutter'),
	          ),
	-         body: Center(
	-           child: Text(wordPair.asPascalCase),
	+         body: const Center(
	+           child: RandomWords(),
	          ),
	        ),
	      );
	    }
```

Reinicie la aplicación. La aplicación debería comportarse como antes, mostrando un emparejamiento de palabras cada vez que recarga o guarda la aplicación.
  
Tip: si ve una advertencia en una hot reload que podría necesitar reiniciar la aplicación, considere reiniciarla. La advertencia puede ser un falso positivo, pero reiniciar su aplicación garantiza que sus cambios se reflejen en la interfaz de usuario de la aplicación.
  
## Paso 4: Cree un `ListView` de desplazamiento infinito

En este paso, expandirá `_RandomWordsState` para generar y mostrar una lista de parejas de palabras. A medida que el usuario se desplaza por la lista (que se muestra en un widget ListView) crece infinitamente. El constructor de fábrica de constructores de ListView le permite crear una vista de lista de forma perezosa, bajo demanda.

Agrega una lista de `_sugerencias` a la clase `_RandomWordsState` para guardar las combinaciones de palabras sugeridas. Además, agregue una variable `_biggerFont` para aumentar el tamaño de la fuente.
  
```dart
  class _RandomWordsState extends State<RandomWords> {
  final _suggestions = <WordPair>[];
  final _biggerFont = const TextStyle(fontSize: 18);
  // ···
}
```
  
A continuación, agregará un widget ListView a la clase `_RandomWordsState` con el constructor `ListView.builder`. Este método crea el `ListView` que muestra el emparejamiento de palabras sugerido.

La clase `ListView` proporciona una propiedad de constructor, `itemBuilder`, que es un generador de fábrica y una función de devolución de llamada especificada como una función anónima. Se pasan dos parámetros a la función: `BuildContext` y el iterador de fila, i. El iterador comienza en 0 y aumenta cada vez que se llama a la función. Se incrementa dos veces por cada combinación de palabras sugerida: una vez para ListTile y otra vez para Divider. Este modelo permite que la lista sugerida siga creciendo a medida que el usuario se desplaza.

Retorna un widget ListView desde el método `build` de la clase `_RandomWordsState` usando el constructor `ListView.builder`:

```dart
return ListView.builder(
  padding: const EdgeInsets.all(16.0),
  itemBuilder: /*1*/ (context, i) {
    if (i.isOdd) return const Divider(); /*2*/

    final index = i ~/ 2; /*3*/
    if (index >= _suggestions.length) {
      _suggestions.addAll(generateWordPairs().take(10)); /*4*/
    }
    return Text(_suggestions[index].asPascalCase);
  },
);
```

* La devolución de llamada `itemBuilder` se llama una vez por combinación de palabras sugerida y coloca cada sugerencia en una fila `ListTile`. Para filas pares, la función agrega una fila `ListTile` para el emparejamiento de palabras. Para filas impares, la función agrega un widget de divisor para separar visualmente las entradas. Tenga en cuenta que el divisor puede ser difícil de ver en dispositivos más pequeños.
  
* Agregue un widget divisor de un píxel de alto antes de cada fila en `ListView`.
  
* La expresión `i ~/ 2` divide `i` entre `2` y devuelve un resultado entero. Por ejemplo: 1, 2, 3, 4, 5 se convierte en 0, 1, 1, 2, 2. Esto calcula el número real de emparejamientos de palabras en `ListView`, menos los widgets divisores.
  
* Si ha llegado al final de los pares de palabras disponibles, genere 10 más y agréguelos a la lista de sugerencias.
  
El constructor `ListView.builder` crea y muestra un widget de texto una vez por combinación de palabras. En el siguiente paso, devolverá cada nuevo par como un `ListTile`, lo que le permite hacer que las filas sean más atractivas en el siguiente paso.
  
3. Replace the returned `Text` in the `itemBuilder` body of the `ListView.builder` in `_RandomWordsState` with a `ListTile` displaying the suggestion:

```dart
  return ListTile(
  title: Text(
    _suggestions[index].asPascalCase,
    style: _biggerFont,
  ),
);
```

Un `ListTile` es una fila de altura fija que contiene texto, así como iconos iniciales o finales u otros widgets.

4. Una vez completado, el método `build()` en la clase `_RandomWordsState` debe coincidir con el siguiente código resaltado:
  
`lib/main.dart (build)`
 
 ```dart
  @override
Widget build(BuildContext context) {
  return ListView.builder(
    padding: const EdgeInsets.all(16.0),
    itemBuilder: /*1*/ (context, i) {
      if (i.isOdd) return const Divider(); /*2*/

      final index = i ~/ 2; /*3*/
      if (index >= _suggestions.length) {
        _suggestions.addAll(generateWordPairs().take(10)); /*4*/
      }
      return ListTile(
        title: Text(
          _suggestions[index].asPascalCase,
          style: _biggerFont,
        ),
      );
    },
  );
}
 ```

5. Para ponerlo todo junto, actualice el título mostrado de la aplicación actualizando el método `build()` en la clase `MyApp` y cambiando el título de `AppBar`:
  
```dart
  @@ -14,12 +14,12 @@
	    @override
	    Widget build(BuildContext context) {
	      return MaterialApp(
	-       title: 'Welcome to Flutter',
	+       title: 'Startup Name Generator',
	        home: Scaffold(
	          appBar: AppBar(
	-           title: const Text('Welcome to Flutter'),
	+           title: const Text('Startup Name Generator'),
	          ),
	          body: const Center(
	            child: RandomWords(),
	          ),
@@ -27,18 +27,36 @@
	      );
	    }
	  }
	- class RandomWords extends StatefulWidget {
	-   const RandomWords({super.key});
	+ class _RandomWordsState extends State<RandomWords> {
	+   final _suggestions = <WordPair>[];
	+   final _biggerFont = const TextStyle(fontSize: 18);
	    @override
	-   State<RandomWords> createState() => _RandomWordsState();
	+   Widget build(BuildContext context) {
	+     return ListView.builder(
	+       padding: const EdgeInsets.all(16.0),
	+       itemBuilder: /*1*/ (context, i) {
	+         if (i.isOdd) return const Divider(); /*2*/
	+ 
	+         final index = i ~/ 2; /*3*/
	+         if (index >= _suggestions.length) {
	+           _suggestions.addAll(generateWordPairs().take(10)); /*4*/
	+         }
	+         return ListTile(
	+           title: Text(
	+             _suggestions[index].asPascalCase,
	+             style: _biggerFont,
	+           ),
	+         );
	+       },
	+     );
	+   }
	  }
	- class _RandomWordsState extends State<RandomWords> {
	+ class RandomWords extends StatefulWidget {
	+   const RandomWords({super.key});
	+ 
	    @override
	-   Widget build(BuildContext context) {
	-     final wordPair = WordPair.random();
	-     return Text(wordPair.asPascalCase);
	-   }
	+   State<RandomWords> createState() => _RandomWordsState();
	  }
```
6. Reinicie la aplicación. Deberías ver una lista de parejas de palabras sin importar cuánto te desplaces.
  
  
### Felicidades has completado tu primer aplicación con Dart y Flutter!
