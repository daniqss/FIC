---
tags:
  - 2º
Fecha: "[[2023-12-12]]"
Asignatura: "[[Paradigmas da Programación]]"
---
# Structs

```ocaml
type person = {
	name: string;
	age: int;
}

let p1 = { name = "Pepe"; age = 42; };;
let p2 = { name = "Juan"; age = 23; };;

  
let older p = {
	p with age = p.age + 1;
}
(* Crea otro struct igual pero con un año más *)

let ord p1 p2 =
	p1.age < p2.age ||
	p1.age = p2.age && p1.name <= p2.name
;;
```


## Mutabilidad

```ocaml
(* Mismo struct pero con campo mutable *)

type person = {
	name: string;
	mutable age: int;
}

  
let aged p = p.age <- p.age + 1;;

(* val aged : person -> unit = <fun> *)
```

## Constructor de tipos mutable

Implementación de 'a ref en ocaml (sirve para crear referencias mutables)

```ocaml
type 'a var = {
	mutable valor: 'a
};;

  
let init_var x = {
	valor = x
};;

  
(* Implementación de re *)
let (!!) v = v.valor;;
let (<<) v x = v.valor <- x;;
```


# Módulos

counter.ml
```ocaml
let n = ref 0;;
(* val n : int ref = {contents = 0} *)

let next () =
	n := !n + 1;
	!n
(* val next : unit -> int = <fun> *)

let reset () =
	n := 0


```

counter.mli
```ocaml
val next : unit -> int
val reset : unit -> unit
```

Compilación
```bash
ocamlc -c counter.mli counter.ml
ocamlc -o mi_programa counter.cmo # compila el programa
```

Uso
```ocaml
(* Cargar el módulo Counter *)
#load "counter.cmo";;
(* Importar las funciones desde el módulo *)
open Counter;;
```

## Functores

```ocaml
module Contador () : sig
	val next : unit -> int
	val reset : unit -> unit
end = struct
	let n = ref 0;;
	let next () =
		n := !n + 1;
		!n
	
	let reset () =
		n := 0
end;;

(* functor () -> sig val next : unit -> int val reset : unit -> unit end *)
```


# Orientación a objetos

No tienes que explicitar el tipo, lo infiere el compilador

El tipo de un objeto lo determina los tipos de sus atributos y sus métodos
Este objeto es inmediato, no esta en una clase.
```ocaml
(* Otro puto contador pero esta vez con POO *)

let counter = object
	val mutable n = 0
	method next: int = n <- n + 1; n
	method reset: unit = n <- 0
end;;

counter#next
(* - : int = 1 *)
```

## Clases

```ocaml
class counter = object
	val mutable n = 0
	method next: int = n <- n + 1; n
	method reset: unit = n <- 0
end;;

let c1 = new counter
and c2 = new counter;;
(*
val c1 : counter = <obj>
val c2 : counter = <obj>
*)
```

`counter` es un alias de `object val mutable n : int method next : int method reset : unit end`

## Herencia

```ocaml
class counter_with_set = object
	inherit counter
	method set x = n <- x
end;;

let c3 = new counter_with_set;;
(* val c3 : counter_with_set = <obj> *)
(c3 :> counter);;
(* - : counter = <obj> *)

let list = [c1; c2; (c3 :> counter)];;
(* val list : counter list = [<obj>; <obj>; <obj>] *)


```

Podemos restringir un objeto a la clase de la que hereda, podiendo hacer cosas como una lista de objetos de clase (y por ende tipo) diferentes, porque en la lista metes la "instancia" del objeto heredado

## Clases abstractas

```ocaml
class virtual foo1 = object
	method virtual m: int
end;;

let o = new foo1;;
(* Error: Cannot instantiate the virtual class foo1 *)

class foo2 = object
	inherit foo1
	method m = 0
end;;



let example = new foo2;;
example#m;;
(* - : int = 0 *)
(example :> foo1)#m;;
# (example :> foo1)#m;;
(* - : int = 0 *)

```

## Encapsulamiento

```ocaml
class foo3 = object
	val o = new foo2
	method m = o#m     
end;;
(* LLamamos al metodo del objeto de dentro *)

```

## Construir con parámetros y inicializador

Volvemos al contador

```ocaml
class counter_with_init ini = object (self)
	inherit counter_with_set
	method reset = self#set ini    (* n <- ini *)
	
	initializer self#reset
end;;
```


## Herencia múltiple

En Ocaml hay herencia múltiple y los inicializadores se ejecutan en orden según se hereden. Los métodos de las clases padre no se eliminan al sobreescribirse, se ocultan y se puede acceder a ellos con los aliases de los padres

```ocaml
class counter_with_step = object (self)
	inherit counter_with_init 0 as super
	val mutable step = 1
	method next = n <- n + step; n
	method set_step s = step <- s
	method reset = super#reset; self#set_step 1
end;;
```

## Clases polimórficas

```ocaml
exception EmptyStack;;

class ['a] stack = object 
	val mutable l = ([]: 'a list)
	method push x =
		l <- x :: l
	method pop = 
		match l with
		| [] -> raise EmptyStack
		| h::t -> l <- t; h
	 method peek =
		 match l with
		 | [] -> raise EmptyStack
		 | h::_ -> h
end;;
```

`['a]` es comparable con 
```ocaml
type 'a bintree =
	Empty
	| Node of 'a * 'a bintree * 'a bintree;;
```



