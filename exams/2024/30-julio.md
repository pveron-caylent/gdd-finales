# FINAL DE GESTIÓN DE DATOS

**Apellido y Nombre:**  
**Legajo:**  
**1a   1b   2a   2b   3a   3b**

A efectos de aprobar este examen final deberá sumar como mínimo 6 (seis) puntos y al menos tener un ejercicio práctico correcto.  
Para los ejercicios que requieran codificación SQL o PL-SQL deberá especificar de qué motor se trata.

**1.a y b)** Respuesta correcta 1 punto, respuesta incorrecta resta 1 punto.  
**2.a)** 2 puntos  
**2.b)** 2 puntos  
**3.a)** 2 puntos  
**3.b)** 2 puntos  

---

## Contestar por Verdadero o Falso

### **1.a**  
Conviene en términos de velocidad buscar en una estructura de hash por una clave que buscar en una estructura de árbol B+.

### **1.b**  
El nivel de aislamiento repeatable read acepta lecturas fantasmas.

---

## Responder exactamente lo solicitado en la pregunta en no más de una carilla.

### **2.a**  
Explique y desarrolle 2 objetos de base de datos que puedan ser utilizados para asegurar la integridad de datos.

### **2.b**  
Comparar procesos OLTP vs. OLAP (DDS) en cuanto a su utilización de base de datos.

---

# Parte Práctica

## **3)** Dado el siguiente modelo de datos resuelva:

<img width="576" height="101" alt="image" src="https://github.com/user-attachments/assets/075bb0c9-06cc-406b-b51b-5094a69e745b" />


---

### **3.a)**  
Cree el/los objetos de base de datos necesarios para implementar la posibilidad de poder borrar una provincia con un comando `DELETE`.

---

### **3.b)**  

Sabiendo que no hay errores de sintaxis en el siguiente código, determine qué sucede dada la ejecución de 2 procesos **A** y **B** que se ejecutan en los tiempos *t(i)*:

| Tiempo t(i) | Proceso A | Proceso B |
|-------------|-----------|-----------|
| 1 | BEGIN TRANSACTION | BEGIN TRANSACTION |
| 2 | Insert into pais (idpais, detalle) values(1000, 'ARG') | SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED |
| 3 | Insert into Provincia (idpcia, idpais, habitantes) values (1000, 1000, 'BS AS', 10000000) | Insert into pais (idpais, detalle) values(1000, 'ARG') |
| 4 | COMMIT | COMMIT |

**Opciones:**

A) El proceso B ingresa el país id = 1000 porque es una transacción no confirmada.  
B) El proceso A no ingresa el país id = 1000 porque se bloquea con la transacción no confirmada B.  
C) Se termina registrando la provincia pero no el país dado que se genera interbloqueo.  
D) Se registra el país pero no la provincia dado que aborta antes el proceso A por error de PK.  
E) Ninguna de las anteriores.
