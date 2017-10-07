---
title: Ejemplo de secuencia de comandos de CLI - aaaAzure crear una VM de Linux con NGINX | Documentos de Microsoft
description: "Ejemplo de script de la CLI de Azure: creación de una máquina virtual Linux con NGINX"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9166ccfd4f2e6eea731a8dc6956575d9f8f85488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-nginx"></a>Creación de una máquina virtual con NGINX

Este script crea una máquina Virtual de Azure y utiliza Hola extensión de Script personalizado de Azure Virtual Machine tooinstall NGINX. Después de ejecutar el script de Hola, puede tener acceso a un sitio Web de demostración de la dirección IP pública de Hola de máquina virtual de Hola.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a>Extensión Custom Script

extensión de script personalizado de Hello copia esta secuencia de comandos en la máquina virtual de Hola. script de Hola, a continuación, se ejecuta tooinstall y configurar un servidor web NGINX. 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a>Limpieza de la implementación 

Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicación del script

Este script usa Hola después comandos toocreate un grupo de recursos, la máquina virtual, y todos los recursos relacionados. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Crea la máquina virtual de Hola. Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.  |
| [az vm open-port](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Crea un tooallow de regla de grupo de seguridad de red el tráfico entrante. En este ejemplo, el puerto 80 está abierto al tráfico HTTP. |
| [azure vm extension set](https://docs.microsoft.com/cli/azure/vm/extension#set) | Agrega y se ejecuta un tooa de extensión de máquina virtual VM. En este ejemplo, la extensión de script personalizado de hello es usado tooinstall NGINX.|
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
