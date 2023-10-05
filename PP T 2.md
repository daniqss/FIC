---
tags:
  - 2º
Fecha: "[[2023-09-29]]"
Asignatura: "[[Paradigmas da Programación]]"
---
## Definición de funciones

```ocaml
let doble = function x -> 2 * x;;
(*igual a *)
let doble x = 2 * x;;
```

```ocaml
let id x = x;;
(*val id : 'a -> 'a = <fun>*)
id int_of_char;;
(*# id int_of_char;;
- : char -> int = <fun>*)
```
Con esta declaración declaramos todas las funciones identidad para cualquier tipo de dato.
Esto es un ejemplo de polimorfismo

```ocaml
id abs (-7)
(* (id abs) (-7) *)
(*La aplicación de funciones es asociativa por la izquierda*)
```

```ocaml
let abs x = if x < 0 then -x else x
abs (-6)
```

### If then else 
```
if <b> then <e1> else <e2> : τ
<b> : bool
<e1> : τ
<e2> : τ (del mismo tipo que e1)
```

Sin if else la podemos definir usando lambda cálculo
```ocaml
let abs = 
	(function x)
```

# funciones con funciones


### (int->int) -> int
```ocaml
let f1 = function f -> f 1;;
(*val f1 : (int -> 'a) -> 'a = <fun>*)
let f2 = function f -> 2 * f 1;
(*val f2 : (int -> int) -> int = <fun>*)
```

### int -> (int->int)
```ocaml
let f1 = function i -> (function j -> i + j);;
(* val f1 : int -> int -> int = <fun> *)

(*
# f1 10;;
- : int -> int = <fun>
# (f1 10) 2;;
- : int = 12
*)
```

El argumento de f1 es 10 y el 2 es el argumento de s(10).