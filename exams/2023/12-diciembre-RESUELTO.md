
### 3.a)

```sql
CREATE TRIGGER TR_CONSECUTIVO
ON Numeros AFTER INSERT
AS
BEGIN
    DECLARE @Insertado INT;
    DECLARE @Ultimovalor INT;
    
    SELECT @Insertado =  clave FROM inserted
    
    SELECT @Ultimovalor = MAX(clave) FROM Numeros WHERE clave <> @Insertado
    
    IF @Ultimovalor IS NULL
       SET @Ultimovalor = 0
    
    IF 
       @Insertado <> @Ultimovalor + 1
    BEGIN
        RAISERROR ('No es consecutivo',16,1);
        ROLLBACK TRANSACTION 
        RETURN
    end
end;
```

### 3.b) 

```sql
CREATE TRIGGER TR_VALIDACION
ON Numeros 
AFTER INSERT
AS
BEGIN
    DECLARE @VALOR INT;
    DECLARE @CLAVE INT;

    SELECT @VALOR = valor,
           @CLAVE = clave
    FROM inserted;

    IF @VALOR IS NULL
        RETURN;

    IF EXISTS (
        SELECT 1 
        FROM Numeros
        WHERE valor = @VALOR
          AND clave <> @CLAVE   -- evita que se detecte a sí mismo
    )
    BEGIN
        RAISERROR ('Valor no puede ser duplicado', 16, 1);
        ROLLBACK TRANSACTION;
        RETURN;
    END
END;
```
