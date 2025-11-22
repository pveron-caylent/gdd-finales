### 3.a)
 
**Opcion d** - El codigo realiza lo solicitado

### 3.b) 

```sql
CREATE TRIGGER TR_RESTRICCION_DIA
ON Horario
FOR INSERT, UPDATE
AS
BEGIN
    -- Detectar conflicto de materia en el mismo día y distinto laboratorio
    IF EXISTS (
        SELECT 1
        FROM inserted i
        JOIN Horario h
            ON h.materia_id = i.materia_id
           AND h.dia_id     = i.dia_id
           AND h.labo_id   <> i.labo_id
    )
    BEGIN
        RAISERROR('Una materia no puede estar asignada en el mismo día en laboratorios diferentes.', 16, 1);
        ROLLBACK TRANSACTION;
        RETURN;
    END
END;
GO
```
