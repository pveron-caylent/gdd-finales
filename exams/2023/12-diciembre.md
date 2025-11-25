# Examen – Gestión de Datos

## Contestar por Verdadero o Falso

### **1.a)**  
Una de las ventajas de los Stored Procedures es que se utilizan para manejar la seguridad en la base de datos.

### **1.b)**  
No es posible realizar *joins* a través de una vista.

---

## Responder exactamente lo solicitado en la pregunta en no más de 30 renglones.

### **2.a)**  
Explicar 2 métodos de ordenamiento recursivos vistos durante la materia.

### **2.b)**  
Dé 1 ejemplo donde sería adecuado aplicar un nivel de aislamiento **Read Uncommitted** y otro para **Serializable**. Justifique claramente su respuesta.

---

# 3) Parte Práctica

Dada la siguiente tabla vacía:

```
Numeros(
   clave INT PRIMARY KEY,
   valor INT
)
```

### **3.a)**  
Realizar un trigger de *insert* que valide que los valores del campo **clave** sean consecutivos desde el 1.  
Se sabe que posee un trigger *INSTEAD OF* que no puede modificarse y una *Constraint* para que no tome valores no positivos.

### **3.b)**  
Realizar otro trigger de *insert* que valide que los datos no nulos del campo **valor** sean únicos.  
Explicar por qué motivo no se puede desarrollar esta funcionalidad a través de una constraint **UNIQUE**.
