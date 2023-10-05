---
tags:
  - 2º
  - DS
Fecha: "[[2023-09-13]]"
Asignatura: "[[Deseño de Software]]"
---
# POO

##### Diseño Top-Down
Consiste en ir descomponiendo el programa sistematicamente en paretes más pequeñas y manejables

##### Diseño Down-Top
Consiste en comenzar el diseño identificando las estructuras básicas de
datos del programa, su comportamiento y sus interacciones. El programa
se construye combinando entre sí estos bloques básicos.

## 

# Clases

```java
public class Caja {
	// Atributos
	private int valor;
	
	// Métodos
	public void setValor (int v) {
		valor = v;
	}
	public int getValor () {
		return valor;
	}
	public void equals(Caja y) {
		return this.valor == y.valor
		// Siempre es recomendable hacer un método equals
	}
	
	// Constructores
	public Caja() {
		valor = 0;
	}
	public Caja(int v) {
		valor = v;
	}
}
```
Ejemplo de una clase en Java con atributos, métodos y constructores

```java
Caja x = new Caja();
x.setValor(11);

Caja y = new Caja();
y.setValor(11);
// OR
Caja x = new Caja();
x.setValor(11);
Caja y = new Caja();
y.setValor(11);


// Comparación de identidad
if (x==y) System.out.println ("x e y son identicos");
else System.out.println ("x e y NO son identicos");

// Comparaci´on de igualdad
if (x.equals(y)) System.out.println ("x e y son iguales");
else System.out.println ("x e y NO son iguales")
```
 
### Equals

#### Reflexividad
x.equals(x) debe devolver true.
#### Simetría
x.equals(y) debe devolver lo mismo que y.equals(x).
#### Transitividad
Si x.equals(y) devuelve true y y.equals(z) devuelve true
entonces x.equals(z) debe devolver true.
#### Consistencia
Si no se modifica el estado de los objetos que se usa para la
comparaci´on repetidas llamadas a x.equals(y) deber´ıan
responder siempre lo mismo.

#### Uso de nulos
x.equals(null) debe devolver false para cualquier valor x no
nulo.





