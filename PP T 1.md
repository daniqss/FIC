---
tags:
  - 2º
  - PP
Fecha: "[[2023-09-12]]"
Asignatura: "[[Paradigmas da Programación]]"
---

ocaml: runtime de ocaml
ocamlopt: produce código máquina

## Ocaml

``` ocaml
2. +. 4.4
;;                    #Para ejecutar 
```

```ocaml
"para" ^ "sol"
;;
```

Concatenar strings

```ocaml
2 *. 3.4;;
Error: This expression has type int but an expression was expected of type
         float
  Hint: Did you mean `2.'?
```

Error en tiempo de compilación.  2 es int y 3.4 es float

```ocaml
# 2 / 0;;
Exception: Division_by_zero.
```

Error en tiempo de ejecución