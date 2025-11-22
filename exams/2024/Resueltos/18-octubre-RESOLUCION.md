### 3.a)
```sql
SELECT  h.nombre    AS nombre_persona,
        h.apellido  AS apellido_persona,
        a.nombre    AS nombre_abuelo,
        a.apellido  AS apellido_abuelo
FROM Persona h
JOIN Persona p ON h.su_padre_es = p.id
JOIN Persona a ON p.su_padre_es = a.id;
```

### 3.b) 

```sql
SELECT p.nombre, p.apellido, COUNT(h.id) AS Cantidad_Hijos
FROM Persona p
LEFT JOIN Persona h ON h.su_padre_es = p.id
GROUP BY p.nombre, p.apellido;
```
