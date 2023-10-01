---
title: GrabThePhisher
date: 2023-09-30 22:22:00 +/-TTTT
categories: [Threat Intel]
tags: [fácil, kit, osint, phishing, blue team]     # TAG names should always be lowercase
img_path: /assets/CDRESOURCES/GRABTHEPHISHER/
image: GrabThePhisher.jpg
---

> Este es un reto de la plataforma de entrenamiento para Blue Team, [CyberDefenders](https://cyberdefenders.org).
{: .prompt-tip}

## Escenario
Un atacante comprometió un servidor y se hizo pasar por [https://pancakeswap.finance/](https://pancakeswap.finance/), un exchange descentralizado nativo de la cadena BNB, para alojar un **kit de phishing** en **https://apankewk.soup.xyz/mainpage.php**. El atacante lo configuró como un directorio abierto con el nombre de archivo **"pankewk.zip"**. 

Habiendo proporcionado el **kit de phishing**, se le pide a usted, como SOC Analyst, que lo analice y haga sus deberes de **inteligencia sobre amenazas** (Threat Intel).

## Recursos
![](Pasted image 20230928213847.png)


## Preguntas
### P1 - ¿Qué wallet se utiliza para pedir la "seed phrase"?
![](Pasted image 20230928215250.png)

Si vemos los directorios dentro de **"pankewk"** nos encontramos con uno llamado **me\*\*\*\*\*\***, nombre de una extensión para navegadores que sirve como **wallet** para interactuar con blockchains.

### P2 - ¿Cuál es el nombre del archivo que contiene el código para el kit de phishing?

Dentro de la misma carpeta podemos encontrar una carpeta y dos archivos, uno de ellos llamado **me\*\*\*\*\*\*.\*\*\***, que contiene el código del **kit**.
 
### P3 - ¿En que lenguaje está escrito el kit?

![](Pasted image 20230928221321.png)
Analizando el código y la extensión del archivo, el **kit** se encuentra programado en P**.

### P4 - ¿Qué servicio usa el kit para extraer la información de la máquina victima?

![](Pasted image 20230928221940.png)
En la primera línea del archivo se puede observar que realiza una solicitud a una API en `http://api.sy******.net/json/` con la **dirección IP** del cliente. De esta manera consigue obtener la geolocalización de la victima.

### P5 - ¿Cuantas "seed phrases" hay recolectadas?

![](Pasted image 20230928222125.png)
En la última función del archivo podemos ver que escribe información dentro de `/log/log.txt`.

![](Pasted image 20230928222501.png)
Leyendo el archivo `log.txt` vemos un total de 36 palabras, como las **"seed phrases"** contienen 12 palabras, podemos dividir 36/12 y obtenemos el total de **"seed phrases"** recolectadas.

### P6 - Escribe la "seed phrase" del incidente de phishing más reciente

![](Pasted image 20230928223306.png)
La **"seed phrase"** más reciente sería `"fa**** al** re***** em**** ba***** co***** me****** be***** ow*** pa** mu**** ho****"`.

### P7 - ¿Qué medio se utilizó para el volcado de credenciales (Credential Dumping)?

![](Pasted image 20230929023103.png)
En la línea 34 del código se utiliza la API de `Te******` para enviar la data almacenada en la variable `$message`.

### P8 - ¿Cuál es el token del canal?

![](Pasted image 20230929023307.png)
Unas líneas más arriba se puede ver el **token** almacenado en la variable `$token`.

### P9 - ¿Cuál es el ID del chat del canal del phisher?

![](Pasted image 20230929023510.png)
De la misma manera podemos ver el **ID** del chat almacenado en la variable `$id`.

### P10 - ¿Cuales son los alias para el desarrollador del "phish kit"?

![](Pasted image 20230929023632.png)

Al inicio del código podemos ver un comentario que dice:

```
Con amor y respeto a todos los buscavidas de ahí fuera,
Este es un pequeño regalo para mis hermanos,
Todo lo mejor con su suerte,

Saludos, 
j1*****@m3**
```

### P11 - ¿Cuál es el nombre completo del "Phish Actor"?

Ya que tenemos el **ID** del atacante junto con la API de te******, podemos realizar una consulta con el siguiente comando:

```bash
curl -s -X GET https://api.te******.org/bot<TOKEN>/getChat?chat_id=<ID> | jq
```

![](Pasted image 20230929025008.png)

### P12 - ¿Cuál es el nombre de usuario del "Phish Actor"?

El nombre de usuario sería `pu*********`.

![](GrabThePhisher2.png)
