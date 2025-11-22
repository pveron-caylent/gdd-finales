### 3.a) Practica SQL  

```sql
CREATE TRIGGER TR_BORRAR_PROVINCIA
ON Provincia
INSTEAD OF DELETE
AS
BEGIN
    DELETE FROM Ciudad
    WHERE idpcia IN (SELECT idpcia FROM deleted);

    DELETE FROM Provincia
    WHERE idpcia IN (SELECT idpcia FROM deleted);
END;
GO
```
### 3.b)
 
**Opcion E** - A inserta Pais y Provincia. B por PK duplicada falla y hace rollback
