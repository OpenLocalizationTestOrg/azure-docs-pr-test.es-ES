---
title: "aaaReset contraseña de VM de Linux y SSH clave desde Hola CLI | Documentos de Microsoft"
description: "Cómo corregir la configuración de SSH Hola Hola toouse la extensión VMAccess de interfaz de línea de comandos (CLI) de Azure de hello tooreset una contraseña de VM de Linux o clave SSH y comprobar la coherencia de disco"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a>Cómo tooreset una contraseña de VM de Linux o clave SSH, corrija la configuración de SSH de Hola y comprobar la coherencia de disco con la extensión VMAccess Hola
Si no se puede conectar la máquina virtual de Linux tooa en Azure debido a una contraseña olvidada, una clave de Shell seguro (SSH) incorrecta o un problema con la configuración de SSH de hello, usar hello extensión VMAccessForLinux con hello Azure CLI tooreset Hola contraseña o una clave SSH, corregir configuración de SSH de Hola y comprobar la coherencia de disco. 

> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Obtenga información acerca de cómo demasiado[realizar estos pasos con el modelo del Administrador de recursos de hello](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).

Con hello CLI de Azure, use hello **conjunto de extensión de máquina virtual de azure** comando de los comandos de tooaccess de interfaz de línea de comandos (intensiva de errores, Terminal, símbolo del sistema). Ejecute el comando **azure help vm extension set** para obtener más información sobre el uso de la extensión.

Con hello CLI de Azure, puede hacer hello las siguientes tareas:

