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

2. While viewing the `pubspec.yaml` file in editor view, click `Pub get`. This pulls the package into your project. You should see the following in the console:
 ```
 flutter pub get
 ```
Ejecutar Pub get también genera automáticamente el archivo `pubspec.lock` con una lista de todos los paquetes incluidos en el proyecto y sus números de versión.
  
