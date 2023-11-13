---
tags:
  - 2º
Fecha: "[[2023-09-25]]"
Asignatura: "[[Deseño de Software]]"
---
# Visibilidad

![[2023-09-20_11-12.png]]

**Strings**: Los strings son inmutables. En java si haces
```java
Cliente cJuan = new Cliente();
String s = cJuan.getName; //s = Juan
s = s + "TONTO";  // s = Juan Tonto
// cJuan.name = Juan
```

S hace una copia y el original queda desreferenciado para q el garbage collector lo elimine

```java
class Cliente {
	...
	public Cuenta getCuenta() {
	return new Cuenta (cuenta);
	}
...
}
```

De esta manera también hacemos inmutables otros tipos diferentes

## Modificadores de atributos

* **static**
	Los atributos pertenecen a la clase y no a una instancia en particular.
	Pueden ser modificados sin que exista una instancia creada de la
	clase
* **final**
	Atributos constantes. Una vez que le hemos asignado un valor no es posible cambiarlo
	El valor debe asignarse en el constructor

```java
public Persona (String identificador) {
DNI = identificador;
}
```

## Record
Los registros (`record`) son una característica introducida en Java a partir de la versión 16. Los registros se utilizan para crear clases inmutables y simples para almacenar datos. Son una forma concisa de definir clases que solo contienen campos y métodos de acceso (getters) para esos campos. Un registro en Java se declara usando la palabra clave `record`. Aquí hay un ejemplo:


```java
record Persona(String nombre, int edad) {     // No es necesario definir métodos getter o equals/hashCode/toString }
```

## abstract 
La palabra clave `abstract` se utiliza para definir una clase abstracta en Java. Una clase abstracta es una clase que no puede ser instanciada directamente, pero puede ser extendida por otras clases concretas. Puedes tener métodos abstractos (sin implementación) dentro de una clase abstracta que deben ser implementados por las clases hijas. Aquí tienes un ejemplo:

```java
abstract class Figura {
abstract double calcularArea();
}
```

## final
La palabra clave `final` se puede aplicar a una clase, método o variable en Java.

- Cuando se aplica a una clase, significa que la clase no puede ser heredada.
- Cuando se aplica a un método, significa que el método no puede ser sobrescrito por clases hijas.
- Cuando se aplica a una variable, significa que la variable es una constante y su valor no puede ser modificado una vez asignado.

Ejemplos:
```java
final class ClaseFinal {
    // Esta clase no puede ser heredada.
}

class Padre {
    final void metodoFinal() {
        // Este método no puede ser sobrescrito por clases hijas.
    }
}

class MiClase {
    final int VALOR_CONSTANTE = 10;
    // VALOR_CONSTANTE es una constante y no puede ser modificado.
}
```
