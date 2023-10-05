---
tags:
  - 2º
Fecha: "[[2023-10-02]]"
Asignatura: "[[Deseño de Software]]"
---
# Herencia

Todas as clases heredan da clase Object. As clases q heredan doutras ou q as teñen como atributos (composición) teñen dentro aos outros obxetos e chámase a todos os constructores. 

### Tipos de herencia
Java ten herencia simple, unha clase solo pode extender a outra
En C++ ou python hai herencia multiple. O árbol de herencia ten forma de grafo e pode dar lugar a duplicidades se unha clase pode herdar de varias clases q herden da mesma clase e sobreescriban os mesmos atributos.

# Clases abstractas

clases q non se poden instanciar e sirven para ser extendidas para outras clases.

```java
public abstract class Animal {
	private String name;
	
	public String getName () {
		return name;
	}
}

public class Gato extends Animal {
	public enum variedadGato
		{SIAMES, ESFINGE}
}
```

Los métodos abstractos están hechos para obligar a las subclases a implementar el método
### Palabra reservada @Override

Dice q sobrescribe un método de la superclase. 

# Interfaces

como clases pero con herencia múltiple. Sirven para capturar las similitudes entre clases no relacionadas
no tiene implementacion y necesita una clase q implemente sus metodos. Una clase puede implementar varias interfaces.

![[2023-10-04_10-48.png]]


