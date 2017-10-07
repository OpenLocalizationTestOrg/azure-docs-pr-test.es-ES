---
title: "aaaAzure ejemplo de secuencia de comandos de CLI - copia (movimiento) administrado toosame de discos u otra suscripción | Documentos de Microsoft"
description: "Azure ejemplo de secuencia de comandos CLI - toosame de discos de copia (movimiento) administrado o de otra suscripción"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: b1fa207bd6e05d7094be08855e7823e3b7686013
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a>Copiar discos administrados toosame u otra suscripción con CLI

Esta secuencia de comandos copia un disco administrado toosame u otra suscripción pero en Hola misma región. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a>Explicación del script

Esta secuencia de comandos que se utiliza después de comandos toocreate un nuevo disco administrado en la suscripción de destino de hello con Hola Id. de origen de hello administra el disco. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [az disk show](https://docs.microsoft.com/cli/azure/disk#show) | Obtiene todas las propiedades de Hola de un disco administrado mediante propiedades de grupo de hello nombre y los recursos de disco administrado Hola. Propiedad ID es toocopy usado Hola administrado disco toodifferent suscripción.  |
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | Copia un disco administrado mediante la creación de un nuevo disco administrado en otra suscripción con el identificador y el nombre primario Hola administrados disco.  |

## <a name="next-steps"></a>Pasos siguientes

[Crear una máquina virtual a partir de un disco administrado](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Máquina virtual adicional y ejemplos de secuencias de comandos CLI de discos administrados pueden encontrarse en hello [documentación de Azure VM de Linux](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
