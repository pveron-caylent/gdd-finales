
# Final de Gestión de Datos — Examen 1

## 1.a) Verdadero o Falso
1. a) El análisis del plan de consulta permite detectar la operatoria interna desarrollada por un RDBMS para procesar la consulta.  
**Respuesta:** (indicar V/F)

1. b) Colocar un nivel de aislamiento muy restrictivo garantiza que siempre se va a poder ejecutar y finalizar con éxito una transacción.  
**Respuesta:** (indicar V/F)

---

## 2.a) Índices
Indique por qué un índice conformado por una clave numérica corta es más rápido que un índice conformado por un string largo.

## 2.b)
Explique en qué situaciones la presencia de un índice en una tabla relacional podría generar una caída de performance y por qué.

---

## 3.a) Consulta SQL

<img width="633" height="172" alt="image" src="https://github.com/user-attachments/assets/e7f4bbb5-8a02-4145-872c-e6cd69333ada" />


Sabiendo que:
Existen 2 turnos (0–Mañana, 1–Tarde)
Todos los días de la semana se encuentran cargados en la tabla día (1–Lunes, 2–Martes, …, 7–Domingo)
Todos los ids de las tablas son de tipo Int y todos los detalles son de tipo varchar(50)
La siguiente consulta debería retornar la ocupación del laboratorio 401 para todos los días de la semana en ambos turnos. Ordenado por el día de la semana (según su detalle).
Retornando el día de la semana, el detalle de la materia que ocupa el laboratorio en el primer turno y el detalle de la materia que ocupa el laboratorio en el segundo turno. En caso que alguno de los turnos no esté ocupado el departamento se muestra la palabra LIBRE.

Consulta dada:

```sql
select d.dia_detalle dia_semana,
       isnull(m1.materia_detalle,'LIBRE') mañana,
       isnull(m2.materia_detalle,'LIBRE') tarde
from dia d
left join horario h1 on d.dia_id=h1.dia_id and h1.labo_id=401 and h1.turno=0
left join materia m1 on h1.materia_id=m1.materia_id
left join horario h2 on d.dia_id=h2.dia_id and h2.labo_id=401 and h2.turno=1
left join materia m2 on h2.materia_id=m2.materia_id
order by 1;
```

Opciones:
a) La consulta no compila  
b) La consulta da error en tiempo de ejecución  
c) Se ejecuta sin errores pero no retorna lo pedido  
d) Se ejecuta bien y retorna lo solicitado

---

## 3.b) Restricción
Defina y codifique cómo implementaría la siguiente restricción:
“Una materia no puede estar asignada en el mismo día en laboratorios diferentes”.
No se permite la alteración de la estructura actual.
