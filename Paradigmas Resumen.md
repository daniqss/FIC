---
tags:
  - 2º
Fecha: "[[2024-01-11]]"
Asignatura: "[[Paradigmas Resumen]]"
---
# Operaciones básicas

ocaml: runtime de ocaml
ocamlopt: produce código máquina
```ocaml
2. +. 4.4;;
# Resultado del Compilador
- : float = 6.4

"para" ^ "sol";;
# Resultado del Compilador
- : string = "parasol"
```

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

## Definiciones

### Como dar nombre a los valores (definirlos): 

`let pi = 2. *. asin 1.;;` -> calcula el valor y una vez calculado deja asociado al nombre el valor, **OJO, SOLO EL VALOR, NO LA EXPRESIÓN DE LA FÓRMULA !!**
Una vez hecha la definición podemos operar con el nombre del valor directamente, sin tener que volver a poner la función, lo que supone una ventaja en ahorro de operaciones y de limpieza del código: P.E.: `2. . pi;;` // `pi /. 2.;;`
**OJO:** estos valores definidos no son variables, son solo definiciones, no podemos editarlas después.

### La expresión "let in":
`let x = 3 in x + 1;;` -> **NO** es una definición global, sino una definición local, no es una definición, es una expresión. El valor dado a la x solo tiene valor después del in, no en el resto del código. Si después preguntamos cuánto vale x, saldrá error, pues "no existe".

`let pi = 5 in 2 * pi;;` -> saldrá que pi vale 10, pero una vez volvamos a preguntar el valor de pi, saldrá que vale 3.14...
Podemos definir un let in dentro de un let:
- let x = (*con solo un let, x es una variable GLOBAL*)
`let y = 3 in y + 2;;` (*con un let in, y es una variable LOCAL*)
Lo que saldrá de esto es que el valor de x = 5, pero el valor de 'y' no existe, pues el 'x' estaba dentro de un let, mientras que la 'y' estaba dentro de un 'let in'.

`let x, y = x + y, x * y in x + y;;` es una expresión, no una definición (a pesar de que tiene una dentro), ya que devuelve un valor.
Primero evalúa x + y = 5, luego x * y = 6, luego asigna los valores a x e y, x = 5 e y = 6, y luego realiza la suma del in x + y = 11.
## Salida por pantalla
```ocaml
print_endline "daniel.queijo.seoane@udc.es";;
Printf.printf "%.15f\n" 3.14;;
```

# Declarar tipos
El compilador de ocaml inferirá los tipos de las definiciones por nosotros, pero lo podemos hacer manualmente
```ocaml
let absf (x:float) : float =
	if x < 0.0 then -.x
	else x
```

# Sistemas de evaluación

## Eager o lazy

## Curryficación
Ejemplo de aplicación: `(s 10) 2;;` o sin parénetsis: `s 10 2;;`
`s` solo tiene un argumento, 10, mientras que 2 es el argumento de `s 10`.
`s` funciona igual que la suma de enteros. Es posible interpretar la suma binaria de enteros como una función.
Lo que permite reducir las operaciones binarias a funciones (lo que recibe el nombre de "a la Curry" o "de Curry", por Haskell Curry).
```ocaml
let s = function x -> function y -> x + y;;
(*También se puede escribir como*)
let s x = function y -> x + y;;
(*y como*)
let s x y = x + y;;
(*se utiliza como*) s 2 3;;
```

**OPERADORES INFIJOS COMO FUNCIONES CURRY:**
```ocaml
(+) (*int -> int -> int = <fun>*)
(^) (*string -> string -> string*)
( * ) (*int -> int -> int*)
( ** ) (*float -> float -> float*)
(<=) (*'a -> 'a -> bool = <fun>*)
(=) (*'a -> 'a -> bool = <fun>*)
(||) (*bool -> bool -> bool = <fun>*)
(&&) (*bool -> bool -> bool = <fun>*)
```

No existen las funciones de dos argumentos, sino las funciones que reciben un argumento de un par de enteros.
**CURRYFICAR (CURRY):** pasar una función que tiene esta forma A x B -> C, a otra de esta forma A -> B -> C
**DESCURRYFICAR (UNCURRY):** pasar de esta función A -> B -> C a esta otra A x B -> C
curry(A * B -> C) -> (A -> B -> C)
# Polimorfismo en pattern matching
```ocaml
let all_to_true = function _ -> true;;
(* val all_to_true : 'a -> bool = <fun> *)
```

# Lambda expresiones

### Sustituir if/else con lambda expresiones

Si `<b>` es una expresión correcta de tipo bool en OCaml y `<e1>` y `<e2>` son también dos expresiones correctas en OCaml (ambas del mismo tipo), entonces: 
```ocaml
if <b> then <e1> else <e2> 
es una expresión correcta en OCaml, del mismo tipo que <e1> y <e2>, que se evalúa igual que 
(function true -> <e1> | false -> <e2>) <b>
```

