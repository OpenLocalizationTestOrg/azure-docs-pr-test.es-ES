---
title: "aaaMove archivos tooand desde máquinas virtuales de Linux de Azure con SCP | Documentos de Microsoft"
description: Mover de forma segura los archivos tooand desde una VM de Linux en Azure mediante el SCP y un par de claves de SSH.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a>Mover archivos tooand desde una VM de Linux mediante SCP

Este artículo muestra cómo se toomove los archivos de la estación de trabajo de tooan VM de Linux de Azure, o de una VM de Linux de Azure hacia abajo de la estación de trabajo tooyour, mediante copia Secure (SCP). El traslado de archivos entre su estación de trabajo y una máquina virtual Linux, de forma rápida y segura, es una parte fundamental de la administración de la infraestructura de Azure. 

En este artículo, necesita una máquina virtual Linux implementada en Azure mediante [archivos de clave privada y pública de SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). También necesita un cliente SCP para el equipo local. Es creado sobre SSH e incluido en el shell de Bash Hola predeterminado de la mayoría de los equipos Linux y Mac y algunos shells de Windows.

## <a name="quick-commands"></a>Comandos rápidos

Copiar un archivo de seguridad toohello VM de Linux

```bash
scp file azureuser@azurehost:directory/targetfile
```

Copiar un archivo hacia abajo de hello VM de Linux

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a>Tutorial detallado

Como ejemplos, se mueve un archivo de configuración de Azure la VM de Linux tooa y tire hacia abajo de un directorio de archivos de registro, ambos utilizando claves SCP y SSH.   

## <a name="ssh-key-pair-authentication"></a>Autenticación del par de claves de SSH

SCP usa SSH para la capa de transporte de Hola. Identificadores de SSH Hola autenticación Hola host de destino, y los mueve archivo hello en un túnel cifrado que se proporcionan de forma predeterminada mediante SSH. Para la autenticación SSH, se pueden utilizar nombres de usuario y contraseñas. Sin embargo, se recomienda la autenticación clave pública y privada de SSH como procedimiento recomendado de seguridad. Una vez SSH autenticó conexión hello, SCP comienza, a continuación, copiar el archivo hello. Con un objeto configurado adecuadamente `~/.ssh/config` y claves públicas y privadas de SSH, conexión Hola SCP se pueden establecer simplemente utilizando un nombre de servidor (o dirección IP). Si solo tiene una clave SSH, SCP lo buscará en hello `~/.ssh/` directorio y lo utiliza de forma predeterminada toolog en toohello máquina virtual.

Para más información acerca de cómo configurar las claves públicas y privadas de SSH y `~/.ssh/config`, consulte [Creación de claves SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="scp-a-file-tooa-linux-vm"></a>SCP un tooa archivo VM de Linux

Para el primer ejemplo de Hola, se copie un archivo de configuración de Azure seguridad tooa VM de Linux que es la automatización de toodeploy usado. Como este archivo contiene las credenciales de la API de Azure, que incluyen secretos, la seguridad es importante. túnel cifrado Hola proporcionada por SSH protege contenido Hola de archivo hello.

Hola siguientes comando copias Hola local *.azure/config* tooan VM de Azure con el FQDN de archivos *myserver.eastus.cloudapp.azure.com*. nombre de usuario de administrador de hello en hello Azure VM es *azureuser* . archivo Hello es destino toohello */home/azureuser/* directory. Sustituya sus valores propios en este comando.

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a>SCP de un directorio desde una máquina virtual Linux

En este ejemplo, se copie un directorio de archivos de registro de hello VM de Linux hacia abajo de la estación de trabajo de tooyour. Un archivo de registro puede contener datos confidenciales o secretos, o no. Sin embargo, el uso de SCP garantiza Hola contenido de archivos de registro de hello está cifrado. Con archivos de SCP tootransfer hello es tooget de manera más fácil de Hola Hola directorio de registro y archivos de estación de trabajo de tooyour pero también segura.

Hello siguiente comando copia archivos en hello */principal/azureuser/logs/* directorio en el directorio de hello Azure VM toohello/tmp local:

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

Hola `-r` cli marca indica SCP toorecursively copiar Hola archivos y directorios del punto de hello del directorio Hola que aparece en el comando de Hola.  También observe que Hola sintaxis de línea de comandos es similar tooa `cp` comando Copiar.

## <a name="next-steps"></a>Pasos siguientes

* [Administrar usuarios, SSH y verificación o reparación de discos sobre el uso de máquinas virtuales de Linux de Azure Hola VMAccess extensión](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
