---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear un disco administrado desde una instantánea | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: creación de un disco administrado a partir de una instantánea"
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
ms.openlocfilehash: f92059353bfb739cff05213a9d206bfde2829a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a>Creación de un disco administrado a partir de una instantánea con CLI

Este script crea un disco administrado a partir de una instantánea. Usar toorestore una máquina virtual de las instantáneas de discos de sistema operativo y los datos. Cree los discos de sistema operativo y datos a partir de las instantáneas correspondientes y, luego, cree una nueva máquina virtual conectando los discos administrados. También puede restaurar los discos de datos de una máquina virtual existente conectando los discos de datos creados a partir de las instantáneas.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli[main](../../../cli_scripts/storage/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a>Explicación del script

Este script usará los siguientes comandos toocreate un disco administrado desde una instantánea. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [az snapshot show](https://docs.microsoft.com/cli/azure/snapshot#show) | Obtiene todas las propiedades de Hola de una instantánea mediante el nombre de Hola y propiedades de grupo de recursos de instantánea de Hola. Propiedad ID es toocreate usado de disco administrado.  |
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | Crea un disco administrado usando un identificador de una instantánea administrada |

## <a name="next-steps"></a>Pasos siguientes

[Creación de una máquina virtual conectando un disco administrado como disco del SO](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Máquina virtual adicional y ejemplos de secuencias de comandos CLI de discos administrados pueden encontrarse en hello [documentación de Azure VM de Linux](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