```ocaml
(*if x > y then "first is greater" else "second is greater";;*)
(function true -> "first is greater"
	| false -> "second is greater")
(x>y);;

(* if x > 0 then x else -x;; *)
(function true -> x | false -> -x) (x>0);;

(* if x > 0 then x else if y > 0 then y else 0;; *)
(function true -> x |
	false -> (function true -> y
		| false -> 0)
	(y>0))
(x>0);;

(* if x > y then if x > z then x else z 
	else if y > z then y
	else z;; *)
(function true -> (function true -> x | false -> z) (x>z)
	| false -> (function true -> y | false -> z) (y>z))
(x>y);;
```

# Tuplas

```ocaml
int * int -> 2,3
(int * int) * int -> (2, 3), 1 
(* una dupla de numeros cuya primera componente también es una dupla *)
int * int * int -> 2, 3, 1
```

#### Tuplas con componentes tupla
```ocaml
true, 0, "trio";;
(* - : bool * int * string = (true, 0, "trio") *)
(true, 0), "falso trio";;
(* - : (bool * int) * string = ((true, 0), "falso trio") *)
```
#### Tipo de la x?
```ocaml
let x = (true, abs);;
(* val x : bool * (int -> int) = (true, <fun>) *)
```
fst y snd nos permite obtener toda la información de un par:
(snd x) (-7);;
`(* - : int = 7 *)`

Las funciones fst y snd ya vienen definidas, pero si tuviéramos que definirlas:
```ocaml
let fst (x, y) = x;;
let fst (x, _ ) = x;; 
(*no le damos nombre a la segunda componente porque no se usa para obtener el resultado*)
```

# Listas

```ocaml
[1; 2; 3; 4; 5];;
- : int list = [1; 2; 3; 4; 5]
  
[6; 0];;
- : int list = [6; 0]

['a'];;
- : char list = ['a']
  
[true; true];;
- : bool list = [true; true]
  
[1,2];;
- : (int * int) list = [(1, 2)]
  
[()];;
- : unit list = [()]  

[(); ()]
- : unit list = [(); ()]
  
[];;
- : 'a list = []
```
Las seuencias deben ser finitas, 0 o más elementos todos del mismo tipo, es decir, las listas son homogéneas.

## Append recursivo terminal

```ocaml
let rec rev_append l1 l2 = match l1 with
	[] -> l2
	| h::t -> rev_append t (h::l2);;

let rev l = rev_append l [];;

let append' l1 l2 = rev_append (rev l1) l2;;
```

## comb recursiva terminal

```ocaml
let comb fn list =
	let rec aux fn list acc = match list with
		| [] -> acc
		| h::[] -> h::acc
		| h1::h2::t -> aux fn t (fn h1 h2::acc)
	in List.rev (aux fn list [])
;;
```

# Excepciones

```ocaml
Failure "hd";;
(* - : exn = Failure "hd" *)

Invalid_argument "ese argumento no vale";;
(* - : exn = Invalid_argument "ese argumento no vale" *)

Failure "no seas burro!";;
(* - : exn = Failure "no seas burro!" *)

Division_by_zero;;
(* - : exn = Division_by_zero *)
```
Tanto `Failure` como `Invalid_argument` pueden crear tantos valores como strings haya.

Pero `Division_by_zero` no acepta strings, por tanto solo puede devolver un valor posible.

```ocaml
let rec last = function
	[] -> raise (Failure "last")
	| h::[] -> h
	| _::t -> last t;;
```

## Intervención de excepciones

```
try <e> with

<p1> -> <e1>

|

.

.

.

| <pn> -> <en>

```
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

Ejemplos de funciones que utilizan Options
```ocaml
let print_first_pos = 
	match List.find_opt((<) 0) l with
	None -> print_endline "No hay ningun positivo"
	| Some n -> print_endline (string_of_int n)
;;

let rec find_opt f l =
	match l with
	| [] -> None
	| h::t -> if f h then h else find_opt f t
;;
(* Devuelve un 'a option *)
```



# Resultados del compilador

