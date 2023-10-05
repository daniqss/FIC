---
tags:
  - 2º
  - PP
Fecha: "[[2023-09-19]]"
Asignatura: "[[Paradigmas da Programación]]"
---

## Salida por Pantalla

**Strings**: 
```ocaml
print_endline "Daniel Queijo Seoane";
print_endline "daniel.queijo.seoane@udc.es";
```

**Printf**:
```ocaml
let pi = 2.0 *. asin 1.0;;
Printf.printf "%.15f\n" pi;
```

## Funciones

```ocaml
let rec factorial n =
    if n <= 1 then
        1
    else
        factorial (n-1) * n;;

let rec aprox_e n =
    let e = ref 0.0 in
    for i = 0 to n do
        e := !e +. 1. /. float_of_int (factorial i);
        (* Printf.printf "%d! = %d\n" i (factorial i) *)
    done;
    !e;;

let () = 
    Printf.printf "%f\n" (aprox_e 10000);

```



