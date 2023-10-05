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

