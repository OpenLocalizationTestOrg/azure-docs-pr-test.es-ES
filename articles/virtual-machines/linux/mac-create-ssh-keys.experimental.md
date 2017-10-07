---
title: "par de claves de aaaCreate un SSH para máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "Cree de forma segura un par de claves SSH pública y privada para máquinas virtuales Linux de Azure."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: c4c7cec77c9b48295f2a28c8179b30a4dc38a555
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a>Creación de un par de claves SSH pública y privada para máquinas virtuales Linux

Este artículo muestra cómo toogenerate una Protocolo versión 2 RSA pública y privada clave SSH archivo toouse par con máquinas virtuales de Linux.  Con un par de claves de SSH, puede crear máquinas virtuales en Azure esos valores predeterminados de las claves SSH de toousing para la autenticación, eliminando la necesidad de Hola de toolog de las contraseñas en.  Las contraseñas pueden ser adivinadas y abrir las máquinas virtuales una tooguess de intentos de toorelentless por fuerza bruta la contraseña. Las máquinas virtuales creadas con plantillas de Azure o hello `azure-cli` puede incluir la clave pública SSH como parte de la implementación de hello, quitar un paso de configuración de implementación de post de deshabilitar los inicios de sesión de contraseña de SSH.

## <a name="quick-commands"></a>Comandos rápidos

Ejecute hello siguientes comandos de shell de Bash, reemplazando los ejemplos de hello con sus propias opciones.

El archivo de clave pública SSH se crea de forma predeterminada en `~/.ssh/id_rsa.pub`. Cuando se le solicite mediante el siguiente comando de hello, debe crear un toosecure "frase de contraseña" su clave privada. (frase de contraseña de hello es que utiliza una contraseña tooencrypt su clave privada).

```bash
ssh-keygen -t rsa -b 2048 
```

Agregar clave de hello recién creado demasiado`ssh-agent`:

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> Hola por encima de trabajo de comandos en sistemas operativos Linux casi todas las distribuciones, pero no funcionan necesariamente en contenedores, como entorno de hello puede restringirse radicalmente. 

## <a name="detailed-walkthrough"></a>Tutorial detallado

