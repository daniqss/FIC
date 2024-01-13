---
tags:
  - 2º
Fecha: "[[2023-12-12]]"
Asignatura: "[[Paradigmas da Programación]]"
---
### Referencias Mutables con la Palabra Clave `ref`

En OCaml, la palabra clave `ref` se utiliza para crear referencias mutables.
En este caso, `contador` es una referencia mutable que inicialmente contiene el valor `0`. Puedes acceder y modificar el valor utilizando las funciones `!` y `:=` respectivamente:

```ocaml
let contador = ref 0;;
let valor_actual = !contador;;  (* Obtiene el valor actual *) contador := 10;;              (* Asigna un nuevo valor *)`
```

Esta forma de referencia mutable es útil cuando necesitas actualizar y compartir valores mutables en diferentes partes de tu programa. Por ejemplo, podrías usarlo para mantener un contador que se actualiza en varias funciones.

Aquí hay un ejemplo más completo utilizando un contador:
```ocaml
let contador = ref 0;;  let incrementar_contador () =   contador := !contador + 1;;  let obtener_valor_contador () =   !contador;;  let reiniciar_contador () =   contador := 0;;
```

En este caso, `incrementar_contador` aumenta el valor del contador, `obtener_valor_contador` devuelve el valor actual, y `reiniciar_contador` restablece el contador a cero.
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

1. **Uso del Functor:**

```ocaml
(* functor () -> sig val next : unit -> int val reset : unit -> unit end *)
```

Este comentario muestra cómo se usa el functor `Contador`. Al aplicar el functor con `()`, se obtiene un módulo que satisface la firma especificada en `sig`.

2. **Ejemplo de Uso del Módulo Generado por el Functor:**


```ocaml
let contador_modulo = Contador ();; (* Crear un módulo usando el functor *)
contador_modulo.next ();;           (* Incrementar el contador *) contador_modulo.reset ();;          (* Reiniciar el contador *)
```

Aquí, `contador_modulo` es un módulo generado por `Contador`, y puedes usar las funciones `next` y `reset` proporcionadas por el módulo. Este enfoque es útil cuando deseas tener múltiples contadores independientes en tu programa y no quieres que compartan el mismo estado.


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

# Arrays

To create an array in OCaml, you can use the `[| ...; ... |]` syntax, which allows you to specify the values of each element directly. For example, to create an array with the values 1, 2, 3, 4, and 5, you will write `[| 1; 2; 3; 4; 5 |]`:

```ocaml
# [| 1; 2; 3; 4; 5 |];;
- : int array = [|1; 2; 3; 4; 5|]
```

Alternatively, you can create an array using the `Array.make` function, which takes two arguments: the length of the array and the initial value of each element. For example, to create an array of length 5 with all elements initialised to 0, you can write:

```ocaml
# let zeroes = Array.make 5 0;;
val zeroes : int array = [|0; 0; 0; 0; 0|]
```

`Array.init` generates an array of a given length by applying a function to each index of the array, starting at 0. The following line of code creates an array containing the first 5 even numbers using a function which doubles its argument:

```ocaml
# let even_numbers = Array.init 5 (fun i -> i * 2);;
val even_numbers : int array = [|0; 2; 4; 6; 8|]
```

## Array Elements

You can access individual elements of an array using the `.(index)` syntax, with the index of the element you want to access. The index of the first element is 0, and the index of the last element is one less than the size of the array. For example, to access the third element of an array `even_numbers`, you would write:

```ocaml
# even_numbers.(2);;
- : int = 4
```

## Array Elements

To modify an element in an array, we simply assign a new value to it using the indexing operator. For example, to change the value of the third element of the array `even_numbers` created above to 42, we have to write:

```ocaml
# even_numbers.(2) <- 42;;
- : unit = ()
```

Note that this operation returns `unit`, not the modified array. `even_numbers` is modified in place as a side effect.

## Standard Library `Array` Module

OCaml provides several useful functions for working with arrays. Here are some of the most common ones:

### of an Array

The `Array.length` function returns the size of an array:

```ocaml
# Array.length even_numbers;;
- : int = 5
```

### on an Array

`Array.iter` applies a function to each element of an array, one at a time. The given function must return `unit`, operating by side effect. To print all the elements of the array `zeroes` created above, we can apply `print_int` to each element:

```ocaml
# Array.iter (fun x -> print_int x; print_string " ") zeroes;;
0 0 0 0 0 - : unit = ()
```

Iterating on arrays can also be made using `for` loops. Here is the same example using a loop:

```ocaml
# for i = 0 to Array.length zeroes - 1 do
    print_int zeroes.(i);
    print_string " "
  done;;
