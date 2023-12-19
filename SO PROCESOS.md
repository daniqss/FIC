---
tags:
  - 2º
Fecha: "[[2023-12-01]]"
Asignatura: "[[Sistemas Operativos]]"
---
# ÍNDICE

- **Procesos**:
	- Procesos en UNIX 
	- Modos de ejecución
	- Hilos y procesos
	- Espacio de direcciones
	- Reentrada en el kernel
-  **Estructuras de datos**:
	- `proc` struct
	- `u_area`
	- Credenciales
	- Variables de entorno
- **Ciclo de vida de los procesos en UNIX**
	- Estado de los procesos
	- fork()
	- exec()
	- exit()
	- Esperando a que finalice un hijo
- **Planificación de la CPU**



# Procesos

Un programa es un conjunto de instrucciones y un proceso es un programa en ejecución (no tiene porque estar siempre ejecutándose). Es una entidad creada por el SO para la ejecución de un programa. Consta de :
1. El espacio de direcciones que podría referenciar. Suele tener tres partes, el código del programa, las variables globales y el heap (memoria asignada dinámicamente) y la pila, con los datos de la función a la que se ha llamado.
2. Un punto de control (siguiente instrucción a ejecutar). Puede tener varios si se ejecuta de manera concurrente (varios hilos de ejecución)

## Procesos en UNIX
UNIX es un término generico para referirse a muchos _sabores_ de UNIX, como Linux, BSD, MAC OS X...
Cada uno cumple o no diferentes estandares como System V, POSIX o BSD.

### Kernel
Término para referirnos al propio SO. El kernel reside en un archivo que se lanza al arrancar la máquina. Inicia el sistema y prepara el ambiente para ejecutar procesos. INIT es el primer proceso del usuario (pid 1) y el es ancestro del resto de procesos.
El kernel interactua con el hardware y el usuario usa llamadas al sistema para interactuar con el kernel. El kernel es el único programa que corre sobre hardware y administra las peticiones de dispositivos externos mediante interrupciones.

## Modos de ejecución

Los SO funcionan con dos modos:
- **Modo usuario**: en el que corre el código del usuario
- **Modo kernel**: en el que corre el kernel
	1. **Llamadas al sistema**: Un proceso del usuario pide servicios al kernel mediante estas llamadas
	2. **Excepciones**: Situaciones excepcionales provocan problemas en el hardware que requieren de la intervención del kernel
	3. **Interrupciones**: Los dispositivos usan interrupciones para notificar al kernel diferentes eventos como la entrada/salida
	4. Algunas instrucciones del procesador también corren en modo kernel

## Hilos y procesos

En los UNIX tradicionales un proceso se define por :
1. El espacio de direcciones que puede referenciar. Los procesos usan **direcciones virtuales**. Una parte de esas direcciones corresponde a código y información del kernel. Se le conoce como _espacio del kernel_. El kernel mantiene estructuras de datos globales y de cada proceso.
 
2. Un punto de control que indica la siguiente instrucción a ejecutar (Program Counter). En los sistemas UNIX modernos puede haber varios puntos de contros => varios hilos de ejecución.

## Reentrada en el kernel

El kernel de UNIX es un programa en C, y como tal, tiene:
- **Código del kernel**: lo que se ejecuta cuando el sistema esta en modo kernel: código de llamadas al sistema, interrupciones y manejadores de excepciones. 
* **Datos del kernel**: variables globales del kernel accesibles por todos los procesos del sistema
* **Stack del kernel**: parte de la memoria utilizada como pila al ejecutar en modo kernel: parámetro que pasa dentro del kernel, variables locales del funciones del kernel...

El kernel de UNIX es reentrante, muchos procesos corren simultaneamente muchas funciones del kernel y muchos procesos pueden estar corriendo simultaneamente la misma función del kernel.

Para que el kernel pueda ser reentrante:
* El código del kernel debe ser de **sólo lectura**
* los datos del kernel deben de estar protegidas frente accesos concurrentes.
* Cada proceso tiene su **propio stack del kernel**

##### Acercamiento tradicional (kernel no adelantable)
* Un proceso que se ejecuta en modo kernel no se puede adelantar, solo sale de la CPU si finaliza, se bloquea o regresa al modo usuario. 
* Sólo ciertas estructuras de datos del kernel necesitan protección
* Son simples de proteger, necesitamos un flag de **en uso/libre**

##### Acercamiento moderno (kernel adelantable)




## wait()

* `wait()` -> espera a que acabe cualquiera de los hijos del proceso
* `waitpid()` y `wait4()` -> esperan a un pid concreto y a `wait4()` le pasas un puntero a un struct 

#### WCONTINUED
Devuelve si un proceso pare

#### WNOHANG
return inmediatamente si no se ha hecho exit ningún hijo

#### WUNTRACED
return si un proceso se ha parado

Con un OR bit a bit miramos todo sin esperar, mirando que ha pasado e informandonos.
si waitpid() no pone nada en la variable entonces tendremos basura
comprobamos el contenido si waitpid devuelve el pid
```c
// waitpid(pid, )
if (waitpid(p->pid, &est, WNOHANG | WUNTRACED | WCONTINUED) == p->pid) {
// hacemos comprobaciones
}
```


## Planificación de la CPU

##### Algoritmos apropiativos

##### Algoritmos no apropiativos

### Tipos de planificador

* Corto plazo -> Decice que proceso entra a CPU entre los procesos corriendo

* Medio plazo -> En sistemas con Swap decide quien va a swap(iba todo el proceso entero)(no existe en sistemas modernos porque hay páginas ) 

* Largo plazo ->  en sistemas modernos con un uso interativo el planificador a largo plazo es el usuario, en uso no interativo si que tenemos 


### Metas del planificador

## Algoritmos de planificación
### SJF, shorterst job first
$$
τ_n+_1 = α · tn + (1 − α) · τn
$$
### Prioridades
la prioridad del proceso es un entero. El rango y el orden (de mayor a menor o al revés) depende del sistema.


## SRTF, shortest remaining time first

## RR, round-robin



