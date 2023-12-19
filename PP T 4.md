---
tags:
  - 2º
Fecha: "[[2023-11-07]]"
Asignatura: "[[Paradigmas da Programación]]"
---
# Listas

### Length

```ocaml
let length l = List.fold_left (fun n _ -> n + 1) 0 l;;
```

- `let length l = ...` : Esta línea define una función llamada `length` que toma un argumento `l`, que se espera que sea una lista.

- `List.fold_left` es una función de la biblioteca estándar de OCaml que toma tres argumentos:
	- El primer argumento es una función anónima `(fun n _ -> n + 1)`. Esta función toma dos argumentos: `n` (que es el acumulador para el recuento) y `_` (que es un marcador para el elemento actual de la lista que no se usa en este caso, por eso se usa el guion bajo). La función incrementa el contador `n` en 1 cada vez que se llama, lo que efectivamente cuenta los elementos de la lista.
	- El segundo argumento es el valor inicial del acumulador, que es `0` en este caso.
	- El tercer argumento es la lista `l` sobre la cual se está operando.

Entonces, lo que hace esta función es recorrer la lista `l` y, para cada elemento, incrementa un contador en 1, comenzando desde 0. Al final del recorrido, devuelve el valor final del contador, que es la longitud total de la lista `l`.

### Sorted
sorted: 'a list -> bool
non compila
```ocaml
let rec sorted l = function 
	[] -> true
	| _::[] -> true (*simplifica si tienen mismo nombre*)
	| h1::h2::t -> h1 <= h2 && sorted (h2::t)
```

g_sorted: ('a -> 'a -> bool)
```ocaml
let rec g_sorted l = function 
	[] -> _::[] -> true (*simplifica si tienen mismo nombre*)
	| h1::h2::t -> h1 ord h2 && g_sorted ord (h2::t);;
```

### Insert

este insert no es recursivo terminal
```ocaml
let rec insert x = function
	[] -> [x]
	| h::t -> if x <= h then x::h::t
			  else h::insert x t

```


### Isort ()

este insertion sort no es recursivo terminal
```ocaml
let rec isort = function 
	[] -> []
	| h::t -> insert h (isort t);;

```


