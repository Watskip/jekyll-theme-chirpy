---
title: Respecto a los File Descriptors
author: Watskip
date: 2020-09-25 22:55:00 -0400
categories: [Nix]
tags: [File Descriptors]
pin: false
---



# File Descriptor

Cada vez que abres un archivo en un sistema *nix (Unix o Linux), para el kernel se crea una entrada para simbolizar la transmición o recepción de datos al archivo a lo largo de su proceso. Esta entrada siempre será un número entero positivo, quien de manera secuencial, son guardados en una tabla. Esta es una definición general de un file descriptor. Pero no nos dice mucho desde una perspectiva prática.

Cada programa con el cual se interactua tiene 3 streams de datos abiertos cuando se inicia. 

1) Para entrada de datos al programa 

2) Para salida de datos del programa

3) Para mostrar errores/alertas durante la ejecución del programa

Y al inicio del programa también son asociados los FD (File Descriptors) a cada una de estos streams de manera respectiva:

0. STDIN - StandardInput (Para entrada)
1. STDOUT - Standard Output (Para Salida)
2. STDERR - Standard Error (Para Errores/Alertas)

Debido un standard POSIX estos valores se mantienen con el mismo valor comunmente.

Esto en sí es un concepto base de qué es un File Descriptor pero aún nos dice mucho de manera prática. Para ello veamos un par de situaciones en las cuales podamos redirigirlos.

## Ejemplo 1

En la captura siguiente tenemos 2 archivos creados el usuario **root** (root.txt) y por el usuario **re**. Vemos que ambos usuarios pueden leer **user.txt** pero solo **root tiene permisos para leer root.txt.**

![https://user-images.githubusercontent.com/25357279/94328554-8bd3d080-ff81-11ea-8db9-17039470697c.png](https://user-images.githubusercontent.com/25357279/94328554-8bd3d080-ff81-11ea-8db9-17039470697c.png)

Cuando intentamos leer root.txt como el usuario inferior tenemos el siguiente mensaje

![https://user-images.githubusercontent.com/25357279/94328559-8e362a80-ff81-11ea-828e-8f6fb508a859.png](https://user-images.githubusercontent.com/25357279/94328559-8e362a80-ff81-11ea-828e-8f6fb508a859.png)

Este mensaje es mostrado como stderr y podemos redirigir la salida de este mensaje, en este caso podemos redirigir la salida hacia un archivo. Hagámoslo hacia un archivo llamado **read_error.** Especificamos el número del File Descriptor que queremos, en este caso 2 (para STDERR), redirigimos la salida y colocamos el nombre del archivo.

```bash
cat root.txt 2> read_error
```

Ahora vemos que tenemos creado el archivo **read_error**  y al abrirlo vemos el contenido del mensaje de error que teníamos antes.

![https://user-images.githubusercontent.com/25357279/94328560-8f675780-ff81-11ea-9ef1-b371a9bad3c2.png](https://user-images.githubusercontent.com/25357279/94328560-8f675780-ff81-11ea-9ef1-b371a9bad3c2.png)

Este ejemplo nos muestra como manipulando FDs podemos redirigir erores o alertas de programas o acciones que estemos ejecutando a archivos, lo cual nos puede servir para guardar logs de los errores que estos programas nos pudieran dar para luego ser revisados.

## Ejemplo 2

Supongamos que se nos ha olvidado la ruta del archivo **user.txt** y queremos encontrarlo. Para ello empleamos del comando:

```bash
find / -name user.txt
```

Pero al ejecutar el comando obtenemos muchos errores, causados por intentar buscar el archivo en directorios a los cuales no tenemos permisos de lectura.

![https://user-images.githubusercontent.com/25357279/94328561-90988480-ff81-11ea-98fa-1d5ad10861a8.png](https://user-images.githubusercontent.com/25357279/94328561-90988480-ff81-11ea-98fa-1d5ad10861a8.png)

Ahora queremos que solamente nos muestre si encuentra el archivo y que omita los errores. Para ello empleamos de nuevo el redirigir la salida de errores, pero esta vez lo haremos a  `/dev/null.`
De manera simple, esta ruta actua como un "hoyo negro" del sistema, lo que le envíemos será perdido. Al enviar (STDERR) los errores del comando a `/dev/null` no serán mostrados en pantalla y solo veremos (a STDOUT) cuando el comando sea exitoso.

![https://user-images.githubusercontent.com/25357279/94328563-91c9b180-ff81-11ea-8a55-511f94c57b3a.png](https://user-images.githubusercontent.com/25357279/94328563-91c9b180-ff81-11ea-8a55-511f94c57b3a.png)


Ahora teniendo estos ejemplos vemos parte de la utilidad que podemos sacarle a los FDs en tareas simples.
