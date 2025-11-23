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
