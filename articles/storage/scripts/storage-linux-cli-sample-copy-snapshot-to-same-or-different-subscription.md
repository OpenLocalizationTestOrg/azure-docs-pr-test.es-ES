---
title: "Ejemplo de secuencia de comandos de CLI: instantánea de copia (movimiento) de un disco administrado toosame u otra suscripción con CLI aaaAzure | Documentos de Microsoft"
description: "Ejemplo de secuencia de comandos CLI Azure - instantánea de copia (movimiento) de un disco administrado toosame u otra suscripción con CLI"
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
ms.openlocfilehash: 4a21fd2435181a033b563100888aba0c5834496d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a>Instantánea de copia de un disco administrado toosame o de otra suscripción con CLI

Este script copia una instantánea de un disco administrado toosame o suscripción diferente. Utilice este toomove script una suscripción de instantánea toodifferent Hola misma región que la instantánea primaria de Hola.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a>Explicación del script

Este script utiliza después comandos toocreate una instantánea en la suscripción de destino de hello con Hola Id. de instantánea de origen Hola. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [az snapshot show](https://docs.microsoft.com/cli/azure/snapshot#show) | Obtiene todas las propiedades de Hola de una instantánea mediante el nombre de Hola y propiedades de grupo de recursos de instantánea de Hola. Propiedad ID es toocopy usado Hola instantánea toodifferent suscripción.  |
| [az snapshot create](https://docs.microsoft.com/cli/azure/snapshot#create) | Copia una instantánea mediante la creación de una instantánea de sesión con otra suscripción Hola identificador y el nombre de Hola instantánea primaria.  |

## <a name="next-steps"></a>Pasos siguientes

[Crear una máquina virtual a partir de una instantánea](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Máquina virtual adicional y ejemplos de secuencias de comandos CLI de discos administrados pueden encontrarse en hello [documentación de Azure VM de Linux](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
