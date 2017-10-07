---
title: "aaaAzure ejemplo de Script de PowerShell: crear una instantánea de un disco duro virtual toocreate varios discos administrados idénticos en pequeña cantidad de tiempo | Documentos de Microsoft"
description: "Script de Azure PowerShell de ejemplo: crear una instantánea de un disco duro virtual toocreate varios discos administrados idénticos en pequeña cantidad de tiempo"
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
ms.openlocfilehash: 5f11793b3669df099b6c31dfdbe906c96ba51786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a>Crear una instantánea de un disco duro virtual toocreate varios discos administrados idénticos en pequeña cantidad de tiempo con PowerShell

Este script crea una instantánea desde un archivo VHD en una cuenta de almacenamiento en una misma suscripción o en una suscripción distinta. Use este tooimport una instantánea de tooa de disco duro virtual (no generalizado/preparada con Sysprep) especializada de script y use después Hola instantánea toocreate varios discos administrados idénticos en poco tiempo. Además, usarlo tooimport una instantánea de tooa de disco duro virtual de datos y, a continuación, Hola instantánea toocreate varios discos administrados en poco tiempo. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a>Explicación del script

Este script usará los siguientes comandos toocreate un disco administrado desde un disco duro virtual en otra suscripción. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Crea la configuración de disco que se usa para la creación del disco. Incluye el tipo de almacenamiento, la ubicación, Id. de cuenta de almacenamiento de Hola donde se almacena el VHD primario de Hola de recurso y URI de VHD de VHD primario de Hola. |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Crea un disco mediante la configuración de disco, el nombre del disco y el nombre del grupo de recursos que se pasan como parámetros. |

## <a name="next-steps"></a>Pasos siguientes

[Creación de un disco administrado a partir de una instantánea](virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[Creación de una máquina virtual conectando un disco administrado como disco del SO](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).

Ejemplos de secuencias de comandos de PowerShell de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
