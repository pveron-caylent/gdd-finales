### 3.a) Practica SQL  

```sql
SELECT idpais, detalle
FROM (
    SELECT TOP 5 idpais, detalle
    FROM Pais
    ORDER BY detalle ASC
) A

UNION ALL

SELECT idpais, detalle
FROM (
    SELECT TOP 5 idpais, detalle
    FROM Pais
    ORDER BY detalle DESC
) B;

```
### 3.b)
 
**Opcion D** 
