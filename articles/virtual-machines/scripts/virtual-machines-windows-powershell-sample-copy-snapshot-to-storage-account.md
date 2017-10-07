---
title: "Ejemplo de Script de PowerShell: instantánea de exportación/copiar como cuenta de almacenamiento de disco duro virtual tooa en otra región aaaAzure | Documentos de Microsoft"
description: "Ejemplo de Script de PowerShell Azure - instantánea de exportación/copiar como cuenta de almacenamiento de tooa de disco duro virtual en la misma región diferente"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: c18ad4fa0bf12033fafe941a807e7b4c8d233a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a>Exportación o copia administrado instantáneas como cuenta de almacenamiento de tooa de disco duro virtual en una región distinta con PowerShell

Este script exporta una cuenta de almacenamiento de instantáneas administrado tooa en otra región. En primer lugar genera Hola URI de SAS de instantánea de hello y, a continuación, usa toocopy se tooa cuenta de almacenamiento en una región diferente. Use esta copia de seguridad de secuencia de comandos toomaintain los discos administrados en una región diferente para la recuperación ante desastres.  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a>Explicación del script

Este script utiliza después toogenerate comandos URI de SAS para una administrado hello instantáneas ni copias instantáneas tooa cuenta de almacenamiento con el URI de SAS. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [Grant-AzureRmSnapshotAccess](/powershell/module/azurerm.compute/New-AzureRmDisk) | URI de SAS se genera para una instantánea que sea utilizado toocopy se tooa cuenta de almacenamiento. |
| [New-AzureStorageContext](/powershell/module/azure.storage/New-AzureStorageContext) | Crea un contexto de la cuenta de almacenamiento mediante la clave y el nombre de la cuenta de hello. Este contexto puede ser operaciones de lectura/escritura tooperform usado en la cuenta de almacenamiento de Hola. |
| [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | Copias Hola VHD subyacente de una cuenta de almacenamiento de instantáneas tooa |

## <a name="next-steps"></a>Pasos siguientes

[Crear un disco administrado a partir de un VHD](virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[Crear una máquina virtual a partir de un disco administrado](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).

Ejemplos de secuencias de comandos de PowerShell de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