**`expr.ml`, práctica 1**
```ocaml
();;
(* unit = () *)
  
2 + 3 * 5;;
(* int = 17 *)
  
1.25 *. 2.;;
(* float = 2.5 *)
  
(* 2 - 2. *);;
(* This expression has type float but an expression was expected of type int *)
  
(* 2. + 3. *);;
(* Error: This expression has type float but an expression was expected of type int *)

5 / 3;;
(* int = 1 *)

5 mod 3;;
(* int = 2 *)
  
2.0 *. 3.0 ** 2.0;;
(* int = 18 *)

2.0 ** 3.0 ** 2.0;;
(* int = 512 *)
  
sqrt;;
(* float -> float = <fun> *)

(* sqrt 4 *);;
(* This expression has type int but an expression was expected of type float *) 

int_of_float;;
(* float -> int = <fun> *)

float_of_int;;
(* int -> float = <fun> *)

(* int_of_float -2.9;; *)
(* Error de tipo derivado de un error de sintaxis *)

int_of_float 2.1 + int_of_float (-2.9);;
(* int = 0 *)

truncate;;
(* float -> int = <fun> *)

truncate 2.1 + truncate (-2.9);;
(* int = 0 *)

floor;;
(* float -> float = <fun> *)

floor 2.1 +. floor (-2.9);;
(* float = -1 *)

ceil;;
(* float -> float = <fun> *)

ceil 2.1 +. ceil (-2.9);;
(* float = 1 *)

int_of_char;;
(* char -> int = <fun> *)

int_of_char 'A';;
(* int = 65*)

char_of_int;;
(* int -> char = <fun> *)

char_of_int 66;;
(* char = 'B'*)

Char.code;;
(* char -> int = <fun> *)

Char.code 'B';;
(* int = 66 *)

Char.chr;;
(* int -> char = <fun> *)

Char.chr 67;;
(* char = 'C' *)

'\067';;
(* char = 'C' *)

Char.chr (Char.code 'a' - Char.code 'A' + Char.code 'M');;
(* char = 'm' *)

Char.lowercase_ascii;;
(* char -> char = <fun> *)

Char.lowercase_ascii 'M';;
(* char = 'm' *)

Char.uppercase_ascii;;
(* char -> char = <fun> *)

Char.uppercase_ascii 'm';;
(* char = 'M' *)

"this is a string";;
(* string = "this is a string";; *)

String.length;;
(* string -> int = <fun> *)

String.length "longitud";;
(* int = 8 *)

(* "1999" + "1";; *)
(* This expression has type string but an expression was expected of type int *)

"1999" ^ "1";;
(* string = "19991" *)

int_of_string;;
(* string -> int = <fun> *)

int_of_string "1999" + 1;;
(* int = 2000 *)

"\065\066";;
(* string = "AB" *)

string_of_int;;
(* int -> string = <fun> *)

string_of_int 010;;
(* string = "10" *)
  
not true;;
(* bool = false *)

true && false;;
(* bool = false *)
  
true || false;;
(* bool = false *)
  
(1<2) = false;;
(* bool = false *)
  
"1" < "2";;
(* bool = true *)

2 < 12;;
(* bool = true *)

"2" < "12";;
(* bool = false *)

"uno" < "dos";;
(* bool = false *)

if 3 = 4 then 0 else 4;;
(* int = 4 *)

if 3 = 4 then "0" else "4";;
(* string = "4" *)

(* if 3 = 4 then 0 else "4";; *)
(* This expression has type string but an expression was expected of type int *)

(if 3 < 5 then 8 else 10) + 4;;
(* int = 12 *)
```

**`frases4.ml`, práctica 4**
```ocaml
let p = (1 + 1, asin 1.), true;;
(* val p : (int * float) * bool = ((2, 1.57079632679489656), true) *)
  
let (x, y), z = p;;
(*
val x : int = 2
val y : float = 1.57079632679489656
val z : bool = true
*)

let p1, p2 = p in let p11, _ = p1 in (p2, 2 * p11);;
(* - : bool * int = (true, 4) *)

let f (x, y) = 2 * x + y;;
(* val f : int * int -> int = <fun> *)

let f2 x y z = x + 2 * y + 3 * z;;
(* val f2 : int -> int -> int -> int = <fun> *)
  
let g x y z = x (y, z);;
(* val g : ('a * 'b -> 'c) -> 'a -> 'b -> 'c = <fun> *)
  
g fst 1 "hola";;
(* - : int = 1 *)

g snd fst true;;
(* - : bool = true *)

g f 2 3;;
(* - : int = 7 *)

g (function (f, x) -> f (f x)) (function x -> x*x) 3;;
(* - : int = 81 *)

let x, y, z= 1, 2, 3;;
(*
val x : int = 1
val y : int = 2
val z : int = 3
*)

f2 x y z;;
(* - : int = 14 *)

let x, y, z= y, z, x in f2 x y z;;
(* - : int = 11 *)

f2 x y z;;
(* - : int = 14 *)

let swap (x,y) = y,x;;
(* val swap : 'a * 'b -> 'b * 'a = <fun> *)

let p = 1, 2;;
(* val p : int * int = (1, 2) *)

f p;;
(* - : int = 4 *)

let p = swap p in f p;;
(* - : int = 5 *)

f p;;
(* - : int = 4 *)
```