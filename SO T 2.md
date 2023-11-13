---
tags:
  - 2º
Fecha: "[[2023-10-05]]"
Asignatura: "[[Sistemas Operativos]]"
---

# Memory management

![[OS-Memory+VM.pdf]]

### Endianness
El término inglés _**endianness**_ (en español **extremidad** y a veces **endianidad**) designa el formato en el que se almacenan los datos de más de un byte en un ordenador. El problema es similar a los idiomas en los que se escriben de derecha a izquierda, como el árabe, o el hebreo, frente a los que se escriben de izquierda a derecha, pero trasladado de la escritura al almacenamiento en memoria de los bytes.

### Fragmentación de memoria
* **Fragmentación Interna**: Memoria malgastada debido a la asignaciónn en bloques de n bytes y las peticiones de procesos que no son exactamente múltiplos de n bytes.

### Arquitectura 64 bits
No son realmente 64 bits. Son 48 bits virtuales y 52 bits físicos.

Los 16 bits más significativos de una dirección virtual (recuerde, sólo 48 bits son significativos) son todos ceros o todos unos. Son iguales al bit más significativo de la dirección virtual de 48 bits.


## Page replacement, fetching and replacement



