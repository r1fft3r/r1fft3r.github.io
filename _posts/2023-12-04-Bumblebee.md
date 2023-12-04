---
title: Bumblebee
date: 2023-12-04 20:00:00 +/-TTTT
categories: [Incident Response]
tags: [fácil, splunk, sql, blue team]
img_path: /assets/sherlockresources/BUMBLEBEE/
image: bumblebee.png
---

> Este es un reto de la sección Sherlocks en [HackTheBox](https://app.hackthebox.com/).
{: .prompt-tip}

---
## Escenario Sherlock

Un contratista externo ha accedido al foro interno aquí en Forela a través del WiFi de invitados y parece que han robado las credenciales para el usuario administrativo.

Hemos adjuntado algunos registros del foro y un volcado completo de la base de datos en formato sqlite3 para ayudarte en tu investigación.

---
## Recursos

![recursos](Pasted image 20231120003420.png)

---
## Tareas

### Tarea 1 - ¿Cuál era el nombre de usuario del contratista externo?

Utilizando DB Browser podemos abrir el archivo sqlite3 y ver las tabla de usuarios de la base de datos.
![tablas](Pasted image 20231120010841.png)

En la tabla `phpbb_users` vemos varios datos de interés para nuestro análisis.
![datos](Pasted image 20231120011205.png)
* **Direcciones IP involucradas**
* **Nombres de usuarios**
* **Correos de usuarios**

Dentro de los que destacan `apoole` y `apoole1`, ambos con correos pertenecientes a `contractor.net`

### Tarea 2 - ¿Qué dirección IP utilizó el contratista para crear su cuenta?

Podemos ocupar la información vista anteriormente para determinar la dirección IP del contratista.
`10.10.0.78`

### Tarea 3 - ¿Cuál es el post_Id del post malicioso que hizo el contratista?

Revisando la tabla `phpbb_posts` vemos las publicaciones con sus respectivos datos, entre ellas la dirección IP del contratista, con el valor de `post_Id=9` y un valor en HTML dentro de `post_text`.
![post](Pasted image 20231120011855.png)

Si copiamos el contenido del post malicioso en un editor online muestra lo siguiente
![editor](Pasted image 20231120012449.png)

Lo que parece ser una plantilla falsa para robar credenciales de un usuario.

Y si miramos el código JavaScript que corre por detrás, en resumen se encarga de mostrar un modal (elemento con ID "zbzbz1234") en la página web a menos que la cookie "phpbb_token" ya exista.

Si la cookie no existe, muestra el modal y establece la cookie, la cual expira después de 24 horas.
![cookie](Pasted image 20231120013023.png)

### Tarea 4 - ¿Cuál es la URI completa a la que el stealer de credenciales envía sus datos?

Si revisamos el código HTML vemos que la etiqueta del formulario envía los datos introducidos hacia `http://10.10.0.78/update.php`, la IP del contratista. 
![html](Pasted image 20231120014029.png)

### Tarea 5 - ¿Cuándo entró el contratista en el foro como el administrador? (UTC)

Para ver los registros de acceso del foro, podemos subir nuestro "access.log" a nuestro SIEM de preferencia, en este caso utilizaremos Splunk.

Podemos ver un total de 697 eventos dentro del `access.log`
![access](Pasted image 20231204161729.png)

Para responder esta pregunta tenemos que saber un par de cosas:
* **URL del Login administrativo.**
* **IP del contratista**
* **Acción que realizó**

Para encontrar la URL que corresponde al Login administrativo, podemos buscar por `uri_path` y ver los valores más accedidos.

Viendo los distintos nombres podemos deducir que el login administrativo se encuentra dentro de la ruta `/adm/`.
![ruta](Pasted image 20231204165527.png)

Ahora que sabemos la ruta a la que accedió el contratista, podemos filtrar por la información relevante que queremos investigar.
* **IP del contratista -> 10.10.0.78**
* **URI a la que accedió -> /adm/index.php* (* significa que muestre todo lo que empiece por `/adm/index.php` y tenga data por delante)**
* **Metodo -> Como buscamos por una acción de login, filtraremos solamente por aquellas alertas con el método POST.**

Y facilitar aún más nuestro analisis, lo mostraremos en una tabla con los campos de tiempo (req_time) y URI.
```
index="bumblebee" clientip="10.10.0.78" uri="/adm/index.php*" method="POST" | table req_time uri
```
![filter](Pasted image 20231204170722.png)

Esto nos deja solamente con 5 eventos para analizar, y gracias al campo req_time podemos indicar si queremos ordenar los datos de manera ascendente o descendente.

La primera alerta que nos aparece es a las `11:53:12` hacia la URI `/adm/index.php?sid=0bc281afeb61c3b9433da9871518295e`.

> Hay que tener en cuenta que el `access.log` nos reporta el tiempo en formato UTC+01:00, por lo que para convertirlo a UTC hay que restarle 1 hora.
{: .prompt-info}

### Tarea 6 - En el foro hay credenciales en texto claro para la conexión LDAP, ¿Cúal es la contraseña?

Para encontrar la contraseña podemos emplear un `strings` al archivo sqlite y filtrar por ldap.
```
strings phpbb.sqlite3 | grep ldap
```
![strings](Pasted image 20231204174401.png)

### Tarea 7 - ¿Cúal es el "user agent" del usuario Administrador?

Dentro del archivo sqlite3 en la tabla `phpbb_users` podemos ver la IP del Administrador.
![ip](Pasted image 20231204175535.png)

Podemos filtrar por los campos `clientip` y `useragent`, agregando un `top` al principio para que muestre los valores más repetidos.

```
index="bumblebee" clientip="10.255.254.2" | top useragent
```
![top](Pasted image 20231204175630.png)

### Tarea 8 - ¿A qué hora el contratista se añadió al grupo de administradores? (UTC)

Para seguir una línea de tiempo de las acciones que realizó el contratista, podemos filtrar por la IP y el método POST, debido a que al agregarse al grupo administradores tuvo que enviar datos hacia SQLite.

```
index="bumblebee" clientip="10.10.0.78" method="POST" | table req_time uri
```
![timeline](Pasted image 20231204183410.png)
Gracias a esto vemos que ingresó a las `11:53:51` como administrador hacia `acp_groups` y agregó información (mode=manage).

### Tarea 9 - ¿A qué hora el contratista descargó la copia de seguridad de la base de datos? (UTC)

Viendo los últimos movimientos que hizo antes de desconectarse, encontramos que accedió como administrador hacia `acp_database&mode=backup`, para posteriormente dirigirse a una ruta `/store/`.
![store](Pasted image 20231204183859.png)

Continuando con la línea de tiempo, vemos que a las `12:01:38` exportó el backup hacia la ruta `/store/` en un formato `.gz`.
![backup](Pasted image 20231204184025.png)

### Tarea 10 - ¿Cuál fue el tamaño en bytes de la copia de seguridad de la base de datos tal y como se indica en `access.log`?

Para obtener más información sobre la alerta podemos hacker click sobre ella para ver más eventos.
![alert](Pasted image 20231204184227.png)

De esta manera podemos ver cuantos bytes pesaba el archivo descargado.
![bytes](Pasted image 20231204184420.png)

![solved](Pasted image 20231204184513.png)