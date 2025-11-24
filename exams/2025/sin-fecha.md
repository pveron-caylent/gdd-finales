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

*La consigna del examen continúa indicando que los usuarios ingresan al sistema y se registran sus ingresos, etc.*

---

## 3.a) Crear una vista

Se presenta la vista original del examen:

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
