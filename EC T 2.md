---
tags:
  - 2º
Fecha: "[[2023-09-22]]"
Asignatura: "[[Estrutura de Computadores]]"
---
# Paralelismo a nivel de instrucción

![[EC2-ES-Procesador_segmentado.pdf]]


Etapas de una instrucción MIPS en el camino de datos:
* IF: búsqueda de instrucciones
* ID: decodificación de instrucciones y lectura del banco de registros
* EX: ejecución o cálculo de direcciones 
* MEM: acceso a memoria para buscar un dato 
* WB: escritura de resultados

# Riesgos

## De datos
* RAW -> j intenta leer un dato antes de que i lo escriba. Se corresponde con una dependencia verdadera ->
	*  Una instrucción depende de los resultados de una instrucción anterior, de forma que ambas no podrían ejecutase de forma solapada.

* WAW -> j intenta escribir un operando antes de que éste sea escrito por i. Se corresponde con una dependencia de salida
	* Una dependencia de salida se produce cuando la instrucción i y la instrucción j escriben en el mismo registro o en la misma posición de memoria.

* WAR -> j trata de escribir en su destino antes de que este sea leído por i. Se corresponde con una antidependencia ->
	* Se produce una antidependencia entre la instrucción i y la j cuando la instrucción j escribe un registro o una posición de memoria que lee la instrucción i.