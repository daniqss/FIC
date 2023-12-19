---
tags:
  - 2º
Fecha: "[[2023-11-14]]"
Asignatura: "[[Paradigmas da Programación]]"
---
# Options

```ocaml
# None;;
- : 'a option = None
# Some 3;;
- : int option = Some 3
# Some true;;
- : bool option = Some true
# [Some 2; Some 3; None];;
- : int option list = [Some 2; Some 3; None]
```

```ocaml
let print_first_pos = 
	match List.find_opt((<) 0) l with
	None -> print_endline "No hay ningun positivo"
	| Some n -> print_endline (string_of_int n)
;;
```

## Problema de las n reinas
[Problema de las 8 reinas](https://es.wikipedia.org/wiki/Problema_de_las_ocho_reinas)

```ocaml
let come (i1, j1) (i2, j2) = 
	i1 = i2 || j1 = j2 || abs (i2-i1) = abs (j2-j1);;

let compatible p l =
	not (List.exists (come p) l);;

let queens n = 
	let rec completa path i j = 
		if i < n then Some path
		else if j > n then None
		else if compatible (i, j) path
			then completa ((i, j)::path) (i + 1, 1)
			else None;;


```
