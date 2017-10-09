---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear un disco administrado desde un archivo de disco duro virtual en una cuenta de almacenamiento en hello misma suscripción | Documentos de Microsoft"
description: "Script de CLI de Azure de ejemplo: crear un disco administrado desde un archivo de disco duro virtual en una cuenta de almacenamiento en hello misma suscripción"
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
ms.openlocfilehash: 6cfb3c54a7692b0f3999c585861340c1a6b4d348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-hello-same-subscription-with-cli"></a>Crear un disco administrado desde un archivo de disco duro virtual en una cuenta de almacenamiento de hello misma suscripción con CLI

Este script crea un disco administrado desde un archivo de disco duro virtual en una cuenta de almacenamiento en hello misma suscripción. Utilice este tooimport script un versión especializada del toocreate de (no generalizado/preparada con Sysprep) VHD toomanaged OS disco una máquina virtual. O bien, use un disco de datos de datos VHD toomanaged tooimport. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a>Explicación del script

Este script usará los siguientes comandos toocreate un disco administrado desde un disco duro virtual. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | Crea un disco administrado usando el identificador URI de un disco duro virtual en una cuenta de almacenamiento de hello misma suscripción |

## <a name="next-steps"></a>Pasos siguientes

[Creación de una máquina virtual conectando un disco administrado como disco del SO](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Máquina virtual adicional y ejemplos de secuencias de comandos CLI de discos administrados pueden encontrarse en hello [documentación de Azure VM de Linux](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
