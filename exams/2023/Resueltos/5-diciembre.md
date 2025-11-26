### 3.1)
 
Muestra lista de jugadas ordenadas por numero de jugada, jugador ganador y si hay empate muestra jugador 1.

### 3.2) 

```sql
SELECT j1.jugador,
       MAX(j1.carta) AS mayor_carta
FROM Juego j1
GROUP BY j1.jugador
ORDER BY MAX(j1.carta) DESC,  
         j1.jugador ASC;      
```
