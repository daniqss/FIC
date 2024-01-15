---
tags:
  - EC 2º
Fecha: "[[2023-09-07]]"
---

# 📚 Apuntes

```dataview
TABLE WITHOUT ID
	link(file.link, title) as Título,
	Fecha as Fecha
FROM "FIC"
WHERE Asignatura = [[Estrutura de Computadores]] and file.name != "Estrutura de Computadores"
SORT Fecha ASC
```

# 💾 Asignatura

##### Porcentaje:
* 40% Examen Problemas
	* 20% procesador segmentado => 0.73/2
	* 20% memoria => 1.3/2
* 20% Prácticas de laboratorio => 1.9/2
* 40% Exame final (Tema 1, 4, 6, 7) =>
##### Nota mínima: 
Non hai nota mínima

##### Profesores
* jose.sanjurjo@udc.gal
	* 117
	* Titorías:
		- MARTES 11:30-13:30
		- MÉRCORES 10:30-11:30 / 12:30-13:30

* basilio.fraguela@udc.gal
	* 

##### Libros
* Patterson, D. A. y Hennessy, J. L. (2020). Computer Organization and
Design MIPS Edition: The Hardware/Software Interface. Morgan
Kaufmann
   
# 📜 Examenes

```dataviewjs

const files = app.vault.getFiles().filter(file => ((file.extension == 'pdf') && file.path.includes("ec/Examenes")));

dv.list(files.map(f => dv.fileLink(f.path)))
dv.sort
```



