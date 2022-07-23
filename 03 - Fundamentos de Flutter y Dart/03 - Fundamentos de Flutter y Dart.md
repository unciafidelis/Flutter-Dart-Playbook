03 - Fundamentos de Flutter y Dart

# Dart

Dart es un lenguaje optimizado para el cliente para aplicaciones rápidas en cualquier plataforma. Es soportado por Google y tiene una gran comunidad en constante crecimiento.

## Hello World
Cada aplicación tiene una función `main()`. Para mostrar texto en la consola, puede usar la función `print()` de nivel superior:
```dart
void main() {
  print('Hello, World!');
}
```
## Variables
Incluso en el código Dart con seguridad de tipos, la mayoría de las variables no necesitan tipos explícitos, gracias a la inferencia de tipos:
```dart
var name = 'Voyager I';
var year = 1977;
var antennaDiameter = 3.7;
var flybyObjects = ['Jupiter', 'Saturn', 'Uranus', 'Neptune'];
var image = {
  'tags': ['saturn'],
  'url': '//path/to/saturn.jpg'
};
```

## Declaraciones de flujo de control
Dart admite las declaraciones de flujo de control habituales:
```dart
if (year >= 2001) {
  print('21st century');
} else if (year >= 1901) {
  print('20th century');
}

for (final object in flybyObjects) {
  print(object);
}

for (int month = 1; month <= 12; month++) {
  print(month);
}

while (year < 2016) {
  year += 1;
}
```

## Funciones
Recomendamos especificar los tipos de argumentos de cada función y el valor de retorno:
```dart
int fibonacci(int n) {
  if (n == 0 || n == 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}

var result = fibonacci(20);
```
Una sintaxis abreviada `=>` (flecha) es útil para las funciones que contienen una sola declaración. Esta sintaxis es especialmente útil cuando se pasan funciones anónimas como argumentos:
```dart
flybyObjects.where((name) => name.contains('turn')).forEach(print);
```
Además de mostrar una función anónima (el argumento de `where()`), este código muestra que puede usar una función como argumento: la función `print()` de nivel superior es un argumento de `forEach()`.

## Comentarios
Los comentarios de Dart generalmente comienzan con `//`.
```dart
// This is a normal, one-line comment.

/// This is a documentation comment, used to document libraries,
/// classes, and their members. Tools like IDEs and dartdoc treat
/// doc comments specially.

/* Comments like these are also supported. */
```

## Imports
Para acceder a las API definidas en otras bibliotecas, usa `import`.
```dart
// Importing core libraries
import 'dart:math';

// Importing libraries from external packages
import 'package:test/test.dart';

// Importing files
import 'path/to/my_other_file.dart';
```
## Classes
Aquí hay un ejemplo de una clase con tres propiedades, dos constructores y un método. Una de las propiedades no se puede configurar directamente, por lo que se define mediante un método getter (en lugar de una variable).
```dart
class Spacecraft {
  String name;
  DateTime? launchDate;

  // Read-only non-final property
  int? get launchYear => launchDate?.year;

  // Constructor, with syntactic sugar for assignment to members.
  Spacecraft(this.name, this.launchDate) {
    // Initialization code goes here.
  }

  // Named constructor that forwards to the default one.
  Spacecraft.unlaunched(String name) : this(name, null);

  // Method.
  void describe() {
    print('Spacecraft: $name');
    // Type promotion doesn't work on getters.
    var launchDate = this.launchDate;
    if (launchDate != null) {
      int years = DateTime.now().difference(launchDate).inDays ~/ 365;
      print('Launched: $launchYear ($years years ago)');
    } else {
      print('Unlaunched');
    }
  }
}
```
Podrías usar la clase Spacecraft así:
```dart
var voyager = Spacecraft('Voyager I', DateTime(1977, 9, 5));
voyager.describe();

var voyager3 = Spacecraft.unlaunched('Voyager III');
voyager3.describe();
```

## Enums
Las enumeraciones son una forma de enumerar un conjunto predefinido de valores o instancias de una manera que garantiza que no puede haber otras instancias de ese tipo.