El uso de claves públicas y privadas de SSH es toolog de manera más fácil de hello en servidores Linux de tooyour. [Criptografía de clave pública](https://en.wikipedia.org/wiki/Public-key_cryptography) proporciona un toolog de manera mucho más seguro en tooyour Linux o BSD VM en Azure que las contraseñas, que pueden forzarse mucho más fácilmente.

> [!IMPORTANT]
> La clave pública se puede compartir con cualquiera. Sin embargo, la clave privada es propiedad exclusivamente suya (o de su infraestructura de seguridad local).  clave privada de Hello SSH debe tener un [contraseña muy segura](https://www.xkcd.com/936/) (origen:[xkcd.com](https://xkcd.com)) toosafeguard se.  Esta contraseña es la clave privada de SSH de tooaccess simplemente hello y **no es** contraseña de cuenta de usuario de Hola.  Cuando se agrega una clave SSH de tooyour de contraseña, cifra la clave privada de hello mediante AES de 128 bits, para que hello clave privada es inútil sin Hola contraseña toodecrypt lo.  Si un atacante robar la clave privada y que la clave no tenía una contraseña, sería capaz de toouse es privada clave toolog en servidores de tooany que tiene la correspondiente clave pública de Hola.  Si una clave privada está protegida con una contraseña, el atacante no podrá usarla, ya que la contraseña constituye un nivel adicional de seguridad en la infraestructura de Azure.

En este artículo se crea versión del protocolo SSH 2 RSA públicos y privados archivos de clave, que se recomiendan para las implementaciones en hello Administrador de recursos.  *SSH-rsa* las claves son necesarias en hello [portal](https://portal.azure.com) para clásico e implementaciones de administrador de recursos.

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a>Deshabilitar contraseñas SSH mediante claves SSH

Azure requiere al menos claves públicas y privadas de 2048 bits con el formato ssh-rsa. uso de claves de hello toocreate `ssh-keygen`, que realiza una serie de preguntas y, a continuación, escribe una clave privada y una clave pública correspondiente. Cuando se crea una máquina virtual de Azure, la clave pública de Hola se copia demasiado`~/.ssh/authorized_keys`.  Claves SSH en `~/.ssh/authorized_keys` son toochallenge usado hello toomatch Hola correspondiente clave privada de cliente en una conexión de inicio de sesión SSH.  Cuando se crea una máquina virtual Linux de Azure mediante claves de SSH para la autenticación, Azure configura Hola SSHD toonot server permite inicios de sesión de contraseña, solo las claves SSH.  Por lo tanto, mediante la creación de máquinas virtuales de Linux de Azure con claves SSH, permiten una implementación segura Hola VM y ahorrarse el paso de configuración posteriores a la implementación típica de Hola de deshabilitar las contraseñas en el archivo de configuración de hello sshd_config.

## <a name="using-ssh-keygen"></a>Uso de ssh-keygen

Este comando crea una contraseña protegida (cifrada) par de claves de SSH mediante RSA de 2048 bits y está marcada como comentario tooeasily identificarlo.  

SSH claves son de forma predeterminada que se mantienen en hello `~/.ssh` directory.  Si no tiene un `~/.ssh` directorio, hello `ssh-keygen` comando crea automáticamente con hello permisos correctos.

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

*Explicación del comando*

`ssh-keygen`= Hola programa utilizado toocreate Hola claves

`-t rsa`= tipo de clave toocreate que es el formato RSA Hola [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)

`-b 2048`= bits de clave de Hola


## <a name="classic-portal-and-x509-certs"></a>Portal clásico y certificados X.509

Si utilizas hello Azure [portal clásico](https://manage.windowsazure.com/), requiere certificados X.509 para las claves SSH de Hola.  No se permite ningún otro tipo de claves públicas SSH, *deben* ser certificados X.509.

toocreate un certificado X.509 de su clave privada SSH-RSA existente:

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a>Implementación clásica mediante `asm`

Si usas clásico de Hola implementar modelo (administración de servicios Azure CLI `asm`), puede usar una clave pública SSH-RSA o un RFC4716 con formato clave en un **.pem** contenedor.  clave pública SSH-RSA Hello es lo que se creó anteriormente en este artículo mediante `ssh-keygen`.

toocreate un RFC4716 formato de clave de una clave pública SSH existente:

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a>Ejemplo de ssh-keygen

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
hello keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

Archivos de clave guardados:

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

nombre del par de claves de Hola de este artículo.  Tener un par de claves denominado **id_rsa** es el valor predeterminado de Hola y algunas herramientas podrían esperar hello **id_rsa** nombre de archivo de clave privada para disponer de uno es una buena idea. directorio de Hello `~/.ssh/` es ubicación predeterminada de Hola para pares de claves de SSH y archivo de configuración SSH de Hola.  Si no se especifica con una ruta de acceso completa, `ssh-keygen` van a crear claves de hello en el directorio de trabajo actual de hello, no Hola predeterminado `~/.ssh`.

Una lista de hello `~/.ssh` directory.

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

Contraseña de la clave:

`Enter passphrase (empty for no passphrase):`

`ssh-keygen`hace referencia la clave privada de tooa contraseña utilizada tooencrypt hello como "una frase de contraseña".  Es *fuertemente* recomienda tooadd un par de claves de tooyour de frase de contraseña. Sin una frase de contraseña protección Hola clave privada, cualquier persona con el archivo de clave de hello puede utilizarse toolog en servidor tooany que tiene una clave pública correspondiente Hola. Agregar una frase de contraseña ofrece una protección más en caso de que alguien es el archivo de clave privada tooyour toogain capaz de acceso, lo que proporciona claves de tiempo toochange Hola usan tooauthenticate.

## <a name="using-ssh-agent-toostore-your-private-key-password"></a>Uso de ssh agente toostore su contraseña de clave privada

frase de contraseña de archivo tooavoid escribir su clave privada con cada inicio de sesión SSH, puede usar `ssh-agent` toocache la contraseña del archivo de clave privada. Si utilizas un equipo Mac, Hola OSX llaveros almacena de forma segura las contraseñas de clave privada de hello al invocar `ssh-agent`.

Compruebe y usar `ssh-agent` y `ssh-add` tooinform Hola SSH sistema acerca de los archivos de clave de Hola para que la frase de contraseña de hello no necesitará toobe usar de forma interactiva.

```bash
eval "$(ssh-agent -s)"
```

Ahora agregue clave privada de hello demasiado`ssh-agent` mediante el comando hello `ssh-add`.

```bash
ssh-add ~/.ssh/id_rsa
```

contraseña de clave privada de Hello ahora se almacena en `ssh-agent`.

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a>Usar `ssh-copy-id` nueva clave de tooinstall Hola
Si ya ha creado una máquina virtual puede instalar Hola nueva SSH pública clave tooyour VM de Linux con el siguiente comando, sustituyendo el nombre de usuario de hello VM y dirección del servidor hello con sus propios valores de hello:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a>Creación y configuración de un archivo de configuración de SSH

Trata de un toocreate de prácticas recomendada y configurar un `~/.ssh/config` toospeed archivo los inicios de sesión y para optimizar el comportamiento de cliente SSH.

Hola de ejemplo siguiente muestra una configuración estándar.

### <a name="create-hello-file"></a>Crear archivo hello

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a>Editar configuración de SSH nuevo de hello archivo tooadd hello:

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a>Archivo `~/.ssh/config` de ejemplo:

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

Esto deja de configuración SSH se secciones para cada servidor tooenable cada toohave su propio par de claves dedicado. Hola configuración predeterminada (`Host *`) son para todos los hosts que no coincide con cualquiera de hello hosts específicos más arriba en el archivo de configuración de Hola.

### <a name="config-file-explained"></a>Explicación del archivo de configuración

`Host`= nombre de hello del host de Hola que se llama en hello terminal.  `ssh fedora22`indica a `SSH` toouse valores de hello en bloque de configuración de hello con la etiqueta `Host fedora22` Nota: Host puede ser cualquier etiqueta que tiene sentido para su uso y no representa Hola hostname real de cualquier servidor.

`Hostname 102.160.203.241`= dirección IP de Hola o nombre DNS de servidor de Hola que se obtiene acceso.

`User ahmet`= toouse de cuenta de usuario remoto hello al iniciar sesión en el servidor de toohello.

`PubKeyAuthentication yes`= indica SSH desea toouse un toolog clave SSH.

`IdentityFile /home/ahmet/.ssh/id_id_rsa`= la clave privada de SSH de Hola y toouse de clave pública correspondiente para la autenticación.

## <a name="ssh-into-linux-without-a-password"></a>SSH en Linux sin contraseña

Ahora que tiene un par de claves de SSH y un archivo de configuración SSH configurado, es capaz de toolog en tooyour VM de Linux rápida y segura. Hola primera vez que inicie en servidor de tooa mediante un símbolo del sistema de hello clave SSH se Hola frase de contraseña para este archivo de clave.

```bash
ssh fedora22
```

### <a name="command-explained"></a>Explicación del comando

Cuando `ssh fedora22` se ejecuta SSH primero busca y carga los valores de configuración de hello `Host fedora22` bloque y, a continuación, carga todos Hola restantes valores de hello último bloque, `Host *`.

## <a name="next-steps"></a>Pasos siguientes

A continuación una es toocreate máquinas virtuales de Linux de Azure con hello nueva SSH clave pública.  Máquinas virtuales de Azure que se crean con una clave pública SSH como inicio de sesión de hello son más segura que las máquinas virtuales creadas con el método de inicio de sesión de hello de forma predeterminada, las contraseñas.  Las máquinas virtuales de Azure creadas con claves SSH están configuradas de forma predeterminada con las contraseñas deshabilitadas, a fin de evitar los intentos de adivinarlas por fuerza bruta. Si necesita más ayuda para crear el par de claves de SSH o requieren certificados adicionales, por ejemplo, para usarlo con el portal clásico de hello, consulte [obtener certificados y pares de claves SSH pasos toocreate](create-ssh-keys-detailed.md).

* [Creación de una máquina virtual Linux protegida mediante una plantilla de Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Crear una VM de Linux segura mediante Hola portal de Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Crear una VM de Linux segura mediante Hola CLI de Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
