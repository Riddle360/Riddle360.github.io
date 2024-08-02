---
title: DockerLabs Domain Machine
published: true
---

## [](#header-0) Descripción de la máquina.
1. Sistema Operativo = Linux
2. Dificultad = media
3. Lanzamiento = 04/11/2024


## [](#header-1)Enumeración.
### [](#header-2) Enumeramos todos los puertos abieros con un nmap
> PORT---STATE--SERVICE-----------VERSION.
>
> 80-------OPEN-----http--------------------Apache httpd 2.4.52 (Ubuntu).
>
> 139----OPEN-----Netbios-ssn------Samba smb 4.6.2 
>
> 445----OPEN-----Netbios-ssn------Samba smb 4.6.2

### [](#header-3)Ahora vamos a revisar el siteo web en busca de algo relevante pero no encontre nada.

![](https://lh3.googleusercontent.com/yBHxhQxhSgc26Jwwscon8K4n8trYLIs1nCErkVSryL1UmPZ0e9HXYUcM8g9-OHIxbv5KIzVrP9w9x3AuMczMqZrOd8Wrr17qiYmXS3coFHtgoKn1k8W4cZiyMJe2d9tmpA=w1280)
### [](#header-4)Ahora voy a tratar de obtener usuarios del samba usando enun4linux
```
enum4linux 172.17.0.2 -a
```
Encontramos los usuarios: boby y james.

## [](#header-5)Fuerza Bruta
### [](#header-6) Aplicaremos un ataque de fuerza bruta a los usuarios boby y james para conseguir las credenciales
```
crackmapexec smb 172.17.0.2 -u users.txt -p /usr/share/wordlists/rockyou.txt
```
### [](#header-7)Tras finalizar el ataque obtenemos la contraseña star del user bob
![](https://lh6.googleusercontent.com/E4fSfiPdMz1mlw_EdHiFnoQADIh2-e-BDcnDrXYMSugxnKU67p0pdJwA-Ve65eupO80ckXTVoi6Vw7wH_HcMmzHTgF6OLqOGleZbzs-hNl-kVP36FLQs2KmeHDsoXYcI4g=w1280)
### [](#header-8)Una vez conocemos el usuario y su contraseña probamos a entrar al recurso compartido html de la máquina Domain con smbclient de la siguiente forma `smbclient //172.17.0.2/html -U bob` Después, se nos pedirá ingresar la contraseña. Podemos ver que este recurso contiene el índice de la página web, lo que sugiere que todo lo que se encuentre en esa carpeta será accesible desde el servidor.