Aquí hay un ejemplo de una enumeración simple que define una lista simple de tipos de planetas predefinidos:
```dart
enum PlanetType { terrestrial, gas, ice }
```
Aquí hay un ejemplo de una declaración `enum` mejorada de una clase que describe planetas, con un conjunto definido de instancias constantes, a saber, los planetas de nuestro propio sistema solar.
```dart
/// Enum that enumerates the different planets in our solar system
/// and some of their properties.
enum Planet {
  mercury(planetType: PlanetType.terrestrial, moons: 0, hasRings: false),
  venus(planetType: PlanetType.terrestrial, moons: 0, hasRings: false),
  // ···
  uranus(planetType: PlanetType.ice, moons: 27, hasRings: true),
  neptune(planetType: PlanetType.ice, moons: 14, hasRings: true);

  /// A constant generating constructor
  const Planet(
      {required this.planetType, required this.moons, required this.hasRings});

  /// All instance variables are final
  final PlanetType planetType;
  final int moons;
  final bool hasRings;

  /// Enhanced enums support getters and other methods
  bool get isGiant =>
      planetType == PlanetType.gas || planetType == PlanetType.ice;
}
You might use the Planet enum like this:

final yourPlanet = Planet.earth;

if (!yourPlanet.isGiant) {
  print('Your planet is not a "giant planet".');
}
```
Obtenga más información sobre las enumeraciones en Dart, incluidos los requisitos de enumeración mejorados, las propiedades introducidas automáticamente, el acceso a nombres de valores enumerados, la compatibilidad con declaraciones de cambio y mucho más.

## Herencia
Dart tiene herencia única.
```dart
class Orbiter extends Spacecraft {
  double altitude;

  Orbiter(super.name, DateTime super.launchDate, this.altitude);
}
Read more about extending classes, the optional @override annotation, and more.

## Mixins
Mixins are a way of reusing code in multiple class hierarchies. The following is a mixin declaration:

mixin Piloted {
  int astronauts = 1;

  void describeCrew() {
    print('Number of astronauts: $astronauts');
  }
}
To add a mixin’s capabilities to a class, just extend the class with the mixin.

class PilotedCraft extends Spacecraft with Piloted {
  // ···
}
```
PilotedCraft ahora tiene el campo de astronauts así como el método `describeCrew()`.

## Interfaces y clases abstractas
Dart no tiene una palabra clave de interfaz. En cambio, todas las clases definen implícitamente una interfaz. Por lo tanto, puede implementar cualquier clase.
```dart
class MockSpaceship implements Spacecraft {
  // ···
}
```
Puede crear una clase abstracta para que una clase concreta la amplíe (o la implemente). Las clases abstractas pueden contener métodos abstractos (con cuerpos vacíos).
```dart
abstract class Describable {
  void describe();

  void describeWithEmphasis() {
    print('=========');
    describe();
    print('=========');
  }
}
```
Cualquier clase que extienda Describable tiene el método `describeWithEmphasis()`, que llama a la implementación del extensor de `describe()`.

Lea más sobre clases y métodos abstractos.

## Async
Evite el infierno de devolución de llamada y haga que su código sea mucho más legible usando `async` y `await`.
```dart
const oneSecond = Duration(seconds: 1);
// ···
Future<void> printWithDelay(String message) async {
  await Future.delayed(oneSecond);
  print(message);
}
The method above is equivalent to:

Future<void> printWithDelay(String message) {
  return Future.delayed(oneSecond).then((_) {
    print(message);
  });
}
```
Como muestra el siguiente ejemplo, `async` y `await` ayudan a que el código asíncrono sea fácil de leer.
```dart
Future<void> createDescriptions(Iterable<String> objects) async {
  for (final object in objects) {
    try {
      var file = File('$object.txt');
      if (await file.exists()) {
        var modified = await file.lastModified();
        print(
            'File for $object already exists. It was modified on $modified.');
        continue;
      }
      await file.create();
      await file.writeAsString('Start describing $object in this file.');
    } on IOException catch (e) {
      print('Cannot create description for $object: $e');
    }
  }
}
```
También puede usar `async*`, que le brinda una forma agradable y legible de crear flujos.
```dart
Stream<String> report(Spacecraft craft, Iterable<String> objects) async* {
  for (final object in objects) {
    await Future.delayed(oneSecond);
    yield '${craft.name} flies by $object';
  }
}
```
Obtenga más información sobre la compatibilidad con la asincronía, incluidas las funciones `async`, `Future`, `Stream` y el bucle asíncrono (`await for`).

## Excepciones
Para generar una excepción, use `throw`:
```dart
if (astronauts == 0) {
  throw StateError('No astronauts.');
}
To catch an exception, use a try statement with on or catch (or both):

try {
  for (final object in flybyObjects) {
    var description = await File('$object.txt').readAsString();
    print(description);
  }
} on IOException catch (e) {
  print('Could not describe object: $e');
} finally {
  flybyObjects.clear();
}
```
Tenga en cuenta que el código anterior es asíncrono; `try` funciona tanto para el código síncrono como para el código en una función `async`.