0 0 0 0 0 - : unit = ()
```

### Map an Array

The `Array.map` function creates a new array by applying a given function to each element of an array. For example, we can get an array containing the square of each number in the `even_numbers` array:

```ocaml
# Array.map (fun x -> x * x) even_numbers;;
- : int array = [|0; 4; 1764; 36; 64|]
```

### Folding an Array

To combine all the elements of an array into a single result, we can use the `Array.fold_left` and `Array.fold_right` functions. These functions take a binary function, an initial accumulator value, and an array as arguments. The binary function takes two arguments: the accumulator's current value and the current element of the array, then returns a new accumulator value. Both functions traverse the array but in opposite directions. This is essentially the same as `List.fold_left` and `List.fold_right`.

Here is the signature of `Array.fold_left`:

```ocaml
# Array.fold_left;;
val fold_left : ('a -> 'b -> 'a) -> 'a -> 'b array -> 'a = <fun>
```

`fold_left f init a` computes `f (... (f(f init a.(0)) a.(1)) ...) a.(n-1)`

Similarly, we can use the `Array.fold_right` function, which switches the order of its arguments:

```ocaml
# Array.fold_right;;
val fold_right : ('b -> 'a -> 'a) -> 'b array -> 'a -> 'a = <fun>
```

`fold_right f a init` computes `f a.(0) (f a.(1) ( ... (f a.(n-1) init) ...))`

These functions derive a single value from the whole array. For example, they can be used to find the maximum element of an array:

```ocaml
# Array.fold_left Int.max min_int even_numbers;;
- : int = 42
```

### Sort an Array

To sort an array, we can use the `Array.sort` function. This function takes as arguments:

- a comparison function
- an array It sorts the provided array in place and in ascending order, according to the provided comparison function. Sorting performed by `Array.sort` modifies the content of the provided array, which is why it returns `unit`. For example, to sort the array `even_numbers` created above, we can use:

```ocaml
# Array.sort compare even_numbers;;
- : unit = ()
# even_numbers;;
- : int array = [|0; 2; 6; 8; 42|]
```

## Part of an Array into Another Array

The `Array.blit` function efficiently copies a contiguous part of an array into an array. Similar to the `array.(x) <- y` operation, this function modifies the destination in place and returns `unit`, not the modified array. Suppose you wanted to copy a part of `ones` into `zeroes`:

```ocaml
# let ones = Array.make 5 1;;
val ones : int array = [|1; 1; 1; 1; 1|]
# Array.blit ones 0 zeroes 1 2;;
- : unit = ()
# zeroes;;
- : int array = [|0; 1; 1; 0; 0|]
```

This copies two elements of `ones`, starting at index `0` (this array slice is `[| 1; 1 |]`) into `zeroes`, starting at index `1`. It is your responsibility to make sure that the two indices provided are valid in their respective arrays and that the number of elements to copy is within the bounds of each array.

We can also use this function to copy part of an array onto itself:

```ocaml
# Array.blit zeroes 1 zeroes 3 2;;
- : unit = ()
# zeroes;;
- : int array = [|0; 1; 1; 1; 1|]
```

This copies two elements of `zeroes`, starting at index `1` into the last part of `zeroes`, starting at index `3`.

