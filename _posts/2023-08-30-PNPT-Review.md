---
title: PNPT Review
date: 2023-08-30 15:31:00 +/-TTTT
categories: [Review]
tags: [blog, certification]     # TAG names should always be lowercase
img_path: /assets/PNPTRESOURCES/
image: badge.png
---

Hoy 30 de Agosto del 2023, después de 5 meses de estudio (compaginándolo con mis estudios universitarios), 1 semana de examen  y un intento fallido, completé mi certificación como **Practical Network Penetration Tester** por la empresa **TCM Security**.

Este post cuenta sobre mi experiencia personal durante el examen, las dificultades y retos a los que me enfrenté y los consejos o tips para aquellas personas interesadas en el mundo del **Pentesting y la Seguridad Ofensiva** que quieran empezar por esta certificación.

## ¿Qué es la certificación PNPT?
Como la propia web lo indica ([https://certifications.tcm-sec.com/pnpt/](https://certifications.tcm-sec.com/pnpt/)) es un examen de certificación de **Hacking Ético** de nivel intermedio **100% práctica** único en su tipo que evalúa la capacidad del estudiante para realizar una **Prueba de Penetración** (Pentest) tanto de forma **externa** como **interna** a un nivel profesional.

> Un **Pentest** consiste en atacar entornos informáticos con una misión: **descubrir y explotar vulnerabilidades** con el objetivo de **documentar el ataque y recopilar información sobre los fallos de seguridad**, para que los administradores del sistema puedan arreglar sus sistemas, mejorar la seguridad de la organización y sirva para prevenir futuros ataques que podrían llevarse a cabo.
{: .prompt-info}

Los estudiantes tendrán 5 días completos para completar el **Pentest** y 2 días adicionales para redactar un informe profesional.

Para recibir la certificación el estudiante deberá:
* Realizar **Open-Source Intelligence (OSINT)** para recopilar información sobre cómo atacar apropiadamente la red.
* Demostrar sus habilidades de explotación en **Active Directory** (Directorio Activo) para realizar **Evasión de Antivirus**, movimientos de red **laterales** (pivoting) y **verticales** y, en última instancia, comprometer el **Domain Controller** (Controlador de Dominio) del examen.
* Redactar un informe **detallado y profesional.**
* Realizar una charla de 15 minutos presentando el informe en frente de los asesores de **TCM Security**.

> El examen PNPT fue diseñado para simular un **entorno real** a la hora de realizar un pentest con un cliente, por lo que:
* **NO HAY** ninguna flag o bandera para capturar (como en un CTF).
* **NO HAY** preguntas de opción multiple.
{: .prompt-tip}

### Precio
Para poder optar al examen es necesario comprar el **Exam Voucher + Training**, que trae:
* **Voucher de por vida:** Puedes rendir el examen cuando **tú quieras**, tú manejas tus tiempos.
* **1 segundo intento gratis:** Si fallas el examen, te dan una segunda oportunidad totalmente gratis, y además te dan una **pista** para ayudarte a descubrir en que fallaste.
* **50+ horas de entrenamiento**: Con acceso a los cursos:
    * Practical Ethical Hacking
    * Windows Privilege Escalation
    * Linux Privilege Escalation
    * Open-Source Intelligence
    * External Pentest Playbook

Esta opción está a **$399 dólares** ($340,071 CLP) que está a la par que la **eCPPTv2** ($400 USD) y por encima de la **eJPTv2** ($249 USD) de **eLearnSecurity**, convirtiéndola en una de las certificaciones **más asequibles del mercado**, teniendo en consideración que otras certificaciones rondan los **$1500 USD** ($1,278,465 CLP).

## Mi Experiencia

> Por temas de confidencialidad del examen, no se pueden entregar detalles especificos del entorno, por lo que mi experiencia **solo cuenta con aspectos generales de lo que experimenté durante la certificación.**
{: .prompt-info}

Compré el **Voucher+Training** el 03 de Marzo, de inmediato me puse a estudiar el contenido completando uno por uno cada curso que venia en el entrenamiento, tomando notas y poniendo en práctica lo que aprendia a medida que avanzaba.

Entonces llegó el 01 de Agosto, dia en el que salí de vacaciones de la universidad y tenía todo el tiempo disponible y la confianza para enfocarme solamente en rendir el examen y aprobar a la primera (cosa que no resultó como esperaba).

### Primer Fracaso
Empecé con el primer día de examen, en el que pude ver la modalidad del mismo así como un primer acercamiento a lo que era un **pentest real**, donde tienes que enumerar todo lo que encuentres a la vista y tener un pensamiento crítico y lateral bien formado.

Una vez finalizado el primer día, ya tenía una idea de lo que podía hacer con la información que habia recolectado y avanzar en mi camino a comprometer la empresa a la que me enfrentaba.

Pero mis esperanzas se fueron de a poco a media que avanzaban las horas y no podía encontrar nada de utilidad, de la misma forma avanzaron los días hasta que llegó el último día de examen en el que seguía en el mismo punto que el día Nº2, logrando llegar a la **2/5 parte del examen**:
* OSINT -> Completado!
* External Pentest -> Hasta aquí llegué :(
* Internal Pentest
* Reporte
* Entrevista

Con la decepción por detrás, escribí mi informe con lo que encontré, recopilando todo lo que hice para poder recibir alguna pista que me ayudara en mi segundo y último intento.

### Segunda Victoria
Luego de 1 semana de descanso y mentalizándome para lo que sería mi segunda oportunidad en el examen, empecé el 19 de Agosto desde cero, realizando todo lo que hice la vez anterior, pero con otro punto de vista siguiendo los consejos que me dieron en la pista del intento anterior.

Esto me llevó a poder pasar la parte en la que me habia atascado aproximadamente 30 min después de que inicié el examen.

Con la esperanza y las ganas de demostrar todo lo que habia aprendido, empecé a completar cada parte del examen y a **disfrutar de la experiencia que brinda la certificación** (que es lo más importante).

Al llegar al 3er día del examen ya habia completado los siguientes puntos:
* OSINT -> Completado!
* External Pentest -> Completado!
* Internal Pentest -> Aquí estaba :)
* Reporte
* Entrevista

Instancia en la que me vi atascado nuevamente, pero esta vez en la red interna de la organización, después de muchos intentos y estar día y medio tratando de cambiar la mentalidad y mirar el problema de otra manera, pude conseguirlo y avanzar hasta comprometer el **Domain Controller** de la empresa y terminar mi periodo de examen satisfactoriamente.

Mientras pasaban los dias iba documentando todo lo que encontraba, de esta manera, iba avanzando en el reporte a medida que completaba los puntos del examen.

Luego de terminar el reporte y tener una entrevista de 15 minutos en inglés, pude pasar el examen y orgullosamente conseguir la certificación como **Practical Network Penetration Tester**.
![](PNPTCERT.png)

## Tips y consejos

Algunos consejos que puedo compartir para las personas que quieren afrontar esta certificación son:
> **No la trates como un CTF o uná máquina de HackTheBox**
{: .prompt-tip}

Si bien la mejor manera de pulir esas skills de hacking y poder ganar soltura es mediante plataformas de CTF, esto no va a ser suficiente para lograr pasar la certificación, ya que como se detalla en puntos anteriores, este examen tiene la particularidad de ser basado en un **"entorno real"**, donde lo que prima es la **metodología de trabajo** (que se enseña en los cursos).

> **Toma descansos**
{: .prompt-tip}

Tienes 5 días completos para poder comprometer el dominio, **no te sobre exijas**, esto solo será contraproducente para tu rendimiento, duerme bien, sal a distraerte y regresa con una mentalidad diferente.

> **Recursos externos:**
{: .prompt-tip}

Los cursos que entrega la certificación son más que suficientes para aprobarla, pero si quieres reforzar lo que aprendiste, aquí hay una lista de recursos que me sirvieron para prepararme aún más para la certificación:

* Máquinas fáciles/medias de Active Directory en HackTheBox.
* Máquina Wreath en TryHackMe (Pivoting)
* [How to Not Suck at Reporting (or How to Write Great Pentesting Reports) (Reporte)](https://www.blackhillsinfosec.com/how-to-not-suck-at-reporting-or-how-to-write-great-pentesting-reports/)
* [[Attack]tive Directory: Compromising a Network in 20 Minutes Through Active Directory (Charla)](https://www.youtube.com/watch?v=MIt-tIjMr08)

> **Disfruta de la experiencia**
{: .prompt-tip}

Solo eso, disfruta, aprende, diviértete.

## Conclusiones

A pesar de que es una certificación que no es tan reconocida como otras en su campo (OSCP/OSWE/CEH), entrega al estudiante una experiencia **lo más realista posible**, junto con una estabilidad en el entorno muy sólida y un equipo de soporte increiblemente rápido para ayudarte a responder cualquier duda o consulta.

Aprovecha cada día del examen, mentalizate que estas realizando un pentest real y disfruta de la experiencia de poder comprometer un entorno empresarial, realizar un informe profesional y tener una charla cara a cara con el cliente para presentar tus hallazgos y la forma de solucionarlos.