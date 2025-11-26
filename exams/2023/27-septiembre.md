# FINAL DE GESTIÓN DE DATOS

## Contestar por Verdadero o Falso

### **1.a)**  
Una función escalar no puede retornar null.

### **1.b)**  
Si el árbol de Huffman posee N niveles, entonces el código de mayor tamaño posee N bits.

---

## Responder exactamente lo solicitado en la pregunta en no más de 20 renglones.

### **2.a)**  
Desarrolle 2 objetos de una base de datos que sirven para asegurar la Integridad de datos.

### **2.b)**  
Explique la funcionalidad de una ETL y el concepto de *staging area* en una implementación de Data Warehouse.

---

# Parte Práctica

## **3.a)**  
Dada la siguiente tabla:

```
PARAMETROS(
    clave INT PRIMARY KEY,
    valor VARCHAR(100) NULL
)
```

Se sabe que el siguiente procedure no posee errores de compilación. Describir los inconvenientes que presenta si se invoca en forma concurrente por muchos usuarios con un nivel de aislamiento **serializable**.

```sql
CREATE PROCEDURE sp_increment_parametro (@id)
AS
BEGIN TRANSACTION

    DECLARE @valor VARCHAR(100)

    SELECT @valor = valor 
    FROM PARAMETROS 
    WHERE clave = @id

    UPDATE PARAMETROS 
    SET valor = @valor + 1
    WHERE clave = @id

COMMIT
GO
```

---

## **3.b)**  
Se sabe que la tabla posee al menos 1000 filas.

```sql
SELECT MIN(f1.clave), MAX(f2.clave) 
FROM parametros f1, parametros f2
WHERE f1.clave > f2.clave;
```

¿Qué devuelve esta consulta?

