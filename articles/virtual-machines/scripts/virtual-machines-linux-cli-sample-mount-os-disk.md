---
title: 'Ejemplo de secuencia de comandos de CLI: el disco del sistema operativo de montaje aaaAzure | Documentos de Microsoft'
description: 'Ejemplo de script de la CLI de Azure: Montaje del disco de sistema operativo'
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
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a>Solución de problemas de un disco de sistema operativo de máquina virtual

Este script monta el disco del sistema operativo Hola de una máquina virtual problemática o con error como datos disco tooa segunda máquina virtual. Esto puede ser útil para solucionar problemas de disco o de recuperación de datos. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a>Explicación del script

Este script usa Hola después comandos toocreate un grupo de recursos, la máquina virtual, y todos los recursos relacionados. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [az vm show](https://docs.microsoft.com/cli/azure/vm#show) | Devuelve una lista de máquinas virtuales. En este caso, la opción de consulta de hello es disco del sistema operativo de máquina virtual de tooreturn usado Hola. Este valor, a continuación, se agrega el nombre de variable tooa "uri". |
| [az vm delete](https://docs.microsoft.com/cli/azure/vm#delete) | Elimina una máquina virtual. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Crea una máquina virtual.  |
| [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) | Asocia una máquina virtual de tooa de disco. |
| [az vm list-ip-addresses](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Devuelve Hola direcciones IP de una máquina virtual. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
