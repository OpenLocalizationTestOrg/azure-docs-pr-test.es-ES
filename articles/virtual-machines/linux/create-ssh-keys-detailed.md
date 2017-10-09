---
title: "par de claves de aaaDetailed pasos toocreate un SSH para máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de pasos adicionales toocreate un par de claves de públicas y privado de SSH para máquinas virtuales de Linux en Azure, junto con certificados específicos para distintos casos de uso."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 6/28/2017
ms.author: danlep
ms.openlocfilehash: 9ac52ef4dc87e73b9c07ccc323adc955829e2014
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a>Tutorial detallado toocreate un par de claves de SSH y certificados adicionales para una VM de Linux en Azure
Con un par de claves de SSH, puede crear máquinas virtuales en Azure esos valores predeterminados de las claves SSH de toousing para la autenticación, eliminando la necesidad de Hola de toolog de las contraseñas en. Las contraseñas pueden ser adivinadas y abrir las máquinas virtuales una tooguess de intentos de toorelentless por fuerza bruta la contraseña. Las máquinas virtuales creadas con plantillas de CLI de Azure o el Administrador de recursos de hello pueden incluir la clave pública SSH como parte de la implementación de hello, quitar un paso de configuración de implementación de post de deshabilitar los inicios de sesión de contraseña de SSH. En este artículo se proporcionan pasos detallados y otros ejemplos de generación de certificados, como los que se usan con las máquinas virtuales Linux. Si desea que tooquickly crear y utilizar un par de claves de SSH, consulte [cómo emparejar toocreate una clave pública y privada de SSH para máquinas virtuales de Linux en Azure](mac-create-ssh-keys.md).

## <a name="understanding-ssh-keys"></a>Descripción de las claves SSH

