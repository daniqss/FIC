---
tags:
  - 2º
Fecha: "[[2023-09-14]]"
Asignatura: "[[Sistemas Operativos]]"
---
## Intervención hardware

en x86 tememos el chip 

Interrupcion que genera un dispositivo externo. Eventos asincronos, no incrementan el contador del programa y no tienen una alta prioridad

## Interrupción software
Simulacion de interr. hardware con una instrucción máquina ("INT86 nº de interrupción" en intel x86). Los procesadores tienen dos modos de funcionamiento
* **Modo privilegiado o kernel**: 
	Se pueden ejecutar todo el repertorio de instrucciones
* **Modo normal o usuario**: 
	No se pueden ejecutar instrucciones IO
Dependiendo de la interrupción el procesador pasa de normal a privilegiado
![[2023-09-14_10-46.png]]

cuando el compilador de c se encuentra una llamada al sistema (como fork() o open()) se da cuenta que no es una función de c. Tiene que realizar una intervencion software y el procesador pasa a modo privilegiado. ![[2023-09-14_10-54.png]]

Cuando se ejecutan nuestras funciones o otras de libreria esta en modo normal.

Los procesos estan cambiando continuamente entre usuario y kernel. Cuando una función de libreria tambien llama al sistema. Por ejemplo printf llama a write() (write(1 *"Descriptor de fichero"*, buffer, nº bytes a escribir))

# Allocation Methods



Cuando se genera un fichero se le asigna un inodo en la lista de inodo
En cada uno de los inodos hay informacion basica del fichero y los sectores del area de datos que ocupa el fichero

Unix surge en los Lab Bell del MIT. Primer operativo en un lenguaje de alto nivel (C). System V es un Unix con éxito comercial y el sistema de fkicheros queda con ese nombre.
Cada sistema operativo tiene una estructuración diferente

Numero mayor y menor investigar, interesan para el inodo


### /proc

En el directorio /prod (con sistema de ficheros virtual) tenemos un directorio por cada proceso multiprogramado.


