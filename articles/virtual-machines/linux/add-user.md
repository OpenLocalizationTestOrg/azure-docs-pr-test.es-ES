---
title: aaaAdd un tooa de usuario Linux VM en Azure | Documentos de Microsoft
description: Agregar una VM de Linux tooa de usuario en Azure.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: eed050154adf0cbed2c168e7aa675bd3ded85fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-user-tooan-azure-vm"></a>Agregar una máquina virtual de Azure tooan de usuario
Una de las primeras tareas de Hola en cualquier nueva VM de Linux es toocreate un nuevo usuario.  En este artículo, le guían por la creación de una cuenta de usuario de sudo, establecer la contraseña de hello, añadir claves públicas SSH y finalmente utilizar `visudo` tooallow sudo sin una contraseña.

Requisitos previos son: [una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/), [claves públicas y privadas de SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), un grupo de recursos de Azure y hello Azure CLI instalados y se cambia el modo de administrador de recursos de tooAzure mediante `azure config mode arm`.

## <a name="quick-commands"></a>Comandos rápidos
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy hello SSH Public Key toohello new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers tooallow no password
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify hello SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a>Tutorial detallado
### <a name="introduction"></a>Introducción
Una tarea primera y más común de hello con un nuevo servidor es tooadd una cuenta de usuario.  Se deben deshabilitar los inicios de sesión de raíz y propia cuenta de raíz hello no debe usarse con el servidor Linux, sólo sudo.  Otorgar privilegios con sudo se Hola tooadminister de manera adecuada y usar Linux a una extensión de la raíz de usuario.

Mediante el comando hello `useradd` vamos a agregar cuentas de usuario toohello VM de Linux.  Si se ejecuta `useradd`, se modifica `/etc/passwd`, `/etc/shadow`, `/etc/group` y `/etc/gshadow`.  Vamos a agregar un indicador de línea de comandos toohello `useradd` comando tooalso agregar Hola nuevo toohello sudo correcto grupo de usuarios en Linux.  Incluso tú `useradd` crea una entrada en `/etc/passwd` nueva cuenta de usuario de hello no se ofrecerá una contraseña.  Vamos a crear una contraseña inicial Hola nuevo usuario con simple hello `passwd` comando.  Hola último paso es toomodify hello sudo reglas tooallow que comandos de tooexecute de usuario con privilegios sudo sin necesidad de tooenter una contraseña para todos los comandos.  Iniciar sesión con la clave privada de Hola se supone que esa cuenta de usuario está protegida de actores no válidos y se va tooallow sudo acceso sin una contraseña.  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a>Agregar un tooan de usuario único sudo máquina virtual de Azure
Inicie sesión en toohello Azure VM utilizar claves de SSH.  Si no ha configurado el acceso de clave pública SSH, lea primero el artículo [Using Public Key Authentication with Azure](http://link.to/article)(Uso de la autenticación de clave pública con Azure).  

Hola `useradd` Hola siguiente las tareas haya completado el comando:

* crear una nueva cuenta de usuario
* crear un nuevo grupo de usuarios con hello mismo nombre
* Agregar una entrada en blanco demasiado`/etc/passwd`
* Agregar una entrada en blanco demasiado`/etc/gpasswd`

Hola `-G` marca de línea de comandos agrega Hola nueva cuenta de usuario toohello apropiado Linux grupo otorgar privilegios de extensión raíz a la cuenta de usuario nueva de Hola.

#### <a name="add-hello-user"></a>Agregar usuario de Hola
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a>Establecer una contraseña
Hola `useradd` comando crea el usuario de Hola y agrega una entrada tooboth `/etc/passwd` y `/etc/gpasswd` , pero realmente no se establece la contraseña de Hola.  Hello contraseña se agrega mediante Hola de entrada de toohello `passwd` comando.

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

Ahora tenemos un usuario con privilegios sudo en servidor hello.

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a>Agregue su cuenta de usuario nueva toohello de clave pública SSH
Desde su equipo, use hello `ssh-copy-id` comando con la nueva contraseña de Hola.

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a>Use visudo tooallow sudo utilización sin una contraseña
Usar `visudo` tooedit hello `/etc/sudoers` archivo agrega unos niveles de protección contra la modificación incorrecta de este archivo importante.  Tras la ejecución de `visudo`, hello `/etc/sudoers` archivo está bloqueado tooensure ningún otro usuario puede realizar cambios mientras activamente se está editando.  Hola `/etc/sudoers` también se comprueba el archivo de errores por `visudo` al intentar toosave o salir por lo que no se puede guardar un archivo de sudoers roto.

Ya tenemos a los usuarios en el grupo predeterminado correcto de Hola para acceso sudo.  Ahora vamos tooenable esos grupos toouse de sudo con ninguna contraseña.

```bash
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-hello-user-ssh-keys-and-sudo"></a>Compruebe el usuario de hello, ssh claves y sudo
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
