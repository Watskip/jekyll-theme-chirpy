---
title: Respecto a los File Descriptors
author: Watskip
date: 2020-09-25 22:55:00 -0400
categories: [Nix]
tags: [File Descriptors]
pin: false
---


Estaba hablando con unos compañeros sobre Linux, el flujo de la conversación me llevó a mencionar los File Descriptors, a lo cual el resto desconocía. Para reforzar la definición que les di y de la misma manera ayudarme a revisitar el concepto he creado lo siguiente.

Antes de continuar, en un sistema \*nix (Unix o Linux), debemos de recordar que podemos usar `<` y `>` para redirigir la salida y entrada de datos. La redirección también puede usarse para abrir y cerrar archivos al momento de ejecución de comandos. A continuación lo estaremos usando en los ejemplos para tener una perspectiva práctica de como funcionan los File Descriptors.

## Definiendo un File Descriptor

Cada vez que abres un archivo en un sistema \*nix , para el kernel se crea una entrada para simbolizar la transmición o recepción de datos al archivo a lo largo de su proceso. Esta entrada siempre será un número entero positivo, quien de manera secuencial, son guardados en una tabla. Esta es una definición general de un file descriptor. Pero no nos dice mucho desde una perspectiva prática.

Cada programa con el cual se interactua tiene 3 streams de datos abiertos cuando se inicia. 

* Uno como entrada de datos al programa 
* Un segundo para salida de datos del programa
* Y otro con el fin de mostrar errores/alertas durante la ejecución del programa

Y al inicio del programa también es asociado un FD (File Descriptor) a cada una de estos streams de manera respectiva:

0. STDIN - StandardInput (Para entrada)
1. STDOUT - Standard Output (Para Salida)
2. STDERR - Standard Error (Para Errores/Alertas)

Debido un standard POSIX estos valores se mantienen con la misma asignación.

Esto en sí es un concepto base de qué es un File Descriptor pero aún nos dice mucho de manera prática. Para ello veamos un par de situaciones en las cuales podamos redirigirlos.

## Ejemplo 1

En la captura siguiente tenemos 2 archivos creados, uno por el usuario **root** (root.txt) y otro el usuario **re**. Vemos que ambos usuarios pueden leer **user.txt** pero solo **root tiene permisos para leer root.txt.**

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

## Ejemplos Finales

Entre otros ejemplos se encuentran:
```bash
cat root.txt 2>&2 read_error
```
El cual nos mostrará STDERR en pantalla y también lo guarda en el archivo especificado.

Y el siguiente ejemplo, el cual nos redirige el contenido del archivo (STDOUT) junto con cualquier error que pueda ocurrir durante la ejecución del comando (STDERR) 
```bash
cat /etc/hosts >& read_error
```

Hay más casos para usarlos, pero teniendo estos ejemplos obtenemos una idea de la utilidad que podemos sacarle a los FDs en tareas frecuentes.
