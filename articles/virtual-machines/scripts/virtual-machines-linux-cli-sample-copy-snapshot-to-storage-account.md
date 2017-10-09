---
title: "Ejemplo de secuencia de comandos de CLI: instantánea de exportación/copiar como cuenta de almacenamiento de disco duro virtual tooa en otra región aaaAzure | Documentos de Microsoft"
description: "Ejemplo de secuencia de comandos CLI Azure - instantánea de exportación/copiar como cuenta de almacenamiento de disco duro virtual tooa de suscripción iguales o distinto"
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
ms.openlocfilehash: 945f83d2ed715642156ca7b252af08559c652b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a>Exportación o copia administrado instantáneas como cuenta de almacenamiento de tooa de disco duro virtual en una región distinta con CLI

Este script exporta una cuenta de almacenamiento de instantáneas administrado tooa en otra región. En primer lugar genera Hola URI de SAS de instantánea de hello y, a continuación, usa toocopy se tooa cuenta de almacenamiento en una región diferente. Use esta copia de seguridad de secuencia de comandos toomaintain los discos administrados en una región diferente para la recuperación ante desastres. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a>Explicación del script

Este script utiliza después toogenerate comandos URI de SAS para una administrado hello instantáneas ni copias instantáneas tooa cuenta de almacenamiento con el URI de SAS. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [az snapshot grant-access](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | Genera SAS de solo lectura que se usa toocopy subyacente de la cuenta de almacenamiento de tooa de archivos de disco duro virtual o descargarlo tooon local  |
| [az storage blob copy start](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | Copia un blob de forma asincrónica desde una tooanother de cuenta de almacenamiento |

## <a name="next-steps"></a>Pasos siguientes

[Crear un disco administrado a partir de un VHD](virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[Crear una máquina virtual a partir de un disco administrado](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Máquina virtual adicional y ejemplos de secuencias de comandos CLI de discos administrados pueden encontrarse en hello [documentación de Azure VM de Linux](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
