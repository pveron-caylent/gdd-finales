### 3.a) Practica SQL  
```sql
SELECT 
    usu.username, 
    usu.fecha_alta, 
    usu.detalle_estado, 
    COUNT(DISTINCT per.id_perfil),

    -- perfil con más fallas
    (
        SELECT TOP 1 p2.nombre_perfil
        FROM Perfil p2
        JOIN Usuario_Perfil upe2 
             ON upe2.id_perfil = p2.id_perfil
            AND upe2.id_usuario = usu.id_usuario
        JOIN Login1 logi2 
             ON logi2.id_usuario = usu.id_usuario
            AND logi2.id_perfil = p2.id_perfil
        WHERE logi2.estado_login = 0
        GROUP BY p2.nombre_perfil, p2.id_perfil
        ORDER BY COUNT(*) DESC, p2.id_perfil ASC
    ) AS perfil_mas_fallido,

    -- total de fallas del usuario
    SUM(CASE WHEN logi.estado_login = 0 THEN 1 ELSE 0 END) AS Login_fallidos

FROM Usuario usu
LEFT JOIN Usuario_Perfil upe ON upe.id_usuario = usu.id_usuario
JOIN Perfil per ON upe.id_perfil = per.id_perfil
JOIN Login1 logi ON logi.id_usuario = usu.id_usuario 
                 AND logi.id_perfil = per.id_perfil

GROUP BY
    usu.id_usuario,
    usu.username,
    usu.fecha_alta,
    usu.detalle_estado;
```
### 3.b) 

```sql
CREATE TRIGGER TR_AUTENTICACION
ON Login1
AFTER INSERT
AS
BEGIN
    SET NOCOUNT ON;

    DECLARE @USER INT;
    DECLARE @ESTADO_LOGIN INT;
    DECLARE @INTENTOS INT;
    DECLARE @PASSWORD VARCHAR(50);
    DECLARE @ESTADO INT;
    DECLARE @PERFIL INT;

    -- Tomar el usuario afectado (1 fila por evaluación)
    SELECT @USER = id_usuario,
           @PERFIL = id_perfil,
           @ESTADO_LOGIN = estado_login
    FROM inserted;

    -- Contar intentos fallidos de hoy
    SELECT @INTENTOS = COUNT(*)
    FROM Login1
    WHERE id_usuario = @USER
      AND estado_login = 0
      AND CONVERT(date, fecha_hora) = CONVERT(date, GETDATE());

    -- 1) BLOQUEAR si llegó a 3 fallos
    IF @ESTADO_LOGIN = 0 AND @INTENTOS >= 3
    BEGIN
        UPDATE Usuario
        SET estado = 0,
            detalle_estado = 'Bloqueado'
        WHERE id_usuario = @USER;

        -- Registrar en logs el bloqueo
        INSERT INTO Login1 (id_usuario, id_perfil, fecha_hora, estado_login)
        VALUES (@USER, @PERFIL, GETDATE(), 0);  -- 0 = fallo

        ROLLBACK TRANSACTION;   -- No permitir el 4to fallo
        RETURN;
    END

    -- 2) REACTIVAR si password genérico y estado_login = 2 (primer ingreso)
    SELECT @PASSWORD = password,
           @ESTADO = estado
    FROM Usuario
    WHERE id_usuario = @USER;

    IF @ESTADO = 0                       -- bloqueado
       AND @PASSWORD = '00x@T3st'        -- clave genérica
       AND @ESTADO_LOGIN = 2             -- primer ingreso
    BEGIN
        UPDATE Usuario
        SET estado = 1,
            detalle_estado = 'Activo'
        WHERE id_usuario = @USER;

        -- Registrar LOGIN como Primer ingreso
        INSERT INTO Login1 (id_usuario, id_perfil, fecha_hora, estado_login)
        VALUES (@USER, @PERFIL, GETDATE(), 2);   -- 2 = Primer ingreso
    END
END;
GO
```
