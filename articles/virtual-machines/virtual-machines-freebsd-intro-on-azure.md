---
title: aaaIntroduction tooFreeBSD en Azure | Documentos de Microsoft
description: "Aprenda a utilizar máquinas virtuales de FreeBSD en Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: eab7aeda7f7ef893740b39c0250aacc29d6fd71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a>Introducción tooFreeBSD en Azure
Este tema proporciona una visión general de la ejecución de una máquina virtual de FreeBSD en Azure.

## <a name="overview"></a>Información general
FreeBSD a Microsoft Azure es que un sistema operativo de equipo avanzada usa toopower moderna servidores, escritorios y plataformas incrustadas.

Microsoft Corporation es ofrecer imágenes de FreeBSD en Azure con hello [agente de invitado de VM de Azure](https://github.com/Azure/WALinuxAgent/) configurado previamente. Actualmente, hello versiones de FreeBSD siguientes se ofrecen como imágenes por Microsoft:

- FreeBSD 10.3-RELEASE
- FreeBSD 11.0-RELEASE

agente de Hello es responsable de la comunicación entre Hola FreeBSD VM y Hola tejido de Azure para operaciones como el aprovisionamiento Hola VM en el primer uso (nombre de usuario, contraseña o clave SSH, nombre de host, etc.) y la funcionalidad habilitación selectiva extensiones de máquina virtual.

Que en versiones futuras de FreeBSD, estrategia de hello es toostay actual y que Hola versiones más recientes disponibles poco después de que se publican por equipo de ingeniería de hello FreeBSD versión.

## <a name="deploying-a-freebsd-virtual-machine"></a>Implementación de una máquina virtual de FreeBSD
Implementar una máquina virtual de FreeBSD es un proceso sencillo con una imagen de hello Azure Marketplace de hello portal de Azure:

- [10.3 de FreeBSD en hello Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [11.0 de FreeBSD en hello Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a>Crear una máquina virtual de FreeBSD mediante la CLI de Azure 2.0 en FreeBSD
En primer lugar debe tooinstall [CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) aunque el siguiente comando en un equipo de FreeBSD.

```bash 
    curl -L https://aka.ms/InstallAzureCli | bash
```

Si intensiva de errores no está instalado en el equipo de FreeBSD, ejecutar el siguiente comando antes de la instalación de Hola. 

```
    sudo pkg install bash
```

Si python no está instalado en el equipo de FreeBSD, ejecute la siguiente comandos antes de la instalación de Hola. 

```
    sudo pkg install python35
    cd /usr/local/bin 
    sudo rm /usr/local/bin/python 
    sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

Durante la instalación de hello, deberá `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`. Si la respuesta es `y` y escriba `/etc/rc.conf` como `a path tooan rc file tooupdate`, puede cumplir problema hello `ERROR: [Errno 13] Permission denied`. tooresolve este problema, debe conceder de usuario de toocurrent derecho de escritura de hello en archivo hello `etc/rc.conf`.

Ahora puede iniciar sesión en Azure y crear su máquina virtual de FreeBSD. A continuación se muestra un ejemplo toocreate una máquina virtual 11.0 de FreeBSD. También puede agregar el parámetro hello `--public-ip-address-dns-name` con un nombre DNS único global para una dirección IP pública recién creado. 

```azurecli
    az login 
    az group create -n myResourceGroup -l westus az vm create -n myFreeBSD11 -g myResourceGroup --image MicrosoftOSTC:FreeBSD:11.0:latest --admin-username azureuser --ssh-key-value /etc/ssh/ssh_host_rsa_key.pub 
```

A continuación, puede iniciar sesión en tooyour FreeBSD VM a través de la dirección ip de Hola que imprime en la salida de hello de por encima de la implementación. 

```bash
    ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a>Extensiones de VM para FreeBSD
A continuación se muestran las extensiones de VM compatibles en FreeBSD.

### <a name="vmaccess"></a>VMAccess
Hola [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extensión puede:

* Hola restablecimiento de contraseñas de usuario de hello original sudo.
* Crear un nuevo usuario de sudo con contraseña Hola especificada.
* Establezca la clave de host público Hola con clave de hello dada.
* Restablecer la clave de host público de hello proporcionada durante la máquina virtual si no se proporcionó una clave de host de Hola de aprovisionamiento.
* Abra el puerto SSH de hello (22) y restaurar Hola sshd_config si reset_ssh se establece tootrue.
* Quitar usuario existente de Hola.
* Comprobar discos.
* Reparar un disco agregado.

### <a name="customscript"></a>CustomScript
Hola [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extensión puede:

* Si se proporciona, descargar scripts de saludo personalizado desde el almacenamiento de Azure o almacenamiento público externo (por ejemplo, GitHub).
* Ejecutar script de punto de entrada de Hola.
* Admitir comandos en línea.
* Convertir la nueva línea de estilo de Windows en scripts de Shell y Python automáticamente.
* Quitar la marca BOM en scripts de Shell y Python automáticamente.
* Proteger la información confidencial en CommandToExecute.

> [!NOTE]
> Por el momento, la máquina virtual de FreeBSD solo es compatible con la versión 1.x de CustomScript.  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a>Autenticación: nombres de usuario, contraseñas y claves SSH
Al crear una máquina virtual de FreeBSD utilizando Hola portal de Azure, debe proporcionar un nombre de usuario, la contraseña o la clave pública SSH.
Nombres de usuario para la implementación de una máquina virtual de FreeBSD en Azure no deben coincidir con los nombres de cuentas del sistema (UID < 100) ya está presente en la máquina virtual de hello (por ejemplo, "raíz").
Actualmente, se admite solo Hola RSA la clave SSH. Una clave SSH multilínea debe comenzar con `---- BEGIN SSH2 PUBLIC KEY ----` y terminar con `---- END SSH2 PUBLIC KEY ----`.

## <a name="obtaining-superuser-privileges"></a>Obtención de privilegios de superusuario
cuenta de usuario de Hola que se especifica durante la implementación de la instancia de máquina virtual en Azure es una cuenta con privilegios. paquete de sudo Hello se instaló una en hello publicado FreeBSD imagen.
Después de que inició sesión a través de esta cuenta de usuario, puede ejecutar comandos como raíz mediante la sintaxis de comando de Hola.

```
    $ sudo <COMMAND>
```

También puede obtener un shell root con `sudo -s`.

## <a name="known-issues"></a>Problemas conocidos
Hola [agente de invitado de VM de Azure](https://github.com/Azure/WALinuxAgent/) versión 2.2.2 tiene un [problema conocido] (https://github.com/Azure/WALinuxAgent/pull/517) que produce error de aprovisionamiento de Hola para FreeBSD VM en Azure. Hello corrección se capturaba [agente de invitado de VM de Azure](https://github.com/Azure/WALinuxAgent/) versión 2.2.3 y versiones posteriores. 

## <a name="next-steps"></a>Pasos siguientes
* Vaya demasiado[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate una VM FreeBSD.
* Si desea toobring su propio tooAzure FreeBSD, consultar demasiado[crear y cargar un VHD FreeBSD tooAzure](linux/classic/freebsd-create-upload-vhd.md).
