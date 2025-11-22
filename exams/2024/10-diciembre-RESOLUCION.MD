### 3.1)
 
Devuelve tres columnas, donde cada fila representa:
a.nombre → el abuelo
b.nombre → el padre
c.nombre → el hijo

¿Qué pasa si no hay padre o abuelo?
Como es LEFT JOIN:
Si una persona no tiene padre, la columna b.nombre es NULL
Si tiene padre pero no tiene abuelo, a.nombre es NULL

### 3.2) 

```sql
CREATE TRIGGER TR_EVITAR_CICLO
ON Persona
FOR INSERT, UPDATE
AS
BEGIN
    IF EXISTS (
        SELECT 1
        FROM inserted c1
        JOIN Persona b1 ON c1.su_padre_es = b1.id
        JOIN Persona a1 ON b1.su_padre_es = a1.id
        WHERE c1.su_padre_es = a1.id   -- A NO puede ser padre de C
    )
    BEGIN
        RAISERROR('Error: relación cíclica detectada (A no puede ser padre de C).', 16, 1);
        ROLLBACK TRANSACTION;
        RETURN;
    END
END;
GO
```
