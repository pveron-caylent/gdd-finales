# FINAL DE GESTIÓN DE DATOS


## Contestar por Verdadero o Falso

### **1.a)**  
Una tabla no puede tener 2 claves foráneas que referencien a la misma tabla.

### **1.b)**  
Si una columna posee la constraint UNIQUE, entonces una sola fila como máximo puede contener NULL en dicha columna.

---

## Responder exactamente lo solicitado en la pregunta en no más de 10 renglones.

### **2.a)**  
Determinar qué índices implementaría sobre las tablas intervinientes en la siguiente consulta, sabiendo que no existen claves implementadas actualmente en el modelo. Especificar por qué:

```sql
SELECT usr_nombre, usr_clave, usr_apellido
FROM usuario, rol
WHERE ( usr_nombre='usuario001' OR usr_apellido LIKE '%Gonzalez%' )
  AND usuario.usr_id = rol.usr_id
  AND rol_tipo = lower('Administrador');
```

---

### **2.b)**  
Enumere y explique al menos tres algoritmos de clasificación que conozca.

---

# Parte Práctica

Dado el siguiente modelo, resuelva:

```
Juego(
    jugador INT,
    jugada INT,
    carta INT
)
```

---

## **3.a)**  
Sabiendo que en la tabla *Juego* se almacenan las jugadas de un juego de cartas de 2 jugadores (jugadores 1 y 2) y que tienen las siguientes características:

- Las jugadas se numeran de forma correlativa y la partida tiene *n* jugadas.  
- Las cartas tienen un valor numérico del 1 al 12 donde el valor mayor le gana al menor.  
- En cada jugada (o mano) juega primero el jugador que ganó la jugada anterior.  
- En la primera jugada de la partida comienza jugando el jugador 1 y en las jugadas siguientes juega primero el jugador que ganó la mano anterior.  
- En caso de que ambos jugadores jueguen una carta de igual valor en la misma jugada, se considera que el jugador 1 ganó dicha jugada.

Describa claramente qué retorna el siguiente query:

```sql
SELECT j1.jugada, j1.jugador, j1.carta
FROM juego j1
ORDER BY j1.jugada,
    (CASE WHEN j1.jugador = (SELECT TOP 1 j2.jugador 
                              FROM juego j2 
                              WHERE j2.jugada = j1.jugada - 1 
                              ORDER BY j2.carta DESC) 
          THEN 1 ELSE 0 END) DESC,
    j1.jugador;
```

---

## **3.b)**  
Dado el modelo anterior, escriba una consulta que retorne el jugador y la mayor carta jugada por cada uno de los dos jugadores en el juego. Apareciendo primero el jugador que haya jugado la mayor carta en todo el partido. En caso de que ambos hayan jugado la misma carta deberá aparecer primero el jugador 1.

No se pueden usar claves autoincrementales, modificación del modelo, uso de *cursors*, uso de subconsultas en la cláusula FROM, vistas, ni el uso de procedimientos ni funciones que retornen tipos no escalares.

