---
title: "aaaCreate y use un SSH par de claves para máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "¿Cómo toocreate y use un par de claves de públicas y privado de SSH para máquinas virtuales Linux en Azure tooimprove Hola seguridad Hola del proceso de autenticación."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: iainfou
ms.openlocfilehash: 7fb94841d34d5bc006f3134adf91102ddce5f174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a>¿Cómo de pares de toocreate y use una clave pública y privada de SSH para máquinas virtuales de Linux en Azure
Con un par de claves de shell seguro (SSH), puede crear máquinas virtuales (VM) en Azure que utilizan claves SSH para la autenticación, elimina la necesidad de Hola para contraseñas toolog en. Este artículo muestra cómo tooquickly generar y usar un par de archivo de clave pública y privada RSA de SSH protocol versión 2 para máquinas virtuales de Linux. Para obtener más pasos y ejemplos adicionales, consulte [obtener certificados y pares de claves SSH pasos toocreate](create-ssh-keys-detailed.md).

## <a name="create-an-ssh-key-pair"></a>Creación de un par de claves SSH
Hola de uso `ssh-keygen` archivos de comandos toocreate SSH públicos y privados claves mediante el valor predeterminado creado en hello `~/.ssh` directorio, pero puede especificar una ubicación diferente y la frase de contraseña adicional (un contraseña tooaccess Hola archivo de clave privada) cuando se le solicite. Ejecute hello siguiente comando desde un shell de Bash, responder a mensajes de Hola con su propia información.

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a>Utilice Hola par de claves de SSH
clave pública de Hola que coloque en la VM de Linux en Azure es de forma predeterminada, almacena en `~/.ssh/id_rsa.pub`, a menos que se ha cambiado la ubicación de hello cuando los creó. Si usas hello [CLI de Azure 2.0](/cli/azure) toocreate la máquina virtual, especificar ubicación de Hola de esta clave pública cuando se utiliza hello [crear vm az](/cli/azure/vm#create) con hello `--ssh-key-path` opción. Si copiar y pegar contenido de Hola de toouse del archivo de clave pública de hello en Hola portal de Azure o una plantilla de administrador de recursos, asegúrese de que no se copian ningún espacio en blanco adicional. Por ejemplo, si utiliza OS X, se puede canalizar el archivo de clave pública de hello (de forma predeterminada, **~/.ssh/id_rsa.pub**) demasiado**pbcopy** contenido de hello toocopy (no hay otros programas de Linux que Hola lo mismo, por ejemplo, `xclip`).

Si no está familiarizado con las claves públicas SSH, puede ver su clave pública ejecutando `cat` de la siguiente manera y reemplazando `~/.ssh/id_rsa.pub` por la ubicación de su propio archivo de clave pública:

```bash
cat ~/.ssh/id_rsa.pub
```

Con la clave pública de hello en la VM de Azure, SSH tooyour VM con Hola dirección IP o nombre DNS de la máquina virtual (recuerde tooreplace `azureuser` y `myvm.westus.cloudapp.azure.com` a continuación con el nombre de usuario de administrador de Hola o una dirección IP y nombre de dominio completo de hello--dirección):

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

Si proporciona una frase de contraseña cuando se creó el par de claves, escriba la frase de contraseña de hello cuando se le solicite durante el proceso de inicio de sesión de Hola. (se agrega el servidor de hello tooyour `~/.ssh/known_hosts` carpeta y no se le pida tooconnect nuevamente hasta la clave pública de hello en los cambios de la máquina virtual de Azure o se quita el nombre del servidor hello de `~/.ssh/known_hosts`.)

## <a name="next-steps"></a>Pasos siguientes

Máquinas virtuales creadas mediante claves SSH están configurados con las contraseñas deshabilitadas de forma predeterminada, fuerza bruta adivinen toomake intenta mucho más caro y, por tanto, difícil. En este tema se describe cómo crear un par de claves SSH simple para uso rápido. Si necesita más ayuda para crear el par de claves de SSH o requieren certificados adicionales, consulte [obtener certificados y pares de claves SSH pasos toocreate](create-ssh-keys-detailed.md).

Puede crear máquinas virtuales que usan el par de claves de SSH mediante Hola portal de Azure, CLI y plantillas:

* [Crear una VM de Linux segura mediante Hola portal de Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Crear una VM de Linux segura mediante hello Azure CLI 2.0)](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Creación de una máquina virtual Linux protegida mediante una plantilla de Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
