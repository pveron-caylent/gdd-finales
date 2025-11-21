
# Final de Gestión de Datos — Examen (Versión recordada)

## 1) Verdadero o Falso

1. La complejidad computacional de los métodos de ordenamiento depende del espacio ocupado por las estructuras que se usan.

---

## 2) Teóricas

1. Describir transaccionalidad, aislamiento y bloqueos.

2. Definir grafos, clasificación y representación computacional.

---

## 3) Práctica

### 3.1) Consulta SQL  
Explicar qué devuelve la siguiente consulta:

```sql
SELECT a.nombre, b.nombre, c.nombre
FROM persona c 
LEFT JOIN persona b ON c.su_padre_es = b.id
LEFT JOIN persona a ON b.su_padre_es = a.id;
```

---

### 3.2) Restricción  
Codificar la restricción de que **no puede haber una relación cíclica** entre padre e hijo, es decir:

- A es padre de B  
- B es padre de C  
- A **no puede** ser padre de C

---
