### 3.a) Practica SQL  

Se ejecuta pero no obtenemos lo solicitado. Puede haber filas duplicadas, 
La forma correcta es usar LEFT JOIN y COALESCE
```sql
CREATE VIEW vw_final (nombre, apellido, ultimoIngreso) AS
SELECT 
    u.nombre,
    u.apellido,
    COALESCE(MAX(i.fecha), u.fechaAlta) AS ultimoIngreso
FROM usuarios u
LEFT JOIN ingresos i ON u.IdUsuario = i.IdUsuario
GROUP BY u.nombre, u.apellido, u.fechaAlta;
```

3.b)
```sql
CREATE TRIGGER TR_DELETE_USUARIO
ON Usuarios
INSTEAD OF DELETE
AS
BEGIN
    DELETE i
    FROM Ingresos i
    INNER JOIN deleted d ON d.IdUsuario = i.IdUsuario;

    DELETE u
    FROM Usuarios u
    INNER JOIN deleted d ON d.IdUsuario = u.IdUsuario;
END;
```
