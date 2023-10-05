---
tags:
  - 2º
Fecha: "[[2023-09-25]]"
Asignatura: "[[Algoritmos]]"
---

### Pseudocódigo

var => variable de entrada salida
para => bucle for
mientras => bucle while
si => bucle if
fin para fin procedimiento fin mientras => en c las llaves
; => separador de las intrucciones, si despues hay un fin no ponemos punto y coma ya        q si no el seudo codigo espera otra instrucción
```
mientras j>0 y T[j]>x hacer
	T[j+1]:=T[j];
	j:=j‐1
fin mientras;;
```
:= operador asignación

algoritmos homogeneos el tiempo q tardan no es influido por la entrada
los no homogeneos son mejores o peores dependiendo de la entrada

#### Selección

Algoritmo homogéneo con complejidad cuadrática
Fai unha operación de intercambio por ciclo, polo que pode ser útil cando a operación de intercambio é moi custosa

#### Búsqueda binaria

``` 
función BúsquedaBinariaRecursiva(x, var a[1...n], i, j): posición
	
	si 
	medio := (i + j) div 2 ;
	
	si a[medio] < x entonces
		BBR(x, a[1...n], i, medio)
		
	sino si a[medio] > x entonces
		BBR(x, a[1...n], medio, j)
		
	sino si a[medio] = x entonces
		devolver a[medio]
		
	sino devolver -1
	
fin función

```

Solución:
```
función BúsquedaBinariaRecursiva(x, var a[1...n], i, j): posición
	
	si i > j entonces devolver 0 
	sino si i = j entonces
		si a[i] = x entonces devolver i
		sino devolver 0
	sino i < j
	medio := (i + j) div 2 ;
	
	si a[medio] < x entonces
		devolver BBR(x, a[1...n], medio + 1 , j)
		
	sino si a[medio] > x entonces
		devolver BBR(x, a[1...n], medio, j) MAL
		
	sino devolver a[medio]
	
fin función

```


