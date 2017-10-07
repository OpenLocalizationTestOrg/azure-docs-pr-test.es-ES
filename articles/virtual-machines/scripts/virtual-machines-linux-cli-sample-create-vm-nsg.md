---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear dos máquinas virtuales con un NSG interno y externo | Documentos de Microsoft"
description: "Ejemplo de script de CLI de Azure: creación de dos máquinas virtuales con un NSG interno y externo"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ba6a70200ca2923369e37b13531bd7ca65b05a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a>Protección del tráfico de red entre máquinas virtuales

Esta secuencia de comandos crea dos máquinas virtuales y protege el tooboth de tráfico entrante. Una máquina virtual es accesible en internet de Hola y ha configurado un grupo de seguridad de red (NSG) tooallow tráfico en el puerto 22 y el puerto 80. Hola segundo una máquina virtual no es accesible en Hola internet y ha un tooonly NSG configurado que permita el tráfico de la máquina virtual de primera Hola. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]

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
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Crea una red virtual y una subred de Azure. |
| [az network vnet subnet create](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | Crea una subred. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Crea la máquina virtual de Hola y lo conecta toohello tarjeta de red, red virtual, subred y NSG. Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.  |
| [az network nsg rule list](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | Devuelve información acerca de una regla de grupo de seguridad de red. En este ejemplo, el nombre de la regla de Hola se almacena en una variable para usarlo más adelante en el script de Hola. |
| [az network nsg rule update](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | Actualiza una regla de NSG. En este ejemplo, la regla de back-end de hello es toopass actualizados por el tráfico sólo de subred de front-end de Hola. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
