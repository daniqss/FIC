---
tags:
  - 2º
Fecha: "[[2023-10-24]]"
Asignatura: "[[Paradigmas da Programación]]"
---
```ocaml
let rec div x y = 
	if x < y then (0,x)
	else 1 + fst (div (x - y) y),
		snd (div (x - y) y);;

let rec fib n = 
	if n <= 1 then n
	else fib (n - 1) + fib (n + 2);;

let crono f x =
	let t = Sys.time () in 
	let _ = f x in 
	Sys.time () -. t;;

let rec fib2 = function
	1 -> (1, 0)
	| n -> let f1, f2 = fib2 (n - 1) in 
		(f1 + f2, f1);;

let ffib n = fst (fib2 n);;

```

```ocaml
let fib' n =
	let rec aux (i, f, a) = 
		if i = n then f
		else aux (i + 1, f + a, f)
	in aux (0,0,1);;

let rec rep n f x = 
	if n = 0 then ()
	else let _ = f x in
		rep (n - 1) f x;;
```



