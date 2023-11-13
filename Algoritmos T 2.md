---
tags:
  - 2º
Fecha: "[[2023-10-05]]"
Asignatura: "[[Algoritmos]]"
---
# Estructuras de datos I

![[pilas_colas_listas.pdf]]


### Pilas
implementacion en vector porque las operaciones sobre la pila será O(1). Sino sería como mínimo O(n).

### Listas
con nodo cabecera para simplificar el código de la inserción y la eliminación eliminando el caso de tener que operar sobre el comienzo de la lista.

##### Doblemente enlazadas
CONTRAS:
* aunque O() no cambia, el tiempo es mayor ya que hay q actualizar dos punteros
* Duplica el uso de memoria. Los punteros ocupan mucha memoria (4 bytes mínimo)
PROS:
* La eliminación se simplifica ya que no hay que buscar el elemento anterior