* [Hola de restablecimiento de contraseña](#pwresetcli)
* [Restablecer la clave SSH Hola](#sshkeyresetcli)
* [Restablecer la clave SSH de hello hello y contraseña](#resetbothcli)
* [Crear una nueva cuenta de usuario de sudo](#createnewsudocli)
* [Restablecer configuración de SSH Hola](#sshconfigresetcli)
* [Eliminar un usuario](#deletecli)
* [Mostrar el estado de Hola de hello extensión VMAccess](#statuscli)
* [Comprobar la coherencia de los discos agregados](#checkdisk)
* [Reparar los discos agregados a la VM de Linux](#repairdisk)

## <a name="prerequisites"></a>Requisitos previos
Se necesita toodo Hola siguiente:

* Necesitará demasiado[instalar hello Azure CLI](../../../cli-install-nodejs.md) y [conectar tooyour suscripción](../../../xplat-cli-connect.md) toouse Azure recursos asociados a su cuenta.
* Establecer modo correcto de hello para el modelo de implementación clásica de hello escribiendo siguiente de hello en línea de comandos de hello:
    ``` 
        azure config mode asm
    ```
* Tiene una nueva contraseña o un conjunto de claves SSH, si desea que tooreset ninguna de ellas. No necesita estos si desea que la configuración de SSH de tooreset Hola.

## <a name="pwresetcli"></a>Hola de restablecimiento de contraseña
1. Cree un archivo en el equipo local denominado "PrivateConf.json" con estas líneas. Reemplace **myUserName** y **myP@ssW0rd** por su propio nombre de usuario y una contraseña y establezca su propia fecha de expiración.

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. Ejecute este comando, sustituyendo el nombre hello de la máquina virtual para **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <a name="sshkeyresetcli"></a>Restablecer la clave SSH Hola
1. Cree un archivo llamado PrivateConf.json con este contenido. Reemplace hello **myUserName** y **mySSHKey** valores con su propia información.

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. Ejecute este comando, sustituyendo el nombre hello de la máquina virtual para **myVM**.
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <a name="resetbothcli"></a>Restablecimiento de contraseña de Hola y clave SSH de Hola
1. Cree un archivo llamado PrivateConf.json con este contenido. Reemplace hello **myUserName**, **mySSHKey** y  **myP@ssW0rd**  valores con su propia información.

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. Ejecute este comando, sustituyendo el nombre hello de la máquina virtual para **myVM**.

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="createnewsudocli"></a>Crear una nueva cuenta de usuario de sudo

Si ha olvidado su nombre de usuario, puede utilizar VMAccess toocreate uno nuevo con autoridad «sudo» de Hola. En este caso, Hola nombre de usuario existente y no se modificará la contraseña.

un nuevo usuario de sudo con acceso de contraseña, usar la secuencia de comandos de hello en toocreate [Hola de restablecimiento de contraseña](#pwresetcli) y especifique el nombre de usuario nuevo de Hola.

toocreate un nuevo usuario de sudo con acceso de clave SSH, usar la secuencia de comandos de hello en [clave SSH de restablecimiento de hello](#sshkeyresetcli) y especifique el nombre de usuario nuevo de Hola.

También puede usar [de restablecimiento de contraseña de Hola y clave SSH de hello](#resetbothcli) toocreate un nuevo usuario con acceso a la clave SSH y la contraseña.

## <a name="sshconfigresetcli"></a>Restablecer configuración de SSH Hola
Si la configuración de SSH Hola está en un estado no deseado, también podría perder acceso toohello máquina virtual. Puede usar hello VMAccess extensión tooreset Hola configuración tooits estado predeterminado. toodo por lo tanto, solo necesita tooset Hola "reset_ssh" clave demasiado "True". extensión de Hello reiniciar servidor SSH de hello, abrir el puerto SSH de hello en la máquina virtual y restablecer los valores de toodefault de configuración de SSH de Hola. no se cambiará la cuenta de usuario de Hello (nombre, la contraseña o claves SSH).

> [!NOTE]
> archivo de configuración de SSH de Hola que restablece se encuentra en /etc/ssh/sshd_config.
> 
> 

1. Cree un archivo llamado PrivateConf.json con este contenido.

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. Ejecute este comando, sustituyendo el nombre hello de la máquina virtual para **myVM**. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="deletecli"></a>Eliminar un usuario
Si desea toodelete una cuenta de usuario sin iniciar sesión en toohello VM directamente, puede utilizar esta secuencia de comandos.

1. Cree un archivo denominado PrivateConf.json con este contenido, sustituyendo hello tooremove de nombre de usuario para **removeUserName**. 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. Ejecute este comando, sustituyendo el nombre hello de la máquina virtual para **myVM**. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="statuscli"></a>Mostrar el estado de Hola de hello extensión VMAccess
estado de hello toodisplay de hello la extensión VMAccess, ejecute este comando.

```
        azure vm extension get
```

## <a name='checkdisk'></a>Comprobar la coherencia de los discos agregados
toorun fsck en todos los discos de la máquina virtual de Linux, se necesita toodo Hola siguiente:

1. Cree un archivo llamado PrivateConf.json con este contenido. Comprobar disco toma un valor booleano para si toocheck discos adjunta la máquina virtual de tooyour o no. 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. Ejecute este tooexecute de comando, sustituyendo el nombre de saludo de la máquina virtual para **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <a name='repairdisk'></a>Reparación de los discos
toorepair los discos que no va a montar o tienen errores de configuración de montaje, use la configuración del montaje hello VMAccess extensión tooreset hello en la máquina virtual de Linux. Nombre de hello sustituyendo del disco para **myDisk**.

1. Cree un archivo llamado PrivateConf.json con este contenido. 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. Ejecute este tooexecute de comando, sustituyendo el nombre de saludo de la máquina virtual para **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a>Pasos siguientes
* Si desea toouse cmdlets de PowerShell de Azure o la contraseña de administrador de recursos de Azure plantillas tooreset Hola o la clave SSH, corrija la configuración de SSH de hello y comprobar la coherencia de disco, vea hello [documentación sobre la extensión VMAccess en GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess). 
* También puede usar hello [portal de Azure](https://portal.azure.com) tooreset contraseña de Hola o clave SSH de una VM de Linux se implementa en el modelo de implementación clásica de Hola. No se utiliza actualmente Hola realice portal toothis para una VM Linux implementada en el modelo de implementación del Administrador de recursos de Hola.
* Consulte [Acerca de las características y extensiones de las máquinas virtuales](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para más información sobre el uso de extensiones de máquinas virtuales para las de Azure.

