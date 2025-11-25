# FINAL DE BASES DE DATOS


## Contestar por Verdadero o Falso

**1.a)** Un árbol binario de búsqueda siempre es más rápido que una lista para ordenar un conjunto de valores.

**1.b)** La cantidad de nodos de un árbol de expresión siempre es par.

---

## Responder exactamente lo solicitado en no más de 20 renglones

**2.a)** Desarrolle el concepto de Grafos. Su clasificación, utilización y representación computacional.

**2.b)** Detalle funcionalidades y características del Nivel Conceptual o Lógico en una Arquitectura ANSI SPARC de una Base de Datos.

---

# Parte Práctica

## 3.a) Dadas las siguientes tablas:

<img width="576" height="159" alt="image" src="https://github.com/user-attachments/assets/9506aad4-1978-4524-b4f7-37e3fc4b1ac2" />

```
USUARIOS
---------
IdUsuario int (pk)
Nombre char(100) not null
Apellido char(100) not null
FechaAlta date not null

INGRESOS
---------
IdUsuario int (fk)
Fecha date not null
```

La interacción entre las tablas: todos los usuarios de un aplicativo, la segunda tabla registra los logueos al mismo, el campo Fecha no contiene la hora; por lo que cuando un usuario ingresa más de una vez en el mismo día, se guarda un solo registro en la tabla. La tabla Ingresos contiene el IdUsuario y la primera fecha de ingreso de ese día.
3.a) Lea la creación de la vista que detalle un número de líneas y que indique el último ingreso del aplicativo de cada usuario mostrando cómo sería la vista sobre la tabla con: nombre, apellido y la fecha de ingreso más reciente indicando la fecha de alta del usuario como uno de los campos.

---

## 3.a) La empresa solicita que se la cree una vista que obtenga el último ingreso del aplicativo de cada usuario mostrando cómo sería la vista sobre la tabla con: nombre, apellido y la fecha de ingreso más reciente, si no accedio, mostrar la fecha de alta del usuario como uno de los campos.


```
CREATE VIEW VW_final (nombre, apellido, ingreso)
AS
select nombre, apellido, max(fecha)
from usuarios, ingresos
where IdUsuario = usuarios.IdUsuario
group by usuarios.IdUsuario, apellido, nombre
union
select nombre, apellido, fechaAlta from usuarios;
```

Opciones:

I. La vista es correcta y devuelve exactamente lo solicitado  
II. La vista se crea pero al consultarla no devuelve lo solicitado  
III. La vista se crea pero da error al consultarla  
IV. La vista no puede crearse

---

## 3.b) Eliminación de usuarios

Se ejecuta:

```
DELETE FROM usuarios WHERE IdUsuario = 8
```

Explique el motivo por el cual da error y luego implemente y desarrolle los objetos necesarios para permitir la eliminación de usuarios mediante sentencias como la anterior.