El uso de claves públicas y privadas de SSH es toolog de manera más fácil de hello en servidores Linux de tooyour. [Criptografía de clave pública](https://en.wikipedia.org/wiki/Public-key_cryptography) proporciona un toolog de manera mucho más seguro en tooyour Linux o BSD VM en Azure que las contraseñas, que pueden forzarse mucho más fácilmente.

La clave pública se puede compartir con cualquiera. Sin embargo, la clave privada es propiedad exclusivamente suya (o de su infraestructura de seguridad local).  clave privada de Hello SSH debe tener un [contraseña muy segura](https://www.xkcd.com/936/) (origen:[xkcd.com](https://xkcd.com)) toosafeguard se.  Esta contraseña es simplemente tooaccess Hola SSH archivo de clave privada y **no es** contraseña de cuenta de usuario de Hola.  Cuando se agrega una clave SSH de tooyour de contraseña, cifra la clave privada de hello mediante AES de 128 bits, para que hello clave privada es inútil sin Hola contraseña toodecrypt lo.  Si un atacante robar la clave privada y que la clave no tenía una contraseña, sería capaz de toouse es privada clave toolog en servidores de tooany que tiene la correspondiente clave pública de Hola.  Si una clave privada está protegida con una contraseña, el atacante no podrá usarla, ya que la contraseña constituye un nivel adicional de seguridad en la infraestructura de Azure.

En este artículo se crea una versión del protocolo SSH 2 pares de archivo de claves públicas y privadas de RSA (también denominado tooas "ssh-rsa" claves), que se recomiendan para las implementaciones con el Administrador de recursos de Azure. *SSH-rsa* las claves son necesarias en hello [portal](https://portal.azure.com) para clásico e implementaciones de administrador de recursos.

## <a name="ssh-keys-use-and-benefits"></a>Uso y ventajas de las claves SSH

Azure se necesita al menos 2048 bits, del protocolo SSH versión 2 RSA formato claves públicas y privadas; archivo de clave pública de Hello tiene hello `.pub` formato de contenedor. uso de claves de hello toocreate `ssh-keygen`, que realiza una serie de preguntas y, a continuación, escribe una clave privada y una clave pública correspondiente. Cuando se crea una máquina virtual de Azure, Azure copias Hola toohello de clave pública `~/.ssh/authorized_keys` carpeta Hola máquina virtual. Claves SSH en `~/.ssh/authorized_keys` son toochallenge usado hello toomatch Hola correspondiente clave privada de cliente en una conexión de inicio de sesión SSH.  Cuando se crea una máquina virtual Linux de Azure mediante claves de SSH para la autenticación, Azure configura Hola SSHD toonot server permite inicios de sesión de contraseña, solo las claves SSH.  Por lo tanto, mediante la creación de máquinas virtuales de Linux de Azure con claves SSH, puede ayudar a proteger la implementación de VM de Hola y ahórrese paso de configuración posteriores a la implementación típica de Hola de deshabilitar las contraseñas en hello **sshd_config** archivo.

## <a name="using-ssh-keygen"></a>Uso de ssh-keygen

Este comando crea una contraseña protegida (cifrada) par de claves de SSH mediante RSA de 2048 bits y está marcada como comentario tooeasily identificarlo.  

SSH claves son de forma predeterminada que se mantienen en hello `~/.ssh` directory.  Si no tiene un `~/.ssh` directorio, hello `ssh-keygen` comando crea automáticamente con hello permisos correctos.

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

*Explicación del comando*

`ssh-keygen`= Hola programa utilizado toocreate Hola claves

`-t rsa`= tipo de clave toocreate que es el formato RSA Hola [wikipedia][paréntesis final](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` = bits de clave de Hola

`-C "azureuser@myserver"`= un comentario final toohello anexado de hello tooeasily de archivo de clave pública para identificarlo.  Normalmente se usa un correo electrónico como comentario Hola pero puede usar cualquier cosa que funcione mejor para su infraestructura.

## <a name="classic-deploy-using-asm"></a>Implementación clásica mediante `asm`

Si está utilizando el modelo de implementación clásica de hello (`asm` modo Hola CLI), puede usar una clave pública SSH-RSA o un RFC4716 con formato clave en un contenedor de pem.  clave pública SSH-RSA Hello es lo que se creó anteriormente en este artículo mediante `ssh-keygen`.

toocreate un RFC4716 formato de clave de una clave pública SSH existente:

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a>Ejemplo de ssh-keygen

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
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

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

nombre del par de claves de Hola de este artículo.  Tener un par de claves denominado **id_rsa** es el valor predeterminado de Hola y algunas herramientas podrían esperar hello **id_rsa** nombre de archivo de clave privada para disponer de uno es una buena idea. directorio de Hello `~/.ssh/` es ubicación predeterminada de Hola para pares de claves de SSH y archivo de configuración SSH de Hola.  Si no se especifica con una ruta de acceso completa, `ssh-keygen` crea claves de hello en no Hola de forma predeterminada, el directorio actual de trabajo hello `~/.ssh`.

Una lista de hello `~/.ssh` directory.

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

Contraseña de la clave:

`Enter passphrase (empty for no passphrase):`

`ssh-keygen`hace referencia tooa contraseña para el archivo de clave privada de hello como "una frase de contraseña".  Es *fuertemente* recomienda tooadd una clave privada de tooyour de contraseña. Sin un contraseña protección Hola archivo de clave, cualquier persona con archivo hello puede usar toolog en servidor tooany que tiene una clave pública correspondiente Hola. Agregar una contraseña (frase de contraseña) ofrece una protección más en caso de que alguien es el archivo de clave privada tooyour toogain capaz de acceso, dado las claves de tiempo toochange hello usan tooauthenticate.

## <a name="using-ssh-agent-toostore-your-private-key-password"></a>Uso de ssh agente toostore su contraseña de clave privada

tooavoid escriba la contraseña del archivo de clave privada con cada inicio de sesión SSH, puede usar `ssh-agent` toocache la contraseña del archivo de clave privada. Si utilizas un equipo Mac, Hola OSX llaveros almacena de forma segura las contraseñas de clave privada de hello al invocar `ssh-agent`.

Compruebe y utilizar a ssh agente y ssh-agregar tooinform Hola SSH sistema acerca de los archivos de clave de Hola para que la frase de contraseña de hello no necesitará toobe usar de forma interactiva.

```bash
eval "$(ssh-agent -s)"
```

Ahora agregue clave privada de hello demasiado`ssh-agent` mediante el comando hello `ssh-add`.

```bash
ssh-add ~/.ssh/id_rsa
```

contraseña de clave privada de Hello ahora se almacena en `ssh-agent`.

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a>Usar `ssh-copy-id` toocopy hello tooan clave existente de la máquina virtual
Si ya ha creado una máquina virtual puede instalar Hola nueva SSH pública clave tooyour VM de Linux con:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a>Creación y configuración de un archivo de configuración de SSH

Es una mejor toocreate de práctica recomendada y configurar un `~/.ssh/config` toospeed archivo los inicios de sesión y para optimizar el comportamiento de cliente SSH.

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

A continuación una es toocreate máquinas virtuales de Linux de Azure con hello nueva SSH clave pública.  Máquinas virtuales de Azure que se crean con una clave pública SSH como inicio de sesión de hello son más segura que las máquinas virtuales creadas con el método de inicio de sesión de hello de forma predeterminada, las contraseñas.  Las máquinas virtuales de Azure creadas con claves SSH están configuradas de forma predeterminada con las contraseñas deshabilitadas, a fin de evitar los intentos de adivinarlas por fuerza bruta.

* [Creación de una máquina virtual Linux protegida mediante una plantilla de Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Crear una VM de Linux segura mediante Hola portal de Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Crear una VM de Linux segura mediante Hola CLI de Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
