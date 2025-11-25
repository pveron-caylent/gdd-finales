# FINAL DE GESTIÓN DE DATOS

# Contestar por Verdadero o Falso

### **1.a)**  
La siguiente consulta retorna como máximo 1 fila:

```sql
SELECT distinct 1 FROM t1_tab1a WHERE campo1 = 1
UNION
SELECT distinct 1 FROM t1_tab1a WHERE campo2 = 2
```

### **1.b)**  
Si un árbol binario está completo, la cantidad de nodos es impar.


# Responder exactamente lo solicitado en la pregunta en no más de 20 renglones.

### **2.a)**  
Desarrolle el concepto de Grafos, su posible utilización, clasificación y representación computacional de los mismos.


### **2.b)**  
Desarrollar el concepto de join, enumere y explique cada uno de los tipos. Ejemplifique.


# Parte Práctica

Dado el siguiente modelo:

<img width="155" height="55" alt="image" src="https://github.com/user-attachments/assets/7e5da6bb-f3cf-494e-9be6-68d7f49e73ef" />

```
TABLITAFINAL  
numero (unique) int
```

Asumiendo que la tabla está vacía y no posee triggers, se ejecutan las siguientes sentencias SQL en dicho orden:

```sql
INSERT INTO TablitaFinal VALUES (1)
INSERT INTO TablitaFinal (numero) VALUES (3)
INSERT INTO tablitafinal VALUES (null)
UPDATE TablitaFinal SET numero = isnull(numero,5) + 1 
WHERE 1 = 1 OR numero IS NOT NULL AND numero > 0
INSERT INTO tablitafinal VALUES (null)
COMMIT
```

En caso de que alguna de las sentencias SQL provoque un error indíquelo, explique claramente por qué se produce y describa cuál sería el contenido de la tabla luego de confirmarse el commit de dichos cambios **obviando** la/las sentencias erróneas.

En caso de que ninguna falle describir cuál es el contenido de la tabla luego de confirmarse el commit de dichos cambios.


### **3.b)**  
Describir los errores de la siguiente consulta SQL, en caso de que no posea describir qué retorna sabiendo que la tabla posee más de 10 registros.

```sql
SELECT MAX(t1.numero), MAX(t2.numero)
FROM tablitafinal t1, tablitafinal t2
WHERE t1.numero > t2.numero
```

