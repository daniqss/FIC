---
tags:
  - 2º
  - DS
Fecha: "[[2023-09-13]]"
Asignatura: "[[Deseño de Software]]"
---
# Práctica 1

### Arrays

```java
int[] numbers1 = {4, 9, 3, 6, 2}; // five positions
int[] numbers2 = new int[10];
for (int i=0; i<numbers1.length; i++) {
	numbers2[i] = numbers1[i]; // copy items
}
numbers1 = numbers2; // numbers1 points to numbers2
System.out.println(numbers1[0]); // 4
System.out.println(numbers1.length); // numbers1 has 10 positions

numbers1[15] = 42; // Throws ArrayIndexOutOfBoundsException
```

#### Matrices

```java
int[][] matrix = {{1, 2, 3},
				  {4, 5, 6},
				  {7, 8, 9}};
System.out.println(matrix[1][2]); // 6
```

En Java las filas de la matriz pueden tener diferentes tamaño de filas

```java

```


### Strings

En java los strings son inmutables. Para hacer strings mutables utilizaremos la clase StringBuilder

```java
String s1 = "Hello World"; // String literals
String s2 = s1.toUpperCase(); // s1 is immutable
System.out.println("s1 = " + s1); // s1 = Hello World
System.out.println("s2 = " + s2); // s2 = HELLO WORLD

StringBuilder sb = new StringBuilder("Hello");
sb.append(" World"); // StringBuilder is mutable
System.out.println("sb = " + sb); // "sb = HelloWorld";
```


#### toString

```java
public class Caja {
	private int valor;
	public void setValor(int v) {valor = v;}
	public int getValor() { return valor; }
	public Caja(int v) {valor = v; }
	
	@Override
	public String toString() {
	return "[Valor: " + valor + "]";
	}
	
	public static void main(String[] args) {
		Caja c = new Caja(5);
		System.out.println("Caja = " + c);
	} // Imprime "Caja = [Valor: 5]"
}
```

### javadoc

Con /** podemos hacer javadocs con etiquetas (@param, @return, @author). Con javadoc podemos generar documentación HTML desde nuestro código

```java
/**
* Fija el valor de x al valor de i
* (si es mayor que cero)
* @param i Valor para inicializar x
*/
```


### If

```java

```

### Switch

```java
switch (day) {
	case MONDAY:
	case FRIDAY:
	case SUNDAY:
		numLetters = 6;
		break;
	case TUESDAY:
		numLetters = 7;
		break;
	case THURSDAY:
	case SATURDAY:
		numLetters = 8;
		break;
	case WEDNESDAY:
		numLetters = 9;
		break;
	default:
		throw new IllegalStateException("Wat: " + day);
}
```

Mejor implementación sin break: 
```java
numLetters = switch (day) {
	case MONDAY, FRIDAY, SUNDAY -> 6;
	case TUESDAY -> 7;
	case THURSDAY, SATURDAY -> 8;
	case WEDNESDAY -> 9;
};
```

### While

```java
// while loop
int count = 0;
while (count < 10) {
	count++;
}
System.out.println("count = " + count);
// do..while loop
count = 0;
do {
	count++;
} while (count < 10) ;
System.out.println("count = " + count);
```

### For y For-each

```java
// Classic for
for(int i = 0; i<10; i++) {
	System.out.println(i);
}

// For-each loop
int[] data = {0, 1, 2, 3, 4, 5};
for(int i : data) {
	System.out.println(i); // 0 1 2 3 4 5
}
```


### Excepciones

Evento an´omalo o excepcional que ocurre durante la ejecuci´on de un
programa y que requiere de un tratamiento especial.

