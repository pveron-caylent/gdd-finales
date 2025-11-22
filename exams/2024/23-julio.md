# FINAL DE GESTIÓN DE DATOS — 23/07/2024


## Contestar por Verdadero o Falso

### **1.a)**  
Un árbol binario completo es un árbol N-ario con N=2, donde todos sus niveles están llenos.

### **1.b)**  
Las funciones creadas por el usuario (objeto FUNCTION) en T-SQL no permiten sentencias INSERT/DELETE/UPDATE en su cuerpo.


## Responder exactamente lo solicitado en no más de 10 renglones.

### **2.a)**  
Explique las diferencias entre los modelos OLAP y OLTP.

### **2.b)**  
Explique los conceptos **LECTURA SUCIA**, **LECTURA REPTIBLE** y **LECTURA FANTASMA**.  
Indique cómo se comportan los niveles **READ COMMITTED** y **REPEATABLE READ** ante los tres conceptos mencionados.

## Dado el siguiente modelo:

<img width="419" height="397" alt="image" src="https://github.com/user-attachments/assets/34db5225-46d9-480b-8517-54b4f056befe" />
<img width="741" height="291" alt="image" src="https://github.com/user-attachments/assets/2a3ce20c-ee5e-4e53-999d-ec5708136816" />

Y sabiendo que:

- Cuando un usuario se registra, **no se le asigna ningún perfil** hasta que se active su cuenta.  
- Referencias de columnas:  
  - `estado (int)`: 1 = Activo / 0 = Bloqueado / NULL = Inactivo  
  - `detalle_estado (char)`: Activo / Bloqueado / Inactivo  
  - `estado_login`: 1 = Login exitoso / 0 = Login fallido / 2 = Primer ingreso

---

## **3.a)**  
Escriba una consulta que, para todos los usuarios, retorne:

- Nombre de usuario  
- Fecha de alta  
- Detalle del estado del usuario  
- Cantidad de perfiles del usuario  
- Nombre del perfil del usuario que más logins fallidos tuvo  
  - (ante igualdad tomar el de menor id)  
- Cantidad total de logins fallidos del usuario  

**Nota:** No se permiten sub-selects en el FROM.

---

## **3.b)**  
Crear el/los objetos de base de datos para que cuando un usuario falle tres veces en autenticarse en el mismo día:

- La cuenta quede **bloqueada**  
- `detalle_estado` pase a **'Bloqueado'**  
- Se registre en la tabla de logs el evento correspondiente  
- También se debe asignar automáticamente el perfil **“00x@T3st”** cuando `estado_login = 2` (primer ingreso)

**Nota:** Debe considerarse que pueden acceder varios usuarios a la vez desde distintas aplicaciones.
