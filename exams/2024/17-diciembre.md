
# Final de Gestión de Datos — Examen 2

## Verdadero o Falso
1.a) ABB — Si el recorrido postorden sobre un árbol binario de búsqueda es “9, 12, 16, 15 y 10”, entonces el barrido en preorden sobre el mismo árbol es “10, 12, 15 y 16”.  
1.b) Huffman — El árbol binario es completo.

---

## 2.a)
Realice una comparación entre Hashing y árbol B como método de acceso a datos.

## 2.b)
Explique un método de implementación de árboles binarios.

---

## Práctica

### Tabla país/provincias/ciudades

<img width="631" height="108" alt="image" src="https://github.com/user-attachments/assets/ecd045d9-220e-4842-91d4-62ac620467de" />

a) Dado que la tabla país posee más de 100 registros, escribir consulta SQL que retorne los 5 primeros países del alfabeto y los últimos 5.  
Columnas: las 2 primeras de la tabla.

b) Dada la consulta:

```sql
select pa.IDPAIS,
       sum(pro.HABITANTES),
       count(*)
from pais pa
inner join provincias pro on pa.IDPAIS = pro.IDPAIS
group by pa.IDPAIS
```

Indicar cuál opción describe correctamente:
<img width="734" height="167" alt="image" src="https://github.com/user-attachments/assets/f41454d1-7d83-4e5d-9751-6edb05be3f55" />

